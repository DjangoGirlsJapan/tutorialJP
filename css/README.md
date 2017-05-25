# CSS - make it pretty!

ブログはつくりましたが、このままだとカッコ良くないですよね。カッコよくしていきましょう。ここからはCSSを使っていきます。

## What is CSS?

Cascading Style Sheets (CSS)とは、HTMLなどのマークアップ言語で書かれたWebサイトの見た目や書式を記述するための言語です。私達のWebページをメイクアップするものとして使います。

でも、またゼロから作りたくないですよね。プログラマーたちがすでに作って無料で公開しているツールを使いましょう。わざわざイチから作り直す必要はないですからね。

## Let's use Bootstrap!

Bootstrap は美しいWebサイトを開発するためのHTMLとCSSのフレームワークとしてとても有名です: http://getbootstrap.com/

これは、もともとTwitterのプログラマーが作成したもので、今は、世界中の有志のボランティアで開発されています。

## Install Bootstrap

Bootstrapをインストールするには、 `.html` ファイル (`blog/templates/blog/post_list.html`)　の`<head>` の中に、次のとおり書き加えます：

    <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
    <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">

これは、あなたのプロジェクトにファイルを追加しているわけではありません。インターネット上にあるファイルを指しているだけです。では、Webサイトを開いてページを再読み込みしてください。

![Figure 14.1](images/bootstrap1.png)

これだけで見た目がずいぶん良くなりましたね！

## Static files in Django

もう１つ、今日ここで学ぶことは、 __静的ファイル__ です. 静的ファイルとは、CSSファイルや画像ファイルといった、動的な変更が発生しないファイルのことです。
そのため、これらのファイルはリクエストに依存せず、どのユーザに対しても中身は同じになります。

CSSは静的ファイルです。そのためCSSをカスタマイズするためには、最初にDjangoの中で設定を行う必要があります。この設定を行うのは1回だけです。さぁはじめましょう：

### Configure static files in Django

始めに、静的ファイルを保存するためのディレクトリを作ります。 `djangogirls` ディレクトリの中に、ディレクトリを作成して`static` と名前をつけてください。.

    djangogirls
    ├─── static
    └─── manage.py

 `mysite/settings.py` ファイルを開き、下にスクロールして次の行を追加して下さい。

    STATICFILES_DIRS = (
        os.path.join(BASE_DIR, "static"),
    )

これで、あなたの静的ファイルの保存場所をDjangoが分かってくれます。

## Your first CSS file!

CSSファイルを作って、Webサイトにあなたのスタイル設定していきましょう。 `static` ディレクトリの中に、`css` という名前の新しいディレクトリを作成してください。. その`css` ディレクトリの中に、`blog.css` という名前の新しいファイルを作成してください。準備はいいですか？

    static
    └─── css
        └── blog.css

CSSを書く時間がやってきました！エディタの中で、`static/css/blog.css`ファイルを開いて下さい。

ここでは、CSSのカスタマイズや学習について深くは踏み込みません。それらについて学ぶことは非情に簡単ですので、興味のある方はこのワークショップが終了した後にご自分でチャレンジしてみて下さい！より良いCSSを使ったWebサイト作成について学びたい方には、[Codeacademy HTML & CSS course](http://www.codecademy.com/tracks/web)をオススメします。（※英語サイトです）

少しだけ触ってみましょう。ヘッダーの色を変更することは出来るでしょうか？色を理解するために、コンピュータでは特殊なコードを利用しています。
コードは、`#`で始まり、6種類のアルファベット（A-F）や数字（0-9）が続きます。色コードのサンプルはこのサイトで確認することができます：http://www.colorpicker.com/  
また、`red`や`green`といった[定義済みの色](http://www.w3schools.com/cssref/css_colornames.asp)を利用することもできます。

 `static/css/blog.css` ファイルに、次のコードを記述しましょう。

    h1 a {
        color: #FCA205;
    }

`h1 a` はCSSセレクタです。`h1` 要素の中にある`a` 要素 （例：このようなコードのこと `<h1><a href="">link</a></h1>`）にスタイルを適用します、という意味になります。この場合、テキストの色を`#FCA205`、オレンジ色にする、という意味です。もちろん、あなたの好きな色に変更してもいいですよ。

CSSファイルで、HTMLの各要素のスタイルを指定していきます。 要素は要素名（i.e. `a`, `h1`, `body`）や`class`属性、`id`属性で識別されます。class名とid名はあなた自身が指定するものです。classは要素のグループを定義し、idは具体的な要素を指します。例えば、以下のタグはCSSによってタグ名が`a`、class名が`external_link`、id名が`link_to_wiki_page`と識別されます：

    <a href="http://en.wikipedia.org/wiki/Django" class="external_link" id="link_to_wiki_page">

より詳細は情報についてはこちらのページを御覧ください（※英語サイトです）：[CSS Selectors in w3schools](http://www.w3schools.com/cssref/css_selectors.asp).

そして、CSSを追加したこともHTMLテンプレートに教える必要があります。`blog/templates/blog/post_list.html`のファイルを開き、先頭に次の行を追加します：

    {% load staticfiles %}

私達は丁度ここに静的ファイルを読み込んでいます^^。次に、Bootstrap CSSファイルへのリンクの後ろにある`<head>`と`</head>`の間に次の行を追加します（ブラウザは与えられた順にファイルを読み込むため、私達のコードはBootstrapファイル中のコードで上書きされています）：

    <link rel="stylesheet" href="{% static 'css/blog.css' %}">

これで、テンプレートにCSSファイルがある場所を教えたわけです。

あなたのファイルは、このようになっていますか：

    {% load staticfiles %}
    <html>
        <head>
            <title>Django Girls blog</title>
            <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
            <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">
            <link rel="stylesheet" href="{% static 'css/blog.css' %}">
        </head>
        <body>
            <div>
                <h1><a href="/">Django Girls Blog</a></h1>
            </div>

            {% for post in posts %}
                <div>
                    <p>published: {{ post.published_date }}</p>
                    <h1><a href="">{{ post.title }}</a></h1>
                    <p>{{ post.text|linebreaks }}</p>
                </div>
            {% endfor %}
        </body>
    </html>

OK、ファイルを保存してサイトを更新してみましょう！

![Figure 14.2](images/color2.png)

お疲れ様です！おそらく表示されたウェブサイトは非常に読みにくいため、左側にもう少しスペースが欲しくなります。試してみましょう！

    body {
        padding-left: 15px;
    }

これをあなたのCSSをに追加し、ファイルを保存してどのように動くのか確認してみましょう！

![Figure 14.3](images/margin2.png)

見出しのフォントはカスタマイズできるでしょうか？これを`blog/templates/blog/post_list.html`ファイルの`<head>`中に貼り付けて下さい：

    <link href="http://fonts.googleapis.com/css?family=Lobster&subset=latin,latin-ext" rel="stylesheet" type="text/css">

この行ではGoogle Fonts (https://www.google.com/fonts) から *Lobster* と呼ばれるフォントを読み込んでいます。


`static/css/blog.css`のファイルを開いて、`h1 a`というのブロック中に`font-family: 'Lobster';`という行を追加してみましょう（コードは`{}`で囲まれています）。そしてページを更新します：

    h1 a {
        color: #FCA205;
        font-family: 'Lobster';
    }

![Figure 14.3](images/font.png)

素晴らしい！

上に示したように、CSSはHTMLコードの一部に名前をつけて、他に影響を与えずにこの部分にだけスタイルを適用するといった、クラスの概念を持っています。
あなたが2つのdiv要素を持っていた場合これは非情に便利でしょう。しかし、見出しと投稿のように、これらの要素は通常全く違う事を行います。そのため、あなたはこれらを区別して扱いたくなるでしょう。

先に進んで、HTMLコードの一部に名前をつけましょう。ヘッダーに含まれる`div`要素に、`page-header`というクラス名をつけましょう：

    <div class="page-header">
        <h1><a href="/">Django Girls Blog</a></h1>
    </div>

さらにブログ投稿を含む`div`要素に`post`というクラス名をつけましょう。

    <div class="post">
        <p>published: {{ post.published_date }}</p>
        <h1><a href="">{{ post.title }}</a></h1>
        <p>{{ post.text|linebreaks }}</p>
    </div>

そして、別のセレクタに宣言ブロックを追加します。`.`で始まるセレクタはクラスに関連します。
Web上にはCSSに関する非常に多くのチュートリアルが存在し、それらは以下に示すコードを理解する手助けになるはずです。今のところは、`djangogirls/static/css/blog.css`のファイルに以下の内容をコピー＆ペーストしましょう：

    .page-header {
        background-color: #ff9400;
        margin-top: 0;
        padding: 20px 20px 20px 40px;
    }

    .page-header h1, .page-header h1 a, .page-header h1 a:visited, .page-header h1 a:active {
        color: #ffffff;
        font-size: 36pt;
        text-decoration: none;
    }

    .content {
        margin-left: 40px;
    }

    h1, h2, h3, h4 {
        font-family: 'Lobster', cursive;
    }

    .date {
        float: right;
        color: #828282;
    }

    .save {
        float: right;
    }

    .post-form textarea, .post-form input {
        width: 100%;
    }

    .top-menu, .top-menu:hover, .top-menu:visited {
        color: #ffffff;
        float: right;
        font-size: 26pt;
        margin-right: 20px;
    }

    .post {
        margin-bottom: 70px;
    }

    .post h1 a, .post h1 a:visited {
        color: #000000;
    }

そして、これをクラス宣言で投稿を表示しているHTMLコードで囲みます。
`blog/templates/blog/post_list.html`中のこの部分を

    {% for post in posts %}
        <div class="post">
            <p>published: {{ post.published_date }}</p>
            <h1><a href="">{{ post.title }}</a></h1>
            <p>{{ post.text|linebreaks }}</p>
        </div>
    {% endfor %}

これで置き換えて下さい：

    <div class="content container">
        <div class="row">
            <div class="col-md-8">
                {% for post in posts %}
                    <div class="post">
                        <div class="date">
                            {{ post.published_date }}
                        </div>
                        <h1><a href="">{{ post.title }}</a></h1>
                        <p>{{ post.text|linebreaks }}</p>
                    </div>
                {% endfor %}
            </div>
        </div>
    </div>

それらのファイルを保存してWebサイトを更新してみましょう。

![Figure 14.4](images/final.png)

やったー！ほら凄いでしょ？この貼り付けたコードを理解するのはそんなに難しいことじゃありません。実際に読んでみることで、そのほとんどを理解することができるでしょう。

CSSをいじることを恐れないで下さい！たとえ何かを壊してしまっても、すぐに元に戻すことができます。

美しいWebサイトを作るために必要な全てのことを学ぶために、この無料のオンライン講座を受講することをおすすめします：[Codeacademy HTML & CSS course](http://www.codecademy.com/tracks/web)（※英語サイトです）

さて、次の章にいく準備はできましたか？^皿^
