#python programming in Storj.md

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

But MetaDisk also has web-core. Web interface uses web-core as the backend server. Web-core provides a JSON API web service. And this JSON API is open for everyone, not like legacy clowds. It means you can freely make programs using 
Storj network.

In this article, we will make a simple CLI python program using JSON API by python. In fact you can use
any program languages, like javascript, golang, java, ruby, C, etc..., bacause almost languages have 
(external or basic) library  that can handle JSON.

