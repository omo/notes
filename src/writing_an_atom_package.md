
# 自分用の Atom Package を書く

目標:

 * この notes ディレクトリの md をセーブしたら git commit; git push する package を書く
 * おまけ機能として一撃で新規ノートを追加するとかもやりたい

知る必要があること:

 * Package の作り方最低限. あるいは設定にバリっと書いておくですむならその方法
 * Git を操作できるのか。あるいは適当にコマンド呼んだりできるのか。
 * Post save hook 的なものはあるのか。というか無いとどうしょうもない。

とりあえず Atom の操作方法: [Getting Started](https://atom.io/docs/v0.158.0/getting-started)

* "プロジェクト" の単位で色々やる。1 プロジェクト 1 window っぽい。
* Ctrl-T でインクリメンタルにファイル名マッチできる。(igrep)
* Ctrl-Shift-T でコマンド検索。(appropos)
* Pane 分割は Ctrl-k, right とか。これはブラウザにはできないワザだから便利だな。
* MD の preview は Ctrl-Shift-M.

Pacakge つくる:

 * [Creating Packages](https://atom.io/docs/v0.158.0/creating-a-package): ディレクトリ校正、提供されるフック
 * [Create Your First Package](https://atom.io/docs/v0.158.0/your-first-package) チュートリアル
   * パッケージ生成コマンドを使うとスタブが作られる。`.atom` 以下にシンボリックリンクが作られてすぐ使えるようになる。
 * なんかテストを書かされるのはやだなあ...
   * `window:reload` で再起動。そのプロジェクトだけ再起動なのはちょっとよい。これはプロジェクト単位に別プロセスなの?

最初のステップ:

 * 自分のいるレポジトリを commit して push する、というコマンドをつくる
 * それをフックする
 * 設定としてノートの場所を指定し、プロジェクトと設定が一致したらフックを登録する

 * Q: 自分で View を作るのではなく、mini-buffer みたいに乗っ取って使える UI は無いのか?
 * Q: DevTools 的なのはないのか? -> Alt-Cmd-I
   * これで interactive に開発できる...かも.

Git まわりの API. [atom.GitRepository](https://atom.io/docs/api/v0.158.0/GitRepository) というのがある...
が,　コミットとか副作用のあることはできないぽいな...

[このスレッドによると](https://discuss.atom.io/t/git-interaction-commands/1159/6)
GitRepository は lightweight API で本気度高いのは [git-utils](http://atom.github.io/git-utils/) という
別パッケージになってるぽい。しかしこれは Atom でなく Node のライブラリなのでどうやって Atom にインストールすればいいの...?
そしてみたかんじコミットできる API なさげだな... GitHub のエディタなのにその中からコミットできないってちょっとすごいね...

こうコマンド呼んじゃうのがはやそうだなあ...
Atom では [BufferedProcess](https://atom.io/docs/api/v0.158.0/BufferedProcess)
を使うのが定石っぽい.
