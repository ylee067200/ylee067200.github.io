# Introduction

GNU **objdump** 是一個強大的 object 檔案工具，可以從中顯示你想要的資料；或是反組譯成 Assembly 碼，方便閱讀。

## Usage

nm [-A|-o|--print-file-name] [-a|--debug-syms]
          [-B|--format=bsd] [-C|--demangle[=style]]
          [-D|--dynamic] [-fformat|--format=format]
          [-g|--extern-only] [-h|--help]
          [-l|--line-numbers] [--inlines]
          [-n|-v|--numeric-sort]
          [-P|--portability] [-p|--no-sort]
          [-r|--reverse-sort] [-S|--print-size]
          [-s|--print-armap] [-t radix|--radix=radix]
          [-u|--undefined-only] [-V|--version]
          [-X 32_64] [--defined-only] [--no-demangle]
          [--plugin name]
          [--no-recurse-limit|--recurse-limit]]
          [--size-sort] [--special-syms]
          [--synthetic] [--with-symbol-versions] [--target=bfdname]
          [objfile...]

If no **objfile**, it will assume *a.out* is the one.

Argument | Description
-------- | -----------
-A / -o / --print-file-name | 在輸出的 Offset 會加上檔案名稱
-C / --demangle | 將低階的符號名稱進行解析，轉換成一般
人看得懂的名稱。譬如說 C++ 的函數名稱

## 欄位說明

```
0000000000001373 T main
```

上面是一個標準的 **nm** 輸出，其輸出的欄位為：

1. Offset
2. Symbol Flag；一般來說大寫是 **Global**，小寫是 **Local**。
3. Symbol 名稱

Symbol Flag | 說明
----------- | -----
A / a | 絕對值。即便之後的 Link 也不會改變該 Symbol 的值 (Offset)
B / b | 存在 BSS 區塊的 Symbol。多是未初始化或是初始值為 0 的變數
C | 
D / d | 有設定初始化的變數
G / g | 同上述 D，但是放在對小量資料最佳化的區塊
I | Indirect rederence to another symbol
i | 未定址的函數參考，需要跟其他 library 進行 link 才會解析出位置
N | Debug 用的 symbol
n | 唯讀的讀資料
p | 
R / r | 類似 n，
S / s | 類似 B，但是用於小型物件
T / t | 存放在 Text 區塊 (程式碼) 的 symbol
U | 未定義的 symbol
u | GNU Extension of ELF；在任何執行中的程式，該 Symbol 只會有一個
V / v | 
W / w |
- |
? |
