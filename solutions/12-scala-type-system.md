## この課題で身につく能力

型システム、AnyとかAnyValとかNothingについて大まかに把握している

ScalaにはNothingなど独特の型があり、他の言語に慣れ親しんでいる人には奇異に映る部分があるかもしれません。
しかしScalaの型システムはJavaと比べても整理されており、いったんその階層構造を理解してしまえば、体系だった知識として定着しやすくなります。(Javaより整っている、といってもJavaの方が劣っているという話ではもちろんなく、長い期間Javaがより後方互換性に気を使って進化してきた、という歴史の違いです。)

## 課題

以下の課題の結果をこのファイルに貼り付けて、Pull Requestを送る形で提出してください

実践Scala入門第２章 p.40 -> ... を読んで以下の問に答えて下さい

---
1. Unitのスーパータイプは`AnyVal`と`AnyRef`どちらでしょう？

解答) Unitのスーパータープは`AnyVal`です。Unit型は副作用を伴うメソッド/関数の戻り値として使われ、Unit型の値は`()`という単一の値のみが許されています。

---
2. `null`の型は何でしょう？

解答) `null`の型は`Null`です。

解答は上記で終わりなのですが、ここからすこし解説をしてみましょう。`Null`型は全ての参照型のサブタイプとなります。このことを示すためにREPLから以下を実行してみましょう。

```
scala> class MyClass
defined class MyClass

scala> val a: MyClass = null
a: MyClass = null
```

つまり参照型である限りはどんな型でも、`null`を値としてもつことができます。これはJavaの動作とも一貫性がありますね。
ただし、Scalaでは`Option`があるため、意図的に`null`を紛れ込ませない限り、直接`null`がソースコードに現れることはないでしょう。
Javaのライブラリを使うときには`null`が使われていることもよくあります。

一方Intは参照型ではないので、エラーになってしまいます。少しエラーメッセージはわかりづらくなっていますが、これは型が合わないためのエラーです。

```
scala> val a: Int = null
                    ^
       error: an expression of type Null is ineligible for implicit conversion
```

---
3. `Exception`, `AnyRef`, `Any`の3つについてexctendsを使ってそれぞれの関係を表して下さい
 - XXXXX exnteds YYYYY, YYYYYY extends ZZZZZZのように

解答) 
```scala
Exception extends AnyRef
AnyRef extends Any

|-----------|  extends   |--------|   extends   |-----|
| Exception | ---------> | AnyRef |  ---------> | Any |
|-----------|            |--------|             |-----|
```

ExceptionとNothingの関係は次の課題でも触れられています。書籍の情報と合わせてしっかり把握するよう心がけて下さい。

---
4. `Nil`, `None`, `Nothing` はそれぞれどういう用途で使われるものですか？この答えは実践Scala入門第２章にはありません。

解答) 
これら３つは似たような名前なので混同しないようにしましょう。

`Nil`は要素数ゼロのListを表します。REPLで確かめるとこうなります。

```
scala> Nil
res3: scala.collection.immutable.Nil.type = List()
```

Scala2.13本体のソースコードではこう定義されています。

```scala
case object Nil extends List[Nothing] {
  ...
}
```

`None`は何も値を持っていない`Option`を表します。

```
scala> None
res4: None.type = None
```

Scala2.13本体のソースコードではこう定義されています。

```scala
case object None extends Option[Nothing] {
  def get: Nothing = throw new NoSuchElementException("None.get")
}
```

`Nothing`はScalaの全ての型のサブタイプとなる型です。p.49に解説があります。`Nothing`があるおかげで、Scalaでは例外を投げるメソッド/関数であっても戻り値の型に矛盾が生じません。

