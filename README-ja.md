PXbase パッケージバンドル
=========================

LaTeX： 他の PX パッケージのためのサポートライブラリ

本バンドルの主な目的は、作者（ZR）の制作する他の pTeX 用パッケージ（名前
が“PX”で始まる）が依拠するライブラリ機能の提供である。

その他に、本バンドルには以下のユーザ・開発者用パッケージが含まれる。

  * pxbabel パッケージ： Babel の機構に基づく CJK 間のフォント切替
  * upkcat パッケージ: 文字指定による kcatcode 操作

### 前提環境

  * TeX フォーマット： LaTeX
  * TeX エンジン： pTeX、upTeX（派生を含む）
  * DVI ウェア（DVI 出力時）： 不問

※upkcat パッケージについては当該の節を参照。

### 構成物

  * `pxbase.sty`: pxbase パッケージ
  * `pxbase.def`: サブモジュール（の残骸）
  * `pxbabel.sty`: pxbabel パッケージ
  * `pxbasenc.def`: サブモジュール
  * `pxjsfenc.def`: サブモジュール
  * `pxbsjc.def`: pxbase 用の補助ファイル
  * `pxbsjc1.def`: pxbase 用の補助ファイル
  * `upkcat.sty`: upkcat パッケージ

※種々の事情により複雑になっている（例えば、`pxbsjc.def` は実際には bxbase
パッケージから読まれている、`pxjsfenc.def` は BXbase／PXbase 内のどの
パッケージからも参照されない、など）が、他のパッケージの動作を確保する
ため敢えて 0.5 版のファイル構成を保っている。

### インストール

TDS 1.1 に準拠するシステムの場合、以下のようにファイルを移動する：

  - `*.sty`, `*.def` → $TEXMF/tex/platex/PXbase

この後必要に応じて mktexlsr を実行する。

### ライセンス

本パッケージは MIT ライセンスの下で配布される。


pxbase パッケージ ― pTeX 用（旧）基礎ライブラリ
------------------------------------------------

他の PX シリーズのパッケージの下請けの役割も果たしていたが、0.9 版において
[bxbase パッケージ]に統合された。今では、単に bxbase を読むだけである。

[bxbase パッケージ]: https://www.ctan.org/pkg/bxbase

### ユーザ向け機能

※bxbase の方で述べていないものを挙げる。（FIXME：bxbase に移すべき。）

※旧版のドキュメントに載っていたのに、ここにも bxbase の方にも載って
いない機能は、非推奨の扱いになったということ。

  * `\infojenc`： 漢字コードの情報を次の形で端末とログに出力する。

        Kanji encoding: source=UTF8 internal=SJIS;

  * `\safecaret`： 一部の箇所で TeX エスケープ形式（`^^ab`）の解釈が
    失敗するのを回避する。詳細は「TeX エスケープ形式（`^^ab`）の処理」
    の節を参照。

#### utf8x 入力エンコーディングの fasterror 設定

ucs パッケージ（バンドル）が提供する「utf8x 入力エンコーディング」では、
パッケージで未定義の Unicode 文字が入力された場合エラーになる。その時の
エラーメッセージ中に該当の文字の Unicode 名を出力するが、この際に高位
バイトを含むファイル（テキスト情報をハフマン符号で圧縮したものと思われる）
を用いるので、pTeX では処理に失敗してしまう。そこで本パッケージでは、ucs
パッケージが読み込まれた場合（utf8x が指定された時も含む）に上記の機能を
抑止するオプション `fasterror` を常に有効にする。

### TeX エスケープ形式（`^^ab`）の処理

現在の pTeX では入力漢字コードが UTF-8 の時に JIS X 0208 に含まれない
文字をエスケープ形式（`^^ab`）の UTF-8 バイト列に変換する。通常はこの
形式は該当のバイト列と等価の解釈をされる。ところがここで `^` の catcode
が本来の値 7 から変更されているとこの処理が失敗してしまう。具体的には
次のような場合が該当する。

  * Babel の一部の言語（esperanto 等）を使用した場合。
  * verbatim や類似の環境の中。

`\safecaret` 命令をプレアンブルで実行した場合、これらの場合でエスケープ
形式の連続する出現をバイト列と解釈するようにする。

### 開発者向け機能

（使用中の漢字コード系の情報表示）

  * `\bxInternalJaEncoding`：［暗黙文字トークン］ 内部漢字コードを表す。
      - `s`： シフトJIS
      - `e`： EUC
      - `u`： Unicode (upTeX)

  * `\bxInputJaEncoding`：［暗黙文字トークン］ 入力 TeX ソースの漢字
    コードを表す。
      - `s`： シフトJIS
      - `e`： EUC
      - `u`： UTF-8
      - `a`： 自動判定が有効

  * `\pxUpScale`：［マクロ］ 和文の標準フォントに対する和文スケール。
    `\Cjascale` が設定済の場合はその値、それ以外で文書クラスが和文標準
    または jsclasses のものの場合は、当該クラスの既定のスケール値。


pxbabel パッケージ ― Babel の機構に基づく CJK 間のフォント切替
---------------------------------------------------------------

詳細についてはマニュアル `pxbabel.pdf` を参照されたい。

upkcat パッケージ ― 文字指定による kcatcode 操作
-------------------------------------------------

※ 本パッケージはパッケージ開発者向けのものである。

文字を指定して（それが属するブロックの）kcatcode を操作する場合

    \kcatcode`<文字>

の形式を使うことになるが、その際にもしその文字の現在の kcatcode が 15
である場合は文字がバイト列とみなされるので、この形式が使えない。この
パッケージはそのような場合でも使用可能な、kcatcode の参照・変更の命令
を提供する。なお、文書作成者はこちらではなく [pxcjkcat パッケージ]を
用いるべきである。

[pxcjkcat パッケージ]: https://www.ctan.org/pkg/pxcjkcat

### 前提環境

  * TeX フォーマット： plain、LaTeX
  * TeX エンジン： upTeX（派生を含む）
  * DVI ウェア（DVI 出力時）： 不問

### パッケージ読込

plain upTeX の場合：

    \input upkcat.sty

upLaTeX の場合：

    \usepackage{upkcat}

### 機能

  * `\getkcatcode{<文字>}`： `<文字>` の現在の kcatcode の値（15～19）
    をマクロ `\thekcatcode` に文字列として返す。
  * `\setkcatcode{<文字>}{<値>}`： `<文字>` の kcatcode の値を `<値>`
    に設定する。


更新履歴
--------

  * Version 1.3  〈2021/05/31〉
      - pxbabel: japanese-otf のコード入力命令（`\UTF` 等）について、
        非標準の和文エンコーディングの適用時でも動作するようにパッチを
        適用する。
      - pxbabel: (試験的) `(no)patchutfcmds` オプションを追加。

  * Version 1.2  〈2021/05/22〉
      - pxbabel: CJK 言語のフォント切替を japanese-otf で多ウェイト拡張
        （`deluxe`）を指定した場合に対応させた。
      - pxbabel: (試験的) `(no)forcedeluxemulti` オプションを追加。
        `forcedeluxemulti` を指定すると、さらに多言語拡張（`multi`）を
        行った場合の日本語以外のフォントにも適用される。

  * Version 1.1b 〈2017/07/03〉
      - upLaTeX で japanese-otf と併用した場合に対応。
      - バグ修正。

  * Version 1.1a 〈2017/06/19〉
      - バグ修正。

  * Version 1.1  〈2017/05/29〉
      - 内容の整理。  
        ※バージョンの値は BXbase と合致させて 1.1 版とした。
      - 一部の機能を非推奨にした。

  * Version 0.5i 〈2017/05/04〉 ― CTAN 公開版
      - 0.5 版から ifuptex と pxcjkcat を削除したもの。  
        ※ifptex パッケージバンドルを CTAN に登録するための経過措置。

  * Version 0.9b 〈2012/08/19〉
      - ifuptex パッケージは「ifptex バンドル」に移動したため削除。
      - pxcjkcat パッケージは専用のバンドルに移動したため削除。

  * Version 0.5  〈2010/06/15〉
      - pxbase: `\JI`／`\KI` を追加。
      - pxbase: `\dvipdfmxmapline`／`\dvipdfmxmapfont` を追加。

  * Version 0.4a 〈2010/02/07〉
      - pxcjkcat: upTeX v0.29 における kcatcode のブロック分割の変更に
        対応。それに伴い `ccv1`, `ccv2` オプションを新設。
      - pxcjkcat: `\cjkcategory` の第 1 引数に文字そのものを指定できる
        ようにした。
      - pxcjkcat: なぜかモード設定時の「Enclosed CJK Letters and Months」
        （`cjk07`）の kcatcode の設定値が 16 になっていた。upTeX 既定値に
        合わせて 18 に修正した。

  * Version 0.4  〈2009/07/05〉
      - safe caret 機構のコード（`\safecaret` の実装の核心）を pxbase.def
        に移動（BXbase と共通に）。
      - Babel に加えて verbatim でも safe caret 機構が働くようにする。
        ただし「pxbase は単に読み込むだけでは他人のコードを書き換えない」
        という指針があるので、`\safecaret` を実行しないと有効にならない。
      - pxbabel は中で `\safecaret` を呼ぶので、pxbabel を読み込むと safe
        caret は自動的に有効になる。
      - pxbabel でエンコーディングを `J20` 等に変えた場合に OTF パッケージ
        の `\CID` が動かなくなるのを修正。

  * Version 0.3  〈2008/04/06〉
      - pxbabel に safe caret 機構を追加。

  * Version 0.2b 〈2008/03/28〉
      pxbabel に `\UTF` の切替を追加。

  * Version 0.2a 〈2008/03/18〉
      pxbabel, pxbase のバグ取り。
      pxbabel の説明書をまだ書いていないことに気づいた ;-) 慌てて作成。

  * Version 0.2  〈2008/03/14〉
      最初の公開版。

-------------------------------------------
Takayuki YATO (aka. "ZR")  
https://github.com/zr-tex8r
