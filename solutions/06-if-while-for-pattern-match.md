## この課題で身につく能力

if/else、パターンマッチを使える

## 課題

以下の課題の結果をこのファイルに貼り付けて、Pull Requestを送る形で提出してください

---
1. 「実践Scala入門」第2章p.71、「2−7」制御構文のif式の例をREPLで書き写して実行し、結果を貼り付けて下さい

解答) 答えは書籍に載っているので省略します。提出の際は必ず自分で実行した結果を貼り付けてください。

---
2. 「実践Scala入門」第2章p.72 -> p.74、「2−7」制御構文のwhile式、for式の例をREPLで書き写して実行し、結果を貼り付けて下さい

解答) 答えは書籍に載っているので省略します。提出の際は必ず自分で実行した結果を貼り付けてください。

---
3. 九九表の出力をforで実現して下さい。↓のような表の出力です。

```
1  2  3  4  5  6  7  8  9
2  4  6  8 10 12 14 16 18
3  6  9 12 15 18 21 24 27
...
...
9 18 27 36 45 54 63 72 81
```

解答) 
ソースコードはこのようになります

```scala
for (i <- 1 to 9; j <- 1 to 9) {
  if(j != 9)
    print(f"${i*j}%2d ") //f"..."はフォーマットを伴う文字列、またprintlnではなくprintなので改行なし
  else
    println(f"${i*j}%2d") //j == 9のみ改行
}
```

`f"${i*j}%2d "`という見慣れない表記が出てきますが、これを変わりに`s"${i*j} "`としてしまうと、以下のように1ケタの数字と2ケタの数字で表示が微妙にずれてしまいます。
それを防ぐためにフォーマットを扱う文字列である`f"${i*j}%2d "`を使っています。

```
// f"${i*j}%2d " ではなく、 s"${i*j} " だとずれてしまう！！
1 2 3 4 5 6 7 8 9
2 4 6 8 10 12 14 16 18
3 6 9 12 15 18 21 24 27
4 8 12 16 20 24 28 32 36
5 10 15 20 25 30 35 40 45
6 12 18 24 30 36 42 48 54
7 14 21 28 35 42 49 56 63
8 16 24 32 40 48 56 64 72
9 18 27 36 45 54 63 72 81
```

---
4. コップ本「Scalaスケーラブルプログラミング第3版」の第15章「ケースクラスとパターンマッチ」からリスト15.1と15.2を書き写して、以下を実行して結果を貼り付けて下さい。

```scala
simplifyTop(UnOp("-", Var("x")))
simplifyTop(UnOp("-", UnOp("-", Var("x"))))
simplifyTop(BinOp("+", Number(1), Number(2)))
simplifyTop(BinOp("+", Number(1), Number(0)))
simplifyTop(BinOp("*", Number(7), Number(8)))
simplifyTop(BinOp("*", Number(7), Number(1)))

val e1 = BinOp("*", Number(3), Number(1))
val e2 = BinOp("+", Number(4), Number(0))
simplifyTop(BinOp("*", simplifyTop(e1), simplifyTop(e2)))
```

解答) それぞれの行をprintlnなどで表示してやると以下になります

```scala
simplifyTop(UnOp("-", Var("x")))              // UnOp(-,Var(x)) : そのまま
simplifyTop(UnOp("-", UnOp("-", Var("x"))))   // Var(x) : -と-で打ち消し合う 
simplifyTop(BinOp("+", Number(1), Number(2))) // BinOp(+,Number(1.0),Number(2.0)) : そのまま
simplifyTop(BinOp("+", Number(1), Number(0))) // Number(1.0) : 0との+なので単純化される
simplifyTop(BinOp("*", Number(7), Number(8))) // BinOp(*,Number(7.0),Number(8.0)) : そのまま
simplifyTop(BinOp("*", Number(7), Number(1))) // Number(7.0) : 1との*なので単純化される

val e1 = BinOp("*", Number(3), Number(1))
val e2 = BinOp("+", Number(4), Number(0))
simplifyTop(BinOp("*", simplifyTop(e1), simplifyTop(e2))) // BinOp(*,Number(3.0),Number(4.0))
```

`simplifyTop`は内部でパターンマッチを使った、(Scalaをよく知らない人には)見慣れない形式の関数ですが、この形式はいわゆるAST(Abstract Syntax Tree)を処理するのに便利です。
ASTはプログラミング言語の処理系を作るのによく使われるテクニックで、Scalaの用途の一つとして「プログラミング言語内のミニプログラミング言語」、つまりDSL(Domain Specific Language)と呼ばれるものを作ることがあります。

自分でDSLを作りたくなったときのために(DSLを作るのは難しいのでおすすめはしませんが)、あるいはプログラミング言語自体の勉強をしたくなったときのために、これらを頭の片隅に入れておくと良いでしょう。
