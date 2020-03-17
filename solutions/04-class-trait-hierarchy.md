## この課題で身につく能力

(クラス図を渡されれば)traitおよびclassをextendsして簡単なクラスを作れる

## 課題

以下の課題の結果をこのファイルに貼り付けて、Pull Requestを送る形で提出してください

1. 「実践Scala入門」第2章p.59 -> p.60、「クラスの継承」にあるShape, Triangle, Rectangle, UnknownShapeの定義およびそれらの`def shape`メソッドを呼び出すコードを書いて呼び出し結果を貼り付けて下さい

答えは書籍に載っているので省略します。提出の際は必ず自分で実行した結果を貼り付けてください。

2. 上記1. Shapeのインスタンスを直接newしてコンパイルエラーが発生するのを確認して下さい

```scala
val shape = new Shape
```

で、以下のようなエラーが発生するはず

```
error: class Shape is abstract; cannot be instantiated
```

3. 上記1. Shapeの定義を以下のように書き換え、Shapeのインスタンスを直接newして、コンパイルエラーが消えるのを確認して下さい

```scala
class Shape {
  def draw(): Unit
}
```

上記2.で発生したエラーが消えるはず

4. 以下のクラス図をもとにtraitとclassを定義してください。それぞれのクラスでのrunメソッドは以下の文字列をprintlnで出力するよう実装し、クラスの定義と実装結果を貼り付けて提出してください。

![Image from iOS (33)](https://user-images.githubusercontent.com/7414320/76874598-bf3af180-68b2-11ea-8659-b076dd4f29d0.jpg)

```scala
class Cat:           // "I can run at 48km/h" 
class Cheetah:       // "I run at 93km/h, you can't see me" 
class Human:         // "20 km/h isn't so bad actually" 
class OlympicAthlete // "40 km/h at maximum" 
```

答えは以下です。

```scala
trait Animal {
  def run(): Unit
}

class Cat extends Animal {
  override def run(): Unit = println("I can run at 48km/h")
}

class Cheetah extends Cat {
  override def run(): Unit = println("I run at 93km/h, you can't see me")
}

class Human extends Animal {
  override def run(): Unit = println("20 km/h isn't so bad actually")
}

class OlympicAthlete extends Human {
  override def run(): Unit = println("40 km/h at maximum")
}

val cat: Animal = new Cat
//結果: "I can run at 48km/h"
cat.run()

val cheetah: Animal = new Cheetah
//結果: "I run at 93km/h, you can't see me"
cheetah.run()

val human: Animal = new Human
//結果: "20 km/h isn't so bad actually"
human.run()

val olympicAthlete: Animal = new OlympicAthlete
//結果: "40 km/h at maximum"
olympicAthlete.run()
```

さて、今回は練習のため継承を使いましたが、本番環境で継承を使うときには気をつけてください。
継承を覚えると、なんでも継承によって表現したくなりますが、そのデメリットは大きいです。

継承でなくtraitのextends(実装)もまた、同じようなデメリットをもたらすので、どちらもextendsには注意しましょう。

継承はつまり、ソースコードの共通化です。子クラスでは親のコードの一部を共通の処理として再利用します。

しかし、共通化は高度なセンスと経験を要する判断の積み重ねですです。これは有名なOSSライブラリを考えてみればわかるでしょう。
有名なOSSライブラリは、多くの場合その分野において世界で最も優れたプログラマたちが保守を行っています。
彼らが長い年月をかけて慎重に、慎重にメソッドのパラメタやクラスの種類(= API)を決めています。

コードの共通化は、それくらい注意しないと、あっというまに破綻してしまう難度の高いものです。
特に継承による共通化は、親子クラス間で密結合をうみだし、一旦うまれた継承関係を後から変えることは大変な労力を要します。

そもそも共通化された部分は長い年月を経ても安定していなければならず、変更が少なくあるべきです。
共通化された部分はいわばAPIなので、APIの利用側よりAPI側のほうがコロコロ頻繁に変化しては使いづらくて仕方がありません。
ソースコードの書き始めに、いきなり長期的に安定するAPIを見いだせるプログラマはいないでしょう。

