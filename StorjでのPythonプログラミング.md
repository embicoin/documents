#StorjでのPythonプログラミング

##1. Storj
Storj（ストレージと発音します）は、検閲監視されることなく、
またシステムダウンすることのないのクラウドストレージプラットフォームとなることを目指しています。
Storjは、ユーザーが安全かつ分散的にデータを保存することができる、分散型アプリケーションのプラットフォーム、
暗号通貨、およびスイートです。セキュリティのため、取引記録、公開鍵/秘密鍵の暗号化、
および暗号化ハッシュ関数のようなブロックチェーン機能を使用しています。さらに、
伝統的なクラウドストレージサービスよりもより早く（10倍〜100倍）、より安く、より安全です。

Storjは、独自のWebアプリケーション、MetaDiskのヘルプ、およびクライアントアプリ、
DriveShareとデータセキュリティの問題を解決するために取り組んでいます。
それはブロックチェーン技術とオンラインのファイルを確保する暗号技術を使用する最初の分散化、
エンドツーエンドの暗号化されたクラウドストレージです。会社、脆弱なサーバー、
または従業員を信頼する必要はありません。 Storjは信頼を必要としません。

ファイルがアップロードされる前に、最善にデータを保護するために、
ファイルはユーザーのコンピュータのクライアント側で暗号化されます
。各ファイルは、最初に暗号化され、その後Storjネットワークのストレージに分散され、
チャンクに分割されます。ネットワークは、Storjcoin X（SJCX）と引き換えに、
未使用のハードドライブの空き容量を貸し出す世界中のユーザーによって実行されたDriveShareノードで構成されています。

Storjの分散化の側面は、妥協すべき中央サーバが存在せず、クライアント側の暗号化を使用することにより、
唯一エンドユーザーが、暗号化されていないファイルや暗号化キーへのアクセス権を持っていることを意味します。

##2.MetaDiskとDriveShare

MetaDiskはノード分散型ネットワークをベースとするオープンソースのファイル共有アプリであり、
Storjプラットフォーム上に構築された最初のアプリケーションです。
ノードは、全世界にあり、MetaDiskを通過するすべてのデータをホストするネットワークとして振る舞います。
各ファイルは、最大限のセキュリティを実現するため分断され暗号化してから、ネットワーク全体に分散されます。
ファイルのオリジナルのアップローダーのみがファイルを復号化し、それらを開くための秘密鍵を持っています。
MetaDiskは、ネットワーク上のファイルを保存することができる、エンド·ユーザー·アプリケーションです。
MetaDiskを使用すると、すべてのファイルを安全に保存・ダウンロード及び共有することができます。

DriveShareはユーザーがSJCXと引き換えに余分なハードドライブの空き容量を貸し出すことを可能にする
オープンソースのアプリケーションです。このソフトウェアは、MetaDiskと連携して動作します。
実行中のDriveshareは、ネットワークで分散型クラウドストレージノードとして機能します。

##3. Storjネットワークへのファイルのアップロード／ダウンロード
MetaDiskはhtml,css,javascriptだけでで構成されるウエブインターフェースをもちます。
もし、ファイルを単にアップロード・ダウンロードしたければ、新たにプログラムを作ることなくこのインターフェースを
使うことができます。これはちょうどdropboxやgoogle等のレガシーなクラウドと同じです。

しかし、MetaDiskはweb-coreももっています。ウエブインターフェースはバックエンドサーバにweb-coreを使用しています。
web-coreはMetaDisk APIを提供しています。そしてレガシーなクラウドは違いMetaDisk APIは全員にオープンです。
これにより、簡単に自由にStorjネットワークを使用したプログラムを作ることができます。
ネットワーク上に自分のアプリをつくり、みんなにファイルを保存してもらい、自分のビジネスを構築することが
できます。

MetaDisk APIはJSONを使用いており、JSONはほとんどのプログラムで（組み込みまたは外部の）
ライブラリとしてJSONを扱えるのでjavas javascript, golang, java, ruby, Cのようなどんなプログラム言語を使用できます。
この記事では、PythonでMetaDisk APIを使った、簡単なファイルのダウンロード・アップロードプログラムを作っていきます。

すでにPython3がインストールされ、基本的なPythonの使い方に慣れ親しんでいる前提とします。

##4. プログラムテンプレート
まず、プログラムテンプレートを作りましょう。現状では、MetaDisk APIをつかったコードあありません。
```
#!/usr/bin/env python

import requests
import sys
from sys import argv, exit

NODE_URL="http://node1.metadisk.org"

#code for getting token
def getToken():

#code for uploading <file> to Storj network
def upload(file):

#code for downloading from Storj network to stdout
def download(key):

def help():
    print('download usage: %s download <key>' % argv[0])
    print('upload   usage: %s upload   <filename>' % argv[0])

if __name__ == '__main__':
    if len(argv) != 3:
        help()
        exit(1)
    if argv[1]=="download":
        download(argv[2])
    else:
        if argv[1]=="upload":
            upload(argv[2])
        else:
            help()

```
You can only use basic library, like json or urllib2, but external library [request](http://docs.python-requests.org/en/latest/) makes handling json and http easier . So we will use this library. Please [install requests library from github](http://docs.python-requests.org/en/latest/user/install/#install), or by using apt-get, pacman, etc.
The usage of requests library can be referred in [here](http://docs.python-requests.org/en/latest/user/quickstart/).
If you only check quickstart, it's sufficient for this article.

And we will use http://node1.metadisk.org as MetaDisk server, where beta MetaDisk is running. When you access
this address by your browser, you can see web interface for uploading/downloading files.

Please remind that now MetaDisk is beta, so not all MetaDisk API is usable, all APIs are subject to change,
and uploaded files are removed periodically.

When argument 1 is "upload", this program  uploads file specified argument 2 to Storj network. When argument 1 is "download", it downloads from network, and outputs to stdout.

##5. Using MetaDisk API
You can check the usage of all MetaDisk APIs  at [github](https://github.com/Storj/web-core#api-documentation).

First you should know that there are some rules for uploading/downloading:

* Before uploading, you must get a "token", which is necessary for accessing Storj network.
* After uploading, you can get "file hash" and "key", which are necessary for downloading the file from Storj network.

Let's check the API for getting token.

```
POST /accounts/token/new
Parameters: None

Normal result:
{
    "token": "adF7WFCpQR2EvFkG"
}
````

This means you must post to http://node1.metadisk.org/accounts/token/new, without parameter. And the return is the JSON text, whose key is "token". So you can write the code by using the [way of handling JSON] (http://docs.python-requests.org/en/latest/user/quickstart/#json-response-content)
```
    r = requests.post(NODE_URL+"/accounts/token/new")
    j=r.json()
    token=j["token"]
```
j is the dict whose keys and values are ones of JSON.

As a result the function getToken should be:
```
def getToken():
    r = requests.post(NODE_URL+"/accounts/token/new")
    j=r.json()
    token=j["token"]
    sys.stderr.write("token="+token+"\n")
    return token
```

In a same manner, API for uploading is explained as:
```
POST /api/upload
Parameters:
- file
```
but in fact, it seems :
```
POST /api/upload
Parameters:
- file
- token
Normal result:
{
    "filehash": "xxxxxx"
    "key": "xxxxx"
}
```
"file" means
[multipart encoded file](http://docs.python-requests.org/en/latest/user/quickstart/#post-a-multipart-encoded-file), 
so by using it with 
[the way of posting data](http://docs.python-requests.org/en/latest/user/quickstart/#more-complicated-post-requests),
code should be:

```
def upload(file):
    token=getToken()
    r = requests.post(NODE_URL+"/api/upload", files={'file':(file,open(file,'rb'))},
            data={"token":token})
    j=r.json()
    key=j["filehash"]+"?key="+j["key"]
    print(file+" is uploaded. key=\n"+key+"\n")
```

This code creates a variable named "key", because when downloading, format of key must be "<filehasah>?key=<key>".

At the end, download API is
```
GET /api/download/<filehash>
Parameters:
- filehash
```
filehash seems to mean the "key" created above, so

```
def download(key):
    r = requests.get(NODE_URL+"/api/download/"+key)
    print(str(r.content))
```

Finally all code should be:
```
#!/usr/bin/env python

import requests
import sys

from sys import argv, exit

NODE_URL="http://node1.metadisk.org"

def getToken():
    r = requests.post(NODE_URL+"/accounts/token/new")
    j=r.json()
    token=j["token"]
    sys.stderr.write("token="+token+"\n")
    return token

def upload(file):
    token=getToken()
    r = requests.post(NODE_URL+"/api/upload", files={'file':(file,open(file,'rb'))},
            data={"token":token})
    j=r.json()
    key=j["filehash"]+"?key="+j["key"]
    print(file+" is uploaded. key=\n"+key+"\n")


def download(key):
    r = requests.get(NODE_URL+"/api/download/"+key)
    print(str(r.content))

def help():
    print('download usage: %s download <key>' % argv[0])
    print('upload   usage: %s upload   <filename>' % argv[0])

if __name__ == '__main__':
    if len(argv) != 3:
        help()
        exit(1)
    if argv[1]=="download":
        download(argv[2])
    else:
        if argv[1]=="upload":
            upload(argv[2])
        else:
            help()

```

When you run this program, it looks like:
```
[utamaro@nowhere ~]$ python storj.py 
download usage: storj.py download <key>
upload   usage: storj.py upload   <filename>

[utamaro@nowhere ~]$ echo "test data" > test.dat

[utamaro@nowhere ~]$ python storj.py upload test.dat
token=8puTA1fjG8sg5zf2
test.dat is uploaded. key=
0c12e76f671e6056b3be9af526acf1f6ca3d42d9066c811c9bceae560f3791cc?key=31292df8fd0ec1d5c3904fc12a4c90ca1f2425e0aaad1e6171970fddb904a823

[utamaro@nowhere ~]$ python storj.py download "0c12e76f671e6056b3be9af526acf1f6ca3d42d9066c811c9bceae560f3791cc?key=31292df8fd0ec1d5c3904fc12a4c90ca1f2425e0aaad1e6171970fddb904a823"
b'test data\n
```
Be careful to use double-quotation to specify the key when downloading because key includes =(equal), which has special meaning for shell.

You can see test.dat is uploaded, and downloaded successfully.


    
##6. Conclusion
I explained the outline of Storj, which is cloud storage platform. And I wrote a 
simple program for uploading  /downloading files across Storj network by using Python.
If you want to check the other programs using MetaDisk API, check [this thread in Storjtalk](https://storjtalk.org/index.php?topic=1492.0). 
If you have an excellent idea that uses MetaDisk API, don't hesitate to post your idea to Storjtalk!
