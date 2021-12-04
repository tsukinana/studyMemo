# pythonメモ

---

## #データの持ち方

### リスト

```python
akutype=["ブラッキー","レパルダス"]
#取り出し:リスト名[iインデックス]
```

### ディレクショナリ

```python
umbreon = {"hp":95,"atk":65,"def":110}
#取り出し:ディレクショナリ[要素のキー]
```

### set(集合)

```python
dyce = {1,2,3,4,5,6}
```

重複して値をもつことができない。インデックスで取り出すこともできない

### タプル

```python
month_names=("January","February")
#取り出し:タプル名[iインデックス]
```

要素の変更はできないが、タプル同士で連結することはできる。

```python
month_names= month_names+("March")
```





## #正規表現

---

## import re subを使う。

subのオプションrはエスケープではなく、バックスラッシュを通常文字扱いする。

後方参照は\1とかを使う。ここに括弧内の文字が記録される。

> raw文字列で指定しないと、文字列のエスケープ文字とみなされるので、`\1` がアスキーコード `0x01` に置換されてしまう。raw文字列にしておくのが無難。



```python
import re
 
text="""\
1234567 東京都千代田区
3334444 東京都港区
9876543 東京都台東区
"""
text_mod = re.sub(r'([0-9]{3})([0-9]{4})', r'\1-\2', text, flags=re.MULTILINE)
print (text_mod)
```

---

## #特殊な変数

```python
__name__
```

* pythonがモジュールとして読まれたとき、モジュール名が格納される。

* 直接実行した場合、

  ```python
  "__main__"という文字列が入る模様。
  ```

```python
__file__
```

* モジュールファイルのパスを文字列として格納する模様。

書いてみた。

```python
#!/use/binenv python
#-*-coding: utf-8-*-

print(__file__)
print(__name__)
```

実施。

```
PS C:\Users\masaya_y\Documents\local\00_Study\python\serverless\application> & python c:/Users/masaya_y/Documents/local/00_Study/python/serverless/application/tes.py
c:/Users/masaya_y/Documents/local/00_Study/python/serverless/application/tes.py
__main__
```



モジュール読み込みの場合(hello.py)

```python
#!/usr/bin/env python
#-*-coding: utf-8-*-

import tes
print("hello")
```

```
PS C:\Users\masaya_y\Documents\local\00_Study\python\serverless\application> & python c:/Users/masaya_y/Documents/local/00_Study/python/serverless/application/hello.py
c:\Users\masaya_y\Documents\local\00_Study\python\serverless\application\tes.py
tes
hello
```



## #logger

### logging

```
from logging import getLogger
```

loggingメソッドは使わない。(ルートにロガーが渡ることになり。名前空間が汚れるから&& 設定の制御が面倒)

### setlevel

```
CRITICAL > ERROR > WARNING > INFO > DEBUG > NOTSET 
```

loggerとhandlerそれぞれに設定できる。

loggerのレベルはhandlerに渡すレベルの設定(デフォルトでNOTSET)

handlerのレベルは出力するログのレベルの設定

### 書いてみた

```
from logging import Formatter, getLogger,StreamHandler,DEBUG
import urllib.request

logger = getLogger(__name__)

#ハンドラに渡すレベル
logger.setLevel(DEBUG)

#伝播無効
logger.propagate = False

#フォーマッター
formatter = Formatter('parent: %(name)s [%(levelname)s] %(message)s')

#ハンドラ生成
handler = StreamHandler()

#出力するレベル
handler.setLevel(DEBUG)

#フォーマット紐づけ
handler.setFormatter(formatter)

#ハンドラ紐づけ
logger.addHandler(handler)
```



## 書いてみたその2

```python
#!/usr/bin/env python
#-*-coding: utf-8-*-

from logging import getLogger,config
import json

if __name__ == "__main__":
    logger = getLogger(__name__)
    with open ("./log_config.json") as f:
        log_conf = json.load(f)
        config.dictConfig(log_conf)
    logger.info("test")
```

設定ファイルで下記を持つ

```json
{
    "version": 1,
    "disable_existing_loggers": false,


    "formatters": {
        "simple": {
            "format": "%(asctime)s %(name)s:%(lineno)s %(funcName)s [%(levelname)s]: %(message)s"
        }
    },

    "handlers": {
        "consoleHandler": {
            "class": "logging.StreamHandler",
            "level": "INFO",
            "formatter": "simple",
            "stream": "ext://sys.stdout"
        },
        "logFileHandler": {
            "class": "logging.FileHandler",
            "level": "INFO",
            "formatter": "simple",
            "filename": "./log.log",
            "mode": "w",
            "encoding": "utf-8"
        }
    },

    "loggers": {
        "__main__": {
            "level": "DEBUG",
            "handlers": ["consoleHandler", "logFileHandler"],
            "propagate": false
        }
    },

    "root": {
        "level": "INFO",
        "handlers": ["consoleHandler"]
    }
}
```











## アンダースコアの謎

### return値を無視する

```
x, _, z = (1, 2, 3)
# x=1, z=3
```

メモリを占有しないで破棄できる。



### 関数名の最初にアンダースコアを1つ

→内部用と定義できる。(privateみたいなもん)





