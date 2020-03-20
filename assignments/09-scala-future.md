## この課題で身につく能力

Futureを使った非同期処理を含むソースコードが読め、スレッドの動きを図に起こして説明できる

## 課題

以下の課題の結果をこのファイルに貼り付けて、Pull Requestを送る形で提出してください

1. Oracle Java Tutorialsの[Defining and Starting a Thread](https://docs.oracle.com/javase/tutorial/essential/concurrency/runthread.html)のコード例を、IDEからScalaで実装して実行結果を貼り付けて下さい。

2. Oracle Java Tutorialsの[Pausing Execution with Sleep](https://docs.oracle.com/javase/tutorial/essential/concurrency/sleep.html)のコード例を、IDEからScalaで実装して実行結果を貼り付けて下さい。

3. Oracle Java Tutorialsの[Interrupts](https://docs.oracle.com/javase/tutorial/essential/concurrency/interrupt.html)のコード例を、IDEからScalaで実装して実行結果を貼り付けて下さい。

4. Oracle Java Tutorialsの[The Simple Threads Example](https://docs.oracle.com/javase/tutorial/essential/concurrency/simple.html)のコード例を、IDEからScalaで実装して実行結果を貼り付けて下さい。

5. 口頭試問: Oracle Java Tutorialsの[Thread Intereference](https://docs.oracle.com/javase/tutorial/essential/concurrency/interfere.html)について図を描いて説明して下さい。コード例は実行しません、なぜなら現代のCPUは速すぎてThread Interferenceを再現するのは難しいからです。

6. 口頭試問: Oracle Java Tutorialsの[Memory Consistency Errors](https://docs.oracle.com/javase/tutorial/essential/concurrency/memconsist.html)について図を描いて説明して下さい。コード例を実行しないのは、現代のCPUは速すぎてMemory Consistency Errorsを再現するのは難しいからです。


7. 「実践Scala入門」第5章「5-2 Futureの基本的な使い方」から以下に挙げたコードを全部実行して結果を貼り付けて下さい
  - HttpTextClient (p.162)
  - responseFuture (p.164)
  - failedFuture (p.165)

8. 「実践Scala入門」第5章 p.170 -> p.172「for式 非同期処理を柔軟に合成する」のコードを全部実行して結果を貼り付けて下さい

9. Oracle Java Tutorialsの[Executor Interfaces](https://docs.oracle.com/javase/tutorial/essential/concurrency/simple.html)のコード例`e.execute(r)`を、IDEからScalaで実装して実行結果を貼り付けて下さい。

10. 口頭試問: ExecutionContext, Executor, ExecutorService, ExecutionContextExecutor, ThreadPoolExecutor, ForkJoinPoolExecutorについてextends/implementsの関係を図に書いて、Java時代からあるものとScala用のものを分類しつつ、なぜこんなに沢山のtrait, interface, classが必要なのか、どう使い分けられているのか説明して下さい。わからなかったらすぐに聞いた上でまとめ直すとよいでしょう。
  - 参考情報10.1 ExecutorとExecutorServiceはJava時代からあります
  - 参考情報10.2 ThreadPoolExecutorは完全な実装を持つクラスであり、ExecutorとExecutorServiceはinterfaceです
  - 参考情報10.3 ForkJoinPoolExecutorはJava時代からありますが、ThreadPoolExecutorより何年か遅れて登場しました。どういう用途で用いられるでしょう？
  - 参考情報10.4 ExecutionContextはScalaのためのものです。Scala Futureのメソッドの中でimplicit parameterとして使われます
  - 参考情報10.5 ExecutionContextExecutorというJavaとScalaをごっちゃにしたようなネーミングのtraitは、まさにScalaプロジェクトの中でJavaのコードを使うときのためにあるものです