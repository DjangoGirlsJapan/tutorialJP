# Introduction to Python

> このチャプターの一部はGeek Girls Carrotsのチュートリアルをもとにしています。 (http://django.carrots.pl/).

さあ、コードを書いてみましょう！

## Python prompt

Pythonであそぶために、*コマンドライン* を開きましょう。 やり方は、チャプター [Intro to Command Line](../intro_to_command_line/README.md) で学びましたね。

準備ができたら、次の指示に従ってやってみましょう。

Pythonコンソールを開きましょう。`python3`とタイプして Enterキーをおしてください。.

    $ python3
    Python 3.4.2 (...)
    Type "copyright", "credits" or "license" for more information.
    >>>

## Your first Python command!

Pythonのコマンドが走ると、プロンプト記号が `>>>`に変わりました。これは、今Pythonの言語を実行できますという意味です。 `>>>`はタイプしなくていいですよ。 - Pythonがあなたの代わりにやってくれます。

Pythonコンソールを終わる時は、`exit()`　とタイプするか、ショートカット`Ctrl + Z` （Windows）、 `Ctrl + D`（Mac/Linux）で終了です。. T `>>>` は現れなくなりました。

けど、今はまだコンソールを終了しないで、もっと動かして学びましょう。最初はとてもシンプルなものからはじめましょう。例えば、簡単な計算をしてみましょう。`2 + 3`とタイプして、Enterキーを押してください。

    >>> 2 + 3
    5

できました！答えがでてきましたね。Pythonは計算ができます。他にも、次のようなコマンドを試してみましょう：
- `4 * 5`
- `5 - 1`
- `40 / 2`

ちょっとの間楽しんであそんでみたら、またココに戻ってきてくださいね。:)

お分かりのとおり、Pythonはステキな計算機ですね. 他になにができるんだろう…と思ったら、次にいってみましょう。

## Strings

あなたのお名前を次のようにクォーテーションをつけてタイプしてください。

    >>> "Ola"
    'Ola'

はじめてのString（文字列）が完成です！Stringとは、文字の集合のことです。シングルクォーテーション (`'`) あるいは、ダブルクォーテーション (`"`) で囲います。最初と最後は同じ記号にしてください。 - クォーテーションの中が文字列であることを意味しています。

複数の文字列を結合することもできます。次のように試してみましょう。:

    >>> "Hi there " + "Ola"
    'Hi there Ola'

文字列を繰り返すためには、演算子を使って繰り返し回数を指定することもできます。You can also multiply strings with a number:

    >>> "Ola" * 3
    'OlaOlaOla'

アポストロフィーを文字列の中に含めたい場合は、２通りの方法があります。

まずは、ダブルクォーテーションを使う方法です。

    >>> "Runnin' down the hill"
    "Runnin' down the hill"

あるいは、バックスラッシュ (`\`)を使う方法もあります。:

    >>> 'Runnin\' down the hill'
    "Runnin' down the hill"

できましたか？次に、あなたの名前を大文字に変えてみましょう。次のように記述してください。

    >>> "Ola".upper()
    'OLA'

ここで`upper` __function__ を使うことができましたね! 関数 (`upper()`など) は、is a sequence of instructions that Python has to perform on a given object (`"Ola"`) once you call it.

あなたの名前の文字数を知りたいときは、その関数もあります！

    >>> len("Ola")
    3

どうして、文字列の後に`.` をつけて関数を呼び出したり (`"Ola".upper()`のように)、あるいは、先に関数を呼び出してかっこの中に文字列をいれているのか、と疑問に思ったかもしれません。 Well, in some cases, functions belong to objects, like `upper()`, which can only be performed on strings. In this case, we call the function a __method__. Other times, functions don't belong to anything specific and can be used on different types of objects, just like `len()`. That's why we're giving `"Ola"` as a parameter to the `len` function.

### Summary

文字列はだいじょうぶですね。ここまでに学んだことをまとめましょう。

- __the prompt__ - typing commands (code) into the Python prompt results in answers in Python
- __numbers and strings__ - in Python numbers are used for math and strings for text objects
- __operators__ - like + and *, combine values to produce a new one
- __functions__ - like upper() and len(), perform actions on objects.

These are the basics of every programming language you learn. もう少し難易度の高いものに挑戦してみましょう。準備はいいですか？

## Errors

さて、新しいことをやってみましょう。あなたの名前の文字数を数えたように、数字の文字列は数えれるでしょうか？ `len(304023)`と記述して、Enterキーを押してみましょう。

    >>> len(304023)
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    TypeError: object of type 'int' has no len()

はじめてのエラーがでました！オブジェクトタイプ"int" (integers, 数値) は文字数がありませんと言っています。では、どうすればよいでしょうか？この数字を文字列として扱えれば、文字数を数えれるはずですよね？

    >>> len(str(304023))
    6

できました！`str` 関数を`len`の中に記述しました。`str()`は、その中身を文字列に変換します。

- The `str` function converts things into __strings__
- The `int` function converts things into __integers__

> 重要！: 数字は文字列にすることはできますが、全ての文字が数字に変換できるわけではありません。 例えば `int('hello')` は数字にはなりませんよね？

## Variables

variables（変数）は、プログラミングの重要なコンセプトです。後で使うためにつける単なる名札ではありません。プログラマーは変数を使ってデータを保管したり、 コードを読みやすくして、後でそれが何だったか覚えておかなくてもいいようにします。

変数`name`を新しくつくってみましょう。

    >>> name = "Ola"

できましたか？簡単ですね。単純に name イコール（=） Olaと記述するだけです。.

見てのとおり、プログラムは、なにも返してくれませんね。では、変数がきちんとあるか、どうやって確かめたらいいのでしょうか？ `name`とタイプして、Enterキーをおしてください。

    >>> name
    'Ola'

やりました！あなたのはじめての変数ができましたね！代入する値を変えることもできます。

    >>> name = "Sonja"
    >>> name
    'Sonja'

関数にも使えます。

    >>> len(name)
    5

素晴らしいですね！変数は、もちろん数値にも使えますよ。

    >>> a = 4
    >>> b = 6
    >>> a * b
    24

もしも、間違えた変数名を使ってしまったら、どうなるでしょうか？予想できますか？やってみましょう！

    >>> city = "Tokyo"
    >>> ctiy
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    NameError: name 'ctiy' is not defined

エラーになりました！前回とは違うエラータイプです。**NameError**という、初めてみるエラータイプですね。作成されていない変数を使った時は、Pythonがエラーを教えてくれます。もし、このエラーに出くわしたら、記述したコードにタイプミスがないか確認してください。

ちょっと遊んで、何ができるか試してみてくださいね！


## The print function

次に挑戦してみましょう。

    >>> name = 'Maria'
    >>> name
    'Maria'
    >>> print(name)
    Maria

単に`name`とタイプした時は、Pythonインタプリタが、変数'name'の *representation* を返します。ここでは、 M-a-r-i-aという単なる文字の集まりで、シングルクォーテーション（''）に囲われています。  しかし、 `print(name)`と記述した時は、Pythonは変数の中身を出力します。クォーテーションはありません。

これからさらに詳しくみていきますが、`print()`は、関数から出力をする時や、複数行の出力を行うときにも便利です。


## Lists

数値と文字列の他にも、すべてのオブジェクトタイプを勉強しておきましょう。__list__というものがあります。リストは、その名のとおり、オブジェクトの並びをもつものですね。:)

まずはリストを作りましょう:

    >>> []
    []

はい、このリストは空っぽです。使いにくいですよね。では、くじ引きの番号のリストを作りましょう。 この番号を何度も繰り返し書きたくはないから、同時に変数に代入してしまいましょう。

    >>> lottery = [3, 42, 12, 19, 30, 59]

よし、これでリストができました！このリストで何をしましょうか？では、くじ引きの番号がいくつあるか、数えてみましょう。何の関数を使えばいいか、予想できますか？すでに知っていますよね！

    >>> len(lottery)
    6

そうです！`len()`がリストにあるオブジェクトの数を取得できます。便利ですね。では、くじ引きの番号をソートしてみましょう。

    >>> lottery.sort()

これは何も返してきません。これはリストに表示される番号を、順番に並べ替えただけです。再度出力して、確かめてみましょう。:

    >>> print(lottery)
    [3, 12, 19, 30, 42, 59]

ご覧のとおり、小さい順に並び替えられましたね。おめでとう！

逆順に並び替えてみたくなりましたか？やってみましょう。

    >>> lottery.reverse()
    >>> print(lottery)
    [59, 42, 30, 19, 12, 3]

簡単でしたね？リストに何かを追加したいときは、次のようにコマンドを記述してください。

    >>> lottery.append(199)
    >>> print(lottery)
    [59, 42, 30, 19, 12, 3, 199]

最初の数字だけを出力したいときは、__indexes__を使って指定することができます。インデックスは、リストの先頭の要素から順に「０」、次に「１」と割り当てられています。次のとおり試してみてください。:

    >>> print(lottery[0])
    59
    >>> print(lottery[1])
    42

このように、リスト名と要素のインデックスを[]に記述することで、指定した要素を取り出すことができます。

他のインデックスも試して遊んでみてください。例えば、 6, 7, 1000, -1, -6, -1000 などをインデックスに指定するとどうなるでしょうか。コマンドを実行する前に予測してみましょう。結果はどうですか？

ご参考に、こちらのドキュメントにリストメソッドがすべて記されています。 https://docs.python.org/3/tutorial/datastructures.html

## Dictionaries

辞書(ディクショナリ)について確認しましょう。リストに似ていますが、インデックスのかわりにキーと呼ばれる識別子で値を参照します。キーは文字列も数値も使えます。ディクショナリは次のように｛｝括弧で囲んで作成します。

    >>> {}
    {}

これで中身が空っぽのディクショナリができましたね。やったね！

では、つぎのコマンドを記述してみましょう。 (あなた自身の情報に値をおきかえてみてもいいですよ)

    >>> participant = {'name': 'Ola', 'country': 'Poland', 'favorite_numbers': [7, 42, 92]}

このコマンドで、`participant`という名前の変数をつくって、３つのキーと値をもつ要素を作成しました。

- キーが`name`で、 値が`'Ola'`の要素です。 (a `string` object),
- キー`country`は、 値`'Poland'` (another `string`),
- キー`favorite_numbers` は リスト`[7, 42, 92]`。 (a `list` with three numbers in it).

次の構文で各キーの値を確認できます。

    >>> print(participant['name'])
    Ola

リストに似ていますね。しかし、ディクショナリーでは、インデックスを記憶する必要がなく、名前でいいのです

もし存在しないキーを参照しようとすると、どうなるでしょうか？予想できますか？実際にやってみましょう！

    >>> participant['age']
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    KeyError: 'age'

またエラーです。今回は **KeyError**というエラーが出ました。Pythonは、このディクショナリにキー`'age'`は存在しませんよ、と教えてくれています。

ディクショナリとリストはどう使い分ければよいのでしょうか？そうですね、これはゆっくり考えてみるべきポイントですね！この後の解答を読むまえに、考えてみてください。

- Do you just need an ordered sequence of items? Go for a list.
- Do you need to associate values with keys, so you can look them up efficiently (by key) later on? Use a dictionary.

Dictionaries, like lists, are *mutable*, meaning that they can be changed after they are created. You can add new key/value pairs to the dictionary after it is created, like:

    >>> participant['favorite_language'] = 'Python'

Like lists, using `len()` method on the dictionaries, returns the number of key-value pairs in the dictionary. Go ahead and type in the command:

    >>> len(participant)
    4

お分かり頂けたでしょうか。 :) では、ディクショナリを使ってもう練習してみましょう。準備ができたら、次の行にいってみましょう。

ディクショナリの要素を削除する時は、`del`コマンドを使います。例えば、 キー`'favorite_numbers'`の要素を削除するには、次のように記述してください。

    >>> del participant['favorite_numbers']
    >>> participant
    {'country': 'Poland', 'favorite_language': 'Python', 'name': 'Ola'}

このように、'favorite_numbers'のキーと値が削除されます。

同様に、次のように記述することで、すでにあるキーの値を変更することができます。:

    >>> participant['country'] = 'Germany'
    >>> participant
    {'country': 'Germany', 'favorite_language': 'Python', 'name': 'Ola'}

これで、キー`'country'`の値は、`'Poland'`から`'Germany'`に変わりました。 :) 面白くなってきましたか？その調子です！

### Summary

素晴らしいです! これで、あなたはプログラミングについて沢山のことを学びました。ここまでのところをまとめましょう。

- __errors__ - you now know how to read and understand errors that show up if Python doesn't understand a command you've given it
- __variables__ - names for objects that allow you to code more easily and to make your code more readable
- __lists__ - lists of objects stored in a particular order
- __dictionaries__ - objects stored as key-value pairs

次に進む準備はいいですか？ :)

## Compare things

比較することは、プログラミングの醍醐味の１つです。簡単に比較できるものといえば、何でしょうか？そうです、数字ですね。さっそくやってみましょう。

    >>> 5 > 2
    True
    >>> 3 < 1
    False
    >>> 5 > 2 * 2
    True
    >>> 1 == 1
    True
    >>> 5 != 2
    True

Pythonにいくつか比較する数字をあたえてみました。数字を比較するだけでなく、演算式の答えも比較することができます。便利でしょ？

２つの数字がイコールであるかどうかを比べる時に、イコールの記号が２つ`==`並んでいます。疑問に思いましたか？ Pythonを記述する時、イコール１つ`=`は、変数に値を代入するときに使います。ですので、値同士が等しいかどうか比較するときは、必ず __必ず__ イコール記号２つ`==`を記述してください。 等しくないとするときは、 上記の例のように `!=`と記述します。

次の２つはどうでしょうか

    >>> 6 >= 12 / 2
    True
    >>> 3 <= 2
    False

`>` と `<` は簡単でしたね。 `>=` と `<=` はどうでしょうか？それぞれの意味は、次のとおりです。

- x `>` y : x は y　より大きい
- x `<` y : x は y　より小さい
- x `<=` y : x は y　以下
- x `>=` y : x は y　以上

すばらしい! もう少しやってみましょう。

    >>> 6 > 2 and 2 < 3
    True
    >>> 3 > 2 and 2 < 1
    False
    >>> 3 > 2 or 2 < 1
    True

条件式が複数あって複雑になっても、その答えを出してくれます。とても賢いですね。

- __and__ - `and`の左辺と右辺が共にTrueの場合、True。
- __or__ -  `or`の左辺あるいは右辺の少なくとも１つがTrueの時、True。

Have you heard of the expression "comparing apples to oranges"? Let's try the Python equivalent:

    >>> 1 > 'django'
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    TypeError: unorderable types: int() > str()

Pythonは、数値(`int`)　と文字列(`str`)の比較はできません。
**TypeError**とエラーが表示され、２つのオブジェクトタイプが比較できないことを教えてくれています。

## Boolean

偶然にも、__Boolean__というあたらしいオブジェクトタイプを学びました。 -- おそらく、Booleanは一番簡単なオブジェクトタイプです。

Booleanは、たった２つの値を持ちます。
- True
- False

Pythonを記述するときは、Trueの最初は大文字のT、残りは小文字です。 __true, TRUE, tRUE は間違いです。 -- True と記述してください__ (もちろん False についても同様です。)

Booleanは、次のように変数に代入することもできます。:

    >>> a = True
    >>> a
    True

このようなこともできます。

    >>> a = 2 > 5
    >>> a
    False

Booleansを使って、練習して遊んでみましょう。次のコマンドを試してみてください。

- `True and True`
- `False and True`
- `True or 1 == 1`
- `1 != 2`

おめでとうございます！Booleansを理解することは、プログラミングでとても大事です。ここまでできましたね！

# Save it!

ここまでインタプリタでPythonのコードをかいてきました。つまり、コードを１行づつしか書くことができませんでした。普通のプログラムはファイルに保存され、__インタプリタ__ あるいは __コンパイラ__でプログラミング言語を処理して実行します。ここまで、私たちはプログラムを１行ごとにPython __インタプリタ__で実行してきました。ここかっらは、１行以上のコードを実行していきましょう。次のような流れになります。

- Pythonインタプリタを終了します。
- お好きなエディタを起動します。
- Pythonファイルとしてコードを保存します。
- 実行します！

これまで使っていたPythonインタプリタを終了しましょう。 ```exit()``` ファンクションを記述してください。

    >>>exit()
    $

これで、コマンドプロンプトに戻りました。

前のチャプター [code editor](../code_editor/README.md) で、エディタを紹介しました。エディタを起動して、新しいファイルにコードを書いてみましょう。

    print('Hello, Django girls!')

あなたは、すでにベテランのpython開発者です。今日学んだコードを自由に書いてみてください。

コードを書いたら、わかりやすい名前をつけて保存しましょう。**python_intro.py**と名前をつけて、デスクトップに保存してください。ファイル名は何でもかまいません。ここで重要なことは、拡張子を__.py__とすることです。コンピュータにこのファイルは**pythonで実行するファイルです**とおしえます。

ファイルを保存したら、実行してみましょう！コマンドラインのセクションで学んだことを思い出して、ターミナルの **ディレクトリを変更**して、デスクトップにしましょう。

Macでは、コマンドは次のようになります。

    cd /Users/<your_name>/Desktop

Linuxでは、次のようになります。(the word "Desktop" might be translated to your language):

    cd /home/<your_name>/Desktop

Windowsでは、次のようになります。

    cd C:\Users\<your_name>\Desktop

うまくできない時は、質問してください。

次に、ファイルのコードを実行します。

    $ python3 python_intro.py
    Hello, Django girls!

できました！これで、あなたはファイルに保存されたPythonプログラムを実行できましたね。いい気分ですね。

では、ここからプログラミングに不可欠のツールを学んでいきましょう

## If...elif...else

ある条件が成立するときに処理を行いたいという時が. That's why Python has something called __if 条件式__.

では、 **python_intro.py** ファイルのコードを次のように書き換えてください。

    if 3 > 2:

これを保存して実行すると、次のようなエラーがでます。

    $ python3 python_intro.py
    File "python_intro.py", line 2
             ^
    SyntaxError: unexpected EOF while parsing

条件式 `3 > 2`　がTrueの時、どのように処理をすべきかが記述されていませんね。では、Python に “It works!”　と出力してもらいましょう。**python_intro.py** ファイルの中身を、次のとおりに書き換えてください。

    if 3 > 2:
        print('It works!')

２行目をスペース４つでインデントしていることに気が付きましたか？if文がTrueの時、どのコードを実行するかPythonに知らせる必要があります。 スペース１つでもできますが、ほぼ全員のPythonプログラマーはスペース４つとしています。タブ１つも、スペース４つと同じです。

保存して、もう一度実行してみましょう。

    $ python3 python_intro.py
    It works!

### What if not?

前述の例では、if文の条件式がTrueの時だけ、コードが実行されました。Pythonは、`elif` や `else` といった記述もできます。

    if 5 > 2:
        print('5 is indeed greater than 2')
    else:
        print('5 is not greater than 2')

これを実行した場合、次のように出力されます。

    $ python3 python_intro.py
    5 is indeed greater than 2

2が５より大きい場合、２行目のコマンドが実行されます。では、 `elif`　はどうなるのでしょうか？

    name = 'Sonja'
    if name == 'Ola':
        print('Hey Ola!')
    elif name == 'Sonja':
        print('Hey Sonja!')
    else:
        print('Hey anonymous!')

それを実行すると...

    $ python3 python_intro.py
    Hey Sonja!

どうなったか、わかりましたか?

### Summary

In the last three exercises you learned about:

- __comparing things__ - in Python you can compare things by using `>`, `>=`, `==`, `<=`, `<` and the `and`, `or` operators
- __Boolean__ - a type of object that can only have one of two values: `True` or `False`
- __Saving files__ - storing code in files so you can execute larger programs.
- __if...elif...else__ - statements that allow you to execute code only when certain conditions are met.

Time for the last part of this chapter!

## Your own functions!

Remember functions like `len()` that you can execute in Python? Well, good news, you will learn how to write your own functions now!

A function is a sequence of instructions that Python should execute. Each function in Python starts with the keyword `def`, is given a name and can have some parameters. Let's start with an easy one. Replace the code in **python_intro.py** with the following:

    def hi():
        print('Hi there!')
        print('How are you?')

    hi()

Okay, our first function is ready!

You may wonder why we've written the name of the function at the bottom of the file. This is because Python reads the file and executes it from top to bottom. So in order to use our function, we have to re-write it at the bottom.

Let's run this now and see what happens:

    $ python3 python_intro.py
    Hi there!
    How are you?

That was easy! Let's build our first function with parameters. We will use the previous example - a function that says 'hi' to the person running it - with a name:

    def hi(name):

As you can see, we now gave our function a parameter that we called `name`:

    def hi(name):
        if name == 'Ola':
            print('Hi Ola!')
        elif name == 'Sonja':
            print('Hi Sonja!')
        else:
            print('Hi anonymous!')

    hi()

As you can see, we needed to put two indents before the `print` function, because `if` needs to know what should happen when the condition is met. Let's see how it works now:

    $ python3 python_intro.py
    Traceback (most recent call last):
    File "python_intro.py", line 10, in <module>
      hi()
    TypeError: hi() missing 1 required positional argument: 'name'

Oops, an error. Luckily, Python gives us a pretty useful error message.
It tells us that the function `hi()` (the one we defined) has one required argument (called `name`) and that we forgot to pass it when calling the function.
Let's fix it at the bottom of the file:

    hi("Ola")

and run it again:

    $ python3 python_intro.py
    Hi Ola!

And if we change the name?

    hi("Sonja")

and run it:

    $ python3 python_intro.py
    Hi Sonja!

Now what do you think will happen if you write another name in there? (Not Ola or Sonja) Give it a try and see if you're right. It should print out this:

    Hi anonymous!

This is awesome, right? This way you don't have to repeat yourself every time you want to change the name of the person the function is supposed to greet. And that's exactly why we need functions - you never want to repeat your code!

Let's do something smarter -- there are more names than two, and writing a condition for each would be hard, right?

    def hi(name):
        print('Hi ' + name + '!')

    hi("Rachel")

Let's call the code now:

    $ python3 python_intro.py
    Hi Rachel!

Congratulations! You just learned how to write functions :)!

## Loops

That's the last part already. That was quick, right? :)

As we mentioned, programmers are lazy, they don't like to repeat themselves. Programming is all about automating things, so we don't want to greet every person by their name manually, right? That's where loops come in handy.

Still remember lists? Let's do a list of girls:

    girls = ['Rachel', 'Monica', 'Phoebe', 'Ola', 'You']

We want to greet all of them by their name. We have the `hi` function to do that, so let's use it in a loop:

    for name in girls:

The ```for``` statement behaves similarly to the ```if``` statement, code below both of these need to be indented four spaces.

Here is the full code that will be in the file:

    def hi(name):
        print('Hi ' + name + '!')

    girls = ['Rachel', 'Monica', 'Phoebe', 'Ola', 'You']
    for name in girls:
        hi(name)
        print('Next girl')

and when we run it:

    $ python3 python_intro.py
    Hi Rachel!
    Next girl
    Hi Monica!
    Next girl
    Hi Phoebe!
    Next girl
    Hi Ola!
    Next girl
    Hi You!
    Next girl

As you can see, everything you put inside a `for` statement with an indent will be repeated for every element of the list `girls`.

You can also use `for` on numbers using the `range` function:

    for i in range(1, 6):
        print(i)

Which would print:

    1
    2
    3
    4
    5

`range` is a function that creates a list of numbers following one after the other (these numbers are provided by you as parameters).

Note that the second of these two numbers is not included in the list that is output by Python (meaning `range(1, 6)` counts from 1 to 5, but does not include the number 6).

## Summary

以上です！__おめでとう！頑張りました！__ これは簡単ではなかったと思います。自分を褒めてあげてくださいね。ここまで進めることができたのは、本当に素晴らしいことです！

You might want to briefly do something else - stretch, walk around for a bit, rest your eyes - before going on to the next chapter. :)

![Cupcake](images/cupcake.png)
