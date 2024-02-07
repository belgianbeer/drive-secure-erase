# drive-secure-erase

drive-secure-erase is a command that erases all data on the SSD. It factory resets the state of the SSD's cells, so it also restores write performance. It works on FreeBSD and Linux.

drive-secure-erase は、SSDのすべてのデータを消去するコマンドです。SSDのセルの状態を工場出荷時にリセットするため、書き込み性能も回復します。FreeBSDとLinuxで動作します。

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
Next example uses FreeBSD. In addition, root privileges are required to run.

最初にドライブがセキュアイレースを実行できる状態かどうかを確認します。
対象のドライブはFreeBSDであれば"da1"、Linuxの場合は"/dev/sdb"のように指定します。
絶対に対象ドライブを間違えないように注意してください。
間違えて重要なドライブのデータを消去しても回復できません。
次の例ではFreeBSDを使用します。また実行にはroot権限が必要です。

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

Be sure not to make a mistake in the drive letter you specify.
If you specify the system drive, many of them cannot be erased with "fronzen".
However, depending on the system configuration you are using, it may be possible to erase it.
Not to mention the damage caused by suddenly erasing the contents of the system drive.

くれぐれも指定するドライブ名を間違えないようにしてください。
誤ってシステムドライブを指定した場合、多くは"fronzen"で消去できません。
しかしシステム構成によっては消去できる場合があります。
システムドライブの内容をいきなり消去した場合の被害は言うまでもありません。
