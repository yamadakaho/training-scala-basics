## この課題で身につく能力

companion objectとcase classを使える

## 課題

以下の課題の結果をこのファイルに貼り付けて、Pull Requestを送る形で提出してください

1. 実践Scala入門第２章、 「2-６ケースクラス」のclass Pointとobject Pointの定義をするコードを書いて下さい

2. 上記1.で定義したPointをもとに、「2-2クラスを定義する」にあるPointを呼び出すコード（まず、先程あげたPointを定義することについて考えましょう…の直後です）を再び書いて出力を確認して貼り付けて下さい。`new` が消えることに気づくはずです。

3. 上記1.のPointの定義を、「2-６ケースクラス」の`case class`で置き換えて下さい、10行近いコードが1行になります。

4. 次のコードの出力結果を確認して下さい

```scala
val p1 = Point(1,2)
val p2 = p1.copy(x = 10)
println(p1)
println(p2)
```
