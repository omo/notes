
# Atom Shell

URL:

  * https://github.com/atom/atom-shell
  * [ドキュメント](https://github.com/atom/atom-shell/tree/master/docs)もチェックインされている

 関係するプロジェクト:

  * [Libchromiumcontent](https://github.com/brightray/libchromiumcontent)
    * Chromium の Content API をリンクする。Atom-shell とかはこれのビルド済バイナリをダウンロードして使っている.
    * エクスポートシンボルまわりでちょっとだけパッチしている
  * [Brightray](https://github.com/brightray/brightray)
    * Libchromiumcontent の薄いラッパ。Delegate の実装とか。Atom-shell はこれを submodule で持ってビルドしている。
  * [Native-mate](https://www.npmjs.com/package/native-mate) V8 の C++ バインディングヘルパ. ドキュメントによると [GIN](https://chromium.googlesource.com/chromium/src/+/HEAD/gin/README)  のフォーク。

見所:

 * V8 のインテグレート: [ドキュメント](https://github.com/atom/atom-shell/blob/master/docs/development/atom-shell-vs-node-webkit.md)
 * RPC: [ドキュメント](https://github.com/atom/atom-shell/blob/master/docs/api/remote.md)
 * プロセスモデルの簡素化 (Window:Content = 1:1. No C++ Tab.)

IPC:

 * パラメタは base::Value, 戻り値は JSON の文字列.
 * Async と Sync がある. Chrome の SyncMessage をつかっている.
 * `EventEmitter` で listen する.
 * Question: レンダラはどう identify されているのか?
