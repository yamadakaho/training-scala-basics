## この課題で身につく能力

forをmapとflatMapに手書き展開できる

## 課題

以下の課題の結果をこのファイルに貼り付けて、Pull Requestを送る形で提出してください

1. コップ本「Scalaスケーラブルプログラミング 第３版」 p.441 -> p.442 の23.1「for式」のコード例を全て実行し、結果を貼り付けて下さい

解答) 答えは書籍に載っているので省略します。提出の際は必ず自分で実行した結果を貼り付けてください。

---
2. コップ本「Scalaスケーラブルプログラミング 第３版」 p.446 -> p.450 の23.4「for式の変換」のコード例を全て実行し、結果を貼り付けて下さい

解答) 答えは書籍に載っているので省略します。提出の際は必ず自分で実行した結果を貼り付けてください。

---
3. `Some("100")`を含むfor loop(一重のfor loop)を作成し、Someの内側のStringをprintlnで表示してください

解答) 

```scala
for (
    a <- Some("100")
) println(a)
```

実行結果は`100`が表示されるはずです。

---
4. 下記のコードを実行し、結果を貼り付けるとともに、`a`, `b`, `c`, `result`の型を答えて下さい。

```scala
def doubleTheNumber(i: Int) = i * 2

val result = for (
    a <- Some("100")
    b <- Some(a.toInt)
    c <- Some(doubleTheNumber(b))
) yield c * 5

println(result)
```

解答) `println(result)`による表示は`1000`になります。aの型は`String`、bも`Int`、cは`Int`です。
IDE上でa, b, cにカーソルを合わせると型を表示してくれるので確認しやすいです。
forのなかの`<-`によってSomeの「中の値を取り出す」ことに注目して下さい。

5. 上記3.と4.をそれぞれforeach, mapとflatMapを使って書き下してください

解答) 3.について

```scala
for (
    a <- Some("100")
) println(a)

// 上は下と等価

Some("100").foreach { a => println(a) }
```

3.について

```scala
val result = for (
    a <- Some("100")
    b <- Some(a.toInt)
    c <- Some(doubleTheNumber(b))
) yield c * 5
println(result)

// 上は下と等価

val result = Some("100").flatMap { 
  a => Some(a.toInt).flatMap {
      b => Some(doubleTheNumber(b)).map {
         c => c * 5
      }
  }
}
println(result)
```

ScalaのforはflatMap/mapもしくはflatMap/foreachを使って等価な書き換えができます。
多重のネストになっているforはflatMap、ネストの一番内側のレベルはmapもしくはforeachです。mapかforeachどちらを使うかは、最後がyieldで終わっているものはmap, そうでなければforeachです。