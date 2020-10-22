.. _net:

====================
2. IT関連サービス
====================


構造やコンセプト
===================

とある企業の構造設定 其の壱
---------------------------

* 社内証明書サーバーからのサインした証明書が必要です。
* サインしたの証明書はメールが入っています。
* 有効期限以内の証明書があれば、社内WIFIや、VPNが使えます。
* VPNの最初は、ローカル持つの証明書をサーバーに検証する、確認できますの場合は接続とアカウントやパスワードなどの認証が可能です。
* VPNはMFA認証サービスが導入し、アカウント、パスワードと認証番号（MFA）はすべてが必要です。
* 社内はLDAP✙ADサーバがあります。社員はLDAP IDとAD IDが持ちます。パスワードが同じです。
* 社内ネットはVPN/Windowsログイン（？）でのSSO(Single Sign-On)があります。
* 社内SMSのMFAのサービスがありましたけど、その後は他のMFAクラウドサービスを使ってます。
* ITサービスはグローバルとして展開です、もし社内の使用者は問題があれば、Caseシステムを使って、ケースを開います。世界からのITエンジニヤがケースを受けます。

とある企業の構造設定 其の弐
---------------------------

* 社内サイトは共用の証明書があります。
* グローバルとしてLDAP✙ADサーバーがあります。
* MFAが導入します、すべてのLDAP/ADや使用しているITサービスはMFAのプラットフォームと連携します。
* 社内ネットは専用ネットで繋がってます。
* ネットワークケーブルはMACアドレスとDHCPで管理する。
* エンドポイントのセキュリティと安全が優先事項。
* コストとセキュリティのバランスで、一部のクラウドADも使用します。
* ITは社内が居ます、もし問題があれば、直接解決可能です。

ゼロから自分のIT考え方
------------------------

ITエンジニアの主な目的が二つ：

#. ユーザーが社内・社外仕事を成功の為にITを求めます。その上に色んなＩＴサービスを提供と連携する。
#. 一般的にはPCサポートが基本です。ユーザーを手伝うと基礎概念を教えるが重要です。

今まで居たの会社は大体グロバール展開企業、だからその上での考えが出発点です。

実際な環境と規模によって、段階的に準備と展開が重要です。

前に述べだ二点を目的として発展は次な結論ができます：

* ITのなかに色んな専門チームが必要です。世界全部のその専門技術の為に提供と支えます。
* 地域なITは集中提供とサポートが良いです。主のサービス提供が上の専門チームからです。
* 地域のITはできる限りまずにユーザーの問題解決が優先です、その上にはグローバルのQA経験システムが必要です。
* 地域なITは専門家と定期に技術討論会を開催する。
* できる限りにはITサービスポートるが必要です、上にはユーザー向けの基礎問題解決集とIT向けの経験システムを提供します。
* 他のはAI技術を使って、ネットから色んなIT技術を収集整理する、最も最新な情報や技術をまとめする。

``PS. ここまでは主に自分の経験です、まだ改善と環境によって改変が必要かもです。``

LDAP
==================

LDAPの技術は、元々は使用者認証と資料の保存と管理が開発理念です。

OpenLDAPというオープンプロジェクトがこの技術を開発して来ました。

LDAPはプラットフォームに依存しないプロトコルである。だから、Linux系、BSD系、アップルマックとWindowsなどのプラットフォームも動作可能です。

今の企業がのこ技術を利用しているのは大分、人との資料を管理、と他のサービスと連携するの身分認証です。

LDAPの構造は8数字が組合わせたのIDです、そのIDは、グループID＋ユーザーIDの構成です。

domainの概念のあります。

流行りの応用はマイクロソフト社のADと連携で使用するの場合が多いです。

**実際インストール**


M$ AD
===================


Azure AD
====================


IP・ネットワーク管理
======================


システムインストール
======================

インストールメディアの作成
------------------------------

公式や技術としては、macOSとLinuxの作り方がとても簡単です。複雑な部分はWindows OSだけです。

Windowsの更新とセキュリティパッチは非常に複雑も長いです、その上に出来れば最新版のメディアを入手がポイントです。

MacOS
^^^^^^^^^^^^^^^^^

基本はアップルマックのハードウェアと現存システムが必要です。

メディアのダウロードは直接アップルストアからで入手可能です。

それからのステップは簡単です、ストアからダウンロードしたとか確認すると、次のコマンドでbootable installerのUSBメディアを作成する。

*Catalina:*

``sudo /Applications/Install\ macOS\ Catalina.app/Contents/Resources/createinstallmedia --volume /Volumes/<Volume名>``

*Mojave:*

``sudo /Applications/Install\ macOS\ Mojave.app/Contents/Resources/createinstallmedia --volume /Volumes/<Volume名>``

*High Sierra:*

``sudo /Applications/Install\ macOS\ High\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/<Volume名>``

*El Capitan:*

``sudo /Applications/Install\ OS\ X\ El\ Capitan.app/Contents/Resources/createinstallmedia --volume /Volumes/<Volume名> --applicationpath /Applications/Install\ OS\ X\ El\ Capitan.app``


Linux
^^^^^^^^^^^^^

各Linuxの公式サイトから、インストールISOがあります。

直接でダウンロード可能です。

インストールメディアの作成は、もし同じLinuxシステムがあれば、システム内は関連ツールで直接作れます。

他には、おすすめの `UNetbootin`_ プロジェクトも簡単で作ります。

もしWindowsシステムで使うなら、ISOをダウンロードし、 `Rufus`_ のソフトで作るもおすすめです。

**公式サイト**

- Ubuntu https://www.ubuntulinux.jp/

- CentOS https://www.centos.org/

- Fedora https://getfedora.org/ja/

- Arch Linux https://www.archlinux.org/download/


Windows
^^^^^^^^^^^^^^^^

Windowsシステムのインストールと更新は最も面倒なシステムです。

今の技術でのUEFI BIOSやSecure Bootなどの技術も彼らが提出されたの。

現在Windowsのインストールメディアは大体ISOの中にのWIMやESDファイルがメインです。

オフィシャルから、現在は `メディア作成ツール`_ がありますけど、最新版ではないです。
便利で作成出来ますけど、システムをインストールすると、いっぱいなアップロードが必要でとても面倒です。

現在、Windows 10はinsiderというプロジェクトの状態で、一程度なESDをりりーすし、もっと最新版のイメージを提供するです。

でもそのESDは実際にインストール不可です、だから変換が必要です。

ESDファイルのおすすめダウンロードサイトはこちらです：https://tb.rg-adguard.net/public.php

ESDファイルを変換で、インストール可能にするなISOメディアのツールは `DECRYPT-MULTI-RELEASE`_ というツールがおすすめです。

DECRYPT-MULTI-RELEASE直接ダウンロード：https://rg-adguard.net/dl-decryp

他には、最新版のISOが欲しいけど、マイクロソフト社がリリースしていないという悩みがあれば、
あるグループな人が努力し、開発したのコマンドツールがあります。

そのツールはマイクロソフト社に直接最新版のアップデートとインストールファイルをダウンロードし、ISOファイルを作成します。
UUPというツールで名を付けました。

おすすめのUUPツールは二つのサイトから使用できます：

* UUP dump - https://uupdump.ml/
* UUP Generation Project (v2.4.10) [by @rgadguard & whatever127] - https://uup.rg-adguard.net/

最後の作業は簡単です。

それぞれ選んだソースから作成されたISOファイルをUSBメモリにインストールメディアを作るは、Rufusが一番おすすめです。

RUFUS(https://rufus.ie/)で作成のメディアは注意事項があります。 

``BIOSはUEFIモードなら、パーティションの構成はGPTが必要です。あとはもしSECURE BOOTのモードがあれば、ファイルシステムは必ずFAT32が必要です。``

USBのメディアはこうして作成します。


ディスクのパーティション
-------------------------

インストール方法
------------------------


.. _UNetbootin: https://unetbootin.github.io/
.. _Rufus: https://rufus.ie/
.. _メディア作成ツール: https://go.microsoft.com/fwlink/?LinkId=691209
.. _DECRYPT-MULTI-RELEASE: https://rg-adguard.net/decrypt-multi-release/