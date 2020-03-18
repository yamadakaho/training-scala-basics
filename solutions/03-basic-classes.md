## この課題で身につく能力

戻り値と引数の型を正しく組み合わせて簡単なクラスを書ける

## 課題

1. IDEを使って新しいプロジェクトを作り、その中でMainクラスを定義し、ソースコードとプロジェクト・ディレクトリの階層構造をを貼り付けて提出して下さい

これは何も見なくても書けるくらいになってください。これがすぐに書けないと「IDEで動作確認するの面倒だなー」となって、ソースコードの動作確認をする頻度が減ります。
ある程度規模の大きなコードはREPLやPlayGroundではどうしても動かしづらく、どうしてもIDEから動作確認する必要があるため、その心理的ハードルをすこしでも下げられるよう手を慣らして下さい。

```scala
object Main{
  def main(args: Array[String]): Unit = {
  }
}
```

![image](https://user-images.githubusercontent.com/7414320/76871319-3de16000-68ae-11ea-9001-42c718a1f5e9.png)

---
2. 「実践Scala入門」第2章p.54 -> p.55「クラスを定義する」のPointクラスを定義して下さい。(p.55「先回りして例示しておくと…」直後です) 

答えは書籍に載っているので省略します。提出の際は必ず自分で実行した結果を貼り付けてください。

---
3. 「実践Scala入門」第2章p.54 -> p.55「クラスを定義する」の (p.55「まず、先程あげたPointを定義することについて考えてみましょう…」直後です）を 上記課題1. のMainクラスのmain関数の中で呼び出して、実行結果を貼り付けて下さい

答えは書籍に載っているので省略します。提出の際は必ず自分で実行した結果を貼り付けてください。

---
4. 3.で定義したPointクラスを参考に、xとy座標のみを持つPoint2Dクラスを定義して、TriangleAreaクラスとそのメソッド`def area: Double`を実装して下さい
  - 4.1 TriangleAreaクラスはPoint2Dを3つフィールドに持つクラスです
  - 4.2 Point2D(1,2),Point2D(3,4),Point2D(0,0)の３頂点をもつ三角形の面積を求めるコードを書いて下さい。答えは面積 = 1です。 https://mathwords.net/x1y2hikux2y1
  - 4.3 Point2D(5,7),Point2D(3,4),Point2D(1,2)の３頂点をもつ三角形の面積を求めるコードを書いて下さい。答えは面積 = 1です。 https://mathwords.net/x1y2hikux2y1

```scala
class Point2D(val x: Int, val y: Int)

class TriangleArea(p1: Point2D, p2: Point2D, p3: Point2D) {
  def area: Double = Math.abs((p1.x-p3.x)*(p2.y-p3.y) - (p2.x-p3.x)*(p1.y-p3.y)) / 2.0
}

val firstTriangle = new TriangleArea(new Point2D(1, 2), new Point2D(3, 4), new Point2D(0,0))
//結果: 1.0
println(firstTriangle.area) 

val secondTriangle = new TriangleArea(new Point2D(5, 7), new Point2D(3, 4), new Point2D(1,2))
//結果: 1.0
println(secondTriangle.area)
```