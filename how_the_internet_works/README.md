# インターネットはどうやって動いているの？

> This chapter is inspired by a talk "How the Internet works" by Jessica McKellar \([http://web.mit.edu/jesstess/www/](http://web.mit.edu/jesstess/www/)\).

私達は毎日インターネットにつながっていますよね。でも、あなたがブラウザのアドレス欄に　[http://djangogirls.org](https://www.gitbook.com/book/djangogirlsjapan/workshop_tutorialjp/edit#)　のように入力をしてEnterキーを押している事がどういう意味がるのかわかりますか？



最初に理解してほしいのは、あなたが自分のパソコンのハードディスクに映画や音楽や写真を沢山保存しているように、Webサイトもハードディスクに保存される沢山のファイルの集合であるという事です。



しかし、Webサイトは映画や音楽、写真のようなデータとは違ってHTMLというコンピュータのコードを持っているのです。もし、あなたがプログラミングに精通していなかったら、最初はHTMLも難しく感じるでしょう。でも、あなたがよく使うWebブラウザ（ChromeやSafariやFirefox等々）はHTMLのコードを理解しているのです。Webブラウザが正しく理解できるように、ファイルを作成する必要があります。



あなたのパソコンへファイルを保存するのと同じで私達はHTMLをハードディスクに格納する必要があります。インターネットの場合、そのハードディスクはサーバーと呼ばれている、パワフルなコンピュータを使います。サーバーの主な目的はデータを格納して、それに供給することであるので、マウスまたはキーボードを持っていません。また、データを供給する役割を持っているので、サーバーと呼ばれるのです。



インターネットはどのように見えますか？

私達は絵をかいてみました。

![Figure 1.1](images/internet_1.png)

Looks like a mess, right? In fact it is a network of connected machines \(the above mentioned _servers_\). Hundreds of thousands of machines! Many, many kilometers of cables around the world! You can visit a Submarine Cable Map website \([http://submarinecablemap.com/](http://submarinecablemap.com/)\) to see how complicated the net is. Here is a screenshot from the website:

![Figure 1.2](images/internet_3.png)

It is fascinating, isn't it? But obviously, it is not possible to have a wire between every machine connected to the Internet. So, to reach a machine \(for example the one where [http://djangogirls.org](http://djangogirls.org) is saved\) we need to pass a request through many, many different machines.

It looks like this:

![Figure 1.3](images/internet_2.png)

Imagine that when you type [http://djangogirls.org](http://djangogirls.org), you send a letter that says: "Dear Django Girls, I want to see the djangogirls.org website. Send it to me, please!"

Your letter goes to the post office closest to you. Then it goes to another that is a bit nearer to your addressee, then to another and another till it is delivered at its destination. The only unique thing is that if you send letters \(_data packets_\) frequently to the same place, each letter might go through totally different post offices \(_routers_\), depending on how they are distributed in each office.

![Figure 1.4](images/internet_4.png)

Yes, it is as simple as that. You send messages and you expect some response. Of course, instead of paper and pen you use bytes of data, but the idea is the same!

Instead of addresses with a street name, city, zip code and country name, we use IP addresses. Your computer first asks the DNS \(Domain Name System\) to translate djangogirls.org into an IP address. It works a little bit like old-fashioned phonebooks where you could look for the name of the person you want to contact and find their phone number and address.

When you send a letter, it needs to have certain features to be delivered correctly: an address, stamp etc. You also use a language that the receiver understands, right? The same is with _data packets_ you send in order to see a website: you use a protocol called HTTP \(Hypertext Transfer Protocol\).

So, basically, when you have a website you need to have a _server_ \(machine\) where it lives. The _server_ is waiting for any incoming _requests_ \(letters that ask the server to send your website\) and it sends back your website \(in another letter\).

Since this is a Django tutorial, you will ask what Django does. When you send a response, you don't always want to send the same thing to everybody. It is so much better if your letters are personalized, especially for the person that has just written to you, right? Django helps you with creating these personalized, interesting letters :\).

Enough talk, time to create!

