## この課題で身につく能力

forをmapとflatMapに手書き展開できる

## 課題

以下の課題の結果をこのファイルに貼り付けて、Pull Requestを送る形で提出してください

1. コップ本「Scalaスケーラブルプログラミング 第３版」 p.441 -> p.442 の23.1「for式」のコード例を全て実行し、結果を貼り付けて下さい

2. コップ本「Scalaスケーラブルプログラミング 第３版」 p.446 -> p.450 の23.4「for式の変換」のコード例を全て実行し、結果を貼り付けて下さい

3. `Some("100")`を含むfor loop(一重のfor loop)を作成し、Someの内側のStringをprintlnで表示してください

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

5. 上記3.と4.をそれぞれmapとflatMapを使って書き下してください