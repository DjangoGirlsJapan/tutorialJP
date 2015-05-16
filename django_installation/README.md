# Django installation
#Djangoのインストール
> Part of this chapter is based on tutorials by Geek Girls Carrots (http://django.carrots.pl/).> このチャプターの一部はGeek Girls Carrots (http://django.carrots.pl/)のチュートリアルに基づいています。

> Part of this chapter is based on the [django-marcador 
tutorial](http://django-marcador.keimlink.de/) licensed under Creative Commons
Attribution-ShareAlike 4.0 International License. The django-marcador tutorial
is copyrighted by Markus Zapke-Gr端ndemann et al.

> このチャプターの一部はCreative Commons Attribution-ShareAlike 4.0 International License のライセンスによる[django-marcador tutorial](http://django-marcador.keimlink.de/)に基づいています。このdjango-marcador tutorialはMarkus Zapke-Gr端ndemann et al.が著作権を保有しています。

## Virtual environment
## 仮想環境

Before we install Django, we'll get you to install an extremely useful tool that will help keep your coding environment tidy on your computer. It's possible to skip this step, but it's highly recommended not to - starting with the best possible setup will save you a lot of trouble in the future!

Djangoをインストールする前に、まずはあなたのコンピュータの中のコーディング環境をきれいにしておくのに役立つとても便利な道具をインストールしてもらいます。このステップをとばすこともできますが、しかし、このステップをとばすことは全くお勧めしまません。可能な限りベストなセットアップで始めることは将来のたくさんのトラブルからあなたを救うはずですから！

So, let's create a **virtual environment** (also called a *virtualenv*). It will isolate your Python/Django setup on a per-project basis, meaning that any changes you make to one website won't affect any others you're also developing. Neat, right?

さあ、**virtual environment** (*virtualenv*とも呼ばれています)を作りましょう。virtual environmentはプロジェクト単位であなたのPython/Djangoセットアップを他から隔離します。つまり、あなたがひとつのウェブサイトにおこなったどんな変更もあなたが開発中の他のサイトに影響を及ぼさないということです。わかりましたか？

All you need to do is find a directory in which you want to create the `virtualenv`; your home directory, for example. On Windows it might look like `C:\Users\Name\` (where `Name` is the name of your login).

あなたがしなければならないのは、あなたが'virtualenv'を作成したいディレクトリを見つけることです（たとえばホームディレクトリなどです）。Windowsでは、ホームディレクトリは`C:\Users\Name\`と書かれているかもしれません (`Name`はあなたのログインネームです)。

For this tutorial we will be using a new directory `djangogirls` from your home directory:

このチュートリアルのために、ホームディレクトリに新しいディレクトリ`djangogirls'を作成します。

    mkdir djangogirls
    cd djangogirls

We will make a virtualenv called `myvenv`. The general command will be in the format:

`myvenv`というvirtualenvを作成します。一般的なコマンドは以下のようになります：

    python3 -m venv myvenv

### Windows

To create a new `virtualenv`, you need to open the console (we told you about that a few chapters ago - remember?) and run `C:\Python34\python -m venv myvenv`. It will look like this:

新しい`virtualenv`を作成するために、コンソールを開き（コンソールについては何章か前にお話ししましたね。覚えてますか？）、`C:\Python34\python -m venv myvenv`を実行して下さい。たとえばこのように入力します：

    C:\Users\Name\djangogirls> C:\Python34\python -m venv myvenv

where `C:\Python34\python` is the directory in which you previously installed Python and `myvenv` is the name of your `virtualenv`. You can use any other name, but stick to lowercase and use no spaces, accents or special characters. It is also good idea to keep the name short - you'll be referencing it a lot!

`C:\Python34\python`はあなたがPythonをインストールしたディレクトリ、`myvenv`はあなたの'virtualenv'の名前です。どんな名前でも使うことができますが、必ず小文字で表記し、スペース・アクセント記号・特殊文字は入れないでください。短い名前にしておくのもいいアイデアですーあなたはこの名前を何度も参照しますから！

### Linux and OS X

Creating a `virtualenv` on both Linux and OS X is as simple as running `python3 -m venv myvenv`.

LnuxやOX Xで'virtualenv'を作るときは、`python3 -m venv myvenv`と実行するだけです。

It will look like this:

たとえばこんな感じです：

    ~/djangogirls$ python3 -m venv myvenv

`myvenv` is the name of your `virtualenv`. You can use any other name, but stick to lowercase and use no spaces. It is also good idea to keep the name short - you'll be referencing it a lot!

`myvenv`はあなたの`virtualenv`の名前です。どんな名前でも使うことができますが、必ず小文字で表記し、スペースは入れないでください。短い名前にしておくのもいいアイデアですーあなたはこの名前を何度も参照しますから！

> __NOTE:__ Initiating the virtual environment on Ubuntu 14.04 like this currently gives the following error:

> __備考:__ この方法によるUbuntu 14.04でのvirtual environmentの初期化は次のエラーが出ます：

>     Error: Command '['/home/eddie/Slask/tmp/venv/bin/python3', '-Im', 'ensurepip', '--upgrade', '--default-pip']' returned non-zero exit status 1

> To get around this, use the `virtualenv` command instead.

> このエラーを回避するために、代わりに`virtualenv`コマンドを使います。

>     ~/djangogirls$ sudo apt-get install python-virtualenv
>     ~/djangogirls$ virtualenv --python=python3.4 myvenv


## Working with virtualenv
## virtualenvを使う

The command above will create a directory called `myvenv` (or whatever name you chose) that contains our virtual environment (basically a bunch of directory and files). All we want to do now is start it by running:

上に示したコマンドは仮想環境（基本的には一連のディレクトリとファイル）を含む`myvenv`という名前（あるいはあなたが選んだ名前）のディレクトリを生成します。次に我々がしたいのは、これを実行し、開始することです。

Windowsではこのように入力してください：

    C:\Users\Name\djangogirls> myvenv\Scripts\activate

on Windows, or:

あるいはOS X、Linuxでは以下のように入力して下さい：

    ~/djangogirls$ source myvenv/bin/activate

on OS X and Linux.

Remember to replace `myvenv` with your chosen `virtualenv` name!
`myvenv`のところをあなたが選んだ`virtualenv`名に置き換えることを忘れないで下さいね！

> __NOTE:__ sometimes `source` might not be available. In those cases try doing this instead:
> __備考:__ ときどき`source`は利用できないかもしれません。その場合は、代わりに以下のように入力してみてください：

>     ~/djangogirls$ . myvenv/bin/activate



You will know that you have `virtualenv` started when you see that the prompt in your console looks like:

あなたのコンソールのプロンプトが以下のように表示されるのを見て、あなたは`virtualenv`が起動したことに気がつくでしょう。

    (myvenv) C:\Users\Name\djangogirls>

or:
あるいはこういう表示かもしれません：

    (myvenv) ~/djangogirls$

Notice the prefix `(myvenv)` appears!

行頭に`(myvenv)`が現れたのに注目して下さい！

When working within a virtual environment, `python` will automatically refer to the correct version so you can use `python` instead of `python3`.

virtual environment(仮想環境)の中で作業しているとき、`python`は自動的に正しいバージョンのPythonを参照しますので、'python3'の代わりに'python'を使うことができます。

OK, we have all important dependencies in place. We can finally install Django!

OK、我々は全ての重要な関連項目を配置しました。ついにDjangoをインストールすることができます！

## Installing Django
##Djangoのインストール
Now that you have your `virtualenv` started, you can install Django using `pip`. In the console, run `pip install django==1.8` (note that we use a double equal sign: `==`).

いまあなたの`virtualenv`は起動しているので、'pip'を使ってDjangoをインストールすることができます。コンソールの中で、`pip install django==1.8`(ここではダブルイコールサイン `==` を使います)と実行して下さい。

    (myvenv) ~$ pip install django==1.8
    Downloading/unpacking django==1.8
    Installing collected packages: django
    Successfully installed django
    Cleaning up...

on Windows

Windowsの場合

> If you get an error when calling pip on Windows platform please check if your project pathname contains spaces, accents or special characters (i.e. `C:\Users\User Name\djangogirls`). If it does please consider moving it to another place without spaces, accents or special characters (suggestion is: `C:\djangogirls`). After the move please try the above command again.

> Windowsでpipを呼んだときにエラーが起きた場合は、あなたのプロジェクトのパス名がスペース・アクセント・特殊文字を含んでいないか確認してみて下さい (例 `C:\Users\User Name\djangogirls`)。もし含まれている場合は、そのディレクトリを他のスペース・アクセント・特殊文字が含まれていない場所（`C:\djangogirls`など）に移動することを検討してみてください。移動したあとに上記のコマンドを試してみてください。

on Linux

Linuxの場合

> If you get an error when calling pip on Ubuntu 12.04 please run `python -m pip install -U --force-reinstall pip` to fix the pip installation in the virtualenv.

> Ubuntu 12.04でpipを呼んだときにエラーが起きた場合は、virtualenv内でpipインストールをフィックスするために`python -m pip install -U --force-reinstall pip`を実行して下さい。

That's it! You're now (finally) ready to create a Django application!

以上です！あなたは（ついに）Djangoアプリケーションを作成する準備が整いました！