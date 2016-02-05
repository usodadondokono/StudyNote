

```python
$ bitcoin-cli -regtest getinfo
{
    "version" : 90500,
    "protocolversion" : 70002,
    "walletversion" : 60000,
    "balance" : 100.00000000,
    "blocks" : 102,
    "timeoffset" : 0,
    "connections" : 0,
    "proxy" : "",
    "difficulty" : 0.00000000,
    "testnet" : false,
    "keypoololdest" : 1453708105,
    "keypoolsize" : 101,
    "unlocked_until" : 0,
    "paytxfee" : 0.00000000,
    "relayfee" : 0.00001000,
    "errors" : ""
}
```


      File "<ipython-input-1-488af1ab583e>", line 1
        $ bitcoin-cli -regtest getinfo
        ^
    SyntaxError: invalid syntax




```python
$ bitcoin-cli  -regtest getnewaddress
myB4gmaNWybsobgAE3MJs2wwUVx5jhcsAN
```


```python
$ bitcoin-cli -regtest getreceivedbyaddress myB4gmaNWybsobgAE3MJs2wwUVx5jhcsAN
0.00000000
```


```python
$ bitcoin-cli -regtest encryptwallet hoge
wallet encrypted; Bitcoin server stopping, restart to run with encrypted wallet.
The keypool has been flushed, you need to make a new backup.
```


```python
$ bitcoin-cli -regtest walletpassphrase hoge 360
```


```python
$ bitcoin-cli -regtest getinfo
{
    "version" : 90500,
    "protocolversion" : 70002,
    "walletversion" : 60000,
    "balance" : 100.00000000,
    "blocks" : 102,
    "timeoffset" : 0,
    "connections" : 0,
    "proxy" : "",
    "difficulty" : 0.00000000,
    "testnet" : false,
    "keypoololdest" : 1453708105,
    "keypoolsize" : 101,
    "unlocked_until" : 1454630334,
    "paytxfee" : 0.00000000,
    "relayfee" : 0.00001000,
    "errors" : ""
}

```


```python
$ more wallet.txt
# Wallet dump created by Bitcoin v0.9.5-beta (2015-05-21 10:48:26 +0200)
# * Created on 2016-02-04T23:56:33Z
# * Best block at time of backup was 102 (0000e3396878fb638dde3cb8242ad33fc6b7e7fe996d1f9fc970ec94f22c41b2),
#   mined on 2016-01-25T06:12:08Z

cNiQ5pH1MCq3DBTBKZLCxqk9NeSn13daDgcXuC1kQavJyq5gXRFA 2016-01-25T05:44:46Z change=1 # addr=mkAXCCnrSCYWcwYGTM9Fjr6NemNH64xt7r
cNtKysCPjvu6HY4CfosbdahjS1nkj74Fr3nFX3rDXxNXbNZYiKwZ 2016-01-25T05:44:46Z change=1 # addr=mzGB5vpcp68qkcdXBmWQFvjvBPDGKvsoSe
cT8pWfeT7r5x2iwzHRhay6KyseXdkGyJYDQCdsj6EvNZz8ZnKByN 2016-01-25T05:44:46Z change=1 # addr=n4pP3YhAw2p9v4nH5nh74XXzMCkvC1uw3o
cMhpWgwXNU9dWpeztLXHx3LQPYHND8Vk3HQCZy8ZAHGLzeWqLnsN 2016-01-25T05:44:46Z label= # addr=mgH9Ne6tsxTSXyswNehydTbzvJdJVqs2mv
cVFYJXsr2WqShPyztQ478oUkQHyWUYNXYsTJuac6FhQ8MLMZpcAJ 2016-01-25T05:44:46Z change=1 # addr=mwHzgu8JnsdmU3jU7xDaLStzkKHR1jg9Cp
cRs6khebsSBq5hvg7K363Ku7ZtjJPnQTPJbj7qfrkFZpPNyPiTU5 2016-01-25T05:44:46Z change=1 # addr=miFLjgtnJMF2vYoZFfvt9FoLcHEG1D9hQM
cVvBKYVhYhnR38WVX7hy915g2utt7WB6Q233JP9Qgoomj5zxRZjn 2016-01-25T05:44:46Z change=1 # addr=mqHoMjLRCx2RQNj7gy8BoFDk9YAp8icNaf
cNYsXAdZ94YMzTteQU85g6YPmA8bQaDxeW5TkFsixLyKDjcfQpKs 2016-01-25T05:44:46Z change=1 # addr=mtUxWAb9jaVjiMLKbGFjkzjgWCSUNkChKL
cQqS9k3u5whvBW341tY3MvWCZwZbnSgim1HuWHZTJEVabZpFaGNZ 2016-01-25T05:44:47Z change=1 # addr=mmXsgxoQ27PssVEwzifoD4LQFEXkvDPzBw
cNuGD7Zp4befTA6Ua9ymnSJjSoy7KCHfiGSFBBmto2XDssRSU14D 2016-01-25T05:44:47Z change=1 # addr=mrwECDQoGJmJmNHsQab9L4frVtxX7JxnA4
cVqoHE6uovUcs3hc7VFL5qsLQKgJYCkUsagz8BjgaKRsWr8rDtvm 2016-01-25T05:44:47Z change=1 # addr=mtoH3rMm3oZHFuDJ2bB4ijVJZCG8pMKuPo
cShmYrioK61nZWUenoU7KH6hue8ibi8VNZLtz621qxzJ4vkg28dV 2016-01-25T05:44:47Z change=1 # addr=mwdUg8tprNNxrTGpxuKNCbrVZ6QDDPVm4M
cVSEuS4Y1zhtFnGXUKwELB8jq3y3CRfVhE5yBitrD9MLbM3L6cxz 2016-01-25T05:44:47Z change=1 # addr=msDFxKECDR7u5suhbQt7Mqy9uQ39GSqoSL
```


```python
$ bitcoin-cli -regtest getaddressesbyaccount ""
[
    "mm3LowreK1dFta9io3oGpQtLJfBrVE7jB8",
    "myB4gmaNWybsobgAE3MJs2wwUVx5jhcsAN",
    "mzV7kFaKr4x2ocKJd24ZuFeiNLtThsh2ft",
    "n2icdqcWckasLFKMRtuSdwu2MXi8RMoW8L",
    "mgH9Ne6tsxTSXyswNehydTbzvJdJVqs2mv"
]
```


```python
$ bitcoin-cli -regtest gettransaction e9f2c73989edf23fbb90afc5e50288c19debfd3ace5f076e8179ff7071e4a61f
{
    "amount" : 0.00000000,
    "fee" : 0.00000000,
    "confirmations" : 1,
    "blockhash" : "0000e3396878fb638dde3cb8242ad33fc6b7e7fe996d1f9fc970ec94f22c41b2",
    "blockindex" : 1,
    "blocktime" : 1453702328,
    "txid" : "e9f2c73989edf23fbb90afc5e50288c19debfd3ace5f076e8179ff7071e4a61f",
    "walletconflicts" : [
    ],
    "time" : 1453702230,
    "timereceived" : 1453702230,
    "details" : [
        {
            "account" : "",
            "address" : "mm3LowreK1dFta9io3oGpQtLJfBrVE7jB8",
            "category" : "send",
            "amount" : -10.00000000,
            "fee" : 0.00000000
        },
        {
            "account" : "",
            "address" : "mm3LowreK1dFta9io3oGpQtLJfBrVE7jB8",
            "category" : "receive",
            "amount" : 10.00000000
        }
    ]
}
```


```python
$ bitcoin-cli -regtest getrawtransaction e9f2c73989edf23fbb90afc5e50288c19debfd3ace5f076e8179ff7071e4a61f
01000000012e67a622128278c1d045d28afe172f3e9d7d7cbe8fc1e34b8a3a8231b1a0bcca000000004847304402203aa364f2ef5cd4579430726559e98174b212fcc99086c553fd4fdd8ff8d0e30502207965dbb38e7d8a2ed18cf159cbc4e952f4a993e8e18f0ccb29da3e1be042e36401ffffffff0200ca9a3b000000001976a9143c97e71596a3f70eb90b95be3686ce807adc915088ac00286bee000000001976a914878e2432c4b94866e95237e8267d0b49c32b83ee88ac00000000
```


```python
$ bitcoin-cli -regtest decoderawtransaction 01000000012e67a622128278c1d045d28afe172f3e9d7d7cbe8fc1e34b8a3a8231b1a0bcca000000004847304402203aa364f2ef5cd4579430726559e98174b212fcc99086c553fd4fdd8ff8d0e30502207965dbb38e7d8a2ed18cf159cbc4e952f4a993e8e18f0ccb29da3e1be042e36401ffffffff0200ca9a3b000000001976a9143c97e71596a3f70eb90b95be3686ce807adc915088ac00286bee000000001976a914878e2432c4b94866e95237e8267d0b49c32b83ee88ac00000000
{
    "txid" : "e9f2c73989edf23fbb90afc5e50288c19debfd3ace5f076e8179ff7071e4a61f",
    "version" : 1,
    "locktime" : 0,
    "vin" : [
        {
            "txid" : "cabca0b131823a8a4be3c18fbe7c7d9d3e2f17fe8ad245d0c178821222a6672e",
            "vout" : 0,
            "scriptSig" : {
                "asm" : "304402203aa364f2ef5cd4579430726559e98174b212fcc99086c553fd4fdd8ff8d0e30502207965dbb38e7d8a2ed18cf159cbc4e952f4a993e8e18f0ccb29da3e1be042e36401",
                "hex" : "47304402203aa364f2ef5cd4579430726559e98174b212fcc99086c553fd4fdd8ff8d0e30502207965dbb38e7d8a2ed18cf159cbc4e952f4a993e8e18f0ccb29da3e1be042e36401"
            },
            "sequence" : 4294967295
        }
    ],
    "vout" : [
        {
            "value" : 10.00000000,
            "n" : 0,
            "scriptPubKey" : {
                "asm" : "OP_DUP OP_HASH160 3c97e71596a3f70eb90b95be3686ce807adc9150 OP_EQUALVERIFY OP_CHECKSIG",
                "hex" : "76a9143c97e71596a3f70eb90b95be3686ce807adc915088ac",
                "reqSigs" : 1,
                "type" : "pubkeyhash",
                "addresses" : [
                    "mm3LowreK1dFta9io3oGpQtLJfBrVE7jB8"
                ]
            }
        },
        {
            "value" : 40.00000000,
            "n" : 1,
            "scriptPubKey" : {
                "asm" : "OP_DUP OP_HASH160 878e2432c4b94866e95237e8267d0b49c32b83ee OP_EQUALVERIFY OP_CHECKSIG",
                "hex" : "76a914878e2432c4b94866e95237e8267d0b49c32b83ee88ac",
                "reqSigs" : 1,
                "type" : "pubkeyhash",
                "addresses" : [
                    "mssho7FyfiUpxZzrDUoQzZuMjK5SqrZ48F"
                ]
            }
        }
    ]
}

```
