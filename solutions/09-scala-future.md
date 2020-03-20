## この課題で身につく能力

Futureを使った非同期処理を含むソースコードが読め、スレッドの動きを図に起こして説明できる

### ねらい

非同期処理は多くのプログラマを悩ませるもので、概念として理解すること自体も難しく、概念としてある程度理解した後でも本番環境で思いもよらないトラブルを発生させることがよくあります。

ScalaのFutureはJavaから連綿と続く非同期処理の発展の歴史に沿って作られたもので、
あるて程度APIが「きれいに」整っています。ただ整っている一方で抽象度が上がっていて「Futureの裏で何が起こっているかわからん」という感想を持たれることもあるでしょう。

そこであえて抽象度が低い、Java 5.0時代のガイドである[Oracle Java Tutorials](https://docs.oracle.com/javase/tutorial/essential/concurrency/index.html)を含めて解説することで、Scala Futureの「裏で」起こっていることもある程度理解することを狙っています。

時間に余裕のある人はリチャードさんの発表資料があるので、参考にしても良いと思います。

- [非同期処理の歴史から見たコンピューティングの進化 (Richard Imaoka) - builderscon tokyo 2019](https://www.youtube.com/watch?v=Ygkjvz_DgiY&feature=emb_logo)
- [非同期処理の歴史から見たコンピューティングの進化 - SpeakerDeck](https://speakerdeck.com/richardimaokajp/fei-tong-qi-chu-li-falseli-shi-karajian-takonpiyuteingufalsejin-hua)
- [Java 5.0時代の非同期処理技術から学び直すScala/Java非同期処理](https://speakerdeck.com/richardimaokajp/javafei-tong-qi-chu-li)

## 課題

以下の課題の結果をこのファイルに貼り付けて、Pull Requestを送る形で提出してください

1. Oracle Java Tutorialsの[Defining and Starting a Thread](https://docs.oracle.com/javase/tutorial/essential/concurrency/runthread.html)のコード例を、IDEからScalaで実装して実行結果を貼り付けて下さい。

解答)

```scala
package example

object Main {
  class HelloRunnable extends Runnable { //Scalaにimplementsはないのでextends
    def run(): Unit = { //void型の戻り値はScalaではUnit

      //Threadの違いを強調するためにThread.currentThread()を表示
      println("Hello from a thread on " + Thread.currentThread())
    }
  }

  def main(args: Array[String]): Unit = {
    //Threadの違いを強調するためにThread.currentThread()を表示
    println("[main] on " + Thread.currentThread())

    new Thread(new HelloRunnable).start()
  }
}
```

出力はこのようになります。`run-main-2`と`Thread-2`と、別々のスレッドが使われていることに注目してください。

```
[info] running example.Main
[main] on Thread[run-main-2,5,run-main-group-2]
Hello from a thread on Thread[Thread-2,5,run-main-group-2]
```

---
2. Oracle Java Tutorialsの[Pausing Execution with Sleep](https://docs.oracle.com/javase/tutorial/essential/concurrency/sleep.html)のコード例を、IDEからScalaで実装して実行結果を貼り付けて下さい。

解答)

```scala
package example

object Main {
  def main(args: Array[String]): Unit = {
    val importantInfo = Array(
      "Mares eat oats",
      "Does eat oats",
      "Little lambs eat ivy",
      "A kid will eat ivy too"
    )

    for (i <- 0 to importantInfo.length-1) {
      Thread.sleep(4000)
      println(importantInfo(i))
    }
  }
}
```

出力結果はこちらです。`Thread.sleep(4000)`があるため、4000ミリ秒間隔で一行ずつ表示されることに注目してください。

```
Mares eat oats
Does eat oats
Little lambs eat ivy
A kid will eat ivy too
```

ちなみに"Mares eat oats"は1943年にアメリカで発表された[ポップス](https://www.youtube.com/watch?v=d4QImbUVHmk)ですね。

---
3. Oracle Java Tutorialsの[Interrupts](https://docs.oracle.com/javase/tutorial/essential/concurrency/interrupt.html)のコード例を、IDEからScalaで実装して実行結果を貼り付けて下さい。


解答)

```scala
package example

class InterruptibleThread extends Thread {
  val importantInfo = Array(
    "Mares eat oats",
    "Does eat oats",
    "Little lambs eat ivy",
    "A kid will eat ivy too"
  )

  override def run(): Unit = {
    // Scalaでは通常returnを使わないので、tryの中にforを移動しています
    try {
      for (i <- 0 to importantInfo.length-1) {
        Thread.sleep(4000)
        println(importantInfo(i) + " on " + Thread.currentThread() )
      }
    } catch {
      case _: InterruptedException =>
        println("we've been interrupted on " + Thread.currentThread() + ". no more println. no more mairzy doatsy.")
    }
  }
}

object Main {
  def main(args: Array[String]): Unit = {
    val thread = new InterruptibleThread
    thread.start()
    Thread.sleep(5000)
    thread.interrupt()
    Thread.sleep(1000)
    println("ends main " + Thread.currentThread())
  }
}
```

実行結果はこちら

```
Mares eat oats on Thread[Thread-5,5,run-main-group-4]
we've been interrupted on Thread[Thread-5,5,run-main-group-4]. no more println. no more mairzy doatsy.
ends main Thread[run-main-4,5,run-main-group-4]
```

<img width=600 src="https://user-images.githubusercontent.com/7414320/77151759-00611a80-6ada-11ea-94d4-3e646936a8d7.jpg" />


---
4. Oracle Java Tutorialsの[The Simple Threads Example](https://docs.oracle.com/javase/tutorial/essential/concurrency/simple.html)のコード例を、IDEからScalaで実装して実行結果を貼り付けて下さい。

---
5. 口頭試問: Oracle Java Tutorialsの[Thread Intereference](https://docs.oracle.com/javase/tutorial/essential/concurrency/interfere.html)について図を描いて説明して下さい。コード例は実行しません、なぜなら現代のCPUは速すぎてThread Interferenceを再現するのは難しいからです。

[Java 5.0時代の非同期処理技術から学び直すScala/Java非同期処理](https://speakerdeck.com/richardimaokajp/javafei-tong-qi-chu-li?slide=28)に最適な図がります。

<img width=400 src="https://user-images.githubusercontent.com/7414320/77151689-d27bd600-6ad9-11ea-9efa-586b9f723d79.png" />
<img width=400 src="https://user-images.githubusercontent.com/7414320/77151687-d14aa900-6ad9-11ea-928c-e297da8ca595.png" />
<img width=400 src="https://user-images.githubusercontent.com/7414320/77176553-9bbcb480-6b07-11ea-82f4-4e2892143968.png" />

---
6. 口頭試問: Oracle Java Tutorialsの[Memory Consistency Errors](https://docs.oracle.com/javase/tutorial/essential/concurrency/memconsist.html)について図を描いて説明して下さい。コード例を実行しないのは、現代のCPUは速すぎてMemory Consistency Errorsを再現するのは難しいからです。

[Java 5.0時代の非同期処理技術から学び直すScala/Java非同期処理](https://speakerdeck.com/richardimaokajp/javafei-tong-qi-chu-li?slide=33)に最適な図がります。

<img width=400 src="https://user-images.githubusercontent.com/7414320/77151269-ed017f80-6ad8-11ea-94a3-019a1a7947d9.png" />
<img width=400 src="https://user-images.githubusercontent.com/7414320/77151271-ee32ac80-6ad8-11ea-9fd8-15a210d26b22.png" />
<img width=400 src="https://user-images.githubusercontent.com/7414320/77151278-eecb4300-6ad8-11ea-9bab-5cfc7e55ec1e.png" />
<img width=400 src="https://user-images.githubusercontent.com/7414320/77151259-e8d56200-6ad8-11ea-867f-380c11531fe1.png" />

---
7. 「実践Scala入門」第5章「5-2 Futureの基本的な使い方」から以下に挙げたコードを全部実行して結果を貼り付けて下さい
  - HttpTextClient (p.162)
  - responseFuture (p.164)
  - failedFuture (p.165)

解答) 答えは書籍に載っているので省略します。提出の際は必ず自分で実行した結果を貼り付けてください。

---
8. 「実践Scala入門」第5章 p.170 -> p.172「for式 非同期処理を柔軟に合成する」のコードを全部実行して結果を貼り付けて下さい

解答) 答えは書籍に載っているので省略します。提出の際は必ず自分で実行した結果を貼り付けてください。

---
9. Oracle Java Tutorialsの[Executor Interfaces](https://docs.oracle.com/javase/tutorial/essential/concurrency/simple.html)のコード例`e.execute(r)`を、IDEからScalaで実装して実行結果を貼り付けて下さい。

---
10. 口頭試問: ExecutionContext, Executor, ExecutorService, ExecutionContextExecutor, ThreadPoolExecutor, ForkJoinPoolExecutorについてextends/implementsの関係を図に書いて、Java時代からあるものとScala用のものを分類しつつ、なぜこんなに沢山のtrait, interface, classが必要なのか、どう使い分けられているのか説明して下さい。わからなかったらすぐに聞いた上でまとめ直すとよいでしょう。
  - 参考情報10.1 ExecutorとExecutorServiceはJava時代からあります
  - 参考情報10.2 ThreadPoolExecutorは完全な実装を持つクラスであり、ExecutorとExecutorServiceはinterfaceです
  - 参考情報10.3 ForkJoinPoolExecutorはJava時代からありますが、ThreadPoolExecutorより何年か遅れて登場しました。どういう用途で用いられるでしょう？
  - 参考情報10.4 ExecutionContextはScalaのためのものです。Scala Futureのメソッドの中でimplicit parameterとして使われます
  - 参考情報10.5 ExecutionContextExecutorというJavaとScalaをごっちゃにしたようなネーミングのtraitは、まさにScalaプロジェクトの中でJavaのコードを使うときのためにあるものです

解答) 

Executor, ExecutorService, ThreadPoolExecutor, ForkJoinPoolExecutorはJava時代から存在するもので、Oracle Java Tutorialsの[Executor Interfaces](https://docs.oracle.com/javase/tutorial/essential/concurrency/exinter.html)でも解説されています。


```                       
|---------------------|                  |----------|             |-----------|
| class               |  implements      | interface|   extends   | interface |
| ThreadPoolExecutor  | ---------------> | Executor |  ---------> | Executor  |
|---------------------|             ---> |----------|             |-----------|
                                    |
|---------------------|             |
| class               |  implements |
| ForkJoinPoolExecutor| ------------|
|---------------------|
```

Executorは最も単純なinterfaceであり、たった一つの`execute`メソッドを持ちます。

```java
public interface Executor {
    void execute(Runnable command);
}
```

JavaではExecutorを直接扱うよりは、より多くメソッドがありExecutorServiceを使うことが多く、

```java
public interface ExecutorService extends Executor {
  void shutdown();
  <T> Future<T> submit(Callable<T> task);
  Future<?> submit(Runnable task);
  <T> List<Future<T>> invokeAll(Collection<? extends Callable<T>> tasks) throws InterruptedException;
  ... //その他もっとたくさんのメソッド
}
```

`execute`もしくは`submit`メソッドを使って「スレッドプールに仕事を投げる」イメージです。Threadを直接使っていたときは単一のスレッドをコントロールしていましたが、Executor/ExecutorServiceではスレッドプールという一段階抽象度が上がった対象を扱っていることに注意してください。

<img width=300 src="https://user-images.githubusercontent.com/7414320/77174778-f1439200-6b04-11ea-8611-c985007c9fc0.png" /> <img width=300 src="https://user-images.githubusercontent.com/7414320/77174782-f30d5580-6b04-11ea-9518-5348227d09bd.png" /> <img width=300 src="https://user-images.githubusercontent.com/7414320/77174788-f6084600-6b04-11ea-9f7e-d80eb63c060a.png" />

ExecutorServiceの実装クラスは`ForkJoinPool`, `ScheduledThreadPoolExecutor`, `ThreadPoolExecutor`などがあります。

`ForkJoinPool`はこちらにもあるように、大きな仕事を小さな仕事にどんどん分割して並列処理する、いわゆる分割統治に便利なThreadPoolとして使われる想定でした。

http://tutorials.jenkov.com/java-util-concurrent/java-fork-and-join-forkjoinpool.html

現代では大規模な分割統治はGPUを使う、あるいはHadoopなどの分散処理システムを使うことが増えて、単一マシン内でForkJoinPoolによる分割統治を行うことは昔ほど頻繁には行われていないです。
一方「Work-Stealing」アルゴリズム用のThreadPoolとしてはForkJoinPoolは今でも非常に有用で、https://akka.io/ のデフォルトThreadPoolとして採用されています。

さて、ここからはScalaの話、`ExecutionContext`と`ExecutionContextExecutor`についてです。Scala標準のFutureをみると、

```scala
trait Future[+T] extends Awaitable[T] {
  def onComplete[U](f: Try[T] => U)(implicit executor: ExecutionContext): Unit
  def transform[S](f: Try[T] => Try[S])(implicit executor: ExecutionContext): Future[S]
  ... //他にもメソッドいっぱい
}
```

上記のように`implicit executor: ExecutionContext`というimplicit parameterが様々なメソッド使われています。
つまりScalaのFutureは裏側で動くThreadPoolを必要としていて、そのThreadPoolが`implicit executor: ExecutionContext`として表現されています。

ThreadPoolはアプリケーション内で無節操に作り出すものではなく、慎重にコントロールした上で、使うべき場所を特定した上で本番環境での負荷をしっかり監視するものです。
つまり、一度つくったThreadPoolはアプリケーション内の複数の箇所で利用する事が多く、ScalaとJavaのソースコードを両方含むプロジェクトでは、
Scalaで作ったThreadPoolをJava側でも利用することがあります。そういう場合は`ExecutionContextExecutor`もしくは`ExecutionContextExecutorService`として作成してやればスムーズに使いやすくなります。

```scala
trait ExecutionContextExecutor extends ExecutionContext with Executor
trait ExecutionContextExecutorService extends ExecutionContextExecutor with ExecutorService
```