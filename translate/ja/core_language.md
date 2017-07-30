This is Japanese translated version of commit 5e58bb7cad13f09ae1c8494566318106905364d9.

# コア言語

このセクションでは、エルムの簡単な言語のコアについて一通り説明します。

このセクションはあなたが一緒に操作をするときに最も効果を発揮するので、[インストール](install.md)のあとに、ターミナルで `elm-repl`を起動してください。(または、[オンラインREPL](http://elmrepl.cuberoot.in/)を使用してください。)いずれの場合にしても、以下のような出力を得るでしょう:

```elm
---- elm repl 0.18.0 -----------------------------------------------------------
 :help for help, :exit to exit, more at <https://github.com/elm-lang/elm-repl>
--------------------------------------------------------------------------------
>
```

REPLはすべての結果の型を出力しますが、概念を徐々に導入するために、**このチュートリアルでは型注釈をオフにします。

[値](#values)、[関数](#functions)、[リスト](#lists)、[タプル](#tuples)、および[レコード](#records)について説明します。 これらのビルディングブロックはすべて、JavaScript、Python、Javaなどの言語の構造と非常に密接に対応しています。


## 値

まずはいくつかの文字列から始めましょう:

```elm
> "hello"
"hello"

> "hello" ++ "world"
"helloworld"

> "hello" ++ " world"
"hello world"
```

Elmは `(++)`演算子を使って文字列をくっつけます。 両方の文字列が正確に保存されることに留意してください。そのため、`"hello"` と `"world"` を組み合わせた場合、その結果にはスペースが含まれません。

数学も通常通りに見えます:

```elm
> 2 + 3 * 4
14

> (2 + 3) * 4
20
```

JavaScriptと異なり、Elmは整数と浮動小数点数を区別します。 Python 3と同様に、浮動小数点の `(/)`と整数の除算`(//)`の両方があります。

```elm
> 9 / 2
4.5

> 9 // 2
4
```

## 関数

まず関数`isNegative`を書く所から始めましょう。これは数値を取込み、それがゼロより小さいかをチェックする関数です。結果は、`True`か`False`になります。

```elm
> isNegative n = n < 0
<function>

> isNegative 4
False

> isNegative -7
True

> isNegative (-3 * -4)
False
```

関数適用は、JavaScriptやPython、Javaなどの言語とは異なった見た目であることに注意してください。 すべての引数をカッコで囲み、カンマで区切る代わりに、関数を適用するためにスペースを使用します。 だから `（add（3,4））`は `（add 3 4）`になり、物事が大きくなるにつれて括弧やカンマの束を避けることになります。 最終的に、これに慣れれば、はるかに綺麗にに見えます！ [elm-htmlパッケージ][elm-html]はこのやり方が物事の見通しをよくするかの良い例です。

[elm-html]: http://elm-lang.org/blog/blazing-fast-html


## If 式

Elmで条件付きの振る舞いを書きたいときは、if式を使います。

```elm
> if True then "hello" else "world"
"hello"

> if False then "hello" else "world"
"world"
```

キーワード `if` `then` `else` は条件と二つの分岐を区切るために使用されるので、括弧や中括弧は必要ありません。

エルムは &ldquo;truthiness&rdquo; の記法を持っていません。 したがって、数字と文字列とリストはブール値として使用できません。 試してみると、(数値や文字列ではない)本当のブール値で記述する必要があることがわかります。

それでは、数値が9000より大きいかどうかを教えてくれる関数を作ってみましょう。

```elm
> over9000 powerLevel = \
|   if powerLevel > 9000 then "It's over 9000!!!" else "meh"
<function>

> over9000 42
"meh"

> over9000 100000
"It's over 9000!!!"
```

REPLでバックスラッシュを使うと、プログラムを複数の行に分割することができます。 上記の `over9000` の定義でこれを使用しています。 さらに、関数の本体を常に行の下に持っていくことがベストプラクティスです。 これはプログラムをより統一して読みやすくするため、通常のコードで定義する関数と値は全てこのようにしたいと思うでしょう。

> **注意:** 関数の2行目の前に空白を追加するようにしてください。 Elmには"構文的に意味を持つ空白"があります。 これはインデントがその構文の一部であることを意味します。


## リスト

リストは、Elmの最も一般的なデータ構造の1つです。 それらは、JavaScriptの配列と同様に、一連の関連するものを保持します。

リストは多くの値を保持できます。 これらの値はすべて同じ型でなければなりません。 [`List`ライブラリ][list]の関数を使用するいくつかの例を以下に示します:

[list]: http://package.elm-lang.org/packages/elm-lang/core/latest/List

```elm
> names = [ "Alice", "Bob", "Chuck" ]
["Alice","Bob","Chuck"]

> List.isEmpty names
False

> List.length names
3

> List.reverse names
["Chuck","Bob","Alice"]

> numbers = [1,4,3,2]
[1,4,3,2]

> List.sort numbers
[1,2,3,4]

> double n = n * 2
<function>

> List.map double numbers
[2,8,6,4]
```

繰り返しになりますが、リストのすべての要素は同じ型でなければなりません。


## タプル

タプルは、また別の便利なデータ構造です。 タプルは決まった数の値を保持でき、各値は任意の型を持つことができます。 一般的な使い方は、関数から複数の値を返す必要がある場合です。 次の関数は名前を取得し、ユーザーにメッセージを出します:

```elm
> import String

> goodName name = \
|   if String.length name <= 20 then \
|     (True, "name accepted!") \
|   else \
|     (False, "name was too long; please limit it to 20 characters")

> goodName "Tom"
(True, "name accepted!")
```

これは非常に便利ですが、状況が複雑になり始めるときには、タプルの代わりにレコードを使用するのが最善の方法です。


## レコード

レコードは、JavaScriptまたはPythonのオブジェクトに似た、キーと値のペアのセットです。 彼らはElmで非常に一般的で有用であることがわかります！ いくつかの基本的な例を見てみましょう。


```elm
> point = { x = 3, y = 4 }
{ x = 3, y = 4 }

> point.x
3

> bill = { name = "Gates", age = 57 }
{ age = 57, name = "Gates" }

> bill.name
"Gates"
```

このように、中括弧を使用してレコードを作成し、ドットを使用してフィールドにアクセスすることができます。 Elmには、関数のように使えるバージョンのレコードアクセスもあります。 変数をドットで始めると、*次の名前のフィールドにアクセスしてください*と言っていることになります。 つまり、 `.name`はレコードの`name`フィールドを取得する関数です。

```elm
> .name bill
"Gates"

> List.map .name [bill,bill,bill]
["Gates","Gates","Gates"]
```

レコードを使って関数を作成する場合、パターンマッチングをつかうことで、プログラムを少し軽くすることができます。

```elm
> under70 {age} = age < 70
<function>

> under70 bill
True

> under70 { species = "Triceratops", age = 68000000 }
False
```

したがって、数値を保持する`age`フィールドがある限り、レコードを渡すことができます。

レコードの値を更新すると便利なことがよくあります。

```elm
> { bill | name = "Nye" }
{ age = 57, name = "Nye" }

> { bill | age = 22 }
{ age = 22, name = "Gates" }
```

我々は*破壊的な*更新をしないことに注意することが重要です。 `bill`のいくつかのフィールドを更新すると、既存のレコードを上書きするのではなく、実際に新しいレコードを作成します。 Elmは、可能な限り多くのコンテンツを共有することで、これを効率的にします。 10個のフィールドの1つを更新すると、新しいレコードは9個の変更されていない値を共有します。


### レコードとオブジェクトの比較

ElmのレコードはJavaScriptのオブジェクトと*似ています*、が、いくつかの重要な違いがあります。 主な違いは、レコードとの違いです:

- あなたは存在しないフィールドにアクセスすることはできません。
- いかなるフィールドも未定義もしくはnullになりません。
- `this`または`self`キーワードを使って再帰的レコードを作成することはできません。

Elmはデータとロジックの厳密な分離を奨励しておりますが、この分離を破るために主に使われるのが`this`と言う能力です。 これは、オブジェクト指向言語の体系的な問題で、Elmが意図的に避けているものです。

レコードは、[構造的型づけ][st]もサポートしています。これは、Elmのレコードが、必要なフィールドが存在する限り、どのような状況でも使用できることを意味します。 これにより、信頼性を損なうことなく柔軟性が得られます。

 [st]: https://en.wikipedia.org/wiki/Structural_type_system "Structural Types"
