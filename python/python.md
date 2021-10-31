# pythonメモ



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





