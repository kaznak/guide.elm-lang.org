This is Japanese translated version of commit 5e58bb7cad13f09ae1c8494566318106905364d9.

# Elm アーキテクチャ

Elmアーキテクチャは、Webアプリケーションを設計するための単純なパターンです。 これは、モジュール性、コードの再利用、およびテストに最適です。  結局のところ、Elmアーキテクチャにより、リファクタリングや機能追加の際に健全性を保ったまま、複雑なWebアプリケーションを簡単に作成することができるようになります。

このアーキテクチャはElmのなかで自然に成長してきたように思えます。 私たちはまず、Elmコミュニティが作っていたゲームにそれを見出しました。 それから[TodoMVC][]や[dreamwriter][]などのWebアプリケーションでも。 今では、[NoRedInk][]と[Pivotal][]のような企業の製品で見ることができます。 アーキテクチャはElm自体の設計の結果であるように思われるので、それを知っているかいないかに関わらず、あなたはそれを知る事になるでしょう。 
このことは新しい開発者に参加してもらうときに非常によい事が分かっています。 彼らのコードは上手く設計されたものとなります。 これはとても不思議なことです。

ElmアーキテクチャーはElmでは*簡単*ですが、どんなフロントエンドのプロジェクトでも便利です。 実際、ReduxのようなプロジェクトはElmアーキテクチャに触発されているので、すでにこのパターンの派生品を見ているかもしれません。 ポイントは、たとえあなたがまだ仕事でElmを使用できないとしても、あなたはElmを使うこと以外にもこのパターンを取込むことから多くを得るでしょう。

[Elm]: http://elm-lang.org/
[TodoMVC]: https://github.com/evancz/elm-todomvc
[dreamwriter]: https://github.com/rtfeldman/dreamwriter#dreamwriter
[NoRedInk]: https://www.noredink.com/
[CircuitHub]: https://www.circuithub.com/
[Pivotal]: https://www.pivotaltracker.com/blog/Elm-pivotal-tracker/


## 基本パターン

すべてのElmプログラムのロジックは、明確に切り分けられた3つの部分に分割されます。

  * **モデル** &mdash; アプリケーションの状態
  * **アップデート** &mdash; 状態を更新する方法
  * **ビュー** &mdash; 状態をHTMLとして表示する方法

このパターンはとても信頼性が高く、私はいつも次の骨格から始めて、個別の特別な場合の詳細を記入します。

```elm
import Html exposing (..)


-- MODEL

type alias Model = { ... }


-- UPDATE

type Msg = Reset | ...

update : Msg -> Model -> Model
update msg model =
  case msg of
    Reset -> ...
    ...


-- VIEW

view : Model -> Html Msg
view model =
  ...
```

これは本当にElmアーキテクチャの本質です! 興味深いロジックで徐々にこのスケルトンを埋めて行く事で進めて行きます。
