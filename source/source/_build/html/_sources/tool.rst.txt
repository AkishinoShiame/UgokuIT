.. _tool:

=================
[おまけ]. ツール
=================


パスワード作るツール
====================

* Python3環境(Ubuntu) `パスワード作る、zipフォーマット`_
* Python3環境(Ubuntu) `パスワード作る、tar.gzフォーマット`_


Windowsの最新イメージを作成ツール
=================================

* `ESDや色んなソフトウェアダウロード`_
* `decrypt-multi-release`_
* `adguard UUP 選択ツール`_
* `UUP Dump の公式サイト`_
* `Rufusツール`_


ハードウェア・ドライブ・資料回復/消す
=====================================

* `CrystalDiskInfo`_ HDD・SSD検査ソフトウェア
* `CPU-Z`_ ハードウェア確認ソフトウェア
* `Kill Disk`_ ストレージを物理で消すツール 
* `UndeletePlus`_ 資料回復
* `HDD Regenerator`_ HDD BadSector 回避ツール


開発環境用
==========

* GitHubとSSH自動認証

.. code-block:: bash
  :linenos:

  FileName:gitssh.sh

  #!/usr/bin/expect -f
  spawn ssh-add
  expect "Enter passphrase for /root/.ssh/id_rsa:"
  send "<passphraseパスワード>\n";
  # expect "Identity added: /root/.ssh/id_rsa (/root/.ssh/id_rsa)"
  interact

.. code-block:: bash
  :linenos:
  
  FileName:.bashrc

  前略
  ..

  # github ssh agent auto complete
  SSH_ENV="$HOME/.ssh/agent-environment"
  
  function start_agent {
          echo "Initialising new SSH agent..."
          /usr/bin/ssh-agent | sed 's/^echo/#echo/' > "${SSH_ENV}"
          echo succeeded
          chmod 600 "${SSH_ENV}"
          . "${SSH_ENV}" > /dev/null
          /root/.gitssh.sh
  }
  
  # Source SSH settings, if applicable
  
  if [ -f "${SSH_ENV}" ]; then
          . "${SSH_ENV}" > /dev/null
          ps ${SSH_AGENT_PID} #doesn't work under cywgin
          ps -ef | grep ${SSH_AGENT_PID} | grep ssh-agent$ > /dev/null || {
                  start_agent;
  }
  else
          start_agent;
  fi

ネットワーク探索
==================


DHCPでホストを確認.sh
-----------------------

.. code-block:: cmd
  :linenos:

  #!/bin/bash
  
  #ここはネットワークの定義コーナー、対話系もスクリプトの後ろでも入力出来ます。
  if [ -z "$1" ] ; then
          echo Network Header Required \(Ex 10.0.1\):
          read NetHead
  else
          NetHead=$1;
  fi
  
  #本番のネットワーク探知
  for i in {1..255}; do
          Result=$(nslookup "$NetHead.$i" <DNS_server_IP> | grep -v 'NXDOMAIN'); #ここの-v NXDOMAIN は 応用として、grep 'arpa' で普通に全ゲットもいいです。
          if [ -z "$Result" ]; then
                  continue;
          else
                  printf "$Result\n";
          fi
  done


PINGでIPとしてのホストが生存確認.sh
-------------------------------------

.. code-block:: bash
  :linenos:
  
  #!/bin/bash
  
  #ここはネットワークの定義コーナー、対話系もスクリプトの後ろでも入力出来ます。
  if [ -z "$1" ] ; then
          echo Network Header Required \(Ex 10.0.1\):
          read NetHead
  else
          NetHead=$1;
  fi
  
  #One Time Pingでホストの存在を確認する
  for i in {1..255}; do
          Result=$(ping "$NetHead.$i" -c 1 | grep 'ttl');
          if [ -z "$Result" ]; then
                  continue;
          else
                  printf "$Result\n";
          fi
  done


自己インストーラ作成
========================

Windows Package 作成
----------------------

パッケージするの進め方法は二つ

* Windows 10 に入った`IExpress`_を使う。
* 7-zip さんが提供したの`7zSD.sfx`_を使う。

他には、自動実行用の.batファイルが必要です。

下の部分はbatやcmdファイルに、windowsの最高権限が必要時追加するコードです。

.. code-block:: cmd
  :linenos:
  
  cd /d "%~dp0" && ( if exist "%temp%\getadmin.vbs" del "%temp%\getadmin.vbs" ) && fsutil dirty query %systemdrive% 1>nul 2>nul || (  echo Set UAC = CreateObject^("Shell.Application"^) : UAC.ShellExecute "cmd.exe", "/k cd ""%~sdp0"" && %~s0 %params%", "", "runas", 1 >> "%temp%\getadmin.vbs" && "%temp%\getadmin.vbs" && exit /B )

他に、おすすめのツールは`resource hacker`_という無料EXE編集ツール。

このツールを使ってると、直接EXEのアイコンや色んな設定が変更可能です。

iconが変更したいなら、元のicon groupを別保存し、変わりたいのEXEファイルに使用で変更可能です。

.. _パスワード作る、zipフォーマット: https://akishinoshiame.github.io/UgokuIT/tool/passcode.zip
.. _パスワード作る、tar.gzフォーマット: https://akishinoshiame.github.io/UgokuIT/tool/passcode.tar.gz
.. _ESDや色んなソフトウェアダウロード: https://tb.rg-adguard.net/public.php
.. _decrypt-multi-release: https://rg-adguard.net/decrypt-multi-release/
.. _adguard UUP 選択ツール: https://uup.rg-adguard.net/
.. _UUP Dump の公式サイト: https://uupdump.ml/
.. _Rufusツール: https://rufus.ie/
.. _CrystalDiskInfo: https://crystalmark.info/en/software/crystaldiskinfo/
.. _CPU-Z: https://www.cpuid.com/softwares/cpu-z.html
.. _Kill Disk: https://www.killdisk.com/erasedata_win.htm
.. _UndeletePlus: https://www.undeleteplus.com/
.. _HDD Regenerator: http://www.dposoft.net/hdd.html
.. _IExpress: https://docs.microsoft.com/internet-explorer/ie11-ieak/iexpress-wizard-for-win-server
.. _7zSD.sfx: https://sevenzip.osdn.jp/chm/cmdline/switches/sfx.htm
.. _resource hacker: http://www.angusj.com/resourcehacker/