## JavaScriptメモ

---

## NaN:not a number 非数のこと。

+演算子で文字列に数字を足すと文字列に変換される。
つまり""を足してやると文字列になる。

---

## 基本的なこと

オブジェクトの生成は{}

配列の生成は[]

:はオブジェクトリテラルに使う。

```javascript
//オブジェクトを作る。

var obj = {
name : 'tsukina',
age : 24
}

//ユーザーにアクセスしたいプロパティを入力させる。
var key = prompt('key plese');

//表示
alert(obj[key]);
```



---

