## SQLite



## #データの型

null 

integer

REAL	浮動小数点数

TEXT　テキスト

BLOB　Binary Large OBject　入力データをそのまま格納

テーブル定義時に絡むごとにデータ型を指定することが必須ではない、その場合、様々な型が格納されることになる。



## #dict型で返す

row_factory = sqlite3.Rowを入れるとdict型でレコードを返すようになる。

```python
def get_dbcur():
    temp_conn = sqlite3.connect(dbname)
    temp_conn.row_factory = sqlite3.Row
    return temp_conn.cursor()
```



