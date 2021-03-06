# MBF Language Interpreter
**THIS PROJECT WAS OPEN SOURCED UNDER MIT LINCESE.**

作者：0cdi2210

 [BrainFuckとは？](https://en.wikipedia.org/wiki/Brainfuck) 

### プラットフォームと紹介

MBF言語は， [BrainFuck](https://en.wikipedia.org/wiki/Brainfuck)言語を基づいた，デバッグFeatureを加えた，Turing 完璧な言語である．

 [BrainFuck](https://en.wikipedia.org/wiki/Brainfuck)言語の文法とてもシンプルですが，Turing 完璧な言語なので，プログラムの複雑さは別にして，C，Java，C++ができることを，BrainFuckで実装できる．

このプログラムは，ISOーC++17で実装された．

Operate System プラットフォーム：C++17が動けるOperate System で動作するはず．

必要なライブラリー：C++ STL(aka, Standard Template Lib, version： c++ std17), 及びC++17標準ライブラリ．

### MBF Language  の文法

| 命令文 | 意味                                                         |
| :----: | :----------------------------------------------------------- |
|  `>`   | データポインタをインクリメントする（右隣のセルを指すようにする）。 |
|  `<`   | データポインタをデクリメントする（左隣のセルを指すようにする）。 |
|  `+`   | データポインタのバイトをインクリメント（1つ増やす）する。    |
|  `-`   | データポインタのバイトをデクリメント（1つ減らす）する。      |
|  `.`   | データポインタのバイトを出力する。                           |
|  `,`   | 1バイトの入力を受け付け、その値をデータポインタのバイトに格納する。 |
|  `[`   | データポインタのバイトが0であれば、命令ポインタを次のコマンドに進めるのではなく、一致する[ ]コマンドの次のコマンドにジャンプさせます。 |
|  `]`   | データポインタのバイトが0でない場合、命令ポインタを次のコマンドに進めるのではなく、一致する[ コマンド] の後のコマンドにジャンプして戻します。 |



その一方、BrainFuckの文法はかなりシンプルなので，プログラム実行中では，「中身はどうなっている？」は分かりづらいので，以下の5つの命令文を実装しました：

| 命令文 | 意味 |
| :----: | :--- |
| `'#'` | 単行コメントする． |
| `';'`  | ランタイムスタックにあるすべてのデータを標準出力に出力する． |
| `':'`  | データポインターの位置を出力する． |
|  `'%'`  | ランタイムスタックの先頭から，データポインターの位置まで，すべてのデータを標準出力に出力する． |
|    `'&'`    | プログラムを一時停止する(=`system(“pause”)`)． |



### プログラムの例

```BrainFuck
>> : +++ -- << :
```

```bash
|  0  |  0  |  0  |  0  |  0  |  0  |  0  |  0  |  0  |  0  | # プログラム開始
   ↑
   data_pointer(=0, value=0)
```

`>>`命令を読み取ったら：

```bash
|  0  |  0  |  0  |  0  |  0  |  0  |  0  |  0  |  0  |  0  |
               ↑
               data_pointer(=2, value=0)
```
`:`命令を読み取ったら：

```bash
|  0  |  0  |  1  |  0  |  0  |  0  |  0  |  0  |  0  |  0  |
               ↑
               data_pointer(=2, value=1)
Output:
2
```

`+++`命令を読み取ったら：

```bash
|  0  |  0  |  3  |  0  |  0  |  0  |  0  |  0  |  0  |  0  |
               ↑
               data_pointer(=2, value=3)
```

`--`命令を読み取ったら：

```bash
|  0  |  0  |  1  |  0  |  0  |  0  |  0  |  0  |  0  |  0  |
               ↑
               data_pointer(=2, value=1)
```

`<<`命令を読み取ったら：

```bash
|  0  |  0  |  1  |  0  |  0  |  0  |  0  |  0  |  0  |  0  |
   ↑
   data_pointer(=0, value=0)
```


`:`命令を読み取ったら：

```bash
|  0  |  0  |  1  |  0  |  0  |  0  |  0  |  0  |  0  |  0  |
   ↑
   data_pointer(=0, value=0)
Output:
0
```

Hello World: 

hello world

```BrainFuck
# test comment
++++++++++
[
    >+++++++>++++++++++>+++>+<<<<-
]
>++.>+.+++++++..+++.>++.<<+++++++++++++++.
>.+++.------.--------.>+.>.
```

### 使う前に

このソフトウェアを使うのに、CMakeのインストールが必要である。

Build手順：
1. gitでこのプロジェクトをcloneする：
```bash
git clone https://github.com/MuxFox/2022-SystemDevelopCourse
```

2. 6-FinalProject ホルダーを開く：
```bash
cd 2022-SystemDevelopCourse
cd 6-FinalProject
```

3. build ホルダーを作る
```bash
mkdir build
```

4. CMakeでbuild
```bash
cd build
cmake ..
```

5. CMakeで作ったMakeFile経由でCompile
```bash
make .
```

ここまでできたら、Executableファイルはbuildホルダーにあるはず、使ってみる：

```bash
BrainFuck -v
```

### 実行オプション

| オプション              | 意味                                                  | 例                         |
| ----------------------- | ----------------------------------------------------- | -------------------------- |
| `-f`                    | ソースコードのパスを指定する．                        | `bf -f hello_wrold.bf`     |
| `-s`                    | ランタイムスタックの大きさを指定する(default = 300)． | `bf -s 1000 -f module.bf ` |
| `-h/-help/--help`       | ヘルプドキュメントをチェック．                        | `bf -h`                    |
| `-v/-version/--version` | インタプリタのバージョンをチェック．                  | `bf -v`                    |
| `--hello_world`         | hello worldプログラムの例をチェック                   | `bf --hello_world`         |

