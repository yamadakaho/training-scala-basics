## この課題で身につく能力

Seq、Set、Mapなど基本的なコレクションとそれらの主な違い、メソッドを把握して使える
(mutable/immutableの違いは別の課題で扱う)

## 課題

以下の課題の結果をこのファイルに貼り付けて、Pull Requestを送る形で提出してください

---
1. 「実践Scala入門」第4章 p.124 -> 125, 「Seq, Set, Map」コード例3つを全部実行して結果を貼り付けて下さい
  - `Seq("A", "B", "C")` の戻り値が `List` であることを確認しましょう。 抽象 `trait Seq`と、実装 `class List`の違いです。

解答) 答えは書籍に載っているので省略します。提出の際は必ず自分で実行した結果を貼り付けてください。
IDEからScala本体のソースコードをたどって、`trait Seq`と`class List`をみつけてください。Scala 2.13では`sealed abstract class List`となっているので、さらにもう一段階具体的な実装クラス、`::` と `Nil`があります。

```scala
// Scala本体のソースコード
final case class :: [+A](override val head: A, private[scala] var next: List[A @uncheckedVariance]) // sound because `next` is used only locally
  extends List[A] {
  releaseFence()
  override def headOption: Some[A] = Some(head)
  override def tail: List[A] = next
}

case object Nil extends List[Nothing] {
  override def head: Nothing = throw new NoSuchElementException("head of empty list")
  override def headOption: None.type = None
  override def tail: Nothing = throw new UnsupportedOperationException("tail of empty list")
  override def last: Nothing = throw new NoSuchElementException("last of empty list")
  override def init: Nothing = throw new UnsupportedOperationException("init of empty list")
  override def knownSize: Int = 0
  override def iterator: Iterator[Nothing] = Iterator.empty
  override def unzip[A1, A2](implicit asPair: Nothing => (A1, A2)): (List[A1], List[A2]) = EmptyUnzip

  @transient
  private[this] val EmptyUnzip = (Nil, Nil)
}
```

---
2. 「実践Scala入門」第4章 「Seqの操作」のコード例をp.128 -> 134まで全部実行して結果を貼り付けて下さい。p.135以降「Seqの要素を変換する」から先は実行する必要はありません。

解答) 答えは書籍に載っているので省略します。提出の際は必ず自分で実行した結果を貼り付けてください。

---
3. 「実践Scala入門」第4章 「Setの操作」のコード例をp.143 -> 144まで全部実行して結果を貼り付けて下さい。p.145以降「可変なSetに対する操作」から先は実行する必要はありません。

解答) 答えは書籍に載っているので省略します。提出の際は必ず自分で実行した結果を貼り付けてください。

---
4. 「実践Scala入門」第4章 「Setの操作」のコード例をp.143 -> 144まで全部実行して結果を貼り付けて下さい。p.145以降「可変なSetに対する操作」から先は実行する必要はありません。

解答) 答えは書籍に載っているので省略します。提出の際は必ず自分で実行した結果を貼り付けてください。

---
5. 「実践Scala入門」第4章 「Mapの操作」のコード例をp.146 -> 148まで全部実行して結果を貼り付けて下さい。p.149以降「可変なMapに対する操作」から先は実行する必要はありません。
  - Mapのapplyメソッド(p.147では`priceList("Banana")`)とMapのgetメソッドの戻り値の違いを確認して下さい

解答) 答えは書籍に載っているので省略します。提出の際は必ず自分で実行した結果を貼り付けてください。
「Mapのapplyメソッド(p.147では`priceList("Banana")`)とMapのgetメソッドの戻り値の違い」はapplyは存在しないキーをパラメタとして渡すと、NuSuchElementExceptionがなげられるのに対し、
getはOptionのNoneが返ってExceptionは投げられない点です。

---
6. 口頭試問: 「実践Scala入門」第4章 p.151 「4-3コレクションの実装ごとの性能特性」を図を描きながら説明し、なぜデータ構造の実装が表でまとめられた性能特性を持つのか、表の一部分だけでいいのでわかるところについて説明してください。
- Listのhead/tail/apply/先頭に追加/最後に追加
- Vectorのhead/tail/apply/先頭に追加/最後に追加
- HashSetの検索を説明できれば十分でしょう。

解答) Listの実態はScala本体では`::`という少し変わった名前のクラスで、以下のように定義されています。

```scala
case class :: [+A](head: A, next: List[A]) extends List[A] { 
  override def tail: List[A] = next
  ... 
}
```

`::`は関数型プログラミングの世界でListデータ構造を表す記号として広く使われ、"Cons"という呼び方をします。
上記より、Listの実態`::`を図で表すと以下のようになります。

つまり`List("a","b","c")`は実際には`::("a", ::("b", ::("c", Nil )))`となっています。

`case class :: [+A](head: A, next: List[A])`とあるようにheadはメンバとして保持しているので定数時間でアクセスできます。
tailは「最後の要素」ではなく、先頭要素を除いた残りのListを返すことに注意してください。tailも同じく定数時間です。
`apply(i)`はi番目の要素へのアクセスで、applyは図を見てわかるように、tailのtailのtailの…と順番にたどっていかなくてはならないため、線形時間のアクセスになります。

<img width=400 src="https://user-images.githubusercontent.com/7414320/77142099-722d6a00-6ac2-11ea-8e7c-3bc97bd9bcd5.png" />

先頭に追加はListの一番「外側」を一つ付け足すだけでよいので定数時間で、

<img width=400 src="https://user-images.githubusercontent.com/7414320/77142564-d997e980-6ac3-11ea-9ed0-5e11c5795ac0.jpg" />
1.最後に追加される要素"d"のみにListを作る
2."c"を先頭に追加

最後に追加の場合はListを全て作り直しなので線形時間がかかります。

次にVectorの性能特性です。Vectorは木構造として定義されています。

> Vectors are represented as broad, shallow trees. Every tree node contains up to 32 elements of the vector or contains up to 32 other tree nodes

<img width=400 src="https://user-images.githubusercontent.com/7414320/77142565-dac91680-6ac3-11ea-82eb-f47232c3d41e.jpg" />

Vectorはhead/tail/apply/の3つ、つまりVector内のどのElementへのアクセスも「実質定数」時間で終わります。
コップ本「Scalaスケーラブルプログラミング 第3版」24章より引用。

> Vectors with up to 32 elements can be represented in a single node. Vectors with up to 32 * 32 = 1024 elements can be represented with a single indirection. Two hops from the root of the tree to the final element node are sufficient for vectors with up to 215 elements, three hops for vectors with 220, four hops for vectors with 225 elements and five hops for vectors with up to 230 elements.

HashSetに関しては https://en.wikipedia.org/wiki/Hash_table が図も含めてわかりやすく書いてあります。一般的なHash Tableの解説なので、ScalaのHashSetの実装とは違うと思いますが、似ている部分もあるのでサラッとWikipediaの記事を読み流してみるといいでしょう。