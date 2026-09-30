# アプリケーション「ラストワンマイル」

[![Java](https://img.shields.io/badge/Java-25-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)](https://openjdk.org/)
[![Apache Tomcat](https://img.shields.io/badge/Apache_Tomcat-11-F8DC75?style=for-the-badge&logo=apache-tomcat&logoColor=black)](https://tomcat.apache.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-18.1-316192?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![AWS](https://img.shields.io/badge/AWS-EC2-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)](https://aws.amazon.com/)
[![Google Gemini](https://img.shields.io/badge/Google_Gemini-API-8E75C2?style=for-the-badge&logo=google-gemini&logoColor=white)](https://ai.google.dev/)
[![Eclipse](https://img.shields.io/badge/Eclipse-IDE-2C2255?style=for-the-badge&logo=eclipse-ide&logoColor=white)](https://www.eclipse.org/)
[![A5:SQL Mk-2](https://img.shields.io/badge/DB_Tool-A5:SQL_Mk--2-2D5986?style=for-the-badge)](https://a5m2.mmatsubara.com/)
[![Antigravity](https://img.shields.io/badge/Dev_Tool-Antigravity-4285F4?style=for-the-badge)](https://antigravity.google/)

避難所・支援先からの物資申請と、ボランティアによる配送対応、管理者による在庫・配送進捗管理を一元化するWebアプリケーションです。  
直感的なUIでの物資申請・リアルタイムな配送ステータス追跡、およびレスポンシブ（スマホ最適化）対応を備え、災害時や緊急支援時にも迅速かつ正確な物資共有を支援します。
> [!NOTE]  
> **本プロジェクトは、Java実習時に作成したコンテンツ（ポートフォリオ）です。**  
> * **開発期間**: 26日  (要件定義、PD、PG)
> * **開発規模**: 2.3Kstep  
> 
> Java実習の内容は以下よりご覧いただけます。  
> 👉 **[Java実習の内容はこちら](https://github.com/hadano-nobuyuki/ai-programming-training-portfolio)**  
> *(※別タブで開く場合は Ctrl + クリック / Cmd + クリック 推奨)*

---

## 📑 目次
1. [💻 画面イメージ](#-画面イメージ)
2. [✨ 主な機能](#-主な機能)
3. [🧰 使用技術・開発環境](#-使用技術開発環境)
4. [📐 システム構成](#-システム構成)
5. [🌐 動作確認（デモ環境）](#-動作確認デモ環境)
6. [📖 要件定義書・画面設計書](#-要件定義書画面設計書)
7. [🛠️ ローカル環境での実行・セットアップ手順](#️-ローカル環境での実行セットアップ手順)
8. [💡 工夫した点](#-工夫した点)
9. [🧗 苦労した点・得られた教訓](#-苦労した点得られた教訓)

---

## 💻 画面イメージ

*(※ 掲載している画像はシステム画面の一部抜粋です。全画面イメージや詳細な画面フローは [要件定義書・画面設計書](#-要件定義書画面設計書) よりご覧いただけます)*

| カレンダー（予定・約束管理）<br><sub>※一部抜粋</sub> | 家計簿（収支管理 & AIアドバイス）<br><sub>※一部抜粋</sub> |
| :---: | :---: |
| <img src="readme_img/main1.png" width="360" alt="カレンダー画面"> | <img src="readme_img/main2.png" width="360" alt="家計簿画面"> |
| 予定や用事、天気を月間カレンダーで一覧確認 | 日別収支、目標残高、Geminiによる個別アドバイス |

---

## ✨ 主な機能

* 📦 **物資申請機能（被災者向け）**
  * カテゴリ別（食料・飲料・衛生用品・生活用品等）のタブ表示と、直感的な数量増減（+/-）UIでの一括申請
  * 申請完了後の注文番号による配送状況リアルタイム照会・申請取り消し機能
* 🚚 **物資配達・配送管理機能（ボランティア向け）**
  * ステータス別（未対応 / 対応中 / 完了 / 配送不可）の配送案件フィルタリング
  * ワンタップでのステータス更新（対応開始・完了報告・配送不可報告）および備考入力
* ⚙️ **管理者機能（管理者向け）**
  * **在庫・物資管理**: 物資の新規登録、編集、削除（論理削除/物理制御）、リアルタイム在庫数管理
  * **全配送状況モニタリング**: 「すべて」タブを含む全注文データの把握、注文強制キャンセル・削除
  * 管理者ログイン・ログアウト認証（安全なセッション破棄・完了モーダル表示）

---

## 🧰 使用技術・開発環境

| カテゴリ | 技術スタック / バージョン |
| :--- | :--- |
| **開発期間** | 26日 |
| **開発規模** | 2.4Kstep |
| **言語・ランタイム** | Java 25 (OpenJDK) |
| **Webコンテナ / APサーバ** | Apache Tomcat 11 |
| **バックエンドフレームワーク** | Java (Servlet / JSP) |
| **データベース** | PostgreSQL 18.1（テーブル生成用 [DDL.sql](DDL.sql) を同梱） |
| **インフラ / ホスティング** | AWS (EC2) |
| **統合開発環境 (IDE)** | Eclipse |
| **DB管理・設計ツール** | A5:SQL Mk-2 |
| **開発支援（AI）** | Antigravity |

---

## 📐 システム構成

```mermaid
graph LR
    User([避難者 / ボランティア / 管理者]) -->|HTTP / HTTPS| WebServer["Web Applications<br>(Apache Tomcat 11 / Java 25)"]
    WebServer -->|Jakarta Servlet 6.1 / JSP| AppLogic["MVC Controller / DAO"]
    AppLogic -->|JDBC Connection| DB[("PostgreSQL 18.1<br>(orders / order_details / items)")]
```

---

## 🌐 動作確認（デモ環境）

AWS上にデプロイしており、実際に動作をご確認いただけます。

👉 **[「やくそくん」デモサイトはこちら](http://13.193.142.78/yakusokun)**  
*(※別タブで開く場合は `Ctrl + クリック` / `Cmd + クリック` 推奨)*

> **テスト用ログイン情報**  
> * **ID**: `guest_user@example.com`  
> * **パスワード**: `password123`

---

## 📖 要件定義書・画面設計書

👉 **[Web版 要件定義書・画面設計書はこちら（GitHub Pages）](https://hadano-nobuyuki.github.io/project/)**  
*(※リンクを別タブで開く場合は `Ctrl + クリック`（Macは `Cmd + クリック`）してください)*  
*(※システム仕様・各画面イメージ・業務フローの詳細をWebページ形式でご覧いただけます)*

---

## 🛠️ ローカル環境での実行・セットアップ手順

ローカル環境で本プロジェクトを実行する場合は、以下の環境準備、データベースのセットアップ、APIキーの設定、およびデータベース接続設定が必要です。

### 1. 前提条件
* **Java**: JDK 25
* **Webコンテナ**: Apache Tomcat 11
* **データベース**: PostgreSQL 18.1
  * ※ プログラムを実行する際に必要な環境として、データベースのテーブル生成用DDL（[`DDL.sql`](DDL.sql)）をプロジェクトルート直下に公開・同梱しています。
* **Gemini APIキー**: Google AI Studio等で取得したAPIキー

### 2. データベースの構築（テーブル生成用DDLの実行）
プログラムの実行に必要なテーブル群を生成するため、公開しているテーブル生成用DDL（[`DDL.sql`](DDL.sql)）を実行してください。

1. PostgreSQLにて任意のデータベース（例: `yakusokun`）を作成します。
2. 作成したデータベースに対して、プロジェクトルート直下の [`DDL.sql`](DDL.sql) を実行してテーブルを作成します。  
   *(※ A5:SQL Mk-2、pgAdmin、または `psql` コマンドライン等から実行可能です)*

### 3. 環境変数の設定（Gemini APIキー）
AIアドバイス機能を利用するためには、**Gemini APIキーの指定が必要**です。  
OSまたは実行環境の環境変数 **`GEMINI_API_KEY`** に取得したAPIキーを登録してください。

* **Windows (PowerShell)**:
  ```powershell
  # 永続設定（ユーザー環境変数）
  [System.Environment]::SetEnvironmentVariable('GEMINI_API_KEY', 'your_gemini_api_key_here', 'User')

  # または現在のセッションのみ一時設定
  $env:GEMINI_API_KEY="your_gemini_api_key_here"
  ```
* **Linux / macOS (Bash / Zsh)**:
  ```bash
  export GEMINI_API_KEY="your_gemini_api_key_here"
  ```
> *(※ TomcatなどのAPサーバを起動する実行環境から本環境変数が参照できるように設定してください)*

### 4. データベース設定ファイルの作成
セキュリティ保護のため設定ファイル自体はリポジトリ管理外となっています。  
`/src/main/java/` 配下に `db.properties` を作成し、ご自身のローカルDB環境に合わせて接続情報を設定してください。

> **リポジトリ内に `db.properties.sample` を用意していますので、リネームしてご利用いただけます。**

#### `db.properties` の記述例
```properties
db.url=jdbc:postgresql://localhost:5432/データベース名
db.user=ユーザ名
db.password=パスワード
db.driver=org.postgresql.Driver
```

---

## 💡 工夫した点

### 1. AIを活用した家計状況の評価
* **Gemini API** を使用し、ユーザーの支出データから支出傾向や改善ポイントを自動分析・評価させる仕組みを構築しました。天候情報と組み合わせるなど、実践的な節約アドバイスが得られるように工夫しています。

### 2. プログラミングの効率化
AI（Antigravity）にコーディングを実施させることで、開発効率を大幅に高める施策をとりました。

* **アプローチ内容**:
  * 要件定義書からプログラム設計書を作成
  * プログラム設計書を基にAIにてコーディングを実施
  * AIが生成したプログラムを確認し、改善箇所を抽出して対策を実施  
    *(※ 着目した改善箇所：セキュリティ上のリスク、性能向上箇所の有無)*

---

## 🧗 苦労した点・得られた教訓

### AIが生成するプログラムの品質確保
プログラム設計書の記載内容に曖昧な箇所があると、生成されるプログラムに想定外のロジックが組み込まれる事象が多発しました。  
その都度プログラム設計書を加筆修正し、AIにてプログラムの再生成を実施する作業を繰り返しました。

この経験から、以下の教訓を得ることができました。
1. **プログラム設計書が満たすべき必要十分条件**
2. **プログラムを修正する際にはプログラム設計書へのフィードバックが重要であること**
3. **全機能を再作成させるか、一部機能のみを再作成するかの判断基準の必要性**

これらの教訓は、実務におけるAI協調型開発や設計書駆動開発においても非常に役立つ知見であると確信しています。
