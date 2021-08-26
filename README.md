# ワクチンの副反応疑いに関する pdf 資料の csv 化

ここに置いてあるデータは、  
厚生科学審議会 (予防接種・ワクチン分科会 副反応検討部会)  
https://www.mhlw.go.jp/stf/shingi/shingi-kousei_284075.html  
の会合の pdf の資料の一部を
- csv 化し、フォーマットを変更したもの、
- 製造会社毎のファイルを1つに統合したもの

です。  

現在のところ置いてあるのは、
- 2021-08-04 の第66回会合  
https://www.mhlw.go.jp/stf/shingi2/0000208910_00028.html  
の「資料１－１－２－１」（＝ファイザー）、「資料１－１－２－２」（＝モデルナ）  
- 2021-08-25 の第67回会合  
https://www.mhlw.go.jp/stf/shingi2/0000208910_00029.html  
の「資料１－１－２－１」（＝ファイザー）、「資料１－１－２－２」（＝モデルナ）  

であり、いずれも「予防接種法に基づく医療機関からの副反応疑い報告状況について」の資料です。

## Last Update

2021-08-26
- 2021-08-25 の第67回の厚生科学審議会 (予防接種・ワクチン分科会 副反応検討部会)が開催されました。
- 資料が公開されましたので、csv 化し、ここに置きました。2021-08-25*.* です。

この資料は、会合の当日に公開されました。  

なお今回のデータ処理に際しては、一部手動でデータを修正する必要がありました。  
詳細は [こちらの「手動によるデータの修正」](2021-08-25/2021-08-25.md#手動によるデータの修正)を参照してください。  

## URL

https://github.com/sarkov28/c19_mhlw_after_vaccination

## Features

### ここに置いてあるデータの特徴
- 表本体しか処理していないので、注の情報は含んでいません。  
  注については、該当の pdf を参照して下さい。  

### 厚生労働省発表のデータの特徴
- 元になった pdf データのサンプリング方法については、こちらを参照してください。  
  https://www.mhlw.go.jp/stf/seisakunitsuite/bunya/vaccine_hukuhannou_youshikietc.html
- 接種の１回目と２回目の区別はありません。
- 1人に複数の副反応があるデータにおいては、幾つかのカラムに複数のデータがあります。  
  ところが、データ数が揃っているべきと思われるのに、揃っていないカラムがあります。
  - 数が揃っているのは、  
    「発生日」「症状名（PT名）」「転機日」「転機内容」
  - 数が揃っていないのは、  
    「接種から発生までの日数」「因果関係（報告医評価）」「重篤度（報告医評価）」

## とりあえずデータを見たいなら

「細かいことはいいから1人1行の全部のデータを見たい」ということなら。  
3.8M ほどのデータになりますが、  
2021-08-25_PfMo_t2.csv  
https://github.com/sarkov28/c19_mhlw_after_vaccination/raw/master/2021-08-25/2021-08-25_PfMo_t2.csv  
がいいと思います。

## データのダウンロード方法

以下の要領でデータをダウンロードすることができます。
- (1) このリポジトリのファイル全部  
zip 形式のアーカイブファイルでのダウンロードになります。  
リポジトリ  
https://github.com/sarkov28/c19_mhlw_after_vaccination  
を開き、やや右上の領域にある「Code▼」を「左クリック」するとメニューが開きます。  
メニューの中から「Download ZIP」を選びます。  
ダウンロード用のダイアログが開き、ダウンロードできます。
- (2) ファイル毎のダウンロード  
リポジトリ  
https://github.com/sarkov28/c19_mhlw_after_vaccination  
で、ダウンロードしたいファイルのファイル名を「左クリック」して下さい。  
そのファイルのページが開きます。  
開いたページのやや右上の領域に「Raw」又は「Download」のボタンがあります。  
このボタンを「右クリック」し、「名前を付けて保存」「Save Link As...」などを選びます。  
ダウンロード用のダイアログが開き、そのファイルがダウンロードできます。  
なお、ファイルのページでは、ファイルが小さければ、内容を確認できます。（例: 2021-08-04_Mo_t3.csv）  
ファイルが大きいと、「Sorry about that, but ・・・」などのメッセージが出て、内容は確認できません。（例: 2021-08-04_Pf_t1.csv）

## ファイル名の命名規則

yyyy-mm-dd_(製造会社)_(データフォーマット).csv
- yyyy-mm-dd は、会が開催された日付です。
- 製造会社は、現在のところ、以下です。
  - Pf: ファイザーのデータ
  - Mo: モデルナのデータ
  - PfMo: ファイザーとモデルナを統合したデータ  
    統合方法については、[「製造会社毎のデータの統合方法」](#製造会社毎のデータの統合方法) の項を参照してください。
- データフォーマットは、[「データフォーマット」](#データフォーマット) の項を参照して下さい。

最初からファイザーとモデルナを統合していないのは、厚生労働省のデータがファイザーとモデルナに分かれているからです。

## データフォーマット

文字コードは shift-jis（cp932）、改行コードは、CR+LF です。

この pdf には「1つの副反応に1行」の情報があります。  
このため、例えば「1人に2つの副反応」の情報がある時は、「1人の情報が2行」になっています。  
（例：モデルナ https://www.mhlw.go.jp/content/10601000/000816272.pdf の上から2つ目の No 9209 のデータ）  

「1人に複数の副反応」に該当するデータは、無数にあります。  
このタイプのデータをどう処理するかで、現在のところ、3つのフォーマットを用意してあります。  
- t1 形式: python + camelot によって csv 化したデータを、文字コードだけ変換したもの。  
  1人1行のデータ。  
  pdf における1つの枠の中の複数項目は、制御コード CR で区切られた文字列になっている。
  （csv への変換処理の参考 url: https://qiita.com/barobaro/items/f8c102d07144ca747099）  
  表中に制御コード CR が混じっているのが欠点だが、もとの状態を復元するには適しているかも知れない。
- t2 形式: t1 形式のデータの CR を、半角ブランクに置き換えたもの。  
  1人1行のデータ。  
  2021-08-25 のデータにおいては、元のデータに1カ所、半角ブランクがありました。[こちらの「例外データについて」](2021-08-25/2021-08-25.md#例外データについて) を参照してください。

- t3 形式: t1 形式のデータを、上掲の No 9209 のデータであれば、2行に分割したもの。  
  1副反応1行のデータ。  

## 製造会社毎のデータの統合方法

製造会社毎に作成した t1、t2、t3 のファイルを、それぞれ統合しました。  
統合に際しては、linux コマンドの sort を以下のオプションで実行しました。  

sort&nbsp; --general-numeric-sort&nbsp; --stable&nbsp; (統合元のファイル名のリスト)&nbsp; >&nbsp; (統合結果のファイル名)  

ただし、このままだと表頭が重複するので、tail&nbsp; -(統合結果のファイルの行数) で表頭を削除しました。  
(統合結果のファイルの行数) = (統合結果のデータ行数の合計値) + 1  
です。（+ 1 は、表頭を1行入れるための調整。）  

統合結果が左端の「No」のカラムの値の順になることを意図しています。  
「No」のカラムは、ほとんど全てのデータで整数なのですが、一部に例外があります。  
今後において、こうした例外のために、統合の処理が困難になる可能性があります。  
例外の詳細については、[こちら](#各資料における例外データについて) をご参照下さい。

## Detail

### 各資料における例外データについて
- 2021-08-04 のデータに関して  
  [2021-08-04/2021-08-04.md](2021-08-04/2021-08-04.md#例外データについて) の「例外データについて」を参照してください。
- 2021-08-25 のデータに関して  
  [2021-08-25/2021-08-25.md](2021-08-25/2021-08-25.md#例外データについて) の「例外データについて」を参照してください。

### 作業する余地があるかも知れないが、行っていない事項
[「厚生労働省発表のデータの特徴」](#厚生労働省発表のデータの特徴) に書いたように、1人に複数の副反応があるデータにおいて、数が揃っているべきなのに、揃っていないデータがあります。  
このうち「接種から発生までの日数」については、以下の事情があります。
- 「接種日」は1つのデータです。  
- 「発生日」は副反応の数だけデータがあります。  
- 「接種から発生までの日数」は副反応の数だけデータがあるべきですが、1つのデータです。

ほとんどのデータにおいては複数の「発生日」データは同じであり、「接種から発生までの日数」も同じとなるので、問題は生じません。  
しかし「発生日」データが異なる場合には、現在のように「接種から発生までの日数」を同じとするのは不適切です。  
調べたところ、
- 2021-08-04 の、No=[30, 2507, 10689, 13094] のデータ  
  （例えば、[こちら](https://github.com/sarkov28/c19_mhlw_after_vaccination/raw/master/2021-08-04/2021-08-04_PfMo_t2.csv) の該当の No の左から 5 カラム目。）
- 2021-08-25 の、No=[30, 2507, 10689, 13052] のデータ  
  （例えば、[こちら](https://github.com/sarkov28/c19_mhlw_after_vaccination/raw/master/2021-08-25/2021-08-25_PfMo_t2.csv) の該当の No の左から 5 カラム目。）

において、「発生日」データが異なっていました。  
（全体で 22000 件ほどあるデータの中の、4 件の事例ではあります。）

こうした事例への対応として、今後、「接種から発生までの日数」を計算で算出したものに置き換えるかも知れません。  
もし、こうした置き換えが不適切だとお考えでしたら、ご意見を頂ければと思います。  
なお、「接種日」や「発生日」のデータは、稀に欠落していたり、不完全だったり（＝"2020/07" など）する事例もあるので、その場合は、この算出は行えません。上記のうち、No=2507 は、一部欠落の事例です。

### 別の会合間での資料の関係について
2 つの会合における、モデルナの pdf ファイルの url は以下になっています。  
- 2021-08-04 モデルナ (04Mo) https://www.mhlw.go.jp/content/10601000/000816272.pdf
- 2021-08-25 モデルナ (25Mo) https://www.mhlw.go.jp/content/10601000/000823360.pdf

(25Mo) は、(04Mo) を更新したデータです。  

(25Mo) と、(04Mo) との差は、
- 共通するほとんどの部分は完全に一致し、
- 「不明」だった項目の一部が埋まり、
- 新しい情報が付加されている、

のかと思っていましたが、「そうではありませんでした」。  

(04Mo) と比べて、(25Mo) は、
- 「No のカラム」が先頭のデータから違いました。  
  「No のカラム」は、個人のデータ毎に割り当てられた ID ではなく、「その日の会合で発表されたデータにおける、製造販売業者をまたいだ、通し番号」ではないかと思われます。
- 「No のカラム」が統一されていないので、細かく照合するのは困難なのですが、
  「項目内での順序の入れ替え」「副作用の記述順序の入れ替え」があります。

### pdf ファイルの csv 化の方法について
私は、こちら  
https://github.com/sarkov28/c19_tokyo_kunishihyou
でも pdf の csv 化の作業をしています。  
c19_tokyo_kunishihyou では、python + tabula で行なっています。  
今回は、python + camelot で行いました。  

今回の pdf を python + tabula で処理しようとしたところ、2021-08-04 のファイザーのデータの 82 ページでエラーとなり、処理できませんでした。  
python + camelot では、正常に処理できました。  
（csv への変換処理の参考 url: https://qiita.com/barobaro/items/f8c102d07144ca747099）  

## Plan

今回処理したデータを更新するものが発表された時には、同様に csv 化し、ここに置く予定です。  
ただし、すぐに作業できるとは限りません。  

## Update Log

2021-08-18
- 2021-08-04 の第66回会合  
https://www.mhlw.go.jp/stf/shingi2/0000208910_00028.html  
の「予防接種法に基づく医療機関からの副反応疑い報告状況について」の pdf データを csv 化し、統合し、ここに置きました。
- 置いて数時間後に、t2 形式のデータに問題があることに気づき、これを修正しました。  
t2 形式のデータは、「t1 形式のデータの全ての CR を半角ブランクに置き換えたもの」であるべきでしたが、一部が置き換わっていませんでした。  
失礼しました。

## Author

https://twitter.com/sarkov28

twitter やブログに、コロナに関することを色々と書いています。

- 新型コロナ関連の主な事柄のリスト  
  https://sarkov28.hatenablog.com/entry/2021/01/25/193020
- 新型コロナ関連の主な事柄のリスト（特に重要な項目）  
  https://sarkov28.hatenablog.com/entry/2021/01/25/193753

## License

このリポジトリにあるデータは、厚生労働省がこちら  
https://www.mhlw.go.jp/stf/shingi/shingi-kousei_284075.html  
以下で公表しているデータを加工したものです。  
自由に使っていただいて構いませんが、内容は保証出来ません。  
