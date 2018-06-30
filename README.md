# npiii for macOS Dictionary

本辞書は[北極三號辭書npiii](https://sites.google.com/site/tidas1974/npiii)をmacOSの辞書.appで読込可能にしたものです。

本辞書を導入すると、北極三號を辞書.appから検索出来る様になります。

## インストール

1. [Releases](https://github.com/akirakubo/releases)から入手したファイルを展開し、`np108_gg_mac.dictionary`を`~/Library/Dictionaries`に置く。
2. 辞書.appを起動し、辞書メニュー→環境設定...を選択。「npiii (マイルド字音版)」のチェックボックスをオンにする。

## アンインストール

1. 辞書.appを終了する。
2. `~/Library/Dictionaries`から`np108_gg_mac.dictionary`を削除する。

## 使用方法

辞書.appや辞書サービスに対応したアプリケーションから使用します。前者の場合は、導入した辞書を指定するか、「すべて」を指定して検索します。

読み、単語どちらからでも検索出来ます。但し、元辞書ほぼそのままのため、入力方法に若干の癖があります(後述)。

品詞情報は元辞書のものをそのまま出力します。動詞なのに名詞と表示される等、品詞の情報は必ずしも正確ではありませんので注意して下さい(元辞書は現代仮名遣用のIMEで歴史的仮名遣入力を実現する為に作成されたものであり、未対応である品詞には「名詞」を指定する必要があった、等の事情によるものです)。

現代仮名遣と歴史的仮名遣が一致する場合等、元辞書の時点で収録外の語もあります。必要に応じ、macOS標準添付の「スーパー大辞林」等と併用して下さい。

### 読みから調べる

歴史的仮名遣かつ平仮名大文字で入力します。

![例: あをあをした](https://github.com/akirakubo/npiii-macdict/raw/master/docs/aoao-kana.png)

### 単語から調べる

![例: 青青した](https://github.com/akirakubo/npiii-macdict/raw/master/docs/aoao-kanji.png)

### 検索しても見付からない場合
(JIS X 0208の範囲内で)正字(旧字)を使用しないと見付からない場合があります。

![例: 圖書館](https://github.com/akirakubo/npiii-macdict/raw/master/docs/toshokan.png)

用言が見付からない場合、語幹のみを入力すると引掛る場合があります。

![例: むづかし](https://github.com/akirakubo/npiii-macdict/raw/master/docs/muzukashi.png)


### 字音仮名遣

元辞書の`np108_gg.txt`と`np108_gg_n.txt`とで重複する語に就いては、字音仮名遣を調べる事が出来ます。

![例: てふてふ](https://github.com/akirakubo/npiii-macdict/raw/master/docs/chouchou.png)

## 辞書作成(めも)

1. `np108_gg.txt`、`np108_gg_n.txt`の読みに登場する「う゛」を全て「ゔ」に置換
2. `sort`で単語品詞をソート
3. `join`で2つのファイルから単語が一致する辞書と一致しない辞書を作成
	1. ggとgg_n両方に含まれる
	2. ggにしか含まれない
	3. gg_nにしか含まれない
4. `sed`で辞書を整形し、タブ形式の1ファイルに統合 (`np108_gg_mac.txt`)
5. [stardict-tools](http://stardict.sourceforge.net/)でStarDict形式のファイルを生成 (`./tabfile np108_gg_mac.txt`)
6. [DictUnifier](https://github.com/jjgod/mac-dictionary-kit)で`np108_gg_mac.dictionary`ファイルを生成 (自動的に `~/Library/Dictionaries`に出力される)

### 注
stardict-toolsのmakeにはGTK+が必要。macOSの場合、`brew`を使ってインストール出来る。make中にエラーが出るが、`src`フォルダ内の`tabfile`コマンドは実行出来たので詳細未調査。

## ライセンス

北極三號辭書npiiiがGPLである為、本辞書もGPLです。

```
npiii for macOS Dictionary
Copyright (C) 2018 akirakubo
Licensed under GPLv2 license.

Includes 北極三號辭書npiii
https://sites.google.com/site/tidas1974/npiii
Copyright (C) 2011 TIDA Syuntaroo
Released under GPL license.
```