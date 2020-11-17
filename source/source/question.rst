.. _question:

============
[疑]. 問題集
============


システムエラー
================


Windows 10をスタートアップすると、BSODで"NTFS FILE SYSTEM"とのSTOP CODEが出てくる
-----------------------------------------------------------------------------------

A: この状況が発生する時、大体はSafe Modeも入れないです。

まずは以下の状況を試す、もし何もできない場合は、ハードウェアが問題ありの方向で考えます。

* 回復モードのターミナルを開います。もしBitLockerがセットするの場合があれば、回復キーを入力してください。
* diskpartを使って、パーティションの状況を確認。 ``diskpart`` ``lis dis`` ``sel dis <num>`` ``lis par``。
* パーティションが見える場合は、大体ハードウェアの問題ではないで確認できます。
* ハードウェアではないの状況として、次のコマンドで修復する

  * ``chkdsk /f C:`` C[システム]ディスクの検索やインデックスを検証と回復する。**大体このステップで修復できます。**
  * ``cd C: && C: && sfc /scannow`` システムの実際エラーを回復する。 「C」はシステムが居るの場所。
  * ``cd C: && C:`` でシステムの場所に確定、 ``DISM /Online /Cleanup-Image /CheckHealth``
  * ``cd C: && C:`` でシステムの場所に確定、 ``DISM /Online /Cleanup-Image /RestoreHealth``
  * 外部で修復： ``DISM /Online /Cleanup-Image /RestoreHealth /Source:F:\Sources\install.wim`` Fがインストールメディアの場所です。


WSUSを使うのWindows 10が0x8024401cのエラー
--------------------------------------------

まずはサーバーとクライアントの接続を試します。::

  ping <WSUS_Server_IP>
  telnet <WSUS_Server_IP>:<WSUS_Port>

それから、問題がない場合、サーバーのハードウェアやパフォーマンスを考えます：

* ＷＳＵＳでダウロードしたの更新パッケージが多すぎ？
* ＷＳＵＳのハードウェア、処理能力が足りない？
* もし、サーバーが2012もはや古いシステムなら、特定なパッチをインストールしましたか？

  * パッチ：https://cloudblogs.microsoft.com/windowsserver/2014/04/16/windows-server-2012-r2-update-availability-of-wsus-fix-and-revised-servicing-timing/
  * ESDサポート：https://support.microsoft.com/en-us/help/3159706/update-enables-esd-decryption-provision-in-wsus-in-windows-server-2012

* サーバーのＩＩＳサービスにＷＳＵＳプールのリソースが足りない？ **更新の量が多い場合やクライアントが多いの場合**

　* WSUS Server 2016 Best Practice https://askme4tech.com/wsus-best-practices-windows-server-2016
  * メモリが足りない：https://www.saotn.org/wsuspool-keeps-crashing-stops/


WSUSを指定したのPCはMicrosoftストアもはや追加機能がエラー
-----------------------------------------------------------

これは設定と観念の問題です。 WSUSサーバーは本来、追加機能や言語パックなどの更新やパッケージもダウンロードとコントロール可能です。

だから、もしWSUSサーバーはセキュリティだけのパッケージをダウロードとインストール用なら、グループポリシーの変更が必要です。

GPedit.mscを開いて、以下のパスがに変更する：

* ローカル コンピューター ポリシー ＞ コンピューターの構成 ＞ 管理用テンプレート ＞ システム

  * **オプション コンポーネントのインストールおよびコンポーネントの修復のための設定を指定する**
  * ↑のポリシーを有効して、↓の選択をチェックする。
  * ☑ Windows Server Update Service (WSUS)の代わりに、Windows Updateから修復コンテンツとオプションの機能を直接ダウロードする

適用されて、システムを再起動がおすすめです。


WSLのフォントとVScodeの設置
-----------------------------

VScodeをWSLに接続すると、フォントを見やすいなMigu 1Mを変更したいの場合。

まずはMigu 1Mを公式サイトにダウンロード：https://mix-mplus-ipa.osdn.jp/migu/

ダウンロードしたのZipを解凍する、以下のフォルダにコピーする::

  [WSL]$ mkdir /usr/share/fonts/truetype/Migu\ 1M
  [WSL]$ cp *ttf /usr/share/fonts/truetype/Migu\ 1M/

最後はVScode内に、設定での"Remote[WSL:ubuntu]"タグ、Editor: Font Familyに'Migu 1M'を追加します。


システムインストール
======================


RufusでWindowsインストールメディアを作成とエラーが出る。
--------------------------------------------------------

A: explorer.exeのプロセスを停止すると、正常に作ることができます。 ::

    tasklist | find "explorer.exe"
    taskkill /F /PID <pid_number>

    explorer.exe