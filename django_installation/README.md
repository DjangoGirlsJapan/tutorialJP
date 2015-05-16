# Django installation
#Django�Υ��󥹥ȡ���
> Part of this chapter is based on tutorials by Geek Girls Carrots (http://django.carrots.pl/).> ���Υ���ץ����ΰ�����Geek Girls Carrots (http://django.carrots.pl/)�Υ��塼�ȥꥢ��˴�Ť��Ƥ��ޤ���

> Part of this chapter is based on the [django-marcador 
tutorial](http://django-marcador.keimlink.de/) licensed under Creative Commons
Attribution-ShareAlike 4.0 International License. The django-marcador tutorial
is copyrighted by Markus Zapke-Gründemann et al.

> ���Υ���ץ����ΰ�����Creative Commons Attribution-ShareAlike 4.0 International License �Υ饤���󥹤ˤ��[django-marcador tutorial](http://django-marcador.keimlink.de/)�˴�Ť��Ƥ��ޤ�������django-marcador tutorial��Markus Zapke-Gründemann et al.���������ͭ���Ƥ��ޤ���

## Virtual environment
## ���۴Ķ�

Before we install Django, we'll get you to install an extremely useful tool that will help keep your coding environment tidy on your computer. It's possible to skip this step, but it's highly recommended not to - starting with the best possible setup will save you a lot of trouble in the future!

Django�򥤥󥹥ȡ��뤹�����ˡ��ޤ��Ϥ��ʤ��Υ���ԥ塼������Υ����ǥ��󥰴Ķ��򤭤줤�ˤ��Ƥ����Τ���Ω�ĤȤƤ�������ƻ��򥤥󥹥ȡ��뤷�Ƥ�餤�ޤ������Υ��ƥåפ�ȤФ����Ȥ�Ǥ��ޤ����������������Υ��ƥåפ�ȤФ����Ȥ����������ᤷ�ޤޤ��󡣲�ǽ�ʸ¤�٥��Ȥʥ��åȥ��åפǻϤ�뤳�ȤϾ���Τ�������Υȥ�֥뤫�餢�ʤ���ߤ��Ϥ��Ǥ����顪

So, let's create a **virtual environment** (also called a *virtualenv*). It will isolate your Python/Django setup on a per-project basis, meaning that any changes you make to one website won't affect any others you're also developing. Neat, right?

������**virtual environment** (*virtualenv*�Ȥ�ƤФ�Ƥ��ޤ�)����ޤ��礦��virtual environment�ϥץ�������ñ�̤Ǥ��ʤ���Python/Django���åȥ��åפ�¾�����Υ���ޤ����Ĥޤꡢ���ʤ����ҤȤĤΥ����֥����Ȥˤ����ʤä��ɤ���ѹ��⤢�ʤ�����ȯ���¾�Υ����Ȥ˱ƶ���ڤܤ��ʤ��Ȥ������ȤǤ����狼��ޤ�������

All you need to do is find a directory in which you want to create the `virtualenv`; your home directory, for example. On Windows it might look like `C:\Users\Name\` (where `Name` is the name of your login).

���ʤ������ʤ���Фʤ�ʤ��Τϡ����ʤ���'virtualenv'������������ǥ��쥯�ȥ�򸫤Ĥ��뤳�ȤǤ��ʤ��Ȥ��Хۡ���ǥ��쥯�ȥ�ʤɤǤ��ˡ�Windows�Ǥϡ��ۡ���ǥ��쥯�ȥ��`C:\Users\Name\`�Ƚ񤫤�Ƥ��뤫�⤷��ޤ��� (`Name`�Ϥ��ʤ��Υ�����͡���Ǥ�)��

For this tutorial we will be using a new directory `djangogirls` from your home directory:

���Υ��塼�ȥꥢ��Τ���ˡ��ۡ���ǥ��쥯�ȥ�˿������ǥ��쥯�ȥ�`djangogirls'��������ޤ���

    mkdir djangogirls
    cd djangogirls

We will make a virtualenv called `myvenv`. The general command will be in the format:

`myvenv`�Ȥ���virtualenv��������ޤ�������Ū�ʥ��ޥ�ɤϰʲ��Τ褦�ˤʤ�ޤ���

    python3 -m venv myvenv

### Windows

To create a new `virtualenv`, you need to open the console (we told you about that a few chapters ago - remember?) and run `C:\Python34\python -m venv myvenv`. It will look like this:

������`virtualenv`��������뤿��ˡ����󥽡���򳫤��ʥ��󥽡���ˤĤ��Ƥϲ��Ϥ����ˤ��ä����ޤ����͡��Ф��Ƥޤ������ˡ�`C:\Python34\python -m venv myvenv`��¹Ԥ��Ʋ����������Ȥ��Ф��Τ褦�����Ϥ��ޤ���

    C:\Users\Name\djangogirls> C:\Python34\python -m venv myvenv

where `C:\Python34\python` is the directory in which you previously installed Python and `myvenv` is the name of your `virtualenv`. You can use any other name, but stick to lowercase and use no spaces, accents or special characters. It is also good idea to keep the name short - you'll be referencing it a lot!

`C:\Python34\python`�Ϥ��ʤ���Python�򥤥󥹥ȡ��뤷���ǥ��쥯�ȥꡢ`myvenv`�Ϥ��ʤ���'virtualenv'��̾���Ǥ����ɤ��̾���Ǥ�Ȥ����Ȥ��Ǥ��ޤ�����ɬ����ʸ����ɽ���������ڡ�������������ȵ��桦�ü�ʸ��������ʤ��Ǥ���������û��̾���ˤ��Ƥ����Τ⤤�������ǥ��Ǥ������ʤ��Ϥ���̾�����٤⻲�Ȥ��ޤ����顪

### Linux and OS X

Creating a `virtualenv` on both Linux and OS X is as simple as running `python3 -m venv myvenv`.

Lnux��OX X��'virtualenv'����Ȥ��ϡ�`python3 -m venv myvenv`�ȼ¹Ԥ�������Ǥ���

It will look like this:

���Ȥ��Ф���ʴ����Ǥ���

    ~/djangogirls$ python3 -m venv myvenv

`myvenv` is the name of your `virtualenv`. You can use any other name, but stick to lowercase and use no spaces. It is also good idea to keep the name short - you'll be referencing it a lot!

`myvenv`�Ϥ��ʤ���`virtualenv`��̾���Ǥ����ɤ��̾���Ǥ�Ȥ����Ȥ��Ǥ��ޤ�����ɬ����ʸ����ɽ���������ڡ���������ʤ��Ǥ���������û��̾���ˤ��Ƥ����Τ⤤�������ǥ��Ǥ������ʤ��Ϥ���̾�����٤⻲�Ȥ��ޤ����顪

> __NOTE:__ Initiating the virtual environment on Ubuntu 14.04 like this currently gives the following error:

> __����:__ ������ˡ�ˤ��Ubuntu 14.04�Ǥ�virtual environment�ν�����ϼ��Υ��顼���Фޤ���

>     Error: Command '['/home/eddie/Slask/tmp/venv/bin/python3', '-Im', 'ensurepip', '--upgrade', '--default-pip']' returned non-zero exit status 1

> To get around this, use the `virtualenv` command instead.

> ���Υ��顼����򤹤뤿��ˡ������`virtualenv`���ޥ�ɤ�Ȥ��ޤ���

>     ~/djangogirls$ sudo apt-get install python-virtualenv
>     ~/djangogirls$ virtualenv --python=python3.4 myvenv


## Working with virtualenv
## virtualenv��Ȥ�

The command above will create a directory called `myvenv` (or whatever name you chose) that contains our virtual environment (basically a bunch of directory and files). All we want to do now is start it by running:

��˼��������ޥ�ɤϲ��۴Ķ��ʴ���Ū�ˤϰ�Ϣ�Υǥ��쥯�ȥ�ȥե�����ˤ�ޤ�`myvenv`�Ȥ���̾���ʤ��뤤�Ϥ��ʤ��������̾���ˤΥǥ��쥯�ȥ���������ޤ������˲桹���������Τϡ������¹Ԥ������Ϥ��뤳�ȤǤ���

Windows�ǤϤ��Τ褦�����Ϥ��Ƥ���������

    C:\Users\Name\djangogirls> myvenv\Scripts\activate

on Windows, or:

���뤤��OS X��Linux�Ǥϰʲ��Τ褦�����Ϥ��Ʋ�������

    ~/djangogirls$ source myvenv/bin/activate

on OS X and Linux.

Remember to replace `myvenv` with your chosen `virtualenv` name!
`myvenv`�ΤȤ���򤢤ʤ��������`virtualenv`̾���֤������뤳�Ȥ�˺��ʤ��ǲ������͡�

> __NOTE:__ sometimes `source` might not be available. In those cases try doing this instead:
> __����:__ �Ȥ��ɤ�`source`�����ѤǤ��ʤ����⤷��ޤ��󡣤��ξ��ϡ�����˰ʲ��Τ褦�����Ϥ��ƤߤƤ���������

>     ~/djangogirls$ . myvenv/bin/activate



You will know that you have `virtualenv` started when you see that the prompt in your console looks like:

���ʤ��Υ��󥽡���Υץ��ץȤ��ʲ��Τ褦��ɽ�������Τ򸫤ơ����ʤ���`virtualenv`����ư�������Ȥ˵����Ĥ��Ǥ��礦��

    (myvenv) C:\Users\Name\djangogirls>

or:
���뤤�Ϥ�������ɽ�����⤷��ޤ���

    (myvenv) ~/djangogirls$

Notice the prefix `(myvenv)` appears!

��Ƭ��`(myvenv)`�����줿�Τ����ܤ��Ʋ�������

When working within a virtual environment, `python` will automatically refer to the correct version so you can use `python` instead of `python3`.

virtual environment(���۴Ķ�)����Ǻ�Ȥ��Ƥ���Ȥ���`python`�ϼ�ưŪ���������С�������Python�򻲾Ȥ��ޤ��Τǡ�'python3'�������'python'��Ȥ����Ȥ��Ǥ��ޤ���

OK, we have all important dependencies in place. We can finally install Django!

OK���桹�����Ƥν��פʴ�Ϣ���ܤ����֤��ޤ������Ĥ���Django�򥤥󥹥ȡ��뤹�뤳�Ȥ��Ǥ��ޤ���

## Installing Django
##Django�Υ��󥹥ȡ���
Now that you have your `virtualenv` started, you can install Django using `pip`. In the console, run `pip install django==1.8` (note that we use a double equal sign: `==`).

���ޤ��ʤ���`virtualenv`�ϵ�ư���Ƥ���Τǡ�'pip'��Ȥä�Django�򥤥󥹥ȡ��뤹�뤳�Ȥ��Ǥ��ޤ������󥽡������ǡ�`pip install django==1.8`(�����Ǥϥ��֥륤�����륵���� `==` ��Ȥ��ޤ�)�ȼ¹Ԥ��Ʋ�������

    (myvenv) ~$ pip install django==1.8
    Downloading/unpacking django==1.8
    Installing collected packages: django
    Successfully installed django
    Cleaning up...

on Windows

Windows�ξ��

> If you get an error when calling pip on Windows platform please check if your project pathname contains spaces, accents or special characters (i.e. `C:\Users\User Name\djangogirls`). If it does please consider moving it to another place without spaces, accents or special characters (suggestion is: `C:\djangogirls`). After the move please try the above command again.

> Windows��pip��Ƥ���Ȥ��˥��顼�����������ϡ����ʤ��Υץ������ȤΥѥ�̾�����ڡ�������������ȡ��ü�ʸ����ޤ�Ǥ��ʤ�����ǧ���ƤߤƲ����� (�� `C:\Users\User Name\djangogirls`)���⤷�ޤޤ�Ƥ�����ϡ����Υǥ��쥯�ȥ��¾�Υ��ڡ�������������ȡ��ü�ʸ�����ޤޤ�Ƥ��ʤ�����`C:\djangogirls`�ʤɡˤ˰�ư���뤳�Ȥ�Ƥ���ƤߤƤ�����������ư�������Ȥ˾嵭�Υ��ޥ�ɤ��ƤߤƤ���������

on Linux

Linux�ξ��

> If you get an error when calling pip on Ubuntu 12.04 please run `python -m pip install -U --force-reinstall pip` to fix the pip installation in the virtualenv.

> Ubuntu 12.04��pip��Ƥ���Ȥ��˥��顼�����������ϡ�virtualenv���pip���󥹥ȡ����ե��å������뤿���`python -m pip install -U --force-reinstall pip`��¹Ԥ��Ʋ�������

That's it! You're now (finally) ready to create a Django application!

�ʾ�Ǥ������ʤ��ϡʤĤ��ˡ�Django���ץꥱ�������������������������ޤ�����