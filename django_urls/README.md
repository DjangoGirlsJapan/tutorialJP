# Django urls

最初のウェブページを立てましょう、あなたのブログです。始めに、djangoのURLについて少し学びましょう。

## What is a URL?

URLは簡単に言えばWEB上のアドレスです。サイトのURLは、ブラウザのアドレスバーで見ることができます。（そう、`127.0.0.1:8000` や [http://djangogirls.com](http://djangogirls.com) がURLです。）

![Url](images/url.png)

インターネットの全てのページはURLを持っています。それによって、これから作るアプリケーションが、URLを指定してアクセスしてきたユーザに、何を見せたらいいのかわかるのです。Djangoでは`URL_conf`（URL設定）と呼ばれるものを使います。これは、指定されたURLに合わせてDjangoがどのviewを返したらいいか判断する仕組みのことです。

## How do URLs work in Django?

`mysite/urls.py`を開いて、中身をみてみると：

```
from django.conf.urls import include, url
from django.contrib import admin

urlpatterns = [
    # Examples:
    # url(r'^$', 'mysite.views.home', name='home'),
    # url(r'^blog/', include('blog.urls')),

    url(r'^admin/', include(admin.site.urls)),
]
```

ご覧のとおり、Djangoは既にこのようなものを置いてくれています。

`#`で始まっている行はコメント行です。これはPythonによって実行されない行です。とっても便利でしょう？

前の章で訪れたadminのURLについてはすでに書いてありますね。

```
url(r'^admin/', include(admin.site.urls)),
```

`admin/`で始まる全てのURLについて、Djangoが返すべき_view_をこの行で指定しています。今回の場合、adminで始まるURLをたくさん作ることになりますが、その全てをこの小さいファイルに書くようなことはしません。この方がきれいで読みやすいですし。

## Regex

どのやってDjangoはビューにURLをマッチするのかと思うかもしれません。そうです、この部分はひとひねりしています。Djangoは`regex`、正規表現を使います。Regexは多くの（本当に多くの）検索パターンのルールを持っています。理解するのは簡単では無いですが、今は心配しないで下さい。将来、それらを正確に理解できるでしょう。今回は必要なものだけ使っています。

あんまり悩まないですむような簡単な例で説明しますね。  
`http://www.mysite.com/post/12345/`のようなアドレスを持つウェブサイトがあるとします。ここで、`12345`はブログポストの番号です。ブログポストの番号ごとに、それぞれ別々のviewを書くなんて絶対無理ですよね。Djangoでは`http://www.mysite.com/post/<a number>/`と書くだけで、後は全部お任せできるんです！

## Your first Django url!

さあ最初のURLを作りましょう！'[http://127.0.0.1:8000/](http://127.0.0.1:8000/)' はブログの入口ページなので、投稿したブログポストのリストを表示したいです。

`mysite/urls.py` ファイルは簡潔なままにしておきたいので、`mysite/urls.py`では`blog`アプリからURLをインポートするだけにしましょう。

コメントされた行（`#`で始まる行）を消して、入口ページのURL（'```'）には``blog.urls\`をインポートするように書いてください。

`mysite/urls.py`ファイルはこのようになります：

```
from django.conf.urls import include, url
from django.contrib import admin

urlpatterns = [
    url(r'^admin/', include(admin.site.urls)),
    url(r'', include('blog.urls')),
]
```

これでDjangoは '[http://127.0.0.1:8000/](http://127.0.0.1:8000/)' に来たリクエストは`blog.urls`へリダイレクトするようになり、それ以降はそちらを参照するようになります。

## blog.urls

新しく`blogs/urls.py`という空のファイルを作って下さい。そして最初の2行を以下のように書きます：

```
from django.conf.urls import include, url
from . import views
```

これはDjangoのメソッドと、`blog`アプリの全てのビュー（といっても、今は一つもありません。すぐに作りますけど！）をインポートするという意味です。

その後、最初のURLパターンを追加します。

```
urlpatterns = [
    url(r'^$', views.post_list),
]
```

これは`^$`というパターンのURLを`post_list`というビューに割り当てたことを意味します。`^$` とは何を意味しているのでしょうか。それは正規表現のマジックです:）分解してみましょう：

* 正規表現での`^`は「文字列の開始」を意味します。ここからパターンマッチを始めます。
* `$`は「文字列の終端」を意味していて、ここでパターンマッチを終わります。

この2つの記号を並べたパターンがマッチするのは、そう、空の文字列です。といっても、DjangoのURL名前解決では '[http://127.0.0.1:8000/](http://127.0.0.1:8000/)' は除いてパターンマッチするので、このパターンは '[http://127.0.0.1:8000/](http://127.0.0.1:8000/)' 自体を意味します。つまり、'[http://127.0.0.1:8000/](http://127.0.0.1:8000/)' というURLにアクセスしてきたユーザに対して`views.post_list`を返すように指定していることになります。

いいですか？ [http://127.0.0.1:8000/](http://127.0.0.1:8000/) を開いて結果を見てみましょう。

![Error](images/error1.png)![](/django_urls/images/error1.png)

どう見ても「うまく動いた」感じはしませんね。でも心配しないで、これはただのエラーページで、怖がるものではありません。むしろ、結構便利なものなんですよ：

'post\_list'というアトリビュートがない、と書いてあるのが見えますね。_post\_list_ と聞いて、何か思い出しませんか？そう、さっきこのURLに、ビューの`post_list`を割り当てたのでした。でも、_ビュー_ をまだ作ってないんですから、このエラーが出るのは当然ですよね。なにもおかしいことはしていません。次の章ではビューを作っていきましょう。

> Django URLconfについて知りたい場合は、公式のドキュメントを見て下さい： [https://docs.djangoproject.com/ja/1.11/topics/http/urls/](https://docs.djangoproject.com/ja/1.11/topics/http/urls/)



