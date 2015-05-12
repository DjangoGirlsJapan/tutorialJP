# ジャンゴ クエリセット

ポスト内容を保存する為の `Post` モデルは、 `models.py` に定義しました。ポストの一覧を表示する `post_list` は `views.py` にあり、そこにテンプレートも加わりました。これらを準備しましたが、実際のところ、ポストをどうやってHTMLファイルに出力すればいいのでしょうか？大まかなイメージとしては、データベースに保存された幾つかの記事を取り出して、テンプレートのHTMLファイルの中に行儀よく並べるだけのことですけど。

正確には、 *ビューが* モデルとテンプレートの橋渡しをしてくれます。私達が作業している `post_list` *ビュー* の場合、表示したいデータを取り出して、テンプレートファイルに渡すことになります。基本的に、どのモデルのデータを、どのテンプレートに表示させるかは、 *ビューに* 記述します。

それでは、実際にやってみましょう。

まず `blog/views.py` を開きます。今のところ `post_list` *ビュー* は、以下のようになっているでしょう。

    from django.shortcuts import render

    def post_list(request):
        return render(request, 'blog/post_list.html', {})

少し前に、別のファイルに用意したコードをどうやってインクルードするか説明したのですけれど、覚えていますか？それでは `models.py` のモデルを、インクルードしてみましょう。 `from .models import Post` という行を追加してみます。

    from django.shortcuts import render
    from .models import Post

`from` の後のドットは `カレントディレクトリ` 、もしくは `カレントアプリケーション` のことです。 `views.py` と `models.py` は、同じディレクトリに置いてありますから、こんな風にドットとファイル名だけを使って、簡単に記述することが出来るのです。ただし、ファイル名に拡張子 `.py` は必要ないですけど。そして、モデルの名前を指定してインポートします(この場合のモデルは `Post` ですね)

さて、次にすべきことは、実際に `Post` モデルからブログの記事を取り出すことですが、それには `クエリセット` が必要です。

## クエリセット

もう、クエリセットの働きについては、知っていますよね。[Django ORM (QuerySets) chapter](../django_orm/README.md) で勉強しましたから。

ブログのポストをリストで取得するやり方については、どうでしょう？既に公開済みのもので、 `published_date` で並べ替えをしたリストですよ。これも、QuerySetsの章でやりましたから、大丈夫でしょう？

    Post.objects.filter(published_date__lte=timezone.now()).order_by('published_date')

そう、このコードですよね。これを `blog/views.py` の `post_list(request)関数` の中に加えてみましょう。

    from django.shortcuts import render
    from django.utils import timezone
    from .models import Post

    def post_list(request):
        posts = Post.objects.filter(published_date__lte=timezone.now()).order_by('published_date')
        return render(request, 'blog/post_list.html', {})

作成したクエリセットは、 *変数* `posts` で参照できることに、注意しましょう。この *変数* `posts` を使って、クエリセットのデータにアクセスします。これから先 `posts` というと、このクエリセットのことです。

最後に一点、クエリセットを参照している変数 `posts` をテンプレートに渡すという作業が、出来ていませんが、これは次の章でやりましょう。

`render` 関数では、既にパラメータとして `request` とテンプレートファイル `blog/post_list.html` が渡されています。リクエストというのは、インターネットを介してユーザから受け取った全ての情報の詰まったものです。最後のパラメータに注目してください。 `{}` こんな風に書かれていますね。この中に指定した情報を、テンプレートが表示してくれます。 `{}` の中に引数を記述する時は、名前と値をセットにしなくてはなりません。表示させたいのはクエリセットのデータなので、 `posts` を指定しましょう。こんな風に、記述することになります。 `{'posts': posts}` 注意して欲しいのは、シングルクォートです。 `コロン` で区切られた、前の方の `posts` は、 `シングルクォート` で囲まれて、 `'posts'` になっていますよね。こちらが名前で、後ろの方の posts は値、クエリセットのことです。

最終的に `blog/views.py` は、以下の様になるはずです。

    from django.shortcuts import render
    from django.utils import timezone
    from .models import Post

    def post_list(request):
        posts = Post.objects.filter(published_date__lte=timezone.now()).order_by('published_date')
        return render(request, 'blog/post_list.html', {'posts': posts})

どうでしたか？次は、このクエリセットをテンプレートで表示させるところを、やってみましょう。

Djangoのクエリセットについて、もっと知りたければ、英語のドキュメントですが、こちらも読んでみてくださいね。 https://docs.djangoproject.com/en/1.8/ref/models/querysets/


