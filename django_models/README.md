# Django models

さて、ブログの中のポストを格納するものが欲しいですよね。そのために`オブジェクト`についてちょっとお話します。

## オブジェクト

プログラミングには`オブジェクト指向プログラミング`という概念があります。それは退屈なプログラムを繰り返し書く代わりにモデルになるものを作って、それが他とどう作用するかを定義するという考え方です。

じゃあオブジェクトって何なの？って思いますよね。オブジェクトは状態（プロパティ）と命令（アクション）の塊です。ピンと来ないでしょうから例を挙げましょう。

猫をモデルにしたいときは、`猫`(`Cat`)オブジェクトを作ります。そのプロパティは、`色`(`color`)、`年齢`(`age`)、`機嫌`(`mood`)（いい、悪い、眠い）、`飼い主`(`owner`)（`人`(`Person`)オブジェクトですね、捨て猫ならそのプロパティは空白）です。

`猫`のアクションは、`喉を鳴らす`(`purr`)、`引っ掻く`(`scratch`)、`餌を食べる`(`feed`)（`キャットフード`(`CatFood`)などで、それはまた`味`(`taste`)というプロパティを持つ別のオブジェクトになるでしょう。）

    Cat
    --------
    color
    age
    mood
    owner
    purr()
    scratch()
    feed(cat_food)


    CatFood
    --------
    taste

つまり、オブジェクト指向とは実際の物をプロパティ（`オブジェクト・プロパティ`と呼びます）を持つコードと命令（`メソッド`と呼びます）で表現するという考え方です。

ではブログポストはどういうモデルになるでしょうか。ブログが作りたいんですよね？

それにはブログポストとは何か、それはどんなプロパティがあるかという問いに答えなければなりません。

まず確実なのはブログポストにはコンテンツと表題がが必要ですね。それからそれを書いた人が分かるといいでしょう。最後にポストの作成公開した時間も分かるといいですね。

    Post
    --------
    title
    text
    author
    created_date
    published_date

ではブログポストがどうなればいいですか？ポストをが公開されるといいですよね？  
なので`publish`メソッドが必要です。

達成したいことが分かったので、Djangoでモデリングの開始です！


## Django model

オブジェクトが何か分かったので、ブログポストのDjangoモデルを作りましょう。

Djangoのモデルは特別なオブジェクトで、`データベース`に格納されます。データベースはデータの集まりです。
ここにユーザーやブログポストの情報を格納します。データを格納するのにSQLiteデータベースを使います。これはDjangoのデフォルトのデータベースで、今はこれで十分です。

データベースの中のモデルは、列（フィールド）と行（データ）があるスプレッドシートと思ってもらっても結構です。

### Creating an application

全部をきちんと整理しておくため、プロジェクトの中に別のアプリケーションを作ります。初めから全てを整理しておくのはとっても良いことです。アプリケーションを作るには、次のコマンドをコンソールの中で走らせなけれなりません。（`manage.py`ファイルがある`djangogirls`ディレクトリから）：

    (myvenv) ~/djangogirls$ python manage.py startapp blog

新しいブログディレクトリが作られて、今沢山のファイルがそこに入っているのに気がついたでしょう。ディレクトリとファイルはこんな風に見えるはずです：

    djangogirls
    ├── mysite
    |       __init__.py
    |       settings.py
    |       urls.py
    |       wsgi.py
    ├── manage.py
    └── blog
        ├── migrations
        |       __init__.py
        ├── __init__.py
        ├── admin.py
        ├── models.py
        ├── tests.py
        └── views.py

アプリケーションを作ったら、Djangoにそれを使うように伝えないといけません。それは`mysite/settings.py`ファイルの中でやります。まず`INSTALLED_APPS`をみつけて`)`の上に`'blog'`という一行を追加します。

    INSTALLED_APPS = (
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'blog',
    )

### Creating a blog post model

`blog/models.py`ファイルで`Models`と呼ばれる全てのオブジェクトを定義します。これがブログポストを定義する場所です。

`blog/models.py`を開いて全部削除し、下のコードを書きます：

    from django.db import models
    from django.utils import timezone

    class Post(models.Model):
        author = models.ForeignKey('auth.User')
        title = models.CharField(max_length=200)
        text = models.TextField()
        created_date = models.DateTimeField(
                default=timezone.now)
        published_date = models.DateTimeField(
                blank=True, null=True)

        def publish(self):
            self.published_date = timezone.now()
            self.save()

        def __str__(self):
            return self.title

> `str`の両側に2つのアンダースコア（`_`）がちゃんと入っているか確認しましょう。これはPythonでよく使われて"ダンダー"(ダブルアンダースコア）と呼んでいます。

難しそうでしょ？でも大丈夫！ちゃんと説明しますから。

`from`とか`import`で始まる行は全部他のファイルから何かをちょこっとずつ追加する行です。なので色んなファイルから必要な部分をコピペする代わりに`from ... import ...`で必要部分を入れられるんです。

`class Post(models.Model):` - この行が今回のモデルを定義します (これが`オブジェクト`です).

- `class`はオブジェクトを定義してますよ、ということを示すキーワードです。
- `Post`はモデルの名前で、他の名前をつけることもできます（が、特殊文字と空白は避けなければいけません）。クラス名は大文字で始めます。
- `models.Model`はポストがDjango Modelだという意味で、Djangoが、これはデータベースに保存すべきものだと分かるようにしています。

さて今度はプロパティを定義しましょう：`title`、`text`、`created_date`、`published_date`、それに`author`ですね。
それにはまずフィールドのタイプを決めなければいけません。（テキスト？数字？日付？他のオブジェクト、例えばユーザーとの関係は？）

- `models.CharField` - テキスト数を定義するフィールド
- `models.TextField` - これは制限無しの長いテキスト用で、ブログポストのコンテンツに理想的なフィールドでしょ？
- `models.DateTimeField` - 日付と時間のフィールド
- `models.ForeignKey` - これは他のモデルへのリンク

コードの細かいところまでは説明し出すと時間がかかるので、ここではしませんが、モデルのフィールドや上記以外の定義のやり方について知りたい方は是非Djangoドキュメントを見てみて下さい。(https://docs.djangoproject.com/ja/1.11/ref/models/fields/#field-types)

`def publish(self):`は何かと言うと、これこそが先程お話したブログを公開するメソッドそのものです。`def`は、これはファンクション（関数）/メソッドといいう意味です。
`publish`というのはこのメソッドの名前で、変えることもできます。
メソッドの名前に使っていいのは、英小文字とアンダースコアで、アンダースコアはスペースの代わりに使います（例えば、平均価格を計算するメソッドは`calculate_average_price`っていう名前にします）

メソッドは通常何かを`return`します。一つの例が`__str__`メソッド にあります。このシナリオでは、`__str__()`を呼ぶと、ポストの表題のテキスト(**string**)が返ってきます。

もしモデルがまだはっきりつかめないようだったら、気軽にコーチに聞いて下さい！特にオブジェクトとファンクションを同時に習ったときはとても複雑なのはよく分かってますから。でも前ほど魔法みたいじゃないといいですけど！

### データベースにモデル用のテーブルを作る

最後のステップは新しいモデルをデータベースに追加することです。まず、（今作った）モデルの中で少し変更があったことをDjangoに知らせなければなりませんから、`python manage.py makemigrations blog`とタイプします。こんな感じです。

    (myvenv) ~/djangogirls$ python manage.py makemigrations blog
    Migrations for 'blog':
      0001_initial.py:
      - Create model Post

Djangoがデータベースに入れる為の移行ファイルを作ってくれているので、`python manage.py migrate blog`とタイプするとこうなるでしょう。

    (myvenv) ~/djangogirls$ python manage.py migrate blog
    Operations to perform:
      Apply all migrations: blog
    Running migrations:
      Applying blog.0001_initial... OK

やった～！ポストモデルがデータベースに入りました。どうなったか見たいでしょ？次へ進みましょう！
