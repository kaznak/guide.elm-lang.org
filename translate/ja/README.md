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

## A Quick Sample

Of course *I* think Elm is good, so look for yourself.

Here is [a simple counter](http://elm-lang.org/examples/buttons). If you look at the code, it just lets you increment and decrement the counter:

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

Notice that the `update` and `view` are entirely decoupled. You describe your HTML in a declarative way and Elm takes care of messing with the DOM.


## Why a *functional* language?

Forget what you have heard about functional programming. Fancy words, weird ideas, bad tooling. Barf. Elm is about:

  - No runtime errors in practice. No `null`. No `undefined` is not a function.
  - Friendly error messages that help you add features more quickly.
  - Well-architected code that *stays* well-architected as your app grows.
  - Automatically enforced semantic versioning for all Elm packages.

No combination of JS libraries can ever give you this, yet it is all free and easy in Elm. Now these nice things are *only* possible because Elm builds upon 40+ years of work on typed functional languages. So Elm is a functional language because the practical benefits are worth the couple hours you'll spend reading this guide.

I have put a huge emphasis on making Elm easy to learn and use, so all I ask is that you give Elm a shot and see what you think. I hope you will be pleasantly surprised!
