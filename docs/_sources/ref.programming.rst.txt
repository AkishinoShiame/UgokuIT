.. _ref.programming:

==========================
#Ref.2 プログラミング
==========================

Python
========


Bash/Shell
===========

ping
-----

pingコマンドは、他のホストが生存確認用のツールです。

普通よ用法は ``ping <ターゲットIP>``  。

他は ``-c 数字`` を何回を確認するです。


nslookup
---------

このコマンドは、IP <=> FQDN の変換と確認です。

デフォルトは、 ``nslookup <IP>`` と ``nslookup <FQDN>``　で確認可能です。

もっと確認出来ますのは、後ろをDNS IPを入力し、特定なDNSに検索可能です。

例えば ``nslookup <IP> <DNS_IP>``


less
-----

知りたいものを多すぎの時、lessを使って、ゆっくりで見えます。

普段は ``<他のコマンド> | less`` を使って場合が多いです。

他のオススメは ``less -S`` を使うことです。


tar
----

パッケージ用のコマンド。

圧縮 ``tar -zcvf xxxx.tar.gz <directory>``

解凍 ``tar -zxvf xxxx.tar.gz``

圧縮 ``tar -Jcvf xxxx.tar.xz <directory>``

解凍 ``tar -Jxvf xxxx.tar.xz``

圧縮 ``tar -cvf xxxx.tar <directory>``

解凍 ``tar -xvf xxxx.tar``


zip
----

パッケージ用のコマンド。

圧縮 ``zip -r xxxx.zip <directory>``

解凍 ``unzip xxxx.zip``


cut
----

資料を分裂する。

普通はファイルの処理が多いです ``cut -f <1,2,4-5> -d, <filename>``

``-f`` は表示されたいセルを指示。

``-d`` は分割の基準文字や特殊文字です。

他にも `` <コマンド> | cut `` の使用も多いです。

awk
----

これは ``cut`` とは似ているコマンド。

普通は ``awk '{print $1}' `` という使う方が多いです、分割の基本文字は" "空白です。 ``$<数字>`` を使うは何列を表示するです。

もっとは ``-F "¥t"`` を使って、分裂文字を変更する。


sed
----

文字を変わる用のコマンドです。

基本は ``sed -i 's/original/new/g'`` の用法です。 文字を<original>から<new>に変更する。

column
-------

テーブルとして、色んなファイルを整理するコマンドです。


Go
======

