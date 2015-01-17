#StorjでのPythonプログラミング

##1. Storjとは
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

##2.MetaDiskとDriveShareとは

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
まず、プログラムテンプレートを作りましょう。現状では、MetaDisk APIをつかったコードはありません。
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
jsonやurllib2のような基本的なライブラリのみを使うこともできますが、外部ライブラリである、
[requests](http://jp.python-requests.org/en/latest/) を使えば、httpやJSONを簡単に扱うことができます。
ここでは、このライブラリを使用します。[requestsライブラリをgithubからインストール](http://jp.python-requests.org/en/latest/latest/user/install/#install), するか、apt-get, pacmanを使用いてインストールしてください。
requestsライブラリの使い方は[ここ](http://jp.python-requests.org/en/latest/user/quickstart/)をみてください。クイックスタートをチェックすれば、この記事には十分です。

そしてMetaDiskサーバーとして http://node1.metadisk.org を使用します。ここでは、MetaDiskのベータ版が走っています。
ブラウザでこのアドレスにアクセスすれば、ファイルをアップロード／ダウンロードするウエブインターフェースを
見ることができます。

現状、MetaDiskはベータで、すべてのMetaDisk APIが使用可能ではなく、変更される可能性があること、また
アップロードされたファイルは定期的に削除されることに気をつけてください。

引数１が"upload"なら、このプログラムは引数２に指定されたファイルをStorjネットワークにアップロードし、
引数１が "download"ならネットワークからダウンロードし、標準出力い内容を出力します。

##5. MetaDisk APIを使う
すべてのMetaDisk APIsは[github](https://github.com/Storj/web-core#api-documentation)で確認できます。

まずアップロード・ダウンロードにいくつかのルールああることを知らないといけません。

* アップロード前に、Storjネットワークにアクセスするのに必要な”トークン”を取得しなければいけません。
* アップロード後、”ファイルハッシュ"と"キー"が得られます。これはStorjネットワークからダウンロードするのに必要です。

トークンを取得するAPIをチェックしましょう。

```
POST /accounts/token/new
Parameters: None

Normal result:
{
    "token": "adF7WFCpQR2EvFkG"
}
````

これは、 http://node1.metadisk.org/accounts/token/new へ、パラメータなしでポストすることを意味しています。
そして、返り値はJSONテキストで、キーが”トークン”です。なので、
[way of handling JSON](http://docs.python-requests.org/en/latest/user/quickstart/#json-response-content)を
使って下記のようにコードがかけます。
```
    r = requests.post(NODE_URL+"/accounts/token/new")
    j=r.json()
    token=j["token"]
```
jはキーと値がJSONのキーと値の、dictです。

結果、getToken関数は下記通りになるでしょう。

```
def getToken():
    r = requests.post(NODE_URL+"/accounts/token/new")
    j=r.json()
    token=j["token"]
    sys.stderr.write("token="+token+"\n")
    return token
```

同じように、アップロード用APIは下記通り説明されています。
```
POST /api/upload
Parameters:
- file
```
しかし、実際には下記のようです。
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
"file"は
[マルチパートエンコードされたファイルのPOST](http://jp.python-requests.org/en/latest/user/quickstart/#id7),なので、
[データのポスト方法](http://jp.python-requests.org/en/latest/user/quickstart/#post)と合わせて、
コードは下記通りなるでしょう。

```
def upload(file):
    token=getToken()
    r = requests.post(NODE_URL+"/api/upload", files={'file':(file,open(file,'rb'))},
            data={"token":token})
    j=r.json()
    key=j["filehash"]+"?key="+j["key"]
    print(file+" is uploaded. key=\n"+key+"\n")
```

このコードは、"key"という変数を作っています、というのはダウンロード時キーのフォーマットは
"<ファイルハッシュ>?key=<キー>"
でないといけないからです。

最後にダウンロードAPIは、
```
GET /api/download/<filehash>
Parameters:
- filehash
```
filehashは、上で作成した"key"を意味するようなので、

```
def download(key):
    r = requests.get(NODE_URL+"/api/download/"+key)
    print(str(r.content))
```

最終的にすべてのコードはこうなります。
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

このプログラムを実行すると、こんな感じです。
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

ダウンロードする際、キーをダブルクォーテーションでくくってください、というのは、
キーは=(イコール）を含んでおり、イコールはシェルでは特別な意味をなします。

正しくtest.datがアップロードされ、ダウンロードされているのがわかります。


    
##6. 結論
クラウドストレージプラットフォームStorjのアウトラインお説明をいました。そして
Pythonを用いてStorjネットワークへファイルをアップロードダウンロードする簡単なプログラムを作成しました。
MetaDiskを使用する他のプログラムをチェックしたければ、
[Storjtalkのこのスレ](https://storjtalk.org/index.php?topic=1492.0)をチェックしてください
もしMetaDisk APIを使った素晴らしいアイデアあ思いつけば、ぜひStorjtalkへ投稿いてみてください。
