
# 電力消費について

OS には電力消費を抑える仕組みがある。Linux や Android を中心に調べたことを書く。

## Basics

電力消費を抑える仕組みは二つの視点で考えると良い。

何をとめるか:

 * CPU, cache, RAM, Disk, それ以外の ephemeral devices. たとえば 画面. WiFi, GPS, Cell, センサー.
 * CPU なら部分的なコアだけとめる, クロック落とす, etc.
   * CPU の "C-State" は CPU の何をどれだけ止めるかを定義する。

何を止めるかについてはデバイスと OS との間に規約が必要。
たとえば ACPI はそうした規約の一つ。
CPU によっては勝手に調整するものもある。(クロック上げ下げするなど。)

いつ止めるか:

 * 何もすることがなくなったらとめる, ユーザからの入力が一定時間なかったたらとめる、など。

主に OS の仕事。アプリケーションとの間には規約が必要な気がする。
Android の wake-lock はそうした規約の一つ。

## Halt と Idle

CPU の `HLT` 命令を実行すると、その CPU は次に割り込みが
来るまで動作をとめる。ふつう `HLT` は特権命令なので
これを実行するのは OS.

OS の中に **HLT するプロセス** を作るのがある種のデザインパターン。
全てのプロセスが待ち状態になったらそのプロセスを動かしCPUをとめる。
Windows にはその idle process がある。

HLT 後にどの CPU core state に遷移するかは OS が決める。
Linux にはそのための [cpuidle subsystem](http://lwn.net/Articles/384146/) がある。

## いつとめるのか

いつシステムを停めるかを判断する基準は自明でない。

一番素朴な戦略は全てのプロセスがアイドルしたとき。
この戦略は行儀の悪いプロセスが起き続けていると都合が悪いし、
サーバなどで下手に寝たくない場合のも嬉しくない。

## Wake-lock


## C-States

TBW

----
 * [Power Management States: P-States, C-States, and Package C-States](https://software.intel.com/en-us/articles/power-management-states-p-states-c-states-and-package-c-states)
 * [The cpuidle subsystem](http://lwn.net/Articles/384146/)
 * [Power Management in Operating Systems](http://www.informit.com/articles/article.aspx?p=25451)
