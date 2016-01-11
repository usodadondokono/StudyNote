
# Avoid else Blocks After for and while Loops

Pythonループでは他に無い特徴がある...

ループの後にelseブロックを置ける


```python
for i in range(3):
    print('Loop %d' % i)
else:
    print('Else block')
```

    Loop 0
    Loop 1
    Loop 2
    Else block


ループが終わるとすぐにelseブロックが走る。
なぜelseなのかandでよくね？

if/elseステートメントなら、その前のブロックが実行されないときに
elseブロックが実行される。

これはtry/except/elseからのelseは同様なパターンになる。
(Item13)

この前のブロックが失敗しなければここを実行する。
(これはtry/finallyでは直感的)

## ややこしいケース

このことはPython初心者に混乱をもたらす。

実際、たとえばbreak文ではelseブロックまで飛ばす。



```python
for i in range(3):
    print('Loop %d' % i)
    if i == 1:
        break
else:
    # ここはスキップされる
    print('Else block!')
```

    Loop 0
    Loop 1



```python
for x in []:
    print('Never runs')
else:
    # ここは通るよ
    print('While else block!')
```

    While else block!



```python
while False:
    print('Never runs')
else:
    # ここも通るよ
    print('While else block!')
```

    While else block!


### この性質を使いたいケース

この性質はループで何か探索するときに便利な時もある。

例として、2つの数値が「互いに素」か探したいケース。
(全ケースを試して、最後まで来たら何か返したい場合)


```python
a = 4
b = 9
for i in range(2, min(a, b) + 1):
    print('Testing', i)
    if a % i == 0 and b % i == 0:
        print('Not coprime')
        break
else:
    print('Coprime')
```

    ('Testing', 2)
    ('Testing', 3)
    ('Testing', 4)
    Coprime


実際はこのように書きたくないので、代わりにへルパー関数を用意してやるべき。

## ヘルパー関数で代用

* その1

見つけたら早めにreturn、最後までいった場合はデフォルト値をreturn。


```python
def coprime(a, b):
    for i in range(2, min(a, b) + 1):
        if a % i == 0 and b % i == 0:
            return False
    return True
```

* その2

フラグを立てて、見つかればbreak。


```python
def coprime2(a, b):
    is_coprime = True
    for i in range(2, min(a, b) + 1):
        if a % i == 0 and b % i == 0:
            is_coprime = False
            break
    return is_coprime
```

上記のケースの方がコードに慣れ親しんでいないリーダーには分かり良い。

elseブロックは将来的に自分を含めた他の人に不便を生じさせるので、
loopの後のelseは避けよう。

## Things to remember

* Pythonはelseブロックについて特殊な文法を持つ
* loop内でbreak文に遭わなければloopの後にelseブロックが実行される
* loopの後にelseを付けるのは直感的でなく混乱させるので避けよう
