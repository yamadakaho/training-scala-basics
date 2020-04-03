## この課題で身につく能力

PlayGround, REPL, IDEで素早くScalaソースコードを書き実行できる

## 課題

以下の課題の結果をこのファイルに貼り付けて、Pull Requestを送る形で提出してください

1. オンラインの[Playground](https://scastie.scala-lang.org/)でScalaの`println("Hello World")`を実行し、結果をブラウザのスクリーンショットとして貼り付けてください

<img width="1081" alt="スクリーンショット 2020-04-03 12 25 08" src="https://user-images.githubusercontent.com/62977633/78321181-3efcd780-75a6-11ea-9b2e-637406368d9b.png">

2. 自分のローカルPCのターミナル/コンソールからScala REPLから`println("Hello World")`を実行して結果を文字コピペもしくはスクリーンショットで貼り付けてください
 - 2.1 Adopt Open JDK 8をインストールしてください
 - 2.2 Scalaをインストールしてください
 - 2.3 scalaコマンドでREPLを立ち上げて下さい

scala> println("Hello World")
Hello World

３. sbt newで最小限のScalaアプリケーションのディレクトリ構造を作って、IntelliJ IDEAからmain関数の中身を`println("Hello World")`に書き換え、sbtから実行して下さい。
 - 3.1 sbtをインストールして下さい
 - 3.2 IntelliJ IDEAをインストールして下さい
 
 sbt:hello-world> run
 [info] Updating 
 https://repo1.maven.org/maven2/org/typelevel/cats-core_2.13/2.0.0/cats-core_2.1…
   100.0% [##########] 4.5 KiB (10.6 KiB / s)
 https://repo1.maven.org/maven2/org/scala-lang/scala-library/2.13.1/scala-librar…
   100.0% [##########] 1.6 KiB (3.4 KiB / s)
 https://repo1.maven.org/maven2/org/typelevel/cats-macros_2.13/2.0.0/cats-macros…
   100.0% [##########] 3.9 KiB (27.4 KiB / s)
 [info] Resolved  dependencies
 [info] Updating 
 https://repo1.maven.org/maven2/org/scala-lang/scala-compiler/2.13.1/scala-compi…
   100.0% [##########] 2.2 KiB (13.8 KiB / s)
 https://repo1.maven.org/maven2/org/scala-lang/scala-reflect/2.13.1/scala-reflec…
   100.0% [##########] 1.8 KiB (12.0 KiB / s)
 [info] Resolved  dependencies
 [info] Fetching artifacts of 
 https://repo1.maven.org/maven2/org/typelevel/cats-macros_2.13/2.0.0/cats-macros…
   100.0% [##########] 305 B (2.2 KiB / s)
 https://repo1.maven.org/maven2/org/typelevel/cats-kernel_2.13/2.0.0/cats-kernel…
   100.0% [##########] 3.3 MiB (1.1 MiB / s)
 https://repo1.maven.org/maven2/org/scala-lang/scala-reflect/2.13.1/scala-reflec…
   100.0% [##########] 3.4 MiB (777.1 KiB / s)
 https://repo1.maven.org/maven2/org/typelevel/cats-core_2.13/2.0.0/cats-core_2.1…
   100.0% [##########] 4.5 MiB (764.1 KiB / s)
 https://repo1.maven.org/maven2/org/scala-lang/scala-library/2.13.1/scala-librar…
   100.0% [##########] 5.5 MiB (429.2 KiB / s)
 https://repo1.maven.org/maven2/org/scala-lang/scala-compiler/2.13.1/scala-compi…
   100.0% [##########] 10.2 MiB (601.6 KiB / s)
 [info] Fetched artifacts of 
 [info] Compiling 1 Scala source to /Users/kaho.yamada/hello-world-template/target/scala-2.13/classes ...
 https://repo1.maven.org/maven2/org/scala-sbt/compiler-bridge_2.13/1.3.0/compile…
   100.0% [##########] 3.0 KiB (22.5 KiB / s)
 [info] Non-compiled module 'compiler-bridge_2.13' for Scala 2.13.1. Compiling...
 8 warnings found
 [info]   Compilation completed in 11.918s.
 [info] running Main 
 Hello World
 [success] Total time: 32 s, completed 2020/04/03 10:28:38

 
