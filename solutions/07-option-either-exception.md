## この課題で身につく能力

Option、Either、Exceptionを使ってエラー表現できる

## 課題

以下の課題の結果をこのファイルに貼り付けて、Pull Requestを送る形で提出してください

---
1. 「実践Scala入門」第2章p.81 throw式、の`RuntimeException`を投げるコードを実行して結果を貼り付けて下さい。
  - 1.1 REPLから実行して下さい
  - 1.2 IDEでプロジェクトをセットアップし、ターミナル/コンソールからプロジェクトディレクトリに移動し、sbtから実行して下さい

解答) 
Exceptionがターミナル/コンソールに表示されるとき、スタックトレースがREPLとsbtで異なるはずです。1.1のREPLでの実行はこのように、

```
scala> throw new RuntimeException("exception")
java.lang.RuntimeException: exception
  ... 28 elided
```

1.2のsbtからの実行ではこの様になります。

```
[error] (run-main-0) java.lang.RuntimeException: aaaaa
[error] java.lang.RuntimeException: aaaaa
[error]         at example.Main$.main(Main.scala:9)
[error]         at example.Main.main(Main.scala)
[error]         at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
[error]         at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
[error]         at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
[error]         at java.base/java.lang.reflect.Method.invoke(Method.java:566)
[error] stack trace is suppressed; run last Compile / bgRun for the full output
[error] Nonzero exit code: 1
[error] (Compile / run) Nonzero exit code: 1
[error] Total time: 4 s, completed Mar 18, 2020, 11:20:09 PM
```

---
2. 「実践Scala入門」第2章 p.81 try式のコード例ひとつめを実行して結果を貼り付けて下さい。
  - 「以下のようなコードで、例外を補足できます。(RuntimeExceptionを投げるのはあまりよいことではありませんが)」の直後、
  - 「より一般的には次のような構文になります」の直前です

解答) 答えは書籍に載っているので省略します。提出の際は必ず自分で実行した結果を貼り付けてください。

---
3. 「実践Scala入門」第2章 p.80 例外機構のJavaコード例、`public class UsingException`をIDE上でScalaに直し、ターミナル/コンソールから実行して下さい。
  - sbtでMain関数に引数を渡すには`sbt run 1`や`sbt run 0`のようにしてください
  - Javaの`public static`はScalaの`object`(コンパニオンオブジェクト)を使えば同等の使い方が出来ます
  - Javaの`Integer.parseInt(args[0])`の代わりにScalaの`args(0).toInt`を使ってください

解答) 
まずは以下のコマンドでIDEで開くことのできるScalaプロジェクトの雛形をつくります。

```
sbt new scala/scala-seed.g8
//この後ターミナル/コンソールでいくつかの質問に対する答えを入力する
```

出来上がるプロジェクト雛形の構成はこのような感じです。

```
project-root-dir
  +-project
  | +-build.properties
  |
  +-src
  | +-main
  |   +-scala
  |     +-example
  |       +-Example.scala
  +-test
  +-build.sbt
```

Example.scalaのファイル名をMain.scalaに書き換えましょう。必須ではなく、好みの問題ですが私はMain.scalaの方が好きです。
次にMain.scalaの中身をこのように書き換えましょう。

```scala
package example

object Main {
  def divide(m: Int, n: Int): Int = {
    if (n == 0) throw new Exception("divided by zero")
    else return m / n
  }

  def main(args: Array[String]): Unit = {
    val n = args(0).toInt
    try {
      println(divide(10, n))
    } catch {
      case e: Exception => println(e)
    }
  }
}
```

最後にsbtから実行しましょう。
`sbt run 1`や`sbt run 0`のように実行しても良いですし、`sbt`だけでsbtシェルを立ち上げてから`run 1` `run 0`のようにしても良いです。

```
sbt:my-proj> run 1
[info] running example.Main 1
10
[success] Total time: 1 s, completed Mar 18, 2020, 11:57:11 PM

sbt:my-proj> run 0
[info] running example.Main 0
java.lang.Exception: divided by zero
```

---
4. 「実践Scala入門」第3章 p.103のコード例3つを全てREPLから実行して結果を貼り付けて下さい 

解答) 答えは書籍に載っているので省略します。提出の際は必ず自分で実行した結果を貼り付けてください。

---
5. 「実践Scala入門」第2章 p.80 例外機構のJavaコード例、`public class UsingException`をIDE上でOptionを使ってScalaに直し、ターミナル/コンソールから実行して下さい。
  - 例外を投げるかわりに`None`を返します
  - `return m/n`を返すかわりに`Some（m／n）`を返します

解答) 
コードはこちら

```scala
package example

object Main {
  def divide(m: Int, n: Int): Option[Int] = {
    if (n == 0) None
    else return Some(m / n)
  }

  def main(args: Array[String]): Unit = {
    val n = args(0).toInt
    divide(10, n) match {
      case Some(i) => println(i)
      case None => println("divided by zero")
    }
  }
}
```

実行結果はこちらです。

```
sbt:my-proj> run 1
[info] running example.Main 1
10
[success] Total time: 0 s, completed Mar 19, 2020, 12:02:25 AM

sbt:my-proj> run 0
[info] running example.Main 0
divided by zero
[success] Total time: 1 s, completed Mar 19, 2020, 12:02:28 AM
```

---
6. [Scala 公式APIドキュメント Either](https://www.scala-lang.org/api/2.13.0/scala/util/Either.html)のコード例
より、IDEから以下のコードをもつmainクラス/メソッドを作って実行して下さい。`readLine`に渡すターミナル/コンソールからの入力は`1`, `2`, `abc`, です。結果を貼り付けて下さい。

```scala
import scala.io.StdIn._
val in = readLine("Type Either a string or an Int: ")
val result: Either[String,Int] =
  try Right(in.toInt)
  catch {
    case e: NumberFormatException => Left(in)
  }

result match {
  case Right(x) => s"You passed me the Int: $x, which I will increment. $x + 1 = ${x+1}"
  case Left(x)  => s"You passed me the String: $x"
}
```

解答) コードは上に載っているので解答を省略します。必ず自分で実行して結果を確かめてください。