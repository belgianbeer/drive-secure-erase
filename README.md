# drive-secure-erase

## about drive-secure-erase

drive-secure-erase is a command that erases all data on the SSD. It factory resets the state of the SSD's cells, so it also restores write performance.

drive-secure-erase は、SSDのすべてのデータを消去するコマンドです。SSDのセルの状態を工場出荷時にリセットするため、書き込み性能も回復します。

**WARNING! 警告！WARNING! 警告！WARNING! 警告！**

drive-secure-erase is very dangerous, the process takes only a few seconds,
and there is no way to recover the erased data.

drive-secure-eraseは大変危険で、処理は数秒で実施され消去したデータを復活する手段はありません。

**WARNING! 警告！WARNING! 警告！WARNING! 警告！**

## How to use drive-secure-erase

### Preparing on Linux

If you are using Linux System, you prepare the **hdparm**.
For example in Debian or Ubuntu:

Linuxを使っている場合は、あらかじめhdparmをインストールします。
DebianやUbuntuではaptコマンドを使ってインストールします。

```code
$ apt install hdparm
```

### Checking secure erase status

First, check to see if the drive is ready to perform secure erase.
The target drive should be da1 for FreeBSD or /dev/sdc for Linux.
Be careful not to make a mistake with the target drive.
Even if you accidentally erase the data on an important drive, you will not be able to recover it.
The example uses FreeBSD. In addition, root privileges are required to run.

最初にドライブがセキュアイレースを実行できる状態かどうかを確認します。
対象のドライブはFreeBSDであればda1、Linuxの場合は/dev/sdcのように指定します。
絶対に対象ドライブを間違えないように注意してください。
間違えて重要なドライブのデータを消去しても回復できません。
例ではFreeBSDを使用します。また実行にはroot権限が必要です。

```code
$ drive-secure-erase da1
......
......

*** da1 is ready for secure erase.
$ 
```

drive-secure-erase reports the status of the drive and lets you know if it can be erased.

drive-secure-erase を実行するとドライブの状態を報告し、消去できるかどうかがわかります。

### Performing Secure Erase

Once you know that you can erase it, add yes to the argument and run it again.
In a few seconds, the drive will be erased.

消去できることがわかったら、引数にyesを追加して再び実行します。
数秒でドライブの消去が完了します。

```code
$ drive-secure-erase da1 yes
.....
.....
$ 
```

## Caution

**TBD**