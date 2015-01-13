#Python programming in Storj

##1. About Storj

Storj (pronounced: storage) aims to become a cloud storage platform that can’t be censored or monitored, 
or have downtime. Storj is a platform, cryptocurrency, and suite of decentralized applications that allows users
to store data in a secure and decentralized manner. It uses blockchain features like a transaction ledger, 
public/private key encryption, and cryptographic hash functions for security. Furthermore, 
it will be way cheaper (10x-to-100x), faster, and more secure than traditional cloud storage services.

Storj is working hard to solve data security issues with the help of its own web app, [MetaDisk](http://metadisk.org/), 
and client app, [DriveShare](http://driveshare.org/). It is the first decentralized, end-to-end encrypted cloud storage 
that uses blockchain technology and cryptography to secure online files. 
There is no need to trust a corporation, vulnerable servers,
or employees with your files. Storj completely removes trust from the equation.

To best protect your data, files are encrypted client-side on users’ computers
before they are uploaded. Each file is split up into chunks which are first encrypted
and then distributed for storage across the Storj network. The network is comprised of DriveShare nodes 
run by users around the world who rent out their unused hard drive space in return for Storjcoin X (SJCX).

The decentralized aspect of Storj means there are no central servers to be compromised, 
and because of the use of client-side encryption, only the end-users have access to their unencrypted files 
and encryption keys.

##2. About MetaDisk and DriveShare.

MetaDisk is an open-source file sharing app that is based on a decentralized network of nodes and is the first application built on top of the Storj platform. These nodes are all around the world and act as a network to host all of the data that goes through MetaDisk.

Each file is shredded, encrypted, and then distributed across the network to achieve maximum security. Only the original uploader of the files has the private keys to decrypt and open them.

MetaDisk is our end user application that allows users to store files on the network. With MetaDisk you will be able to store, download, and share all of your files securely.

DriveShare is an open-source application that allows users to rent out their excess hard drive space in exchange for SJCX. This software works in conjunction with Metadisk. Those running Driveshare will act as decentralized cloud storage nodes for the network.

##3. Uploading files to / Downloading files from Storj Network
MetaDisk has web interface, which is composed of only html, css and javascript. If you want only just upload/download 
files across Storj network, you can use this interface without creating new program. It is same as the legacy 
clowds, like dropbox, google, etc.

But MetaDisk also has web-core. Web interface uses web-core as the backend server. Web-core provides a JSON API web service. And this JSON API is open for everyone, unlike most legacy clowds. It means you can easiy and freely create 
programs using Storj network.

You can use any program languages, like javascript, golang, java, ruby, C, etc..., 
bacause almost languages have (external or basic) library  that can handle JSON.
In this article, we will make a simple program that donwloads/uploads files by using JSON API in Python.

I assume you have already installed Python3, and are familiar with basic Python usage.

## tempalte for program
First let's make a template for program.
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
You can only use basic library, like json or urllib2, but external library (request)[http://docs.python-requests.org/en/latest/] is more easy for handling json and http get/post. So we will use this library. Please install requests library (from github)[http://docs.python-requests.org/en/latest/user/install/#install], or by using apt-get, pacman, etc.

And we will use "http://node1.metadisk.org" as MetaDisk server, where beta MetaDisk is running. When you access
this address by browser, you can see web interface for uploading/downloading files.

When argument 1 is "upload", this program  uploads file specified argument 2 toStorj network. When argument 1 is "download", it downloads from network to stdout.

##4. Using JSON API
You can check the usage of all JSON APIs at [here](https://github.com/Storj/web-core#api-documentation).

First you should know that there are some rules for uploading/downloading:

* Before uploading, you should get "token", which is neccsary for accesing Storj network.
* After uploading, you can get "file hash" and "key", which is nessary for downloading from Storj network.

and check the API for getting token.

```
POST /accounts/token/new
Parameters: None

Normal result:
{
    "token": "adF7WFCpQR2EvFkG"
}
````

This means you must post to 

POST /api/upload
Parameters:
- file

