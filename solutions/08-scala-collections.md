## この課題で身につく能力

Seq、Set、Mapなど基本的なコレクションとそれらの主な違い、メソッドを把握して使える
(mutable/immutableの違いは別の課題で扱う)

## 課題

以下の課題の結果をこのファイルに貼り付けて、Pull Requestを送る形で提出してください

1. 「実践Scala入門」第4章 p.124 -> 125, 「Seq, Set, Map」コード例3つを全部実行して結果を貼り付けて下さい
  - `Seq("A", "B", "C")` の戻り値が `List` であることを確認しましょう。 抽象 `trait Seq`と、実装 `class List`の違いです。

答えは書籍に載っているので省略します。提出の際は必ず自分で実行した結果を貼り付けてください。
IDEからScala自体のソースコードをたどって、`trait Seq`と`class List`をみつけてください。Scala 2.13では`sealed abstract class List`となっているので、さらにもう一段階具体的な実装クラス、`::` と `Nil`があります。

```scala
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

2. 「実践Scala入門」第4章 「Seqの操作」のコード例をp.128 -> 134まで全部実行して結果を貼り付けて下さい。p.135以降「Seqの要素を変換する」から先は実行する必要はありません。

答えは書籍に載っているので省略します。提出の際は必ず自分で実行した結果を貼り付けてください。

3. 「実践Scala入門」第4章 「Setの操作」のコード例をp.143 -> 144まで全部実行して結果を貼り付けて下さい。p.145以降「可変なSetに対する操作」から先は実行する必要はありません。

答えは書籍に載っているので省略します。提出の際は必ず自分で実行した結果を貼り付けてください。

4. 「実践Scala入門」第4章 「Setの操作」のコード例をp.143 -> 144まで全部実行して結果を貼り付けて下さい。p.145以降「可変なSetに対する操作」から先は実行する必要はありません。

答えは書籍に載っているので省略します。提出の際は必ず自分で実行した結果を貼り付けてください。

5. 「実践Scala入門」第4章 「Mapの操作」のコード例をp.146 -> 148まで全部実行して結果を貼り付けて下さい。p.149以降「可変なMapに対する操作」から先は実行する必要はありません。
  - Mapのapplyメソッド(p.147では`priceList("Banana")`)とMapのgetメソッドの戻り値の違いを確認して下さい

答えは書籍に載っているので省略します。提出の際は必ず自分で実行した結果を貼り付けてください。

6. 口頭試問: 「実践Scala入門」第4章 「4-3コレクションの実装ごとの性能特性」を図を描きながら説明し、なぜデータ構造の実装が表でまとめられた性能特性を持つのか、表の一部分だけでいいのでわかるところについて説明してください。

Listのhead/tail/apply/先頭に追加/最後に追加