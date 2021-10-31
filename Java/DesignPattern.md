## デザインパターン



#### UMLの矢印の向き

extendするクラスに対して矢印を向ける。

(サブクラスのみがスーパークラスを知っている。)



#### 抽象クラスやインターフェイスをうまく使おう

メリット:実装とは切り離して作ることができる。

インターフェイスを経由しないでいきなり具体的なクラスで解決してしまうと、クラス間の結合が強くなってしまい、部品として再利用することが難しくなる。

(修正も多岐に及ぶ。)



結合を弱めてクラスを再利用しやすくするために、

抽象クラスやインターフェイスを使ってプログラミングする。


