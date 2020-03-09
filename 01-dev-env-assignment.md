## この課題で身につく能力

PlayGround, REPL, IDEで素早くScalaソースコードを書き実行できる

#### ねらい

ソースコードを書いて動作確認をする際、IDE（統合開発環境）を最も頻繁に使うことになりますが、それだけが使えればいいというわけではありません。
動作確認したいコードの規模など、状況によってPlayGround, REPL, IDEを適切に使い分けると動作確認の効率が向上します。
「3つの方法全てを、面倒と思う暇もなくサクッと実行できるくらい手に馴染んだ状態」を目指して下さい。素早く、数多くのコードを動作確認した経験は、そのまま技術力の向上につながると思って下さい。

## 課題

以下の課題の結果を[01-dev-env-solution.md](./01-dev-env-solution.md)に貼り付けて、Pull Requestを送る形で提出してください

1. オンラインの[Playground](https://scastie.scala-lang.org/)でScalaの`println("Hello World")`を実行し、結果をブラウザのスクリーンショットとして貼り付けてください

2. 自分のローカルPCのコマンドライン/ターミナルからScala REPLから`println("Hello World")`を実行して結果をコピペもしくはスクリーンショットで貼り付けてください
  2.1 Adopt Open JDK 8をインストールしてください
  2.2 Scalaをインストールしてください
  2.3 scalaコマンドでREPLを立ち上げて下さい

2. sbt newで最小限のScalaアプリケーションのディレクトリ構造を作って、IntelliJ IDEAからmain関数の中身を`println("Hello World")`に書き換え、sbtから実行して下さい。
