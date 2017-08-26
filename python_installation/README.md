# Let’s start with Python {#lets-start-with-python}

ついにここまで来ました！

まずは、最初にPythonとは何かお話させて下さいね。Pythonはとても人気のあるプログラミング言語です。Webサイトや、ゲーム、サイエンス、グラッフィックス、などなど、たくさんの場面で使われています。

Pythonは1980年台の終わりに、人間が読みやすい（機械だけでなく）言語を目的に開発されました。だから、他の言語に比べて、Pythonはとてもシンプルで、勉強しやすいのです。でもご心配なく、Pythonはとってもパワフルな言語でもありますから！

# Python installation

> **Note** このセクションは、Geek Girls Carrots \([http://django.carrots.pl/\)のチュートリアルをもとに作成されています。](http://django.carrots.pl/%29のチュートリアルをもとに作成されています。)

Django は、Pythonで開発されています。なにをするにせよ、まずはPythonが必要です。インストールしましょう！ Python 3.5 をインストールします。3.5以前のバージョンをインストール済みの場合は、アップグレードしてください。

# Python installation {#python-installation}

> **Note**If you're using a Chromebook, skip this chapter and make sure you follow the[Chromebook Setup](https://tutorial.djangogirls.org/en/chromebook_setup/README.md)instructions.
>
> **Note**If you already worked through the Installation steps, there's no need to do this again – you can skip straight ahead to the next chapter!
>
> For readers at home: this chapter is covered in the[Installing Python & Code Editor](https://www.youtube.com/watch?v=pVTaqzKZCdA)video.
>
> This section is based on a tutorial by Geek Girls Carrots \([https://github.com/ggcarrots/django-carrots](https://github.com/ggcarrots/django-carrots)\)

Django is written in Python. We need Python to do anything in Django. Let's start by installing it! We want you to install Python 3.5, so if you have any earlier version, you will need to upgrade it.

### Windows

Windowsをお使いのかたは、 次のリンクからダウンロードすることができます。 [https://www.python.org/downloads/release/python-352/](https://www.python.org/downloads/release/python-352/).  **\*.msi** ファイルをダウンロードしたら、ダブルクリックして実行して、指示のとおりインストールしてください。Pythonをどのディレクトリにインストールしたか確認して、おぼえておいてくださいね。後ほど必要になってきます。

## Windows {#windows}

First check whether your computer is running a 32-bit version or a 64-bit version of Windows, by pressing the Windows key + Pause/Break key which will open your System info, and look at the "System type" line. You can download Python for Windows from the website[https://www.python.org/downloads/windows/](https://www.python.org/downloads/windows/). Click on the "Latest Python 3 Release - Python x.x.x" link. If your computer is running a**64-bit**version of Windows, download the**Windows x86-64 executable installer**. Otherwise, download the**Windows x86 executable installer**. After downloading the installer, you should run it \(double-click on it\) and follow the instructions there.

One thing to watch out for: During the installation you will notice a window marked "Setup". Make sure you tick the "Add Python 3.5 to PATH" checkbox and click on "Install Now", as shown here:

![](/assets/python-installation-options.png)



In upcoming steps, you'll be using the Windows Command Line \(which we'll also tell you about\). For now, if you need to type in some commands, go to Start menu → All Programs → Accessories → Command Prompt. You can also hold in the Windows key and press the "R"-key until the "Run" window pops up. To open the Command Line, type "cmd" and press enter in the "Run" window. \(On newer versions of Windows, you might have to search for "Command Prompt" since it's sometimes hidden.\)

![](/assets/windows-plus-r.png)

Note: if you are using an older version of Windows \(7, Vista, or any older version\) and the Python 3.5.x installer fails with an error, you can try either:

1. install all Windows Updates and try to install Python 3.5 again; or
2. install an
   [older version of Python](https://www.python.org/downloads/windows/)
   , e.g.,
   [3.4.4](https://www.python.org/downloads/release/python-344/)
   .

If you install an older version of Python, the installation screen may look a bit different than shown above. Make sure you scroll down to see "Add python.exe to Path", then click the button on the left and pick "Will be installed on local hard drive":

![](/assets/add_python_to_windows_path.png)



### OS X

Webサイトからダウンロードしてインストールしましょう。 [https://www.python.org/downloads/](https://www.python.org/downloads/)

* _Mac OS X 64-bit/32-bit installer_ _DMG_ ファイルをダウンロードして下さい。
* ダブルクリックで開いてください。
* _Python.mpkg_ をダブルクリックして、インストーラーを実行してください。

インストールが正しく行われたか確認するために、 _ターミナル_ を開いて、`python3` コマンド次のようにタイプしてみましょう。

```
$ python3 --version
Python 3.5.2
```

> **Note**Before you install Python on OS X, you should ensure your Mac settings allow installing packages that aren't from the App Store. Go to System Preferences \(it's in the Applications folder\), click "Security & Privacy," and then the "General" tab. If your "Allow apps downloaded from:" is set to "Mac App Store," change it to "Mac App Store and identified developers."

You need to go to the website[https://www.python.org/downloads/release/python-351/](https://www.python.org/downloads/release/python-351/)and download the Python installer:

* Download the
  _Mac OS X 64-bit/32-bit installer_
  file,
* Double click
  _python-3.5.1-macosx10.6.pkg_
  to run the installer.

### 

### Linux

おそらく殆どの場合、Pythonはすでにインストール済みでしょう。インストールされているか確認するためには（バージョンを確認するためにも）、コンソールを起動して次のコマンドを打ってください。

```
$ python3 --version
Python 3.5.2
```

もし、Pythonがインストールされていない場合、あるいはバージョンが古い場合は、次の指示に従ってインストールしてください。

#### Ubuntu

次のコマンドをコンソールに打って下さい。

```
sudo apt-get install python3.5 python3.5-venv
```

#### Fedora

次のコマンドをコンソールに打って下さい。

```
sudo yum install python3.5
```

---

分からない時や、質問がある時は、コーチに質問してくださいね。ときどき上手くいかないこともあります。そんな時は、経験豊富な人に聞くといいですよ。

