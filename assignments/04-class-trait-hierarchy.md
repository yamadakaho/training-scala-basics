## この課題で身につく能力

(クラス図を渡されれば)traitおよびclassをextendsして簡単なクラスを作れる

## 課題

1. 実践Scala入門第２章、「クラスの継承」にあるShape, Triangle, Rectangle, UnknownShapeの定義およびそれらの`def shape`メソッドを呼び出すコードを書いて呼び出し結果を貼り付けて下さい

2. 上記1. Shapeのインスタンスを直接newしてコンパイルエラーが発生するのを確認して下さい

3. 上記1. Shapeの定義を以下のようにかきかえ、Shapeのインスタンスを直接newして、コンパイルエラーが発生するのを確認して下さい

```scala
abstract class Shape {
  def draw(): Unit
}
```
