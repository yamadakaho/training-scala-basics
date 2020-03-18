## この課題で身につく能力

PlayGround, REPL, IDEで素早くScalaソースコードを書き実行できる

#### ねらい

ある程度の規模のソースコードを継続開発・保守していく際、IDE（統合開発環境）を最も頻繁に使うことになりますが、それだけが使えればいいというわけではありません。
ソースコードの動作確認をしたいとき、状況によってPlayGround, REPL, IDEを適切に使い分けると動作確認の効率が向上します。
「3つの方法全てを、面倒と思う暇もなくサクッと実行できるくらい手に馴染んだ状態」を目指して下さい。

**数多くのコードを動作確認した経験は、そのまま技術力の向上につながると思って下さい。**

## 課題

以下の課題の結果をこのファイルに貼り付けて、Pull Requestを送る形で提出してください

---
1. オンラインの[Playground](https://scastie.scala-lang.org/)でScalaの`println("Hello World")`を実行し、結果をブラウザのスクリーンショットとして貼り付けてください

解答)
最近は多くのプログラミング言語はオンライン上の実行環境でブラウザから手軽にコードスニペットを実行でき、そのような実行環境を一般にPlaygroundと呼びます。
Go言語やJava、CやJavaScriptなど様々な言語でそれぞれ別のPlaygroundがあり、Scalaの場合は https://scastie.scala-lang.org/ が公式のPlaygroundです。

![image](https://user-images.githubusercontent.com/7414320/76193460-6373c700-6227-11ea-8f6d-0a3cc8997b46.png)

---
2. 自分のローカルPCのターミナル/コンソールからScala REPLから`println("Hello World")`を実行して結果を文字コピペもしくはスクリーンショットで貼り付けてください
  - 2.1 Adopt Open JDK 8をインストールしてください
  - 2.2 Scalaをインストールしてください
  - 2.3 scalaコマンドでREPLを立ち上げて下さい
 
解答)
[Scala公式](https://www.scala-lang.org/download/)にも書いてあるのですが、Scalaをインストールするには先にJDKをインストールしておく必要があります。
ところが2020年現在、これが少し厄介な状況になっていて、少し古いバージョンである**JDK 8**でないといけません。
[ScalaのコンパイラがJDK 8を前提としている](https://docs.scala-lang.org/overviews/jdk-compatibility/overview.html)ためで、JDK 9以降でScalaコンパイラを実行するとごくまれにエラーが起きる場合があります。(ほとんどの場合は問題なく動くらしい)。

> We recommend using Java 8 for compiling Scala code. Since the JVM is backward compatible, it is usually safe to use a newer JVM to run your code compiled by the Scala compiler for older JVM versions

そしてJavaのサポートモデルが変わったためにOpen JDK本家のサポートは切れてしまっており、Adopt Open JDKなど他のベンダから配布されているJDK 8を入手する必要があります。そこで2.1の手順は以下のようになります。

```
# java がインストールされていないことを確認、ここでエラーが出るはず
# javaがすでにインストールされていたら、アンインストールするか、もしくは後述のjenvで複数バージョンのJDKを管理する
> java -version

## brew自体のインストール https://brew.sh/
> /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

## AdoptOpenJDKをbrewのレポジトリ(インストール元)に追加
> brew tap AdoptOpenJDK/openjdk

> brew cask install adoptopenjdk8
> java -version
openjdk version "1.8.0_242"
OpenJDK Runtime Environment (AdoptOpenJDK)(build 1.8.0_242-b08)
OpenJDK 64-Bit Server VM (AdoptOpenJDK)(build 25.242-b08, mixed mode)
```

Javaがすでにインストールされていて、そのJavaはそのまま残して起きたいならjenvを使って複数のJavaバージョンを切り替えるとよいでしょう。詳細な使い方はここでは說明しませんが、公式ページを皆が裂蹄すれば動きます。

2.2, 2.3 は

```
# Scalaのインストールは単純にこれだけ
brew install scala

# scalaコマンドでREPLに入る。出力にJava 1.8のようなバージョンを表す文字が現れることを確認
> scala
Welcome to Scala 2.13.1 (OpenJDK 64-Bit Server VM, Java 1.8.0_242).
Type in expressions for evaluation. Or try :help.

# REPLに入ったらHello Wolrd実行
scala> println("Hello World")
Hello World
```

---
3. sbt newで最小限のScalaアプリケーションのディレクトリ構造を作って、IntelliJ IDEAからmain関数の中身を`println("Hello World")`に書き換え、sbtから実行して下さい。
 - 3.1 sbtをインストールして下さい
 - 3.2 IntelliJ IDEAをインストールして下さい
 
 ```
 # 3.1 sbtをインストールして下さい
 brew install sbt
 ```
 
3.2 IntelliJ IDEAはこちらからダウンロード。無料版で大丈夫です。 https://www.jetbrains.com/idea/

```
> sbt new sbt/scala-seed.g8
[info] Loading settings for project global-plugins from plugins.sbt ...
[info] Loading global plugins from /Users/yu.nishiyama/.sbt/1.0/plugins
[info] Loading project definition from /Users/yu.nishiyama/project
[info] Set current project to yu-nishiyama (in build file:/Users/yu.nishiyama/)
[info] Set current project to yu-nishiyama (in build file:/Users/yu.nishiyama/)

A minimal Scala project. 

# ここで入力を要求されます
> name [Scala Seed Project]: hello-scala-world

Template applied in /Users/yu.nishiyama/./hello-scala-world

# 作成されたプロジェクトのディレクトリに移動します
> cd hello-scala-world 

# プロジェクトディレクトリ内でsbtを立ち上げて下さい
> sbt
```

IntelliJ IDEAで同プロジェクトを開いたら、Mainクラスを以下のように書き換えて下さい。Mainクラスの書き方、mainメソッドのシグネチャ（引数の型`args: Array[String]`と戻り値の型`Unit`）は覚えておくといいと思います。

```scala
object Main {
  def main(args: Array[String]): Unit = {
    println("Hello World")
  }
}
```

先程のsbtのシェルから`run`を実行します

```
sbt:hello-scala-world> run
[info] Done compiling.
[info] Packaging /Users/＊＊＊＊＊/hello-scala-world/target/scala-2.12/hello-scala-world_2.12-0.1.0-SNAPSHOT.jar ...
[info] Done packaging.
[info] Running example.Main 
Hello World
[success] Total time: 7 s, completed 2020/03/09 17:41:12
```
 
