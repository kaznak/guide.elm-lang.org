This is Japanese translated version of commit 5e58bb7cad13f09ae1c8494566318106905364d9.

> **情報:** まだインストールしたくない場合は、リンク先のガイドの[オンラインエディタ](http://elm-lang.org/try)と[オンラインREPL](http://elmrepl.cuberoot.in/)を参照してください。

# インストール

  * Mac &mdash; [インストーラ][mac]
  * Windows &mdash; [インストーラ][win]
  * その他 &mdash; [npm インストーラ][npm] もしくは [ソースコードからビルド][build]

[mac]: http://install.elm-lang.org/Elm-Platform-0.18.pkg
[win]: http://install.elm-lang.org/Elm-Platform-0.18.exe
[npm]: https://www.npmjs.com/package/elm
[build]: https://github.com/elm-lang/elm-platform

これらのルートのいずれかによりインストールした後は、次のコマンドラインツールを使用できます:

- [`elm-repl`](#elm-repl) &mdash; エルムの式で遊ぶ
- [`elm-reactor`](#elm-reactor) &mdash; すばやくプロジェクトを始める
- [`elm-make`](#elm-make) &mdash; Elmコードを直接コンパイルする
- [`elm-package`](#elm-package) &mdash; パッケージをダウンロードする

あなたがエディタをセットアップしたらすぐに、これらがどのように働くのか詳しく説明します!

> **トラブルシュート:** 何かを学ぶ最も速い方法は、エルムのコミュニティの他の人と話すことです。 フレンドリーで喜んでお手伝いします！ だから、インストール中にはまったり、何か変わったことがあった場合は、[Elm Slack](http://elmlang.herokuapp.com/)にアクセスして質問してください。 実際に、エルムを学んだり、使用したりしているときに、何か混乱した場合は、私たちに聞いてみてください。 自分で時間を節約することができます。 早く聞いて！

## エディタの設定

あなたを助けるコードエディタを持っていると、Elmを使う事はより容易でしょう。 少なくとも以下のエディタ用のElmプラグインがあります:

  * [Atom](https://atom.io/packages/language-elm)
  * [Brackets](https://github.com/lepinay/elm-brackets)
  * [Emacs](https://github.com/jcollard/elm-mode)
  * [IntelliJ](https://github.com/durkiewicz/elm-plugin)
  * [Light Table](https://github.com/rundis/elm-light)
  * [Sublime Text](https://packagecontrol.io/packages/Elm%20Language%20Support)
  * [Vim](https://github.com/ElmCast/elm-vim)
  * [VS Code](https://github.com/sbrink/vscode-elm)

エディタを持っていない場合は、[Sublime Text](https://www.sublimetext.com/)を使い始めるのがいいです！

あなたのコードをきれいにする[elm-format] []を試してみてください！

[elm-format]: https://github.com/avh4/elm-format


## コマンドラインツール

Elmをインストールして、`elm-repl`、`elm-reactor`、`elm-make`、`elm-package`を得ました。 しかし、それらは正確には何をしているのでしょうか?

### elm-repl

[`elm-repl`](https://github.com/elm-lang/elm-repl)では、簡単なElm式で遊ぶことができます。

```bash
$ elm-repl
---- elm-repl 0.18.0 -----------------------------------------------------------
 :help for help, :exit to exit, more at <https://github.com/elm-lang/elm-repl>
--------------------------------------------------------------------------------
> 1 / 2
0.5 : Float
> List.length [1,2,3,4]
4 : Int
> String.reverse "stressed"
"desserts" : String
> :exit
$
```

この後に続く &ldquo;Core Language&rdquo; で`elm-repl`を使用します。 これがどのように動作するかについての詳細は、こちらをご覧ください(https://github.com/elm-lang/elm-repl/blob/master/README.md)。

> **情報:** `elm-repl`はコードをJavaScriptにコンパイルすることで動作しますので、[Node.js](http://nodejs.org/)がインストールされていることを確認してください。 これを使用してコードを評価します。


### elm-reactor

[`elm-reactor`](https://github.com/elm-lang/elm-reactor)は、コマンドラインを駆使することなくElmプロジェクトを構築するのに役立ちます。 プロジェクトのルートで次のように実行するだけです:

```bash
git clone https://github.com/evancz/elm-architecture-tutorial.git
cd elm-architecture-tutorial
elm-reactor
```

これは[`http://localhost:8000`](http://localhost:8000)でサーバを起動します。 任意のElmファイルに移動して、それがどのように見えるかを見ることができます。 `examples/01-button.elm`をチェックしてみてください。

**知っておいた方が良い実行オプション:**

- `--port`によりポート8000以外を選ぶことができます。したがって、
  `http://localhost:8123`で動作させるために `elm-reactor --port=8123` と実行することができます。
- `--address`は`localhost`を他のアドレスに置き換えることができます。
  たとえば、ローカルネットワーク経由でモバイルデバイス上でElmプログラムを試したい場合は、
  `elm-reactor -address=0.0.0.0`を使用することができます。


## elm-make

[`elm-make`](https://github.com/elm-lang/elm-make)はElmプロジェクトをビルドします。 ElmコードをHTMLまたはJavaScriptにコンパイルできます。 Elmコードをコンパイルするもっとも一般的な方法です。もしあなたのプロジェクトが`elm-reactor`には進歩しすぎたならば、` elm-make`を直接使用したいと思うでしょう。

`main.elm`を` main.html`という名前のHTMLファイルにコンパイルしたいとします。 次のコマンドを実行します:

```bash
elm-make Main.elm --output=main.html
```

**知っておいた方が良い実行オプション:**

- `--warn`はコード品質を改善するための警告を表示します


### elm-package

[`elm-package`](https://github.com/elm-lang/elm-package)は、[パッケージカタログ](http://package.elm-lang.org/)からパッケージをダウンロードして公開します。 コミュニティメンバーが[上手い方法で](http://package.elm-lang.org/help/design-guidelines)問題を解決すると、誰もが使用できるように、パッケージカタログのコードを共有します!

[`elm-lang/http`][http]と[`NoRedInk/elm-decode-pipeline`][pipe]を使ってHTTPリクエストをサーバーに送り、結果のJSONをElm値に変換したいとします。 その時はこうなります:

[http]: http://package.elm-lang.org/packages/elm-lang/http/latest
[pipe]: http://package.elm-lang.org/packages/NoRedInk/elm-decode-pipeline/latest

```bash
elm-package install elm-lang/http
elm-package install NoRedInk/elm-decode-pipeline
```

これにより、あなたのプロジェクトを記述する `elm-package.json`ファイルに依存関係が追加されます。（またはまだ作成していない場合は作成してください！）詳細情報は[こちら](https://github.com/elm-lang/elm-package)


**知っておいた方が良いコマンド:**

- `install`: `elm-package.json` に記述された依存パッケージをインストール
- `publish`: ライブラリをElmパッケージカタログに公開する
- `dump` : APIの変更に基づいてバージョン番号をバンプする
- `diff`: 2つのAPIの違いを得る
