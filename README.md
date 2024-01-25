# 『古典分類語彙表』データ版 v0.2.0

© 2023–2024 鈴木泰、安部清哉、于拙

## 概要

『古典分類語彙表』のデータを整理し、構造化した上で公開したものです。また、近日中検索用インタフェースも併せて公開する予定です。

## 構成

```
├── CHANGELOG.md
├── README.md
├── 分類ツリー.json
├── 分類語彙表.csv
├── 統計情報
│   ├── A.項目総数.tsv
│   ├── B.分類項目数内訳（類・部門）.tsv
│   ├── C.語彙項目数内訳（類・部門）.tsv
│   └── D.分類項目数（語彙項目数）内訳（類・部門）.tsv
└── 項目一覧
    ├── 0_全項目.csv
    ├── 1_類.csv
    ├── 2_部門.csv
    ├── 3_中項目.csv
    └── 4_分類項目.csv
```

### [CHANGELOG.md](./CHANGELOG.md)

変更履歴を記したファイルです。

### [README.md](./README.md)

本ファイルです。利用方法・ファイル構成などを記載しています。

### [分類ツリー.json](./分類ツリー.json)

分類語彙表をツリー状に構造化されたデータをJSON形式で表したものです。データスキームは以下のTypeScriptの型定義によって表されます。

```typescript
type Root = Category[];

type Level = '類' | '部門' | '中項目' | '分類項目';

type Digit = '1' | '2' | '3' | '4' | '5' | '6' | '7' | '8' | '9';
type CategoryNumber =
  | `${Digit}.${Digit}${Digit}${Digit}${Digit}` // 1.1000
  | `${Digit}.${Digit}${Digit}` // 1.10
  | `${Digit}.${Digit}` // 1.1
  | `${Digit}`; // 1

type Category = {
  level: Level;
  number: CategoryNumber;
  description: string;
  count: number;
  children: (Category | Word)[];
};

type TextTitle =
  | '徒然草'
  | '平家物語'
  | '宇治拾遺物語'
  | '方丈記'
  | '新古今和歌集'
  | '大鏡'
  | '更級日記'
  | '紫式部日記'
  | '枕草子'
  | '蜻蛉日記'
  | '後拾遺和歌集'
  | '土佐日記'
  | '古今和歌集'
  | '伊勢物語'
  | '竹取物語'
  | '万葉集';

type Word = {
  lemma: string;
  kanji: string;
  attested: { [text in TextTitle]?: number };
};

```

分類ツリーをJSON形式で表したものです。

### [分類語彙表.csv](./分類語彙表.csv)

分類語彙表をCSV表データとして整理したものです。

```csv
類,部門,中項目,分類項目,分類番号,語番号,語彙素,表記,徒然草,平家物語,宇治拾遺物語,方丈記,新古今和歌集,大鏡,更級日記,紫式部日記,枕草子,蜻蛉日記,後拾遺和歌集,土佐日記,古今和歌集,伊勢物語,竹取物語,万葉集
```

#### 列の一覧
- 類: 類の名称（[項目一覧/1_類.csv](./項目一覧/1_類.csv)参照）
- 部門: 部門の名称（[項目一覧/2_部門.csv](./項目一覧/2_部門.csv)参照）
- 中項目: 中項目の名称（[項目一覧/3_中項目.csv](./項目一覧/3_中項目.csv)参照）
- 分類項目: 分類項目の名称（[項目一覧/4_分類項目.csv](./項目一覧/4_分類項目.csv)参照）
- 分類番号: 分類番号（`1`, `1.2`, `1.23`, `1.2345`のような形式）
- 語番号: 分類番号の語の番号（`1`, `2`, `3`, ...）
- 語彙素: 語彙素（`あまりこと`, `いちじ`, `いちだいじ`, ...）
- 表記: 漢字表記（`余事`, `一事`, `一大事`, ...）
- 徒然草：『徒然草』における出現回数（以下同じ）
- […]

### [統計情報](./統計情報)

TSV形式で表された本データに関する統計情報です。

#### [A.項目総数.tsv](./統計情報/A.項目総数.tsv)

各階層の項目数、語彙の総数などが含まれます。

#### [B.分類項目数内訳（類・部門）.tsv](./統計情報/B.分類項目数内訳（類・部門）.tsv)

〈類〉〈部門〉の分類項目数の内訳のクロス集計表が含まれます。

#### [C.語彙項目数内訳（類・部門）.tsv](./統計情報/C.語彙項目数内訳（類・部門）.tsv)

〈類〉〈部門〉の語彙項目数の内訳のクロス集計表が含まれます。

#### [D.分類項目数（語彙項目数）内訳（類・部門）.tsv](./統計情報/D.分類項目数（語彙項目数）内訳（類・部門）.tsv)

〈類〉〈部門〉の分類項目数と語彙項目数の内訳のクロス集計表が含まれます。

### [項目一覧](./項目一覧)

分類語彙表の各階層の項目一覧表です。

#### [0_全項目.csv](./項目一覧/0_全項目.csv)

階層に関わらず、すべての項目を含む表です。それぞれの分類番号、語彙素、総語数が含まれるCSVファイルです。

#### [1_類.csv](./項目一覧/1_類.csv)

類の階層のみの項目一覧表です。以下同じ。

## 利用
以下を参考文献として引用してください。

* 于 拙（2024）「宮島達夫他編『古典分類語彙表』データの構造化及びその応用」『情報処理学会研究報告』Vol. 2024-CH-134（発表予定）
* 宮島 達夫・鈴木 泰・石井 久雄・安部 清哉（2013）『古典分類語彙表』
