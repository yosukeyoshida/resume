# 職務経歴書

## 基本情報
|key|value|
|---|-----|
|Name|吉田 陽祐|
|Email|y.yoshida0327@gmail.com|
|Kaggle|[https://www.kaggle.com/yosukey](https://www.kaggle.com/yosukey)|
|Blog|[https://yosukeyoshida.netlify.app/](https://yosukeyoshida.netlify.app/)|

## 学歴・職歴

|年月|職歴|
|---|-----|
|2008.03|東京工業大学工学部経営システム工学科 卒業|
|2008.04|株式会社ベネフィット・ワン 入社|
|2014.06|株式会社ベネフィット・ワン 退社|
|2014.08|iemo株式会社 入社|
|2017.06|iemo株式会社 退社|
|2017.07|株式会社フリークアウト・ホールディングス 入社 (株式会社カンムへ出向)|
|2019.01|株式会社フリークアウト・ホールディングス 退社 (株式会社カンムへ転籍)|
|2019.01|株式会社カンム 入社|

## 職務経歴
### 株式会社カンム (2017.07 - 現在)
```
Visaプリペイドカード「バンドルカード」の開発
バックエンドや機械学習を活用した機能開発に従事
```

#### プロセシングシステム内製化
##### 課題/背景
* サービス開始から決済, カード発行, チャージ, 残高管理といった主要な機能は外部のSaaSを利用していたが障害がそれなりの頻度で発生していたこと、トランザクションの増加に伴うコストの増加が問題となってきていた
* プロセシングシステムを内製化することでコスト削減とシステムの安定化の実現

##### 実績
* 外部APIのドキュメントと既存コードからすべてのシーケンス図を作成 
* カード発行やチャージ, 決済通知等を担うREST APIサーバをマイクロサービスとして新規に設計/開発
* バンドルカードのAPIサーバとのインテグレーション

##### 技術
Go, Python, EC2, RDS

#### 後払い機能開発 (ポチっとチャージ)
##### 課題/背景
* バンドルカード事業の収益の柱として立ち上げと数値目標の達成

##### 実績
* 後払いチャージや支払いまわりのAPI開発
* push, sms, emailによる督促やIVRによる自動架電システムの構築
* 不履行処理開発
* 複数アカウントや不正の検出
* 機械学習モデルの開発 (教師あり/二値分類)
* 機械学習パイプラインの構築
    * https://tech.kanmu.co.jp/entry/2021/06/11/120953
* ルールベースと機械学習によるスコアリング
* 返済率, 売上等の数値コントロールの為のルールベースや機械学習モデルの閾値のチューニング

##### 技術
Go, Python, RDS, ECS/Fargate, SageMaker, Cloud Storage, Cloud Dataflow, Step Functions, Elasticsearch, scikit-learn, LightGBM, PyTorch, Optuna, MLflow,
BigQuery, Embulk, Digdag
    
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
* 自動で記事のカテゴリ分類を行う機械学習モデルの開発
	* カテゴリ毎に特徴語を抽出(約40,000語)しLSIで300程度に次元削減した特徴量で多クラス分類/ロジスティック回帰 
	* 教師データのアノテーションを能動学習することによって効率化
* アノテーション用の管理画面を開発
* 推論APIサーバの構築
* 自動タグ付け機能開発
* 新しいタグ・カテゴリ構造に合わせUIもリニューアル

##### 技術
Ruby on Rails, Sinatra, Python, scikit-learn, Gensim, Elasticsearch, MySQL

#### 検索エンジンのElasticsearchへの移行
##### 課題/背景
* Groongaという検索エンジンが使われていたが仕様を詳しく把握しているエンジニアがいなかった為チューニングや機能追加が困難 
* トークナイザもN-gramのみで目的の記事を探すのが困難
* 記事が更新されてもインデックス更新までに時間がかかる

##### 実績
* Elasticsearchに移行 
* 形態素解析用の辞書やシノニムを整備し、継続的に誰でもメンテナンスができるように管理画面を用意 
* 記事更新時に非同期でElasticsearchのインデックスを更新
* 関連記事のようなコンテンツベースのレコメンデーションによる回遊率の向上 
* 検索後の離脱率の改善 (25.28% -> 15.40%) 

##### 技術
Ruby on Rails, Elasticsearch, SQS, MySQL

#### その他実績
* 記事作成CMS開発 (Rails, AngularJS)
* Ruby on Rails/Grapeを用いたREST API開発
* バンディットアルゴリズムを用いた関連記事最適化

### 株式会社ベネフィット・ワン (2008.04 - 2014.06)
```
福利厚生代行事業会社にて新規事業立ち上げやサイトリニューアル、業務システムの開発にPMとして従事
```

#### ソフトバンクとの協業によるB2C向け優待サービス開発
* API, バッチ処理設計 (会員情報登録・更新 / 認証)

#### インセンティブポイントASPサービスリニューアル
* UIリニューアル / 物販システムとの統合

#### グルメクーポンサイトリニューアル
* Ruby on RailsをJavaで再構築 / DBの統合 (Oracle, SQLServer)
