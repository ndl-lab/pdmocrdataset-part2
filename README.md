# パブリックドメインOCR学習用データセット（令和3年度OCR処理プログラム開発事業分）

国立国会図書館（以下、「当館」といいます。）が令和3年度に株式会社モルフォAIソリューションズに委託して実施したデジタル化資料のOCR処理プログラム開発事業の成果物を公開するリポジトリです。


## 概要
テキスト化性能の改善を目的として当館の提供するデジタル化資料から、再委託を受けた凸版印刷株式会社が作成したOCR学習用途の機械学習データセットのうち、
著作権保護期間の満了した資料から作成されたデータセットを公開しています。

2022年4月末現在、3,997画像分を公開しています。

本リポジトリで公開しているデータセット及び著作権保護期間存続資料から作成したデータセット（非公開）を利用して、NDLOCR(https://github.com/ndl-lab/ndlocr_cli
)の学習を行いました。

## 対応字種の範囲

* [対応字種一覧(PDF 418KB)](https://lab.ndl.go.jp/dataset/r3ocrproject/ocrprogram/ocrprogram_web.pdf)

なお、いずれの形式においても、文字コードの包摂を行っています。
包摂前後の対応関係については次の対応表（タブ区切りテキストの左側が包摂前、右側が包摂後）をご確認ください。

* [対応表(TSV 18KB)](https://lab.ndl.go.jp/dataset/r3ocrproject/ocrprogram/housetsulist_NDL.tsv)

## データセットのURL

次に挙げる2種類の形式で公開しています。


### 1. NDLOCR XML形式(https://lab.ndl.go.jp/dataset/pdm_ocr_dataset/morpho/ndlocr_xml.zip) (※ファイルサイズ:4.8 GB)

XMLフォーマットで作成したアノテーションデータ及びアノテーションデータに対応する画像データからなります。


### 2. PascalVOC 1.1形式(https://lab.ndl.go.jp/dataset/pdm_ocr_dataset/morpho/ndlocr_pascalvoc1.1.zip) (※ファイルサイズ:1.8 GB)

当館で納入物の検品を実施した際にNDLOCR XML形式をもとに変換したPascalVOC形式のアノテーションデータ（xmlフォーマット）及びアノテーションデータに対応する画像データからなります。
ファイルサイズを小さく抑えるため、NDLOCR XML形式の画像データのサイズ（縦幅及び横幅）を半分にしています。（アノテーションデータに含まれる座標情報も同様）
内部のテキスト情報はオブジェクト毎にattributeとして記述しています。
出力にはcvat(https://github.com/openvinotoolkit/cvat
)のエクスポート機能を利用しています。

## データセットの権利
「PDM（パブリック・ドメイン・マーク）」&lt; https://creativecommons.org/publicdomain/mark/1.0/deed.ja &gt;

※著作権保護期間満了資料のみを利用しています。

このデータセットは、自由な二次利用が可能です。ただし、二次利用に際しては、次の事項へのご配慮をお願いいたします。これらのお願いは法的な契約ではありませんが、できる限りご留意の上でご利用くださるよう、ご協力をお願いします。

- データを編集・加工等して利用する場合は、それを行ったことを記載してください。編集・加工等を、元となる作品・原資料の作者や当館が行なったかのような態様で公表しないようご留意ください。
- 当該データが自由に二次利用可能であることの表記を保持してください。
- 元となる作品や、その作者の名声を傷つける形での利用は行わないようご留意ください。また、元となる作品に関わる文化やコミュニティへの配慮を行ってください。
- 著作権以外の権利（著作者人格権、著作隣接権、肖像権、パブリシティ権、プライバシー権、商標権等）にも留意し、関連法令を遵守してください。


## ディレクトリ構成
データセット作成対象とした図書資料の刊行年代（10年刻み）によりディレクトリを分けています。

### 1. NDLOCR XML形式

```
ndlocr_morphoxml
├── 1870
│?? ├── 753742
│?? │?? ├── img
│?? │?? │?? ├── R0000038_contents_L.jpg
│?? │?? │?? └── R0000038_contents_R.jpg
│?? │?? └── xml
│?? │??     └── 753742.xml
│?? ├── 755053
│?? ・・・
├── 1880
├── 1890
├── 1900
├── 1910
├── 1920
├── 1930
├── 1940
├── 1950
└── 1960
```

### 2. PascalVOC 1.1形式

```
tosho_all_pascalvoc1.1
├── tosho_1870_bunkei
│?? ├── Annotations
│?? │?? └── pdmlinetrainimg
│?? │??     └── tosho_1870_bunkei
│?? ├── ImageSets
│?? │?? ├── Action
│?? │?? ├── Layout
│?? │?? ├── Main
│?? │?? └── Segmentation
│?? └── JPEGImages
│??     └── pdmlinetrainimg
│??         └── tosho_1870_bunkei
├── tosho_1870_rikei
│?? ├── Annotations
│?? │?? └── pdmlinetrainimg
│?? │??     └── tosho_1870_rikei
│?? ├── ImageSets
│?? │?? ├── Action
│?? │?? ├── Layout
│?? │?? ├── Main
│?? │?? └── Segmentation
│?? └── JPEGImages
│??     └── pdmlinetrainimg
│??         └── tosho_1870_rikei
（以下略）
```


## データセットの形式
### 1. NDLOCR XML形式
①「画像情報（PAGE）」、②「⾏矩形情報（LINE）」及び「LINEに該当する行矩形情報以外の領域情報（BLOCK）」、③「インライン情報(INLINE)」及び「⽂字矩形情報（CHAR）」の3階層で構成される。

NDLOCRの学習には、①及び②の階層の情報を利用している。

#### 1.1.	PAGEの定義
* PAGEは「対象画像ファイル名（IMAGENAME）」、「高さ（HEIGHT）」、「幅（WIDTH）」及び「匡郭有無（KYOKAKU）」の各属性を持つ。
* PAGEは子要素として、LINE若しくはBLOCK又はその両方を持つ。

#### 1.2.	BLOCK及びLINEの定義
* BLOCKは「左上座標（X,Y）」、「高さ（HEIGHT）」、「幅（WIDTH）」及び「種類（TYPE）」の各属性を持つ。
* TYPEは「図版」、「表組」、「柱」、「ノンブル」、「ルビ」、「組織図」、「数式」、「化学式」及び「欧文」のいずれか該当するものを入力する。
* BLOCKは正立を前提とし、傾きや蛇行の情報は保持しない。
* 行内文字列が存在する場合について、BLOCKはCHARを子要素に持たなくてもよい。
* LINEは「左上座標（X,Y）」、「高さ（HEIGHT）」、「幅（WIDTH）」、「書字方向（DIRECTION）」、「種類（TYPE）」及び「行内文字列情報（STRING）」の各属性を持つ。
* TYPEは、「キャプション」、「頭注」、「割注」のいずれかに該当する場合にその旨を入力し、いずれにも該当しない場合には「本文」を入力する。
* LINEの矩形は、内包するCHARの集合の外接矩形とする。
* LINEは正立を前提とし、傾きや蛇行の情報は保持しない。
* STRINGに1文字以上の文字列が含まれる場合、LINEは子要素としてCHAR若しくはINLINE又はその両方を持つ。
* STRINGに包摂不可能なJIS第二水準外文字及び汚れやかすれなどで文字が判読不能な文字が含まれる場合には、当該文字を「〓」で表現する。

#### 1.3.	INLINE及びCHARの定義
* LINEの内部に、BLOCKに該当する領域が含まれる場合には、当該領域をINLINEとする。
* INLINEの持つ属性は「数式」、「化学式」、「欧文」、「手書き」、「縦横中」、「色付き文字」、「回転欧文」のいずれかである。STRINGにおける当該位置の文字列は「〓」で表現する。
* LINEの内部にあって、INLINEに該当しない文字列は、個々の文字情報を分割してCHAR要素として子要素に記述する。
* CHARは「左上座標（X,Y）」、「高さ（HEIGHT）」、「幅（WIDTH）」及び「文字情報（MOJI）」の各属性を持つ。
* MOJIに包摂不可能なJIS第二水準外文字及び汚れやかすれなどで文字が判読不能な文字が含まれる場合には、当該文字を「〓」で表現する。


### 2. PascalVOC 1.1形式
(後から入れる)


## 作成対象とした画像のメタデータ

以下を参照してください。

[metadata](./info.csv)



## XMLスキーマ礼例


### 1. NDLOCR XML形式

```
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<OCRDATASET xmlns=“NDLOCRDATASET">
    <PAGE IMAGENAME=“ページ名_L.jpg” WIDTH=“2000” HEIGHT=“3000“ KYOKAKU =“true”>
        <BLOCK TYPE= "図版|表組|柱|ノンブル|ルビ|組織図|数式|化学式|欧文|" “TITLE="TRUE" AUTHOR= "FALSE" X="20" Y="20" WIDTH="1800" HEIGHT=300" />
        <LINE DIRECTION=“縦|横|右から左” TYPE=“本文|割注|頭注|キャプション“ “TITLE=”TRUE“ AUTHOR= ”FALSE“ STRING="あいうえお" X="20"
        Y="340" WIDTH="540" HEIGHT="31">
            <CHAR MOJI="あ" X="20" Y="340" WIDTH="30" HEIGHT="30"/>
            <CHAR MOJI="い" X="80" Y="340" WIDTH="30" HEIGHT="30"/>
            <CHAR MOJI="う" X="150" Y="340" WIDTH="31" HEIGHT="31"/>
            <CHAR MOJI="え" X="210" Y="340" WIDTH=29" HEIGHT="29"/>
            <CHAR MOJI="お" X="260" Y="340" WIDTH="30" HEIGHT="30"/>
            <INLINE TYPE=“欧文|手書き|縦中横|色付文字|回転欧文" X="420" Y="340" WIDTH="140" HEIGHT="30"/>
        </LINE>
        <LINE DIRECTION=“縦|横|右から左” TYPE=“本文|割注|頭注|キャプション” TITLE=”TRUE“ AUTHOR= ” FALSE “ STRING=“かきくけこ" X="20"
        Y="350" WIDTH=640" HEIGHT="30">
            <CHAR MOJI="か" X=20"" Y="370" WIDTH="30" HEIGHT="30"/>
            <CHAR MOJI="き" X="78" Y="370" WIDTH="29" HEIGHT="29"/>
            <CHAR MOJI="く" X="147" Y="370" WIDTH="28" HEIGHT="28"/>
            <CHAR MOJI="け" X="209" Y="370" WIDTH="30" HEIGHT="30"/>
            <CHAR MOJI="こ" X="261" Y="370" WIDTH="28" HEIGHT="28"/>
        </LINE>
    </PAGE>
</OCRDATASET>


```

### 2. PascalVOC 1.1形式

```
後から入れる
```


## 一般公開していない成果物の利用について

著作権保護期間の存続している資料から作成したOCR学習用データセットについては、原資料の著作権保護の観点から不特定多数に向けて公開することができません。

これらのデータに関しては、当館との協議のうえで著作権法上認められた範囲内での利用（著作権法第30条の4の規定による機械学習目的など）に限り、当館と書面を取り交わした上で提供することが可能です。

特に図書館サービスの向上に資する調査研究・技術開発を目的とした利用を歓迎します。

データの提供を希望される方は下記の連絡先までお問い合わせください。

lab(アットマーク)ndl.go.jp

その際、①利用者、②利用したいデータ（内容・範囲）、③利用目的、④利用方法、⑤利用期間　をお知らせください。
