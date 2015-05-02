# CSS - make it pretty!

ブログはつくりましたが、このままだとカッコ良くないですよね。カッコよくしていきましょう。ここからはCSSを使っていきます。

## What is CSS?

Cascading Style Sheets (CSS)とは、HTMLなどのマークアップ言語で書かれたWebサイトの見た目や書式を記述するための言語です。私達のWebページをメイクアップするものとして扱います。

でも、またゼロから作りたくないですよね。プログラマーたちがすでに作って無料で公開しているツールを使いましょう。わざわざイチから作り直す必要はないですからね。

## Let's use Bootstrap!

Bootstrap は美しいWebサイトを開発するためのHTMLとCSSのフレームワークとしてとても有名です: http://getbootstrap.com/

これは、もともとTwitterのプログラマーが作成したもので、今は、世界中の有志のボランティアで開発されています。

## Install Bootstrap

Bootstrapをインストールするには、 `.html` ファイル (`blog/templates/blog/post_list.html`)　の`<head>` の中に、次のとおり書き加えてください。:

    <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
    <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">


これは、あなたのプロジェクトにはファイルを追加していません。インターネット上にあるファイルを指しているだけです。
では、Webサイトを開いてページを再読み込みしてください。

![Figure 14.1](images/bootstrap1.png)

これだけで見た目がずいぶん良くなりましたね！

## Static files in Django

もう１つ、今日ここで学ぶことは、 __静的ファイル__ です. 静的ファイルとは、CSSファイルや画像ファイルといった、Static files are all your CSS and images -- files that are not dynamic, so their content doesn't depend on request context and will be the same for every user.

CSS is a static file, so in order to customize CSS, we need to first configure static files in Django. You'll only need to do it once. Let's start:

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
            blog.css

Time to write some CSS! Open up the `static/css/blog.css` file in your code editor.

We won't be going too deep into customizing and learning about CSS here, because it's pretty easy and you can learn it on your own after this workshop. We really recommend doing this [Codeacademy HTML & CSS course](http://www.codecademy.com/tracks/web) to learn everything you need to know about making your websites more pretty with CSS.

But let's do at least a little. Maybe we could change the color of our header? To understand colors, computers use special codes. They start with `#` and are followed by 6 letters (A-F) and numbers (0-9). You can find color codes for example here: http://www.colorpicker.com/. You may also use [predefined colors](http://www.w3schools.com/cssref/css_colornames.asp), such as `red` and `green`.

 `static/css/blog.css` ファイルに、次のコードを記述しましょう。

    h1 a {
        color: #FCA205;
    }

`h1 a` はCSSセレクタです。`h1` 要素の中にある`a` 要素 （例：このようなコードのこと `<h1><a href="">link</a></h1>`）にスタイルを適用します、という意味になります。この場合、テキストの色を`#FCA205`、オレンジ色にする、という意味です。もちろん、あなたの好きな色に変更してもいいですよ。

CSSファイルで、HTMLの各要素のスタイルを指定していきます。 The elements are identified by the element name (i.e. `a`, `h1`, `body`), the attribute `class` or the attribute `id`. Class and id are names you give the element by yourself. Classes define groups of elements, and ids point to specific elements. For example, the following tag may be identified by CSS using the tag name `a`, the class `external_link`, or the id `link_to_wiki_page`:

    <a href="http://en.wikipedia.org/wiki/Django" class="external_link" id="link_to_wiki_page">

Read about [CSS Selectors in w3schools](http://www.w3schools.com/cssref/css_selectors.asp).

Then, we need to also tell our HTML template that we added some CSS. Open the `blog/templates/blog/post_list.html` file and add this line at the very beginning of it:

    {% load staticfiles %}

We're just loading static files here :). Then, between the `<head>` and `</head>`, after the links to the Bootstrap CSS files (the browser reads the files in the order they're given, so code in our file may override code in Bootstrap files), add this line:

    <link rel="stylesheet" href="{% static 'css/blog.css' %}">

これで、テンプレートにCSSファイルがある場所を教えたわけです。

あなたのファイルは、このようになっていますか:

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

OK, save the file and refresh the site!

![Figure 14.2](images/color2.png)

Nice work! Maybe we would also like to give our website a little air and increase the margin on the left side? Let's try this!

    body {
        padding-left: 15px;
    }

Add this to your CSS, save the file and see how it works!

![Figure 14.3](images/margin2.png)

Maybe we can customize the font in our header? Paste this into your `<head>` in `blog/templates/blog/post_list.html` file:

    <link href="http://fonts.googleapis.com/css?family=Lobster&subset=latin,latin-ext" rel="stylesheet" type="text/css">

This line will import a font called *Lobster* from Google Fonts (https://www.google.com/fonts).

Now add the line `font-family: 'Lobster';` in the CSS file `static/css/blog.css` inside the `h1 a` declaration block (the code between the braces `{` and `}`)  and refresh the page:

    h1 a {
        color: #FCA205;
        font-family: 'Lobster';
    }

![Figure 14.3](images/font.png)

Great!


As mentioned above, CSS has a concept of classes, which basically allows you to name a part of the HTML code and apply styles only to this part, not affecting others. It's super helpful if you have two divs, but they're doing something very different (like your header and your post), so you don't want them to look the same.

Go ahead and name some parts of the HTML code. Add a class called `page-header` to your `div` that contains your header, like this:

    <div class="page-header">
        <h1><a href="/">Django Girls Blog</a></h1>
    </div>

And now add a class `post` to your `div` containing a blog post.

    <div class="post">
        <p>published: {{ post.published_date }}</p>
        <h1><a href="">{{ post.title }}</a></h1>
        <p>{{ post.text|linebreaks }}</p>
    </div>

We will now add declaration blocks to different selectors. Selectors starting with `.` relate to classes. There are many great tutorials and explanations about CSS on the Web to help you understand the following code. For now, just copy and paste it into your `djangogirls/static/css/blog.css` file:

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

Then surround the HTML code which displays the posts with declarations of classes. Replace this:

    {% for post in posts %}
        <div class="post">
            <p>published: {{ post.published_date }}</p>
            <h1><a href="">{{ post.title }}</a></h1>
            <p>{{ post.text|linebreaks }}</p>
        </div>
    {% endfor %}

in the `blog/templates/blog/post_list.html` with this:

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

Save those files and refresh your website.

![Figure 14.4](images/final.png)

Woohoo! Looks awesome, right? The code we just pasted is not really so hard to understand and you should be able to understand most of it just by reading it.

Don't be afraid to tinker with this CSS a little bit and try to change some things. If you break something, don't worry, you can always undo it!

Anyway, we really recommend taking this free online [Codeacademy HTML & CSS course](http://www.codecademy.com/tracks/web) as some post-workshop homework to learn everything you need to know about making your websites prettier with CSS.

Ready for the next chapter?! :)
