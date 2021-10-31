# オブジェクト指向でなぜつくるのか　要約

従来の構造型プログラミングでは、

グローバル変数と貧弱な再利用に課題があった。

それを補ったのがOOP



## #クラス

関連性の強いサブルーチンとグローバル変数を1つにまとめて粒度の大きいソフトウェアを作る仕組み。

---

## #ポリモーフィズム

---

多様性、メソッドを呼び出す側(メインルーチン)を共通化させる。

→メソッドが増えても呼び出す側を修正する必要ない

---

## #継承

重複するクラス定義を共通化する。

→クラスの共通部分を別クラスにまとめて無駄を省く

つまり、ロジックの共通化できる。

---

## プログラムのメモリ

静的領域、ヒープ領域、スタック領域の3つに分けて管理する。

### 静的領域

プログラム開始時に確保され、終了まで配置が固定される領域。

グローバル変数やコード情報(プログラムの命令を実行可能な形式に変換したもの)が格納される。

JAVAに限ってはメソッドエリアとも呼ぶ

### ヒープ領域

プログラムの実行時に動的に確保するためのメモリ領域。

アプリケーションから必要なサイズを要求することで割り当てる。

不要になればもとに戻す。(OSや仮想マシンが管理機能を提供)

### スタック領域

スレッド制御のメモリ領域

各スレッドに1つずつ用意される。スレッドはサブルーチンを次々呼び出すことで動作する。

スタック領域はサブルーチン呼び出しの制御のために使われるメモリ領域。サブルーチンの引数やローカル変数、戻り先などの情報を格納します。もちろんスタック方式での出し入れ

ーーー

JAVAはクラス情報のロードを静的領域で逐次実施し、インスタンスをヒープ領域に充てる。

インスタンスを格納する変数の中身はヒープ領域を指すポインタである。