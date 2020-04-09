## この課題で身につく能力

戻り値と引数の型を正しく組み合わせて簡単なクラスを書ける

## 課題

以下の課題の結果をこのファイルに貼り付けて、Pull Requestを送る形で提出してください

1. IDEを使って新しいプロジェクトを作り、その中でMainクラスを定義し、ソースコードとプロジェクト・ディレクトリの階層構造をを貼り付けて提出して下さい

これは何も見なくても書けるくらいになってください。これがすぐに書けないと「IDEで動作確認するの面倒だなー」となって、ソースコードの動作確認をする頻度が減ります。
ある程度複雑なコードはどうしてもIDEから動作確認する必要があるため、そのハードルをすこしでも下げられるよう手を慣らして下さい。

```
object Main {
  def main(args: Array[String]): Unit = {
  }
```

<img width="304" alt="スクリーンショット 2020-04-03 16 56 52" src="https://user-images.githubusercontent.com/62977633/78636548-83101500-78e3-11ea-85cc-bb652f8b5859.png">

2. 「実践Scala入門」第2章p.54 -> p.55「クラスを定義する」のPointクラスを定義して下さい。(p.55「先回りして例示しておくと…」直後です) 

```
class Point(val x: Int, val y: Int) {
 def distance(that: Point): Int = {
  val xdiff = math.abs(this.x - that.x)
  val ydiff = math.abs(this.y - that.y)
  math.sqrt(xdiff * xdiff + ydiff * ydiff).toInt
  }
  
  def +(that: Point): Point =
   new Point(x + that.x, y + that.y)

  override def toString: String = s"Point(${x}, ${y})"
 }
 ```
3. 「実践Scala入門」第2章p.54 -> p.55「クラスを定義する」の (p.55「まず、先程あげたPointを定義することについて考えてみましょう…」直後です）を 上記課題1. のMainクラスのmain関数の中で呼び出して、実行結果を貼り付けて下さい

```
object Main {
  def main(args: Array[String]): Unit = {

    val p1: Point = new Point(10, 10)
    val p2: Point = new Point(100, 100)

    println(p1.distance(p2))
    println(math.abs(p1.x - p2.x))
    println(p1 + p2)
  }
}
```
```
sbt:hello-world> run
[info] running Main 
127
90
Point(110, 110)
[success] Total time: 0 s, completed 2020/04/07 12:53:58

```

4. 3.で定義したPointクラスを参考に、xとy座標のみを持つPoint2Dクラスを定義して、TriangleAreaクラスとそのメソッド`def area: Double`を実装して下さい
  - 4.1 TriangleAreaクラスはPoint2Dを3つフィールドに持つクラスです
  - 4.2 Point2D(1,2),Point2D(3,4),Point2D(0,0)の３頂点をもつ三角形の面積を求めるコードを書いて下さい。答えは面積 = 1です。 https://mathwords.net/x1y2hikux2y1
  - 4.3 Point2D(5,7),Point2D(3,4),Point2D(1,2)の３頂点をもつ三角形の面積を求めるコードを書いて下さい。答えは面積 = 1です。 https://mathwords.net/x1y2hikux2y1

```
class Point2D(val x: Int, val y: Int)

class TriangleArea(p1: Point2D, p2: Point2D, p3: Point2D ) {
  def area: Double = Math.abs((p1.x-p3.x)*(p2.y-p3.y) - (p2.x-p3.x)*(p1.y-p3.y)) / 2.0


object Main {
  def main(args: Array[String]): Unit = {

    val firstTriangle = new TriangleArea(new Point2D(1, 2), new Point2D(3, 4), new Point2D(0,0))
    println(firstTriangle.area)

    val secondTriangle = new TriangleArea(new Point2D(5, 7), new Point2D(3, 4), new Point2D(1, 2))
    println(secondTriangle.area)
  }
}
```

```
sbt:hello-world> run
[info] Compiling 1 Scala source to /Users/kaho.yamada/assignment-03-template/target/scala-2.13/classes ...
[info] running Main 
1.0
1.0
[success] Total time: 1 s, completed 2020/04/07 13:18:39
```