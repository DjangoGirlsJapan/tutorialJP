# Deploy!

> __補足__: このチャプターはちょっと難しいことが沢山書かれています。頑張って最後までやりきってください。デプロイはウェブサイトを開発するプロセスの上で、とても重要な部分ですが、躓きやすいポイントも多く含まれています。チュートリアルの途中にこのチャプターを入れています。そういった躓きやすい箇所はメンターに質問して、あなたが作っているウェブサイトをオンラインでみれるようにしてください。言い換えれば、もし時間切れでワークショップ内でチュートリアルを終わらせることができなかったとしても、この後のチュートリアルはきっと自分で終わらせることができるでしょう。

今、あなたのウェブサイトはあなたのコンピューターでのみ見ることができますね。では、これをデプロイする方法を学んでいきましょう。デプロイとは、あなたが作っているアプリケーションをインターネットで公開することです。あなた以外の人もウェブサイトを見ることができるようになりますよ。 :)

これまでに学んだとおり、ウェブサイトはサーバーに置かれています。様々なサーバーがありますが、ここでは最もシンプルなやり方でデプロイすることができるものを使いましょう。[Heroku](http://heroku.com/)です。Herokuは、多くの人がアクセスするものではない小さいアプリケーションは無料で公開できます。今回には最適でしょう。

Heroku のチュートリアル (https://devcenter.heroku.com/articles/getting-started-with-django) に従ってすすめていきます。以下に同内容を記していますので、このまま進めていってください。

## The `requirements.txt` file

最初に、`requirements.txt`ファイルを作成します。あなたのサーバーにどんなPythonパッケージがインストールされる必要があるか、Herokuに伝えるものです。

その前に、Herokuを使うために必要ないくつかのパッケージをインストールしておきましょう。コンソールを開いて、 `virtualenv` を実行し、次のように入力して下さい:

    (myvenv) $ pip install dj-database-url gunicorn whitenoise

インストールが終わったら、`djangogirls`ディレクトリに行き、次のコマンドを実行します:

    (myvenv) $ pip freeze > requirements.txt

これで、`requirements.txt`とよばれるファイルが作成されます。必要なパッケージのリストが書かれています。どんなPythonライブラリを使っているかといった情報です。（例えばDjangoとか）:)).

> __補足__: `pip freeze` は、あなたのvirtualenvにインストール済みの全てのPythonライブラリを一覧にして出力します。その`pip freeze`した出力先を、`>`　の後に示しファイルに保存します。`> requirements.txt` を含まずに `pip freeze` だけで実行してみて、何が起こるか試してみるとよいでしょう。

ファイルを開いて、最終行に次の1行を追加しましょう:

    psycopg2==2.5.4

これは、あなたのアプリケーションをHerokuで動かすために必要な１行です。


## Procfile

次に必要なものは、Procfileです。このファイルが、どのコマンドを実行してウェブサイトをスタートするかHerokuに伝えます。エディタを開いて、`djangogirls` ディレクトリに`Procfile`という名前のファイルを作成して下さい。ファイルに次のとおり入力しましょう:

    web: gunicorn mysite.wsgi

この１行が何を意味しているのでしょうか。私たちは`web` アプリケーションをデプロイしようとしていること、そして`gunicorn mysite.wsgi`というコマンドを実行することでデプロイすることを意味しています。（`gunicorn`は、Djangoの`runserver`コマンドのもっとパワフルなものと考えて下さい。）

これで完了です！保存しましょう。

## The `runtime.txt` file

Herokuに使っているPythonのバージョンを伝えなければいけません。`djangogirls`ディレクトリに`runtime.txt` ファイルを作ってその中に書きます。エディタで新規ファイルを作成して、次のように書いてください:

    python-3.4.2

## mysite/local_settings.py

コンピューター上のローカルとサーバーでは設定に違いがあります。Herokuとコンピューターでは別のデータベースをそれぞれつかっています。そこで、別途ファイルを作成し、ローカル環境で動かすための設定を保存しておく必要があります。

では、ファイルを作成しましょう。`mysite/local_settings.py`というファイルです。その中には、`mysite/settings.py`ファイルからの `DATABASE` の設定が必要です。次のように記述してください:

    import os
    BASE_DIR = os.path.dirname(os.path.dirname(__file__))

    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.sqlite3',
            'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
        }
    }

    DEBUG = True

保存しておきましょう :)

## mysite/settings.py

すべき事がまだあります。ウェブサイトの`settings.py` ファイルに変更を加えておきましょう。エディタで、`mysite/settings.py` ファイルを開いて下さい。最終行に、次のとおり追加しましょう:

    import dj_database_url
    DATABASES['default'] = dj_database_url.config()

    SECURE_PROXY_SSL_HEADER = ('HTTP_X_FORWARDED_PROTO', 'https')

    ALLOWED_HOSTS = ['*']

    STATIC_ROOT = 'staticfiles'

    DEBUG = False

    try:
        from .local_settings import *
    except ImportError:
        pass

このファイルは、Herokuに必要な構成だけでなく、`mysite/local_settings.py`ファイルがある時にはローカルの設定にも重要な役割となります。

保存してください。

## mysite/wsgi.py

次に`mysite/wsgi.py`ファイルを開き、最終行に次のとおり追加してください:

    from whitenoise.django import DjangoWhiteNoise
    application = DjangoWhiteNoise(application)

よし、できましたね!

## Heroku account

では、Heroku toolbeltをインストールしましょう。Herokuをコマンドライン操作を行うためのアプリケーションです。（すでに設定でインストール済みでしたら飛ばしてください。）インストーラーはここから入手できます: https://toolbelt.heroku.com/

> WindowsでHeroku toolbelt をインストールする方は、インストールするコンポーネントを選択する際に"Custom Installation" を選択してください。コンポーネントを選択すると、さらにチェックボックスがありますので、"Git and SSH"にチェックを入れて下さい。

> Windowsの方は、コマンドプロンプトの`PATH`にGitとSSHを追加するために、次のように入力し実行してください: `setx PATH "%PATH%;C:\Program Files\Git\bin"`.
コマンドプロンプトを一旦閉じて、再度起動しましょう。すると変更が適用されます。

> コマンドプロンプトを再起動したら、`djangogirls`フォルダに移動し、virtualenvを実行することを忘れないでくださいね！(ヒント: [Check the Django installation chapter](../django_installation/README.md#working-with-virtualenv))

Herokuの無料アカウントを作成してください: https://id.heroku.com/signup/www-home-top

コマンドプロンプトでHerokuにログインします。コマンドプロンプトを起動して、次のコマンドを入力しましょう:

    $ heroku login

SSHキーがない場合はここで自動的に作成されます。SSHキーは、コードをHerokuにプッシュするために必要なものです。

## Git
Gitとは、バージョン管理システムです。多くのプログラマーがつかっています。ファイルの変更履歴を記録・追跡するシステムです。そのため、一度編集したファイルを特定の変更前の状態に戻したり、編集箇所の差分を表示したりすることができます。Herokuでは、Gitのリポジトリを使って、プロジェクトのファイルを管理します。

`djangogirls`ディレクトリに、`.gitignore`という名前のファイルを作成しましょう。次のとおりに記述してください:

    myvenv
    __pycache__
    staticfiles
    local_settings.py
    db.sqlite3
    *.py[co]

Git に `local_settings.py` は無視してアップロードしないように伝えています。あなたのコンピューター上（ローカル環境）でのみ動作します。それでは保存しておきましょう。ファイル名の最初にあるドットはとても重要ですよ。

次に、Gitのリポジトリを作成し、これまでの変更を記録しておきましょう。

> __補足__: リポジトリを作成する前に、現在作業しているディレクトリを確認しておきましょう。`pwd`コマンドでしたね。 `djangogirls`フォルダになっていればOKです。

コンソールを開き、次のコマンドを実行しましょう:

    $ git init
    Initialized empty Git repository in ~/djangogirls/.git/
    $ git config user.name "Your Name"
    $ git config user.email you@example.com

Gitリポジトリを作成するのは、プロジェクトにつき最初の１度だけです。

間違ったファイルを追加したりコミットすることがないように、 `git add` コマンドを実行する前や、どのような変更を加えたか定かでない時は、 `git status` コマンドを実行しておくとよいでしょう。 `git status` コマンドを実行すると、ステージされた変更内容、されていない変更内容、Git による追跡の対象外となっているファイルやブランチのステータス等が表示されます。次のような情報が出力されることでしょう:

    $ git status
    On branch master

    Initial commit

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

      .gitignore
      Procfile
      mysite/__init__.py
      mysite/settings.py
      mysite/urls.py
      mysite/wsgi.py
      manage.py
      requirements.txt
      runtime.txt

    nothing added to commit but untracked files present (use "git add" to track)

この変更を保存しましょう。コンソールで次のコマンドを実行してください:

    $ git add -A .
    $ git commit -m "My Django Girls app"
    [master (root-commit) 2943412] My Django Girls
     7 files changed, 230 insertions(+)
     create mode 100644 .gitignore
     create mode 100644 Procfile
     create mode 100644 mysite/__init__.py
     create mode 100644 mysite/settings.py
     create mode 100644 mysite/urls.py
     create mode 100644 mysite/wsgi.py
     create mode 100644 manage.py
     create mode 100644 requirements.txt
     create mode 100644 runtime.txt

## Pick an application name

アプリケーションの名前を考えましょう。オンライン上にブログを作る際に、そのURLは `[your blog's name].herokuapp.com` となります。 `[your blog's name]` には、だれもつけていない名前をつける必要があります。この名前は、Django `blog` app や `mysite`といったこれまでに作成したプロジェクト名等と関連している必要はありません。あなたの好きな名前をつけていいですよ。ただし、小文字の英数字とダッシュ(`-`)の組み合わせにしてください。大文字や記号はつかえません。

アプリケーション名が決まれば（おそらくあなたの名前やニックネームが入ったものでしょう。）、次のコマンドを実行してください。ここでは、アプリケーションの名前を`djangogirlsblog` としていますので、あなたのアプリケーション名に置き換えてください:

    $ heroku create djangogirlsblog

> __補足__: `djangogirlsblog`を、Herokuで使うあなたのアプリケーション名に置き換えることを忘れずに！

もし名前が自分で思いつかない時は、かわりに次のコマンドを実行してください。

    $ heroku create

Herokuが代わって名前をつけてくれます。(おそらく `enigmatic-cove-2527`といった感じに。)

もし、あとでHerokuのアプリケーション名を変更したくなれば、次のコマンドでいつでも変更することができます。 (`the-new-name` を変更する新しい名前におきかえてください。):

    $ heroku apps:rename the-new-name

> __補足__: アプリケーション名を変更したら、あなたのウェブサイトのURLは `[the-new-name].herokuapp.com` に変わります。

## Deploy to Heroku!

ここまで沢山のインスト―ルや設定がありましたね。けど、次がこのチャプターの最後です。いよいよデプロイします！

先ほど`heroku create`を実行した時に、自動的にherokuという名前でリモートリポジトリが作成されています。アプリケーションをデプロイするには、これをGitでプッシュするだけです:

    $ git push heroku master

> __補足__: これを最初の実行後は、Heroku が psycopg をコンパイルしてインストールするのにともない*沢山*の出力が表示されることでしょう。暫く待って、最後の方に `https://yourapplicationname.herokuapp.com/ deployed to Heroku` というような出力があれば、成功した印です。

## Visit your application

これであなたのコードをHerokuにデプロイすることができました。そして、プロセスは`Procfile`と指定されています。(先ほど、プロセスタイプを`web`と選びましたね。)最後に、Herokuのウェブプロセスを起動します。

次のコマンドを実行してください:

    $ heroku ps:scale web=1

ウェブプロセスが１つ起動しました。このブログアプリケーションはとてもシンプルなものですので、沢山のパワーは必要ありません。１つのウェブプロセスで十分です。Herokuでそれ以上のウェブプロセスを起動することは可能ですが、今は無料ではないようです。（ところで、Herokuではこのプロセスを”Dynos”と呼んでいます。この言葉が出てきてもびっくりしないでくださいね。）

さて、ブラウザでアプリケーションを開いてみましょう。`heroku open`コマンドです。

    $ heroku open

> __補足__: エラーページが表示されますね。これについては、すぐ説明するので心配しなくていいですよ。

コマンドで、[https://djangogirlsblog.herokuapp.com/]()といったあなたのアプリケーションのURLがブラウザで開かれます。おそらくエラーページが表示されることでしょう。これは、私たちがまだadmin viewしか作成していないからです。URLの後ろに `admin/` をつけてアプリケーションが動いているのをみてみましょう。(例 [https://djangogirlsblog.herokuapp.com/admin/]())

エラーが表示されたのは、Herokuにデプロイする時に新しいデータベースを作成したため、まだデータベースが空っぽの状態だからです。そこで、プロジェクトの最初にローカルにデータベースをセットアップした時のように、再度```migrate``` コマンドを実行します:

    $ heroku run python manage.py migrate

    $ heroku run python manage.py createsuperuser

コマンドプロンプトは、ユーザーネームとパスワードを選ぶよう再度きいてきます。これは、オンライン上のウェブサイトのログインに必要となるログイン情報です。ブラウザを再読み込みして、完了です！

これで、あなたのウェブサイトがブラウザでみられるようになりました！おめでとう！！ :)
