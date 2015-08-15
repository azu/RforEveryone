---
title: "6章 R へのデータ取り込み"
author: "azu"
date: "2015年8月15日"
output: html_document
---

## 6.1: CSVの読み込み


```r
theUrl <- "http://www.jaredlander.com/data/Tomato%20First.csv"
tomato <- read.table(file = theUrl, header =  TRUE, sep = ",")
```

headで内容を見られる


```r
head(tomato)
```

```
##   Round             Tomato Price      Source Sweet Acid Color Texture
## 1     1         Simpson SM  3.99 Whole Foods   2.8  2.8   3.7     3.4
## 2     1  Tuttorosso (blue)  2.99     Pioneer   3.3  2.8   3.4     3.0
## 3     1 Tuttorosso (green)  0.99     Pioneer   2.8  2.6   3.3     2.8
## 4     1     La Fede SM DOP  3.99   Shop Rite   2.6  2.8   3.0     2.3
## 5     2       Cento SM DOP  5.49  D Agostino   3.3  3.1   2.9     2.8
## 6     2      Cento Organic  4.99  D Agostino   3.2  2.9   2.9     3.1
##   Overall Avg.of.Totals Total.of.Avg
## 1     3.4          16.1         16.1
## 2     2.9          15.3         15.3
## 3     2.9          14.3         14.3
## 4     2.8          13.4         13.4
## 5     3.1          14.4         15.2
## 6     2.9          15.5         15.1
```

`stringsAsFactors`というオプションで、FALSEとすればfactorではなくなるので、
重複したものも扱えて便利

`read.csv2`はヨーロッパで一般的である小数点がコンマで区切り文字がセミ コロンの CSV ファイルを読み込むための関数です

## 6.2: Excelの読み込み

Excelは今のところまともな方法がない。
XML経由で行ける?でもパッケージがない

## 6.3 : データベースからの読み込み

ODBC接続

## 6.4 : 他社統計ツールからの読み込み

一般的に使われてる統計ツールからデータ読み込む関数

SPSS Stata SAS Octave Minitab Systat

それぞれに対応するものが`read.*`に存在してる。

## 6.5 : R バイナリファイル

RDataファイルという任意のRオブジェクトを表現するためのバイナリファイルがある。
OS間関係なく渡せる。


```r
save(tomato, file ="data/tomato.rdata")
# 自動でディレクトリは作れてないため事前に`data/`は必要
rm(tomato)
load("data/tomato.rdata");
head(tomato)
```

```
##   Round             Tomato Price      Source Sweet Acid Color Texture
## 1     1         Simpson SM  3.99 Whole Foods   2.8  2.8   3.7     3.4
## 2     1  Tuttorosso (blue)  2.99     Pioneer   3.3  2.8   3.4     3.0
## 3     1 Tuttorosso (green)  0.99     Pioneer   2.8  2.6   3.3     2.8
## 4     1     La Fede SM DOP  3.99   Shop Rite   2.6  2.8   3.0     2.3
## 5     2       Cento SM DOP  5.49  D Agostino   3.3  3.1   2.9     2.8
## 6     2      Cento Organic  4.99  D Agostino   3.2  2.9   2.9     3.1
##   Overall Avg.of.Totals Total.of.Avg
## 1     3.4          16.1         16.1
## 2     2.9          15.3         15.3
## 3     2.9          14.3         14.3
## 4     2.8          13.4         13.4
## 5     3.1          14.4         15.2
## 6     2.9          15.5         15.1
```

## 6 . 6 : R に 入 って い る デ ー タ

> 例えば、ggplot2 パッケージには diamonds というデータセッ トが同梱されています。このデータは、data 関数によって読み込むことができます。

パッケージにデータセットが入ってる場合がある。


```r
require(ggplot2)
```

```
##  要求されたパッケージ ggplot2 をロード中です
```

```r
data(diamonds)
head(diamonds)
```

```
##   carat       cut color clarity depth table price    x    y    z
## 1  0.23     Ideal     E     SI2  61.5    55   326 3.95 3.98 2.43
## 2  0.21   Premium     E     SI1  59.8    61   326 3.89 3.84 2.31
## 3  0.23      Good     E     VS1  56.9    65   327 4.05 4.07 2.31
## 4  0.29   Premium     I     VS2  62.4    58   334 4.20 4.23 2.63
## 5  0.31      Good     J     SI2  63.3    58   335 4.34 4.35 2.75
## 6  0.24 Very Good     J    VVS2  62.8    57   336 3.94 3.96 2.48
```

## 6.7 : Web サイトからの抽出

XMLパッケージの`readHTMLTable`を使ってHTMLテーブルからデータを取り出す事が出来る


```r
require(XML)
```

```
##  要求されたパッケージ XML をロード中です
```

```r
theUrl <- "http://www.jaredlander.com/2012/02/another-kind-of-super-bowl-pool/"
bowlPool <- readHTMLTable(theUrl, which = 1, header = FALSE, stringAsFactors = FALSE)
bowlPool
```

```
##                V1      V2        V3
## 1   Participant 1 Giant A Patriot Q
## 2   Participant 2 Giant B Patriot R
## 3   Participant 3 Giant C Patriot S
## 4   Participant 4 Giant D Patriot T
## 5   Participant 5 Giant E Patriot U
## 6   Participant 6 Giant F Patriot V
## 7   Participant 7 Giant G Patriot W
## 8   Participant 8 Giant H Patriot X
## 9   Participant 9 Giant I Patriot Y
## 10 Participant 10 Giant J Patriot Z
```



