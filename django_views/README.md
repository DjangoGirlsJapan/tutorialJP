# Django views - time to create!

それでは前の章の続きをやりましょう。確かビューの作成がまだだったので、エラーになっていましたね。

*ビュー* はアプリのロジックを担当しています。ビューは要求に応じて `model` から情報を取得し `template` に渡します。モデルはついさっき作りましたし、テンプレートもすぐ次の章で作ります。ビューは、Pythonで記述されているだけです。__Introduction to Python__ の章でやったことよりも、ちょっと複雑なだけですよ。

ビューは、`views.py` に記述します。私達の場合 `blog/views.py` に書くことになります。

## blog/views.py

では、早速 blog/views.py を開いてみましょう。

    from django.shortcuts import render

    # Create your views here.

まだ何もないですね。とりあえず、次のような、ちょっとした *ビュー* を作ってみましょう。

    def post_list(request):

        return render(request, 'blog/post_list.html', {})

よく見てみましょうか。まず `post_list` というメソッド( `def` から始まる部分のことです)を、記述しています。この `post_list` は `request` を引数に取り、`render` メソッドを `return` しています。`render` メソッドは `blog/post_list.html` というテンプレートファイルを使って、引数で受け取った `request` の内容を出力しています。

ファイルを保存したら、どんな風に表示されるか、ブラウザで http://127.0.0.1:8000/ を確認してみましょう。

今度は別のエラーになりましたね。なんと書いてあるでしょうか。

![Error](images/error.png)

この *TemplatedoesNoteExist* エラーの解決は、簡単です。テンプレートファイルがないだけなので、それでは次の章でテンプレートを作ってみましょう！

> Djangoのビューについてもっと知りたいのなら、英語で書かれていますが、オフィシャルドキュメントを是非読んでみてください：https://docs.djangoproject.com/en/1.8/topics/http/views/
