## この課題で身につく能力

Option、Either、Exceptionを使ってエラー表現できる

## 課題

以下の課題の結果をこのファイルに貼り付けて、Pull Requestを送る形で提出してください

1. 「実践Scala入門」第2章p.81 throw式、の`RuntimeException`を投げるコードを実行して結果を貼り付けて下さい。
  - 1.1 REPLから実行して下さい
  - 1.2 IDEから実行して下さい

2. 「実践Scala入門」第2章 p.81 try式のコード例ひとつめを実行して結果を貼り付けて下さい。
  - 「以下のようなコードで、例外を補足できます。(RuntimeExceptionを投げるのはあまりよいことではありませんが)」の直後、
  - 「より一般的には次のような構文になります」の直前です

3. 「実践Scala入門」第2章 p.80 例外機構のコード例、`public class UsingException`をIDEで書き写して、コマンドラインから実行して下さい。コマンドラインから`main`メソッドに渡す引数は1, 2, 3と渡して、結果を貼り付けて下さい

4. 「実践Scala入門」第3章 p.103のコード例3つを全てREPLから実行して結果を貼り付けて下さい 

5. 「実践Scala入門第2章」p.80 例外機構のコード例、`public class UsingException`をOptionを使って書き換えて下さい
  - 例外を投げるかわりに`None`を返します
  - `return m/n`を返すかわりに`Some（m／n）`を返します

6. [Scala 公式APIドキュメント Either](https://www.scala-lang.org/api/2.13.0/scala/util/Either.html)のコード例
より、IDEから以下のコードをもつmainクラス/メソッドを作って実行して下さい。`readLine`に渡すコマンドラインからの入力は`1`, `2`, `abc`, です。結果を貼り付けて下さい。
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
