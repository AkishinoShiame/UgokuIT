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