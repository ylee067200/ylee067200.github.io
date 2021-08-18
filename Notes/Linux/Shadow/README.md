在 Linux 環境中，帳號的密碼是存放在 /etc/shadow 檔案。每一個帳號的格式是這樣：

root:$6$6x.0NmGjJud3jmeW$mqBwTdkAoA0uXsqfZX9N3u6NTV9rdCyrsXu9AFLw0R0/UQems0HeHMGAebm3nmaS.lac1QJwsqMWFuzO8YorC/:18753:0:99999:7:::

每筆記錄有九個欄位，每個欄位用 ":" 作為分隔符號：

1. 帳號
2. 加密後的密碼
3. 上次密碼變更日期
4. 密碼最短使用期限
5. 密碼最長使用期限
6. 密碼過期警告期間
7. 密碼暫停使用期間
8. 帳號過期日
9. 保留

# 加密密碼

## 密碼格式

我們先看看密碼的格式：

```
$6$6x.0NmGjJud3jmeW$mqBwTdkAoA0uXsqfZX9N3u6NTV9rdCyrsXu9AFLw0R0/UQems0HeHMGAebm3nmaS.lac1QJwsqMWFuzO8YorC/
```

這一串加密後的密碼，有 3 個 "$" 號。這個 "$" 就是用來分隔密碼資料用的。前兩項的說明如下，第三項即為加密後的密碼。

### 演算法

第一個 "$" 後面的數字，是表示加密的演算法。目前有以下兩種：
1. SHA512 (6) 
2. SHA256 (5)

### SALT

SALT 算是 DES 的 IV，用來避免不同使用者使用相同密碼導致加密後的密碼相同問題。多是使用亂數


## 使用 OpenSSL 建立加密密碼

```
gigo@DESKTOP-U6KVGB9:/etc$ openssl passwd --help
Usage: passwd [options]
Valid options are:
 -help               Display this summary
 -in infile          Read passwords from file
 -noverify           Never verify when reading password from terminal
 -quiet              No warnings
 -table              Format output as table
 -reverse            Switch table columns
 -salt val           Use provided salt
 -stdin              Read passwords from stdin
 -6                  SHA512-based password algorithm
 -5                  SHA256-based password algorithm
 -apr1               MD5-based password algorithm, Apache variant
 -1                  MD5-based password algorithm
 -aixmd5             AIX MD5-based password algorithm
 -crypt              Standard Unix password algorithm (default)
 -rand val           Load the file(s) into the random number generator
 -writerand outfile  Write random data to the specified file
```

假設我們要使用 SHA-512 演算法，且 Salt 為 1qaz@WsX 加密我們的密碼 PASSword：

```
gigo@DESKTOP-U6KVGB9:/etc$ openssl passwd -6 -salt 1qaz@WsX PASSword
$6$1qaz@WsX$eieY1HvkkT5YEOxHhaW1YMGuv3tC0QOIYstA8geMsme07DjskbhjRxqvcgUuhdkCpj86teLgEgfEXLZayiyxU.
gigo@DESKTOP-U6KVGB9:/etc$
```

