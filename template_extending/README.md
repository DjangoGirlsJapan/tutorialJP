# テンプレートの拡張

Djangoの便利な機能の一つに、 __テンプレートの拡張機能__ があります。ウェブサイトを作る時、どのページでも同じHTMLタグを使うことがありますよね。たとえば、ヘッダーやフッター部分は、どのページでも同じものを使いませんか？そういう時に、便利な機能です。

この機能を使えば、ウェブサイトの共通部分(ヘッダーやフッター、メニューバーなど)に変更を加えたい時、全てのHTMLファイルに対して、同じ作業を繰り返さなくてすみます。一箇所だけ変更すれば、その変更は全てのページに適用されます。

## ベースとなる骨組みのテンプレートファイルの作成

ベーステンプレートは、ウェブサイトの全てのページの骨組みともいうべきテンプレートです。

`blog/templates/blog/` に、 `base.html` というファイル名で、ベーステンプレートファイルを作ってみましょう。

    blog
    └───templates
        └───blog
                base.html
                post_list.html

`base.html` ファイルを開いて `post_list.html` の内容を全部 `base.html` にコピーしたら、以下の様になるでしょう。

    {% load staticfiles %}
    <html>
        <head>
            <title>Django Girls blog</title>
            <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
            <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap-theme.min.css">
            <link href='//fonts.googleapis.com/css?family=Lobster&subset=latin,latin-ext' rel='stylesheet' type='text/css'>
            <link rel="stylesheet" href="{% static 'css/blog.css' %}">
        </head>
        <body>
            <div class="page-header">
                <h1><a href="/">Django Girls Blog</a></h1>
            </div>

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
        </body>
    </html>

コピーしたら `BODYタグ` 部分を、以下の内容に書き換えましょう。 `BODYタグ` は、わかりますよね？  `<body>` から `</body>` までの部分のことですよ。

    <body>
        <div class="page-header">
            <h1><a href="/">Django Girls Blog</a></h1>
        </div>
        <div class="content container">
            <div class="row">
                <div class="col-md-8">
                {% block content %}
                {% endblock %}
                </div>
            </div>
        </div>
    </body>

続いて `{% for post in posts %}{% endfor %}` という部分も、以下の様に書き換えましょう。

    {% block content %}
    {% endblock %}

どうしてこんな風に書くのか、考えてみましょう。 `base.html` に `block タグ` を記述しました。そうすると、別のテンプレートの内容を、この `block タグ` の部分に挿入することが出来るようになります。これが、テンプレートの拡張です。それでは、この `block タグ` に挿入する `post_list.html` も修正してみましょう。

`base.html` を保存して `blog/templates/blog/post_list.html` を開きましょう。まず、BODYタグの中身以外は全て削除してしまいます。 `<div class="page-header"></div>` も削除してしまって、最終的には以下の様にします。

    {% for post in posts %}
        <div class="post">
            <div class="date">
                {{ post.published_date }}
            </div>
            <h1><a href="">{{ post.title }}</a></h1>
            <p>{{ post.text|linebreaks }}</p>
        </div>
    {% endfor %}

修正出来たら、次の行をファイルの先頭に書き加えましょう。

    {% extends 'blog/base.html' %}

こんな風にすると `base.html` の `block` 部分に `post_list.html` を組み込んで使うことが出来るという訳です。実際に `block` 部分に組み込むには、以下の様に `{% block content %}` と `{% endblock content %}` タグで囲わなくてはなりません。

    {% extends 'blog/base.html' %}

    {% block content %}
        {% for post in posts %}
            <div class="post">
                <div class="date">
                    {{ post.published_date }}
                </div>
                <h1><a href="">{{ post.title }}</a></h1>
                <p>{{ post.text|linebreaks }}</p>
            </div>
        {% endfor %}
    {% endblock content %}

うまくテンプレート機能が動作しているか、ウェブサイトにを開いて確認してみましょう。

> `blog/base.html` が見当たらない場合、 `TemplateDoesNotExists` のエラーが出るかもしれません。その場合は、コンソールで動いている `runserver` を一旦止めてみましょう。停止させるには、コントロールボタンとCボタンを同時に押し、もう一度起動させるには `python manage.py runserver` コマンドを使います。
