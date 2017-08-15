# インターネットはどうやって動いているの？

> This chapter is inspired by a talk "How the Internet works" by Jessica McKellar \([http://web.mit.edu/jesstess/www/](http://web.mit.edu/jesstess/www/)\).

We bet you use the Internet every day. But do you actually know what happens when you type an address like [http://djangogirls.org](http://djangogirls.org) into your browser and press 'Enter'?

The first thing you need to understand is that a website is just a bunch of files saved on a hard disk. Just like your movies, music or pictures.  
However, there is one part that is unique for websites: they include computer code called HTML.

If you're not familiar with programming, it can be hard to grasp HTML at first, but your web browsers \(like Chrome, Safari, Firefox, etc.\) love it. Web browsers are designed to understand this code,  
follow its instructions and present all these files that your website is made of exactly the way you want them to be presented.

As with every file, we need to store HTML files somewhere on a hard disk. For the Internet, we use special, powerful computers called _servers_. They don't have  
a screen, mouse or a keyboard, because their main purpose is to store data and serve it. That's why they're called _servers_ -- because they _serve_ you data.

OK, but you want to know how the Internet looks like, right?

We drew you a picture! It looks like this:

![Figure 1.1](images/internet_1.png)

Looks like a mess, right? In fact it is a network of connected machines \(the above mentioned _servers_\). Hundreds of thousands of machines! Many, many kilometers of cables around the world! You can visit a Submarine Cable Map website \([http://submarinecablemap.com/](http://submarinecablemap.com/)\) to see how complicated the net is. Here is a screenshot from the website:

![Figure 1.2](images/internet_3.png)

It is fascinating, isn't it? But obviously, it is not possible to have a wire between every machine connected to the Internet. So, to reach a machine \(for example the one where [http://djangogirls.org](http://djangogirls.org) is saved\) we need to pass a request through many, many different machines.

It looks like this:

![Figure 1.3](images/internet_2.png)

Imagine that when you type [http://djangogirls.org](http://djangogirls.org), you send a letter that says: "Dear Django Girls, I want to see the djangogirls.org website. Send it to me, please!"

Your letter goes to the post office closest to you. Then it goes to another that is a bit nearer to your addressee, then to another and another till it is delivered at its destination. The only unique thing is that if you send letters \(_data packets_\) frequently to the same place, each letter might go through totally different post offices \(_routers_\), depending on how they are distributed in each office.

![Figure 1.4](images/internet_4.png)

簡単ですよね。あなたはメッセージを送信し、何らかの応答を期待します。 もちろん、紙とペンではなく、データのバイトを使用しますが、アイデアは同じです！

市町村名、郵便番号、国名の住所の代わりに、IPアドレスを使用します。 お使いのコンピュータは、まずdjangogirls.orgをIPアドレスに変換するようにDNS（Domain Name System）に依頼します。 あなたが連絡したい人の名前を探し、電話番号と住所を見つけることができる昔ながらの電話帳のようなものです。

手紙を送るときには、住所、切手など、正しく配送される特定の機能が必要ですよね。また、受信者が理解できる言語も使用している必要がありますよね？ Webサイトを表示するために送信するデータパケットにも同じように特定の機能があります。それはHTTP（Hypertext Transfer Protocol）というプロトコルを使用します。

だから、基本的に、あなたがウェブサイトを持っているときには、サーバー（マシン）が必要です。 サーバーは着信要求（サーバーにWebサイトの送信を要求する文字）を待機し、Webサイトに別の手紙を送信します。

これはDjangoチュートリアルなので、あなたはDjangoが何をしているのかを知りたでしょう？ あなたが返事を返す時、 みんなに同じ返事を返すより、個々にパーソナライズされた返事を返せた方が良いでしょう？（Djangoはこれらのパーソナライズされた興味深い文字を作成するのに役立ちます:\)。



インターネットの話は以上です！さあ、いよいよあなたのブログサイトを作成する時間です！

