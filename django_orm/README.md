# DjangoのORMとクエリセット

この章では、Djangoのデータベース接続方法と、データストアについて学びます。やってみましょう！

## クエリセットとは？

クエリセットが何かと言うと、モデルが提供しているオブジェクトのリストのことです。クエリセットは、データベースからデータを読み込んだり、抽出したり、言われた通りにやってくれます。

実際に動かしてみるのが一番わかりやすいので、試してみましょう。

## Django shell

コンソール画面を開いて、次のコマンドを入力してみましょう。

    (myvenv) ~/djangogirls$ python manage.py shell

次のような表示に切り替わるでしょう。

    (InteractiveConsole)
    >>>

今、Djangoのインタラクティブコンソールが起動しています。Pythonプロンプトしかないように見えますが、ちゃんとDjangoも動いています。勿論このコンソール画面では、Pythonのコマンドは何でも使えます。

### All objects

最初に、ポストデータを全部表示させてみましょう。次のコマンドで、ポストのデータを全部表示させることが出来ます。

    >>> Post.objects.all()
    Traceback (most recent call last):
          File "<console>", line 1, in <module>
    NameError: name 'Post' is not defined

ごめんなさい、エラーになってしまいましたね。Postがないというエラーです。その通りなんです。最初にインポートをしなくてはならないのに、忘れていました。

    >>> from blog.models import Post

こんな風に書くだけで、`blog.models`から`Post`モデルをインポート出来ます。それでは、もう一度試してみましょう。

    >>> Post.objects.all()
    [<Post: my post title>, <Post: another post title>]

さっきDjangoの管理画面から作ったポストのリストが表示されました。だけど、次はこのコンソール画面から、新たにポストを作ってみたいですよね。それはどうすればいいのでしょうか。

### Create object

データベースに、新しいPostを作成するには、次のようにします。

    >>> Post.objects.create(author=me, title='Sample title', text='Test')

いい感じなのですが、1つだけマズイことをしているんです。authorに `me` を渡していますが、これは `User` モデルのインスタンスでないといけませんよね。それは、どうやればいいと思います？、

そうです、さっきと同じです。Userモデルも先にインポートしておきましょう。

    >>> from django.contrib.auth.models import User

どんなユーザが、データベースに登録されてましたっけ？覗いてみましょうか。

    >>> User.objects.all()
    [<User: ola>]

作成しておいたスーパーユーザがいますね。このユーザを使ってみましょう。

    me = User.objects.get(username='ola')

`ola` というユーザ名の `User` モデルのインスタンスを、取り出せたでしょう？よかった！勿論、他のユーザ名のユーザを取り出しても構いません。

さあ、遂にコンソール画面から、最初のポストを作成出来ますね。

    >>> Post.objects.create(author = me, title = 'Sample title', text = 'Test')

どうでしょうか？ちゃんと出来ているか、確認しておきましょうね。

    >>> Post.objects.all()
    [<Post: Sample title>]

### Add more posts

この先の楽しみの為にも、もう2〜3個、記事を作っておきましょう。そうすれば、もっとよくこの章を理解出来ると思います。

### Filter objects

クエリセットの大部分は、フィルタ機能だと言えるでしょう。ユーザolaさんのポストを全部確認してみましょうか。全部のポストを取り出すのではなく、olaさんのポストだけを取り出したい場合は、`Post.objects.all()` の `all` を `filter` に変更します。クエリセットの結果として、カッコの中に、blogの内容が一覧で表示されました。以下の例だと、 `author` が `me` と等しいものだけが抽出されています。

    >>> Post.objects.filter(author=me)
    [<Post: Sample title>, <Post: Post number 2>, <Post: My 3rd post!>, <Post: 4th title of post>]

もしかすると `title` フィールドに `title` という単語が含まれているポストだけを取り出したくなるかもしれませんね。

    >>> Post.objects.filter(title__contains='title')
    [<Post: Sample title>, <Post: 4th title of post>]

> **Note** `title` と `contains` の間に、アンダーバーが2個続いていますが、これはDjangoのORMの構文です。フィールド名のtitleと、照合タイプのcontainsを、2つのアンダーバーで連結させています。もしアンダーバーが1個だけだと、title_contains というフィールド名だと判断されてしまい、エラーになります。("FieldError: Cannot resolve keyword title_contains")

また、公開済みの全ポストを取り出すことも出来ます。全てのポストの中から、既に公開済みのポストを取り出してみましょう。それには、 `published_date` を指定します。


    >>> from django.utils import timezone
    >>> Post.objects.filter(published_date__lte=timezone.now())
    []

そうでした、残念なことに、まだどのポストも公開されていませんね。じゃあ、ポストを公開してみるとしましょう。まず公開するポストを決めましょう。

    >>> post = Post.objects.get(id=1)

そして、 `publish` メソッドを呼び出します。

    >>> post.publish()

じゃあ、もう一度公開済みのポストを取り出しましょう。(上方向キーを3回押せば、さっきのコマンドを呼び出せるでしょう。コマンドを表示出来たら、Enterキーを押してみましょう)

    >>> Post.objects.filter(published_date__lte=timezone.now())
    [<Post: Sample title>]

### Ordering objects

クエリーセットは、オブジェクトのリストの並べ替えもやってくれます。試しに `created_date` フィールドで並べ替えてみましょう。

    >>> Post.objects.order_by('created_date')
    [<Post: Sample title>, <Post: Post number 2>, <Post: My 3rd post!>, <Post: 4th title of post>]

逆順、つまり新しく追加した順に並べ替えることもできます。それには、`-` ハイフンを使います。

    >>> Post.objects.order_by('-created_date')
    [<Post: 4th title of post>,  <Post: My 3rd post!>, <Post: Post number 2>, <Post: Sample title>]

どうです？次の章への準備は万端ですね！このプロンプトを閉じるには、以下のようにします。

    >>> exit()
    $
