## この課題で身につく能力

companion objectとcase classを使える

## 課題

以下の課題の結果をこのファイルに貼り付けて、Pull Requestを送る形で提出してください

1. 「実践Scala入門」第2章p.67 -> p.69、「2-６ケースクラス」のclass Pointとobject Pointの定義をするコードを書いて下さい

```
class Point(val x: Int, val y: Int) {
  override def hashCode(): Int = x + y
  override def equals(that: Any): Boolean = that match {
    case that: Point => x == that.x && y == that.y
    case _ => false
  }
  override def toString(): String = "Point(" + x +", " + y + ")"
}

object Point {
  def apply(x: Int, y: Int): Point = new Point(x, y)
}
```
2. 上記1.で定義したPointをもとに、「2-2クラスを定義する」にあるPointを呼び出すコード（まず、先程あげたPointを定義することについて考えましょう…の直後です）を再び書いて出力を確認して貼り付けて下さい。`new` が消えることに気づくはずです。

```
//pointの定義は省略

object Main{
  def main(args: Array[String]): Unit = {
    val p1: Point = Point(10, 10)
    val p2: Point = Point(100, 100)
  }
}
```

```
sbt:assiginment-05> run
[info] running example.Main 
[success] Total time: 0 s, completed 2020/04/09 11:21:02
```

3. 上記1.のPointの定義を、「2-６ケースクラス」の`case class`で置き換えて下さい、10行近いコードが1行になります。
```
case class Point(x: Int, y: Int)

object Main{
  def main(args: Array[String]): Unit = {
    val p1: Point = Point(10, 10)
    val p2: Point = Point(100, 100)
  }
}
```
```
sbt:assiginment-05> run
[info] Compiling 1 Scala source to /Users/kaho.yamada/assiginment-05/target/scala-2.13/classes ...
[info] running example.Main 
[success] Total time: 1 s, completed 2020/04/09 11:26:11
```

4. 次のコードの出力結果を確認して下さい

```scala
val p1 = Point(1,2)
val p2 = p1.copy(x = 10)
println(p1)
println(p2)
```
```
sbt:assiginment-05> run
[info] running example.Main 
Point(1,2)
Point(10,2)
[success] Total time: 0 s, completed 2020/04/09 16:43:08

```