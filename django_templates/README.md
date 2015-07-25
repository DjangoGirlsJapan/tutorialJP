# Djangoテンプレート

何かデータを表示しましょう！Djangoはそれをビルトインの __テンプレートタグ__ で実現できます。

## テンプレートタグとは？

HTMLではブラウザがpythonを認識できないのでpythonのコードは書けません。HTMLはより静的でpythonは動的です。

__Djangoテンプレートタグ__ はHTMLにPyhtonのようなコードを埋め込むことができて、動的なウェブサイトがより早く簡単に作れます!

## ブログ一覧テンプレート

前の章で、posts変数でテンプレートに記事のリストを渡しました。今からHTMLで表示をしてみましょう。

Djangoテンプレートで変数を表示する為には、変数の名前を二重括弧で括ります:

    {{ posts }}

これを`blog/templates/blog/post_list.html`に書いてみて下さい。（２つめと３つ目の`<div></div>`タグをまるごと `{{posts}}` に置き換えて下さい。）ファイルを保存してページをリロードしますと：

![Figure 13.1](images/step1.png)

見たとおり、このようになります。

    [<Post: My second post>, <Post: My first post>]

Djangoはオブジェクトのリストと認識します。__Introduction to Python__を思い出して下さい。ループを使ってリストを表示しましたよね。Djangoテンプレートではこう書きます:

    {% for post in posts %}
        {{ post }}
    {% endfor %}

これをブログのテンプレートで使ってみましょう。

![Figure 13.2](images/step2.png)

動きましたね。しかし、__Introduction to HTML__で作った静的な記事のような表示です。HTMLとテンプレートタグを混ぜてみましょう。bodyタグの中を次のように書いてください:

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

`{% for %}`と`{% endfor %}`の間にリストの中のオブジェクトごとに表示したい内容を書くとオブジェクトの数だけ繰り返し書かれます。ページをリロードしてみましょう。

![Figure 13.3](images/step3.png)

`post` 変数がさっきと違って、`{{ post.title }}` や `{{ post.text }}` になっていることに気づきましたか？ `Post` モデルで定義したそれぞれのフィールドにアクセスしています。`|linebreaks` はPostのテキスト中の改行を段落に変換するフィルタに通すという意味です。

## もう一つ...

PythonAnywhereでデプロイして、インターネットでウェブサイトを公開できます。おさらいしましょう。

$ git status
[...]
$ git add -A .
$ git status
[...]
$ git commit -m "Added views to create/edit blog post inside the site."
[...]
$ git push

そしたら、Pythonanywhereに戻って、Bashコンソール（か、新しいコンソール）に入って、動かしましょう：

$ cd my-first-blog
$ git pull
[...]

最後にブラウザのタブを開いてアプリをリロードします。更新が反映されています！

おめでとう！これができたら、Django adminとして新しい投稿を追加しましょう。（published_dateを忘れないで！）それから、投稿したものがそこに見えるか、リロードしましょう。

動くのが楽しくなってきたでしょう？少しパソコンから離れて、休憩しましょう：）

![Figure 13.4](images/donut.png)
