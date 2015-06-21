# Djangoのインストール
> このチャプターの一部はGeek Girls Carrots (http://django.carrots.pl/)のチュートリアルに基づいています。

> このチャプターの一部はCreative Commons Attribution-ShareAlike 4.0 International License のライセンスによる[django-marcador tutorial](http://django-marcador.keimlink.de/)に基づいています。このdjango-marcador tutorialはMarkus Zapke-Gründemann et al.が著作権を保有しています。

## 仮想環境

Djangoをインストールする前に、まずはあなたのコンピュータの中のコーディング環境をきれいにしておくのに役立つとても便利な道具をインストールしてもらいます。このステップをとばすこともできますが、しかし、このステップをとばすことは全くお勧めしまません。可能な限りベストなセットアップで始めることは将来のたくさんのトラブルからあなたを救うはずですから！

さあ、**virtual environment** (*virtualenv*とも呼ばれています)を作りましょう。virtual environmentはプロジェクト単位であなたのPython/Djangoセットアップを他から隔離します。つまり、あなたがひとつのウェブサイトにおこなったどんな変更もあなたが開発中の他のサイトに影響を及ぼさないということです。わかりましたか？

あなたがしなければならないのは、あなたが'virtualenv'を作成したいディレクトリを見つけることです（たとえばホームディレクトリなどです）。Windowsでは、ホームディレクトリは`C:\Users\Name\`と書かれているかもしれません (`Name`はあなたのログインネームです)。

このチュートリアルのために、ホームディレクトリに新しいディレクトリ`djangogirls'を作成します。

    mkdir djangogirls
    cd djangogirls

`myvenv`というvirtualenvを作成します。一般的なコマンドは以下のようになります：

    python3 -m venv myvenv

### Windows

新しい`virtualenv`を作成するために、コンソールを開き（コンソールについては何章か前にお話ししましたね。覚えてますか？）、`C:\Python34\python -m venv myvenv`を実行して下さい。たとえばこのように入力します：

    C:\Users\Name\djangogirls> C:\Python34\python -m venv myvenv

`C:\Python34\python`はあなたがPythonをインストールしたディレクトリ、`myvenv`はあなたの'virtualenv'の名前です。どんな名前でも使うことができますが、必ず小文字で表記し、スペース・アクセント記号・特殊文字は入れないでください。短い名前にしておくのもいいアイデアですーあなたはこの名前を何度も参照しますから！

### Linux and OS X

LnuxやOX Xで'virtualenv'を作るときは、`python3 -m venv myvenv`と実行するだけです。

たとえばこんな感じです：

    ~/djangogirls$ python3 -m venv myvenv

`myvenv`はあなたの`virtualenv`の名前です。どんな名前でも使うことができますが、必ず小文字で表記し、スペースは入れないでください。短い名前にしておくのもいいアイデアですーあなたはこの名前を何度も参照しますから！

> __備考:__ この方法によるUbuntu 14.04でのvirtual environmentの初期化は次のエラーが出ます：

>     Error: Command '['/home/eddie/Slask/tmp/venv/bin/python3', '-Im', 'ensurepip', '--upgrade', '--default-pip']' returned non-zero exit status 1

> このエラーを回避するために、代わりに`virtualenv`コマンドを使います。

>     ~/djangogirls$ sudo apt-get install python-virtualenv
>     ~/djangogirls$ virtualenv --python=python3.4 myvenv


## virtualenvを使う

上に示したコマンドは仮想環境（基本的には一連のディレクトリとファイル）を含む`myvenv`という名前（あるいはあなたが選んだ名前）のディレクトリを生成します。次に我々がしたいのは、これを実行し、開始することです。

Windowsではこのように入力してください：

    C:\Users\Name\djangogirls> myvenv\Scripts\activate

あるいはOS X、Linuxでは以下のように入力して下さい：

    ~/djangogirls$ source myvenv/bin/activate

`myvenv`のところをあなたが選んだ`virtualenv`名に置き換えることを忘れないで下さいね！

> __備考:__ `source`ではできない場合もあります。その場合は、代わりに以下のように入力してみてください：

>     ~/djangogirls$ . myvenv/bin/activate


あなたのコンソールのプロンプトが以下のように表示されるのを見て、あなたは`virtualenv`が起動したことに気がつくでしょう。

    (myvenv) C:\Users\Name\djangogirls>

あるいはこういう表示かもしれません：

    (myvenv) ~/djangogirls$

行頭に`(myvenv)`が現れたのに注目して下さい！

virtual environment(仮想環境)の中で作業しているとき、`python`は自動的に正しいバージョンのPythonを参照しますので、'python3'の代わりに'python'を使うことができます。

OK、これでDjangoのインストール前に入れておきたい依存関係の準備がすべて整いました。いよいよDjangoのインストールです！

##Djangoのインストール

いまあなたの`virtualenv`は起動しているので、`pip`を使ってDjangoをインストールすることができます。コンソールの中で、`pip install django==1.8`(ここではダブルイコールサイン `==` を使います)と実行して下さい。

    (myvenv) ~$ pip install django==1.8
    Downloading/unpacking django==1.8
    Installing collected packages: django
    Successfully installed django
    Cleaning up...

Windowsの場合

> Windowsでpipを呼んだときにエラーが起きた場合は、あなたのプロジェクトのパス名がスペース・アクセント・特殊文字を含んでいないか確認してみて下さい (例 `C:\Users\User Name\djangogirls`)。もし含まれている場合は、そのディレクトリを他のスペース・アクセント・特殊文字が含まれていない場所（`C:\djangogirls`など）に移動することを検討してみてください。移動したあとに上記のコマンドを試してみてください。

Linuxの場合

> Ubuntu 12.04でpipを呼んだときにエラーが起きた場合は、virtualenv内でpipインストールをフィックスするために`python -m pip install -U --force-reinstall pip`を実行して下さい。

以上です！あなたは（ついに）Djangoアプリケーションを作成する準備が整いました！
