
# Take advantage of each block in try/except/else/finally

Pythonでの例外ハンドリングにおける実施したい動作は4つに大別できる。

それらはtry, except, else, finallyブロックで実施できる

これらはそれぞれ固有の使いかたがあり、異なる複数の使い方が役立つ(Item51)

## finally blocks

try/finallyの組み合わせは例外を投げたい時に使えるが、
例外が起きた時の後処理コードを走らせたい時にも使える。

よくあるのは、ファイルハンドラをきちんと閉じたい時。(Item43も参照)


```python
handle = open('/tmp/random_data.txt')  # raise IOError
try:
    data = handle.read()  # raise UnicodeDecodeError
finally:
    # tryの後に必ず実行される
    handle.close() 
```


    ---------------------------------------------------------------------------

    FileNotFoundError                         Traceback (most recent call last)

    <ipython-input-27-0fc13b35a457> in <module>()
    ----> 1 handle = open('/tmp/random_data.txt')  # raise IOError
          2 try:
          3     data = handle.read()  # raise UnicodeDecodeError
          4 finally:
          5     # tryの後に必ず実行される


    FileNotFoundError: [Errno 2] No such file or directory: '/tmp/random_data.txt'



```python
try:
    handle = open('/tmp/random_data.txt')  # raise IOError
    data = handle.read()  # raise UnicodeDecodeError
finally:
    # tryの後に必ず実行される
    handle.close() # ここでも例外
```


    ---------------------------------------------------------------------------

    FileNotFoundError                         Traceback (most recent call last)

    <ipython-input-28-ffc126402bd8> in <module>()
          1 try:
    ----> 2     handle = open('/tmp/random_data.txt')  # raise IOError
          3     data = handle.read()  # raise UnicodeDecodeError


    FileNotFoundError: [Errno 2] No such file or directory: '/tmp/random_data.txt'

    
    During handling of the above exception, another exception occurred:


    NameError                                 Traceback (most recent call last)

    <ipython-input-28-ffc126402bd8> in <module>()
          4 finally:
          5     # tryの後に必ず実行される
    ----> 6     handle.close() # ここでも例外
    

    NameError: name 'handle' is not defined


readを使うとなんらかの例外が起こるが、
finallyブロックでhandleのcloseメソッドが保証される。

tryブロックの前にopenを呼ばないといけない
(openの時に発生する例外ではfinallyブロックは呼ばれて欲しくない)

## else blocks

try/except/elseの組み合わせは例外捕捉を分かりやすくする。

tryで例外が出ない時、elseブロックが実行される。
elseブロックはtryブロックのコード量を減らし、可読性を向上させる。

例えば、JSONのDictionaryデータを読み込み含まれるkeyを返したい時。


```python
import json 
def load_json_key(data, key):
    try:
        result_dict = json.loads(data)
    except ValueError as e:
        raise KeyError from e # 例外時にKeyErrorとして例外発出
    else:
        return result_dict[key]
```


```python
# JSON decode successful
assert load_json_key('{"foo": "bar"}', 'foo') == 'bar'
try:
    load_json_key('{"foo": "bar"}', 'does not exist') # 例外KeyErrorが発生
    assert False
except KeyError:
    pass  # Expected
```


```python
assert load_json_key('{"foo": "bar"}', 'foo') == 'bar'
load_json_key('{"foo": "bar"}', 'does not exist') # 例外KeyErrorが発生
```


    ---------------------------------------------------------------------------

    KeyError                                  Traceback (most recent call last)

    <ipython-input-31-10c1fde47b52> in <module>()
          1 assert load_json_key('{"foo": "bar"}', 'foo') == 'bar'
    ----> 2 load_json_key('{"foo": "bar"}', 'does not exist') # 例外KeyErrorが発生
    

    <ipython-input-29-ad60e2fa66b7> in load_json_key(data, key)
          6         raise KeyError from e # 例外時にKeyErrorとして例外発出
          7     else:
    ----> 8         return result_dict[key]
    

    KeyError: 'does not exist'



```python
# JSON decode fails
try:
    load_json_key('{"foo": bad payload', 'foo') # def内にてKeyErrorが無理やり発出
    assert False
except KeyError:
    pass  # Expected
```


```python
load_json_key('{"foo": bad payload', 'foo') # def内にてKeyErrorが無理やり発出
```


    ---------------------------------------------------------------------------

    JSONDecodeError                           Traceback (most recent call last)

    <ipython-input-29-ad60e2fa66b7> in load_json_key(data, key)
          3     try:
    ----> 4         result_dict = json.loads(data)
          5     except ValueError as e:


    /Users/kohno/.pyenv/versions/3.5.1/lib/python3.5/json/__init__.py in loads(s, encoding, cls, object_hook, parse_float, parse_int, parse_constant, object_pairs_hook, **kw)
        318             parse_constant is None and object_pairs_hook is None and not kw):
    --> 319         return _default_decoder.decode(s)
        320     if cls is None:


    /Users/kohno/.pyenv/versions/3.5.1/lib/python3.5/json/decoder.py in decode(self, s, _w)
        338         """
    --> 339         obj, end = self.raw_decode(s, idx=_w(s, 0).end())
        340         end = _w(s, end).end()


    /Users/kohno/.pyenv/versions/3.5.1/lib/python3.5/json/decoder.py in raw_decode(self, s, idx)
        356         except StopIteration as err:
    --> 357             raise JSONDecodeError("Expecting value", s, err.value) from None
        358         return obj, end


    JSONDecodeError: Expecting value: line 1 column 9 (char 8)

    
    The above exception was the direct cause of the following exception:


    KeyError                                  Traceback (most recent call last)

    <ipython-input-33-1421b829e327> in <module>()
    ----> 1 load_json_key('{"foo": bad payload', 'foo') # def内にてKeyErrorが無理やり発出
    

    <ipython-input-29-ad60e2fa66b7> in load_json_key(data, key)
          4         result_dict = json.loads(data)
          5     except ValueError as e:
    ----> 6         raise KeyError from e # 例外時にKeyErrorとして例外発出
          7     else:
          8         return result_dict[key]


    KeyError: 


適切なJSONデータでない時、json.dataのデコードはValueErrorの例外を投げる。
例外はexceptブロックで捕捉されハンドルされる。

デコードが成功した場合、elseブロックのkey探索が実施される。
その際に例外が発生した場合、tryブロックの外のため、callerに伝わる。

elseはtry/exceptの後に続くことが見た目的に見分けることができ、
例外時の流れがわかりやすくなる。

### おまけ

exceptの後は何か書く必要がある(passなど)


```python
try:
    result_dict = json.loads(data)
except:
    # nothing
```


      File "<ipython-input-34-a11ac08163fb>", line 4
        # nothing
                 ^
    SyntaxError: unexpected EOF while parsing




```python
try:
    result_dict = json.loads(data)
except:
    pass
```

## 全部入り

try/except/else/finallyの組み合わせを一度に全部使う。

例として、ファイルから読み込み、それを実行し、ファイルを上書きするケース。

* tryブロックはファイルの読み込みと実行時に使われる。
* exceptブロックはtryブロックからの例外ハンドルに使用される。
* elseブロックはファイルの上書きと関連する例外を出すために使われる。
* finallyブロックはファイルハンドラの後処理をする。


```python
UNDEFINED = object()

def divide_json(path):
    handle = open(path, 'r+')  # raise IOError
    try:
        data = handle.read()   # raise UnicodeDecodeError
        op = json.loads(data)  # raise ValueError
        value = (
            op['numerator'] /
            op['denominator']) # raise ZeroDivisionError
    except ZeroDivisionError as e:
        return UNDEFINED
    else:
        op['result'] = value
        result = json.dumps(op)
        handle.seek(0)
        handle.write(result)  # raise IOError
        return value
    finally:
        # 常に実行される
        handle.close()
```

このレイアウトは全てのブロックが直感的に動作するので便利。

例えば、ファイルの上書き時に、elseブロックで例外が発生した場合でも、
きちんとfinallyブロックでファイルハンドラが閉じられる。

## Things to remember

* 例外が出るかにかかわらず、try/finally文ではコードを綺麗にしよう
* elseブロックはtryブロックのコード量を最小化するのに役立ち、見た目にも区分けできる
* elseブロックは成功したtryブロック後やfinallyブロックのクリーンアップ前の追加動作に使われる
