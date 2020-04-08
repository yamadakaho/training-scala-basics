## この課題で身につく能力

(クラス図を渡されれば)traitおよびclassをextendsして簡単なクラスを作れる

## 課題

以下の課題の結果をこのファイルに貼り付けて、Pull Requestを送る形で提出してください

1. 「実践Scala入門」第2章p.59 -> p.60、「クラスの継承」にあるShape, Triangle, Rectangle, UnknownShapeの定義およびそれらの`def shape`メソッドを呼び出すコードを書いて呼び出し結果を貼り付けて下さい

```
abstract class Shape {
  def draw(): Unit = {
    println("不明な図形")
  }
}

class Triangle extends Shape {
  override def draw(): Unit = {
    println("三角形")
  }
}

class Rectangle extends Shape {
  override def draw(): Unit = {
    println("四角形")
  }
}

class UnknownShape extends Shape


object Main {
  def main(args: Array[String]): Unit = {
    var shape: Shape = new Triangle
    shape.draw()

    shape = new Rectangle
    shape.draw()

    shape = new UnknownShape
    shape.draw()
  }
}
```
```
[info] Compiling 1 Scala source to /Users/kaho.yamada/assiginment-04/target/scala-2.13/classes ...
[info] running example.Main 
三角形
四角形
不明な図形
[success] Total time: 1 s, completed 2020/04/07 18:45:33
```

2. 上記1. Shapeのインスタンスを直接newしてコンパイルエラーが発生するのを確認して下さい

```
object Main {
  def main(args: Array[String]): Unit = {
    val shape = new Shape

  }
}
```
```
sbt:assiginment-04> run
[info] Compiling 1 Scala source to /Users/kaho.yamada/assiginment-04/target/scala-2.13/classes ...
[error] /Users/kaho.yamada/assiginment-04/src/main/scala/example/main.scala:26:17: class Shape is abstract; cannot be instantiated
```
3. 上記1. Shapeの定義を以下のように書き換え、Shapeのインスタンスを直接newして、コンパイルエラーが消えるのを確認して下さい

```scala
class Shape {
  def draw(): Unit = {
    println("不明な図形")
  }
}
```
```
sbt:assiginment-04> run
[info] Compiling 1 Scala source to /Users/kaho.yamada/assiginment-04/target/scala-2.13/classes ...
[error] /Users/kaho.yamada/assiginment-04/src/main/scala/example/main.scala:57:9: shape is already defined as value shape
[error]     var shape: Shape = new Triangle
[error]         ^
[error] one error found
[error] (Compile / compileIncremental) Compilation failed
[error] Total time: 0 s, completed 2020/04/08 16:08:50
```
上記2で発生したエラーは消えました

4. 以下のクラス図をもとにtraitとclassを定義してください。それぞれのクラスでのrunメソッドは以下の文字列をprintlnで出力するよう実装し、クラスの定義と実装結果を貼り付けて提出してください。

<img width=400 src="https://user-images.githubusercontent.com/7414320/76874598-bf3af180-68b2-11ea-8659-b076dd4f29d0.jpg" />

```scala
class Cat:           // "I can run at 48km/h" 
class Cheetah:       // "I run at 93km/h, you can't see me" 
class Human:         // "20 km/h isn't so bad actually" 
class OlympicAthlete // "40 km/h at maximum" 
```

```
trait Animal {
  def run(): Unit
}

class Cat extends Animal {
  override def run(): Unit = {
    println("I can run at 48km/h")
  }
}

class Cheetah extends Animal {
  override def run(): Unit = {
    println("I run at 93km/h, you can't see me")
  }
}

class Human extends Animal {
  override def run(): Unit = {
    println("20 km/h isn't so bad actually")
  }
}

class OlympicAthlete extends Animal {
  override def run(): Unit = {
    println("40 km/h at maximum")
  }
}


object Main {
  def main(args: Array[String]): Unit = {

    val cat: Animal = new Cat
    cat.run()

    val cheetah: Animal = new Cheetah
    cheetah.run()

    val human: Animal = new Human
    human.run()

    val olympicAthlete: Animal = new OlympicAthlete
    olympicAthlete.run()

  }
}
```
```
sbt:assiginment-04> run
[info] Compiling 1 Scala source to /Users/kaho.yamada/assiginment-04/target/scala-2.13/classes ...
[info] running example.Main 
I can run at 48km/h
I run at 93km/h, you can't see me
20 km/h isn't so bad actually
40 km/h at maximum
[success] Total time: 1 s, completed 2020/04/08 12:14:53

```