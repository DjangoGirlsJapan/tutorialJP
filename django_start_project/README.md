# Your first Django project!

> このチャプターの一部はGeek Girls Carrots \([http://django.carrots.pl/](http://django.carrots.pl/)\) のチュートリアルに基づいています。
>
> このチャプターの一部はCreative Commons Attribution-ShareAlike 4.0 International License のライセンスによる [django-marcador  
> tutorial](http://django-marcador.keimlink.de/)  に基づいています。このdjango-marcador tutorialはMarkus Zapke-Gründemann らが著作権を保有しています。

ここからは、シンプルなブログを作っていきますよ！

最初のステップは、Djangoのプロジェクトを新しく作成します。つまり、Djangoのスクリプトを実行し、これから使う沢山のファイルやディレクトリを自動生成して、プロジェクトの骨格を作ります。

Djangoでは、ファイルやディレクトリの名前がとても重要です。ここで作成するファイルの名前は、後から変えるべきではありません。ファイルを移動させるのもいいアイディアとはいえません。Djangoでは、重要なファイルを決められたファイル構成で作成しておくことが必要です。

> virtualenv（仮想環境）を実行しているでしょうか。コンソールに`(myvenv)`という括弧が表示されていなければ、virtualenvを実行してください。 チャプター**Django installation**の**Working with virtualenv** で、仮想環境を実行する方法を説明しました。覚えていますか？次のコマンドを入力ですよ。: Windowsでは、`myvenv\Scripts\activate`, Mac OS / Linuxでは、  
> `myvenv/bin/activate` でしたね。

プロジェクトは、コンソール上で次のコマンドで作成します。\(いいですか？`(myvenv) ~/djangogirls$`は入力の必要がありませんよ。\):

> 補足 コマンドのコマンドの最後にピリオド \(`.`\) があることを確認してくださいね。これば、現在の作業ディレクトリにDjangoをインストールするということを示すので、とても重要なのです。

```
(myvenv) ~/djangogirls$ django-admin startproject mysite .
```

On Windows:

```
(myvenv) C:\Users\Name\djangogirls> python myvenv\Scripts\django-admin.py startproject mysite .
```

> ~~**補足** コマンドの最後にピリオド \(`.`\) があることを確認してくださいね。これば、現在の作業ディレクトリにDjangoをインストールするということを示すので、とても重要なのです。~~

`django-admin.py` は、必要なディレクトリとファイルを作成するスクリプトです。次のようなファイル構造が作成されましたね。:

```
djangogirls
├───manage.py
└───mysite
        settings.py
        urls.py
        wsgi.py
        __init__.py
```

`manage.py` はサイト管理用のスクリプトです。これで、他のものを一切インストールすることなく、コンピューター上でWebサーバーを動かすことができます。

`settings.py`は、サイトの設定ファイルです。

どこに手紙を配達するか番地を確認する郵便配達員の話を覚えていますか？ `urls.py`ファイルは、`urlresolver`をつかったURLのパターンのリストを含んでいます。

今は他のファイルについては無視しておきましょう。触ることはありません。間違って削除してしまわないようにさえしておけば大丈夫です！

## Changing settings

次に、`mysite/settings.py`の中を少し変更していきましょう。エディタでファイルを開いて下さい。

サイトのタイムゾーンを修正しておきましょう。［ウィキペディアのtimezones list］\([http://en.wikipedia.org/wiki/List\_of\_tz\_database\_time\_zones](http://en.wikipedia.org/wiki/List_of_tz_database_time_zones)\) に一覧がありますので、あなたがいるタイムゾーン\(TZ\)を探してください。\(例 `Europe/Berlin` `Asia/Tokyo`\)

開いたファイルの中に、`USE_TZ` や`TIME_ZONE`と書かれた行をみつけてください。 タイムゾーンを次のように変更しましょう。:

```
LANGUAGE_CODE = 'ja-JP'

TIME_ZONE = 'Asia/Tokyo'

USE_TZ = False
```

## Setup a database

世の中には沢山のデータベースソフトウェアがありますが、今日は`sqlite3`というデータベースを使います。

これは、`mysite/settings.py`ファイルの次の箇所で、すでにセットアップされています。:

```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
```

次のコマンドをコンソールで実行して、データベースをこのブログに作成しましょう。：`python manage.py migrate`　  
（`manage.py`ファイルが含まれている`djangogirls`ディレクトリでコマンドを実行してください。）次のような画面になれば、実行は上手くいっています。:

```
(myvenv) ~/djangogirls$ python manage.py migrate
Operations to perform:
  Apply all migrations: admin, contenttypes, auth, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying sessions.0001_initial... OK
```

これでデータベースができました。サーバーを動かして、Webサイトがうまく動いているか確認しましょう！

`manage.py`ファイルを含むディレクトリ（`djangogirls`ディレクトリ）にいることを確認してください。コンソールで、 `python manage.py runserver`とコマンドを入力してサーバーを動かします。:

```
(myvenv) ~/djangogirls$ python manage.py runserver
```

サイトがきちんと動いているか確認してみましょう。ブラウザを開いてください。\(Firefox, Chrome, Safari, Internet Explorerなど、いつも使っているブラウザでいいですよ\) 次のアドレスを入れてください。:

```
http://127.0.0.1:8000/
```

ウェブサーバーは、あなたがコマンドプロンプトで実行を停止するまで動き続けています。さらにコマンドを実行する場合は、新しいターミナルウィンドウを開くか（その時、virtualenvをまた実行することを忘れないで下さい）、あるいは、実行中のウェブサーバーを停止してください。停止する時は、CTRL+C（コントロールとCボタンを同時に押す）です。（Windowsの方は、Ctrl+Breakで停止することがあります。）

おめでとうございます!　これで、はじめてのWebサイトを作成して、サーバーを使って動かすことができました。すごいですね！

![It worked!](images/it_worked2.png)

次のステップに進みましょう！いよいよ、コンテンツを作成していきます！

