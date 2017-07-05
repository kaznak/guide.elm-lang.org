This is Japanese translated version of commit 5e58bb7cad13f09ae1c8494566318106905364d9.

# Elm の紹介

**Elm は JavaScript へとコンパイルされる関数型言語です。**ウェブサイトやウェブアプリケーションを作成するためのツールとして React のようなプロジェクトと競合します。  Elm はシンプルさ、使いやすさ、品質の高いツールを非常に重視しています。

このガイドは以下のようなものです。

  - Elm でのプログラミングの基礎を教えます。
  - *Elm アーキテクチャ*に基づいて、どのようにインタラクティブなアプリケーションを作るか、説明します。
  - いかなる言語でのプログラミングにとっても一般的な原則とパターンを強調します。

読み終えたときには、 Elm で素晴らしい Web アプリケーションを作成できるようになるだけでなく、 Elm ヲ使いやすくしている、基本的なアイデアやパターンを理解していただければ幸いです。

どうしようか迷っているばあいは、 Elm をちょっと試して、実際にプロジェクトをつくれば、より良い JavaScript とリアクションコードを書き上げることができるでしょう。アイディアが簡単に実現出来ますよ!

%訳注% : If you are on the fence : Elm の採用を迷っている?

## クイックサンプル

当然、*私*はエルムが良いと思うので、あなたにもそう思ってもらいたいです。

%訳注% : Of course *I* think Elm is good, so look for yourself. 

ここに[簡単なカウンタ](http://elm-lang.org/examples/buttons)の例があります。コードをみれば、それは単純にカウンタをインクリメント、デクリメント出来るようにしているものだと分かるでしょう。

```elm
import Html exposing (Html, button, div, text)
import Html.Events exposing (onClick)

main =
  Html.beginnerProgram { model = 0, view = view, update = update }

type Msg = Increment | Decrement

update msg model =
  case msg of
    Increment ->
      model + 1

    Decrement ->
      model - 1

view model =
  div []
    [ button [ onClick Decrement ] [ text "-" ]
    , div [] [ text (toString model) ]
    , button [ onClick Increment ] [ text "+" ]
    ]
```

`update`と` view`は完全に分離されています。 あなたは HTML を宣言的な方法で記述し、 Elm はごちゃごちゃした DOM の操作の面倒を見ます。

## なぜ*関数型*言語か?

あなたが関数型プログラミングについて聞いた事は忘れて下さい。変わった言葉、奇妙なアイディア、ひどいツール。うげえ。 Elm はこういったものです:

  - 実際に使っていてランタイムエラーは発生しません。 `null` は存在しません。 `undefined` は関数ではありません。
  - 素早く機能を追加するのを助けてくれる便利なエラーメッセージ
  - 上手く構成されたコード、アプリケーションが成長しても上手い構成が*維持*されるような
  - 全ての Elm パッケージに自動的に強制される意味論的バージョニング
  
JS ライブラリの組み合わせはあなたにこれを与えることはできませんが、それはエルムではすべて自由で簡単にえられます。これらの素晴らしいことは*唯一*可能ですが、それは、 Elm は型付き関数型言語の40年以上の成果の上に構築されているからです。 Elm は関数型言語ですが、それは実際のメリットがこのガイドを読むのに費やす時間の価値があるからです。

私は Elm を学びやすく使いやすくすることに重点を置いています。だから私があなたに求めるのは、 Elm をちょっと試してみて、どう考えるか見る事です。私はあなたが嬉しい驚きを得る事を願っています。
