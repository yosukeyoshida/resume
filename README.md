# 職務経歴書

## 基本情報
|key|value|
|---|-----|
|Name|吉田 陽祐|
|Birthday|1985/03/27|
|GitHub|[yosukeyoshida](https://github.com/yosukeyoshida)|
|Kaggle|[yosukey](https://www.kaggle.com/yosukey)|
|Facebook|[Yosuke Yoshida](https://www.facebook.com/yosuke.yoshida.71/)|
|LinkedIn|[Yosuke Yoshida](https://www.linkedin.com/in/yosuke-yoshida-)|

## 学歴・職歴

|年月|職歴|
|---|-----|
|2008.03|東京工業大学工学部経営システム工学科 卒業|
|2008.04|株式会社ベネフィット・ワン 入社|
|2014.06|株式会社ベネフィット・ワン 退社|
|2014.08|iemo株式会社 入社|
|2017.06|iemo株式会社 退社|
|2017.07|株式会社フリークアウト・ホールディングス 入社 (株式会社カンム出向)|
|2019.01|株式会社フリークアウト・ホールディングス 退社 (株式会社カンム転籍)|
|2019.01|株式会社カンム 入社|

## 職務経歴
### 株式会社カンム (2017.07 - 現在)
```
Visaプリペイドカード 「バンドルカード」 のバックエンドや機械学習を活用した機能開発に従事
後払いチャージ機能に関しては機械学習モデルの開発やデータパイプラインの整備, APIサーバの開発まですべてを担当
```

#### 決済システム内製化
##### 課題/背景
* サービス開始からカード発行, 決済, 残高管理といった主要な機能は外部のSaaSを利用していたが障害がそれなりの頻度で発生していたことやトランザクションの増加に伴うコスト増が問題となってきていた
* これらを内製化することでコスト削減とシステムの安定化を図る

##### 実績
* カード発行やチャージ, 決済通知等を担うマイクロサービスの設計/開発 (REST API)
    * バンドルカードのAPIサーバ(以下バンドルAPI)から以下のリクエストを受け処理を行う
        * カード発行, 上位のカードへのアップグレード
        * チャージ, 手数料徴収
        * カードの一時停止/解除
    * 決済時にバンドルAPIに決済情報を通知 (webhook)
        * Visaの電文を処理するサーバとジョブキューを介して非同期に処理を行う
    * OpenAPIでスキーマを定義しサーバ/クライアントのコードを自動生成
* バンドルAPIの改修
    * SaaSを利用していたAPIやバッチ処理を内製化にあわせて改修
    * 分散トランザクションの考慮が甘くリトライ時の多重実行の懸念があったので冪等性を担保できるように改修

##### 技術
* Go
* PostgreSQL
* OpenAPI 3.0

#### ポチっとチャージ (後払いチャージ)
##### 課題/背景
* ポチっとチャージとはアプリからすぐにチャージができて翌月末までに返済すればよいという後払いサービス
    * それまでのバンドルカードは買い物に使う前にコンビニやペイジーなど事前にチャージが必須であった
    * ちょっとお金が足りなかったり、コンビニまで行くのが手間といった問題を解消する機能
* バンドルカード事業の収益の柱として後払いチャージ機能の立ち上げとグロースを担当

##### 実績
* アプリからリクエストされるREST API開発
    * 認証 (メール, SMS)
    * スコア更新, 申込み可能額算出
    * 残高へチャージ
    * 請求, 支払い (コンビニ, ネット銀行, ペイジー etc)
    * 返済期限超過による機能制限
* 督促処理
    * Email, SMS, Push Notificationによる督促
    * IVRを用いた自動架電による督促
        * 自動音声による入金のご案内とCSへの転送
* 機械学習によるスコアリング
    * 機械学習モデルの開発 (教師あり/二値分類)
    * 機械学習パイプラインの構築
        * https://tech.kanmu.co.jp/entry/2021/06/11/120953
* 複数アカウントや不正の検出

##### 技術
* Go
* PostgreSQL
* Python (scikit-learn, LightGBM, Optuna etc)
* SageMaker
* BigQuery
* Step Functions
* ECS/Fargate
* Cloud Dataflow
* Elasticsearch
* MLflow
* Embulk, Digdag

    
### iemo株式会社 (2014.08 - 2017.06)
```
住まい・インテリアのメディアでバックエンドや検索, 機械学習を活用した開発に従事
```
#### タグ・カテゴリ構造の再構築及び機械学習を用いた記事の自動分類
##### 課題/背景
* サービス開始から1年以上経過し、既存のカテゴリに収まらない記事が出てきたり人によってカテゴリの分類に差異が目立つようになってきた
* 記事のタグも執筆者により設定されていたが、まったくタグのついていない記事や内容に相応しくないタグが設定されていた

##### 実績
* 既存の記事をサンプリングし必要なカテゴリの洗い出しを行い、1階層8区分だったカテゴリを2階層30区分へ拡張 
* 記事のカテゴリ分類を行う機械学習モデルの開発
	* カテゴリ毎に特徴語を抽出(約40,000語)しLSIで300程度に次元削減した特徴量で多クラス分類/ロジスティック回帰 
	* 教師データのアノテーションを能動学習することによって効率化
* アノテーション用の管理画面を開発
* 推論APIサーバの構築
* 自動タグ付け機能開発
* 誤った分類を執筆者が教師データに追加できるようにした
* 新しいタグ・カテゴリ構造に合わせUIもリニューアル

##### 技術
* Ruby on Rails
* MySQL
* Python (scikit-learn, Gensim)
* Elasticsearch

#### 検索基盤の整備
##### 課題/背景
* 全文検索にGroongaが使われていたが仕様を詳しく把握しているエンジニアがいなかった為チューニングや機能追加ができていなかった
* 単純なN-gramによる検索だったので検索結果が雑多になりユーザの求める記事に到達することが困難であった
* インデックスの更新がバッチ処理で行われており記事が更新されてから検索に反映されるまでに時間がかかっていた

##### 実績
* 検索エンジンをGroongaからElasticsearchに移行し形態素解析を用いたトークナイザの追加, タイトル, 本文, タグ等のウェイトの調整を行い検索後の離脱率の改善 (25.28% -> 15.40%) 
* 形態素解析の辞書やシノニムの整備と継続的に誰でもメンテナンスができるように辞書の管理画面を用意
* 記事更新時に非同期でElasticsearchのインデックスを更新することで即座に検索に反映
* コンテンツベースのレコメンデーションを関連記事に活用し、更に表示する関連記事をバンディットアルゴリズムを用いてCTRの最大化, 回遊率の改善

##### 技術
* Ruby on Rails
* MySQL
* Elasticsearch
* SQS

### 株式会社ベネフィット・ワン (2008.04 - 2014.06)
```
福利厚生代行事業会社にて新規事業の立ち上げやシステムリニューアル, 業務システムの開発にPMとして従事

* ソフトバンクとの協業によるB2C向け優待サービスの立ち上げ, API設計
* NTTドコモのショップスタッフ向けインセンティブシステムの設計
* グルメクーポンサイトリニューアル
etc
```

## 業務外活動
* Kaggle
    * Competitions Expert (Solo Silver 2, Solo Bronze 1)
    * https://www.kaggle.com/yosukey

## ブログ等
* 個人ブログ
    * https://yosukeyoshida.netlify.app/
* 企業ブログ
    * [カンムを支える技術 機械学習編](https://tech.kanmu.co.jp/entry/2021/06/11/120953)
* インタビュー記事
    * https://kanmu.co.jp/interviews/yy/
