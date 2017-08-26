# Pythonを始めましょう {#lets-start-with-python}

ついにここまで来ました！

まずは、最初にPythonとは何かお話させて下さいね。Pythonはとても人気のあるプログラミング言語です。Webサイトや、ゲーム、サイエンス、グラッフィックス、などなど、たくさんの場面で使われています。

Pythonは1980年台の終わりに、人間が読みやすい（機械だけでなく）言語を目的に開発されました。だから、他の言語に比べて、Pythonはとてもシンプルで、勉強しやすいのです。でもご心配なく、Pythonはとってもパワフルな言語でもありますから！

# Pythonのインストール {#python-installation}

> 注意：すでにインストール手順を実行している場合は、これをもう一度行う必要はありません。次の章に進むことができます。
>
> このセクションはGeek Girls Carrots（[https://github.com/ggcarrots/django-carrots](https://github.com/ggcarrots/django-carrots)）のチュートリアルに基づいています。

Django は、Pythonで開発されています。なにをするにせよ、まずはPythonが必要です。インストールしましょう！ Python 3.5 をインストールします。3.5以前のバージョンをインストール済みの場合は、アップグレードしてください。

## Windows {#windows}

Windowsをお使いのかたは、まずシステム情報を開き、システムの種類が32-bitバージョンか64-bitバージョンかを確認します。

（システム情報の開き方：Windowsキー + Pause/Break キー　もしくは　コントロールパネル&gt;システムとセキュリティ&gt;システムを開く\)

Python for Windowsは　[https://www.python.org/downloads/windows/](https://www.python.org/downloads/windows/)　からダウンロードできます。 「最新のPython 3 Release - Python x.x.x」リンクをクリックしてください。 お使いのコンピュータが64ビット版のWindowsを実行している場合は、Windows x86-64実行可能インストーラをダウンロードしてください。 32ビット版の場合は、Windows x86実行可能インストーラーをダウンロードします。 インストーラをダウンロードしたら、それを実行して（ダブルクリックして）インストーラの指示に従ってください。（画像は3.5.1ですが2017/08/26時点の最新バージョンは3.6.2です。）

**インストール時に必ずAdd Python 3.x to Path にチェックをいれましょう**:

![](/assets/python-installation-options.png)

次のステップでは、Windowsコマンドラインを使用します。 今のところ、いくつかのコマンドを入力する必要がある場合は、**スタートメニュー→すべてのプログラム→アクセサリ→コマンドプロンプト\(Windows10 Windowsロゴマーク→Windowsシステムツール→コマンドプロンプト）**を開きます。 または、**Windowsキー + 「R」キー**　「ファイル名を指定して実行」ウィンドウを起動して　"cmd" と入力しenterキーを押します。（新しいバージョンのWindowsでは、コマンドプロンプトが非表示になることがあるため、「コマンドプロンプト」を検索する必要があるかもしれません）。

![](/assets/windows-plus-r.png)

> 注意：古いバージョンのWindows（7、Vista、またはそれ以前のバージョン）を使用していて、Python 3.5.xインストーラがエラーで失敗した場合、次のいずれかを試みることができます：

1. すべてのWindowsアップデートをインストールして、Python 3.5を再インストールしてみる。
2. 古いバージョンのPythonをインストールしてみる。\([https://www.python.org/downloads/windows/](https://www.python.org/downloads/windows/)\)

古いバージョンのPythonをインストールした場合、インストール画面は上記のものとは多少異なる場合があります。 下にスクロールして「python.exeをパスに追加」し、左側のボタンをクリックして「ローカルハードドライブにインストールされます」を選択してください。:

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

> 注意:OS XにPythonをインストールする前に、Macの設定でApp Store以外のパッケージをインストールできるようにする必要があります。 「システム環境設定」（「アプリケーション」フォルダ内）に移動し、「セキュリティとプライバシー」、「一般」タブの順にクリックします。 「ダウンロードしたアプリを許可する」が「Mac App Store」に設定されている場合は、「Mac App Storeと識別された開発者」に変更します。

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

