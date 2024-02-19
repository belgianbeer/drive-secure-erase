# drive-secure-erase <!-- omit in toc -->

drive-secure-erase is a command that erases all data on the SSD.
It works on FreeBSD and Linux.

drive-secure-erase は、SSDのすべてのデータを消去するコマンドです。
FreeBSDとLinuxで動作します。

- [WARNING! WARNING! WARNING!](#warning-warning-warning)
- [How to use drive-secure-erase](#how-to-use-drive-secure-erase)
	- [Preparing on Linux](#preparing-on-linux)
	- [Checking Secure Erase status](#checking-secure-erase-status)
	- [Performing Secure Erase](#performing-secure-erase)
- [Caution](#caution)
- [drive-secure-erase for HDD](#drive-secure-erase-for-hdd)
- [What does drive-secure-erase do?](#what-does-drive-secure-erase-do)

## WARNING! WARNING! WARNING!

drive-secure-erase is very dangerous command.
The process takes only a few seconds, and there is no way to recover the erased data.
If used incorrectly, it will lead to irreparable consequences.

drive-secure-eraseは大変危険なコマンドです。
処理は数秒で完了し、消去したデータを復活する手段はありません。
誤って使用すると取り返しのつかない結果を招きます。

## How to use drive-secure-erase

### Preparing on Linux

If you are using Linux System, you prepare the **hdparm**.
For example in Debian or Ubuntu:

Linuxを使っている場合は、あらかじめhdparmをインストールします。
DebianやUbuntuではaptコマンドを使います。

```code
$ apt install hdparm
```
FreeBSD requires no special preparation.

FreeBSDでは特別な準備は必要ありません。

### Checking Secure Erase status

First, check to see if the drive is ready to perform secure erase.
The target drive should be "da1" for FreeBSD or "/dev/sdb" for Linux.
Be careful not to make a mistake with the target drive.
Even if you accidentally erase the data on an important drive, you will not be able to recover it.
Next example uses FreeBSD. Root privileges are required to run.

最初にドライブがセキュアイレースを実行できる状態かどうかを確認します。
対象のドライブはFreeBSDであれば"da1"、Linuxの場合は"/dev/sdb"のように指定します。
絶対に対象ドライブを間違えないように注意してください。
間違えて重要なドライブのデータを消去しても回復できません。
次の例ではFreeBSDを使用します。実行にはroot権限が必要です。

drive-secure-erase reports the status of the drive and lets you know if it can be erased.

drive-secure-erase を実行するとドライブの状態を報告し、消去できるかどうかがわかります。

```code
$ drive-secure-erase da1
......
*** da1 is ready for secure erase.
$ 
```

If the drive supports enhanced secure erase, the following is displayed:

ドライブがEnhanced Secure Eraseをサポートしている場合は、次のように表示します。

```code
$ drive-secure-erase da1
......
*** da1 is ready for enhanced secure erase.
$ 
```

### Performing Secure Erase

Once you know that you can erase it, add yes to the argument and run it again.
If the drive is capable of enhanced secure erase, it will be used, otherwise it will perform secure erase.
In a few seconds, the drive will be erased.

消去できることがわかったら、引数にyesを追加して再び実行します。
Enhanced Secure Erase可能ならそれを使い、そうでない場合は通常のSecure Eraseを実行します。
数秒でドライブの消去が完了します。

```code
$ drive-secure-erase da1 yes
```

## Caution

In the case of FreeBSD, it may exit with an error message similar to the following, but it will be erased normally.

FreeBSDの場合次のようなエラーメッセージが表示されて終了することがありますが、正常に消去されます。

```
camcontrol: ATA SECURITY_ERASE_UNIT via pass_16 failed
```

It does not support erasing NVMe storage and USB flash drive.

NVMeストレージとUSBメモリの消去はサポートしていません。

> To erase NVMe storage, use the nvmecontrol command on FreeBSD or the nvme command in nvme-cli on Linux.
> USB flash drives do not seem to have the ability to erase them.
>
> NVMeのストレージを消去するためには、FreeBSDではnvmecontrolコマンドをLinuxではnvme-cliにあるnvmeコマンドを使います。
> USBメモリには、消去する機能は存在しないようです。

Be sure not to make a mistake in the device-name you specify.
If you specify the system drive, many of them cannot be erased with "fronzen".
However, depending on the system configuration you are using, it may be possible to erase it.
Not to mention the damage caused by suddenly erasing the contents of the system drive.

くれぐれも指定するデバイス名を間違えないようにしてください。
誤ってシステムドライブを指定した場合、多くは"fronzen"で消去できません。
しかしシステム構成によっては消去できる場合があります。
システムドライブの内容をいきなり消去した場合の被害は言うまでもありません。

In the case of the author, the target SSD is connected with a SATA USB conversion adapter and drive-secure-erase is used.

作者の場合は、対象のSSDを、SATAのUSB変換アダプタで接続してdrive-secure-eraseを使っています。

## drive-secure-erase for HDD

drive-secure-erase can also be used on HDDs.
However, the process can take a long time, depending on the capacity of the drive and the transfer speed, and can take anywhere from a few hours to a day or more.
Even if you turn off the power in the middle because it takes a long time, the HDD status will remain locked. To release a locked drive, specify the unlock command.

HDDでもdrive-secure-eraseは利用できます。
しかしながらその処理にはドライブの容量と転送速度に応じた時間を必要とし、数時間から場合によっては1日以上かかることもあります。
時間がかかるからといって途中で電源を切って中段しても、HDDの状態はロックされたままになります。ロックされたドライブを解除するにはunlockコマンドを指定します。

```code
$ drive-secure-erase da1 unlock
```

## What does drive-secure-erase do?

Erasing drive-secure-erase does not require any special processing.
You don't need this command if you use camcontrol's security command on FreeBSD or hdperm's --secure-erase option on Linux.
However, using these commands requires a bit of work and is simply not available.
drive-secure-erase makes use of them internally to make erasure easy to perform.

drive-secure-eraseの消去は特別な処理を行っているわけではありません。
FreeBSDであればcamcontrolのsecurityコマンド、Linuxではhdpermの--secure-eraseオプションを使えば本コマンドは不要です。
ただしこれらのコマンドを使うには少しばかりの手続きが必要で、単純には利用できません。
drive-secure-eraseは内部でそれらを利用して、消去が簡単に実行できるようにしています。
