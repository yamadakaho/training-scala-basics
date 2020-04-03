## この課題で身につく能力

数値型や文字型などの基本型を使った結合などの基本操作ができる

## 課題

以下の課題の結果をこのファイルに貼り付けて、Pull Requestを送る形で提出してください

1. 「実践Scala入門」第2章p.42 -> p.46 Int, Long, Short, Char, Double, Float, Booleanのコード例をREPLで実行し、結果をコピペで貼り付けて下さい

[Int]
scala> 1 + 2
res0: Int = 3

scala> 3 * 4
res1: Int = 12

[Long]
scala> 1L
res2: Long = 1

scala> 2L
res3: Long = 2

scala> 1L + 2L
res4: Long = 3

[Short]
scala> val a:Short = 32767
a: Short = 32767

scala> val b:Short = 32768
                     ^
       error: type mismatch;
        found   : Int(32768)
        required: Short

scala> val c:Short = -32768
c: Short = -32768

scala> val d:Short = -32769
                     ^
       error: type mismatch;
        found   : Int(-32769)
        required: Short

scala> a + c
res5: Int = -1

[Char]
scala> '\n'
res6: Char =

scala> '\r'
res7: Char =

scala> '"'
res8: Char = "

scala> '\u0022'
res9: Char = "

[Double]
scala> 'a'
res10: Char = a

scala> 1.0
res11: Double = 1.0

scala> 1.5
res12: Double = 1.5

scala> 2.0
res13: Double = 2.0

scala> 2.5d
res14: Double = 2.5

scala> 2.6D
res15: Double = 2.6

[Float]
scala> 1.0f
res16: Float = 1.0

scala> 1.5F
res17: Float = 1.5

scala> 2.0F
res18: Float = 2.0

scala> 3.0F
res19: Float = 3.0

[Boolean]
scala> true
res20: Boolean = true

scala> false
res21: Boolean = false

scala> true || true
res24: Boolean = true

scala> true || false
res25: Boolean = true

scala> false || false
res26: Boolean = false

scala> true && true
res27: Boolean = true

scala> true && false
res28: Boolean = false


2. 「実践Scala入門」第2章p.50 -> p.52 、Stringの単一行文字リテラル、複数行文字リテラル、stripMargin、文字列補間のコード例をREPLで実行し、結果をコピペで貼り付けて下さい

[単一行文字列リテラル]
scala> "Hoge"
res30: String = Hoge

scala> "Foo"
res31: String = Foo

scala> "Hoge\r\nHoge"
res32: String =
Hoge
Hoge

scala> "Hoge\\u0022Hoge"
res33: String = Hoge\u0022Hoge

[複数行文字リテラル]
scala> """
     | This is
     | a multiline String
     | literal
     | """
res34: String =
"
This is
a multiline String
literal
"

scala> """\r\n"""
res35: String = \r\n

[stripMargin]
scala> """
     |  This is
     |  a multiline String
     |  literal
     | """
res36: String =
"
 This is
 a multiline String
 literal
"

scala> """| This is
     |    | a multiline String
     |    | literal """.stripMargin
res37: String =
" This is
 a multiline String
 literal "

[文字列補間]
scala> s"1 + 2 = ${1 + 2}"
res38: String = 1 + 2 = 3

scala> val a = 1
a: Int = 1

scala> s"a = $a"
res39: String = a = 1

scala> s"${List(1, 2, 3, 4)}"
res40: String = List(1, 2, 3, 4)

scala> s"""|${1 + 2}
     |     |${2 + 3}
     |     |${3 + 4}""".stripMargin
res41: String =
3
5
7