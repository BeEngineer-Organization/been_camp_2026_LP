# BeEngineer合宿案内サイト - プロジェクト詳細

## 基本情報

- **テンプレートファイル**: 参考なし（新規作成）
- **プロジェクト名**: BeEngineer合宿案内サイト
- **プロジェクトタイトル**: BeEngineer Programming Camp - ロゴスランド合宿案内Webサイト

## 画像リソース

- **画像フォルダパス**: `assets/` 配下
  - `assets/fav/` - ロゴ・ファビコン
  - `assets/logos/` - フロアマップ画像
  - `blog/images1/`, `blog/images2/`, `blog/images3/` - ブログ用写真
- **使用する画像枚数**: 多数（ロゴ、フロアマップ、ブログ写真など）

## プロジェクト詳細

### プロジェクト概要

BeEngineerプログラミング合宿（2025年11月22日〜24日）の案内用Webサイトです。ロゴスランド京都で開催される2泊3日の合宿に向けて、参加者に必要な情報を分かりやすく提供することを目的として開発されました。HTML5、CSS3、Vanilla JavaScriptを使用した静的サイトで、レスポンシブデザインに対応しています。

### 開発目的

- 合宿参加者への情報提供を効率化する
- レスポンシブデザインによるPC・タブレット・スマホ対応の実現
- フレームワークを使わない軽量なサイトの構築
- 持ち物チェックリストなど、実用的な機能の実装
- ロゴスランド風の温かみのあるデザインの実現

### 使用技術

**プログラミング言語**
- HTML5
- CSS3
- JavaScript (ES6+)

**フロントエンド**
- Vanilla JavaScript（フレームワーク不使用）
- CSS Custom Properties（CSS変数）
- CSS Grid / Flexbox
- Intersection Observer API

**その他**
- localStorage（チェックリスト状態保存）
- Google Maps API（地図埋め込み）
- GitHub Pages（デプロイ環境）

### 主な機能

**1. レスポンシブナビゲーション**
- PC版：固定サイドバーナビゲーション
- SP版：ハンバーガーメニューによるスライドメニュー
- サブメニュー対応（ブログメニュー）
- スクロールスパイ機能（現在のセクションをハイライト）

**2. インタラクティブなUI要素**
- スケジュール表のタブ切り替え（1日目/2日目/3日目）
- アクセス方法のタブ切り替え（車/電車・バス/京都駅）
- フロアマップのタブ切り替え（1F/2F/3F）
- SP版でのアコーディオン形式のコンテンツ展開

**3. 持ち物チェックリスト機能**
- localStorageによるチェック状態の自動保存
- ページ再読み込み後も状態を保持
- チェック済み項目の視覚的フィードバック

**4. ブログ機能**
- 日別ブログページ（day1.html, day2.html, day3.html）
- 画像ギャラリー表示
- 前後日へのナビゲーション

**5. スムーススクロール**
- ページ内リンクのスムーズなスクロール
- URL履歴の更新

### システム構成

```
ユーザー
  ↓
index.html（トップページ）
  ├─ サイドバーナビゲーション（script.js制御）
  ├─ ヒーローセクション
  ├─ ご案内セクション
  ├─ 日程・会場セクション
  ├─ 学習プログラムセクション
  ├─ スケジュールセクション（タブ切り替え）
  ├─ フロアマップセクション（タブ切り替え）
  ├─ 持ち物リストセクション（localStorage連携）
  ├─ アクセスセクション（タブ切り替え + Google Maps）
  ├─ 健康管理セクション
  └─ お問い合わせセクション
  ↓
blog/
  ├─ day1.html（1日目のブログ）
  ├─ day2.html（2日目のブログ）
  └─ day3.html（3日目のブログ）
```

**データフロー**
- チェックリスト：ユーザー操作 → localStorage保存 → ページ再読み込み時に復元
- タブ切り替え：クリックイベント → JavaScriptでactiveクラス切り替え → CSSで表示制御
- スクロールスパイ：Intersection Observer → セクション検出 → ナビゲーションのactiveクラス更新

### 工夫した点

**1. フレームワークを使わない軽量設計**
- ReactやVue.jsなどのフレームワークを使用せず、Vanilla JavaScriptで実装
- バンドルサイズを最小限に抑え、高速なページ読み込みを実現
- 依存関係がなく、メンテナンスが容易

**2. レスポンシブデザインの徹底**
- PC版とSP版で異なるUIパターンを採用
  - PC版：固定サイドバー + タブ切り替え
  - SP版：ハンバーガーメニュー + アコーディオン形式
- メディアクエリを活用した段階的なレイアウト調整
- タッチデバイスでの操作性を考慮したUI設計

**3. ユーザビリティの向上**
- localStorageを活用したチェックリストの状態保存
- スムーススクロールによる快適なナビゲーション体験
- スクロールスパイによる現在位置の可視化
- アクセシビリティ対応（キーボードナビゲーション、フォーカス表示）

**4. デザインの一貫性**
- CSS Custom Propertiesによる統一されたカラーパレット管理
- ロゴスランド風の温かみのあるデザイン
- パステルカラーを活用した視覚的な階層構造

**5. 保守性の高いコード構造**
- 機能ごとに分割されたJavaScript関数
- セマンティックHTMLの使用
- コメントによる詳細な説明

### 技術的ハイライト

**1. Intersection Observer APIによるスクロールスパイ実装**

```javascript
const observerOptions = {
  root: null,
  rootMargin: '-20% 0px -70% 0px',
  threshold: 0
};

const observer = new IntersectionObserver(observerCallback, observerOptions);
sections.forEach(section => {
  observer.observe(section);
});
```

スクロール位置に応じて、現在表示されているセクションに対応するナビゲーションリンクを自動的にハイライトする機能を実装。パフォーマンスを考慮し、Intersection Observer APIを使用。

**2. localStorageを活用した状態管理**

```javascript
function initChecklistFeature() {
  checklistItems.forEach(item => {
    const itemKey = item.getAttribute('data-item');
    const savedState = localStorage.getItem(itemKey);
    
    if (savedState === 'true') {
      item.checked = true;
      item.parentElement.classList.add('checked');
    }
  });
}
```

サーバーサイドの実装なしで、クライアント側のみでチェックリストの状態を永続化。ページを閉じても状態が保持される。

**3. CSS Custom Propertiesによるテーマ管理**

```css
:root {
  --color-primary: #0E8B62;
  --color-secondary: #F47F2E;
  --color-accent: #FF6B6B;
  --color-bg: #FAFAF8;
  --border-radius: 16px;
  --shadow-soft: 0 4px 20px rgba(0, 0, 0, 0.08);
}
```

CSS変数を使用することで、カラーパレットやデザイントークンの一元管理を実現。テーマ変更が容易。

### 活用シーン

**1. イベント・合宿の案内サイト**
- 開催情報の一元管理
- 参加者への情報提供
- スケジュールや持ち物リストの共有

**2. 教育機関のイベント告知**
- 学習プログラムの紹介
- 会場情報の提供
- 参加者向けの詳細情報

**3. カスタマイズ可能なランディングページ**
- テンプレートとして再利用可能
- セクションの追加・削除が容易
- デザインのカスタマイズが簡単

### 今後の展望

**短期（1-2ヶ月）**
- パフォーマンス最適化（画像の遅延読み込み、CSS/JSのminify）
- PWA対応（オフライン機能、ホーム画面追加）
- アクセシビリティのさらなる向上（ARIA属性の追加）

**中期（3-6ヶ月）**
- 多言語対応（英語版の追加）
- CMS連携（WordPress等との統合）
- アナリティクス連携（Google Analytics等）

**長期（6ヶ月以上）**
- 管理画面の追加（コンテンツ更新を容易に）
- ユーザー認証機能（参加者限定コンテンツ）
- モバイルアプリ化（React Native等）

### 開発情報

- **開発形態**: 個人開発
- **役割**: フロントエンド開発、UI/UX設計、デザイン実装
- **開発期間**: 2025年11月（約1ヶ月）
- **開発環境**: Visual Studio Code、Git

### デモ動画（オプション）

- **YouTube URL**: （未公開）
- **動画タイトル**: （未作成）

### その他の情報

- **GitHubリポジトリ**: （非公開）
- **デプロイURL**: （GitHub Pages対応可能）
- **特記事項**: 
  - フレームワークを使用しない軽量設計
  - 静的サイトとして動作（サーバーサイド不要）
  - GitHub Pagesでのホスティングに対応
  - モバイルファーストな設計思想

## 技術スタック詳細

### フロントエンド技術

**HTML5**
- セマンティックHTMLの使用（`<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`）
- アクセシビリティ属性の適切な使用（`aria-label`等）

**CSS3**
- CSS Custom Properties（変数）
- CSS Grid Layout
- Flexbox
- CSS Animations & Transitions
- Media Queries（レスポンシブデザイン）
- CSS Selectors（属性セレクタ、疑似クラス等）

**JavaScript (ES6+)**
- Arrow Functions
- Template Literals
- const/let
- Array Methods（forEach, map等）
- Event Listeners
- DOM Manipulation
- Intersection Observer API
- localStorage API

### 開発ツール・環境

- **エディタ**: Visual Studio Code
- **バージョン管理**: Git
- **デプロイ**: GitHub Pages（想定）
- **ブラウザテスト**: Chrome, Firefox, Safari, Edge

## ファイル構成

```
BeEn合宿_案内/
├── index.html              # トップページ
├── styles.css              # メインスタイルシート（約3,400行）
├── script.js               # JavaScript機能実装（約850行）
├── README.md               # プロジェクト説明書
├── SETUP_HASH.md           # セットアップ情報
├── blog/                   # ブログ記事
│   ├── day1.html          # 1日目のブログ
│   ├── day2.html          # 2日目のブログ
│   └── day3.html          # 3日目のブログ
└── assets/                 # アセット管理
    ├── fav/               # ファビコン・ロゴ
    │   ├── BeEngineer_logo.svg
    │   ├── LOGOSLAND_logo.svg
    │   ├── dot_boy.svg
    │   └── dot_girl.svg
    ├── logos/             # フロアマップ画像
    │   ├── floor-1f.jpg
    │   ├── floor-2f.jpg
    │   └── floor-3f.jpg
    └── README.md          # アセット管理ガイド
```

## デザインシステム

### カラーパレット

**メインカラー**
- Primary: `#0E8B62`（緑）
- Secondary: `#F47F2E`（オレンジ）
- Accent: `#FF6B6B`（赤）

**パステルカラー**
- Pastel Blue: `#A8D5E2`
- Pastel Yellow: `#FFF4B8`
- Pastel Pink: `#FFD4D4`
- Pastel Green: `#C8E6C9`

**ニュートラル**
- Background: `#FAFAF8`（ベージュ白）
- White: `#FFFFFF`
- Text: `#333333`
- Text Light: `#666666`

### タイポグラフィ

- **フォントファミリー**: 'Segoe UI', 'Yu Gothic UI', 'Meiryo', sans-serif
- **フォントサイズ**: 
  - ヒーロータイトル: 3rem（PC）/ 2rem（SP）
  - セクションタイトル: 2.5rem（PC）/ 2rem（SP）
  - 本文: 1rem
- **行間**: 1.7

### スペーシング

- **基本単位**: 1rem
- **セクションパディング**: 5rem 3rem（PC）/ 3rem 1.5rem（SP）
- **カードパディング**: 2rem（PC）/ 1rem（SP）
- **ギャップ**: 2rem（PC）/ 1.2rem（SP）

### コンポーネント

**カード**
- 角丸: 16px
- シャドウ: `0 4px 20px rgba(0, 0, 0, 0.08)`
- ホバー時: `translateY(-8px)` + シャドウ拡大

**ボタン**
- 角丸: 50px（ピル型）
- グラデーション背景
- ホバー時: `translateY(-3px)` + シャドウ拡大

## パフォーマンス

- **ページサイズ**: 軽量（フレームワーク不使用）
- **読み込み速度**: 高速（静的ファイルのみ）
- **レスポンシブ対応**: 完全対応（PC/タブレット/スマホ）
- **ブラウザ対応**: モダンブラウザ全対応

## セキュリティ

- 静的サイトのため、サーバーサイドの脆弱性なし
- XSS対策：innerHTMLの使用を避け、textContentを使用
- 外部リソース：Google Maps埋め込みのみ（信頼できるソース）

## まとめ

BeEngineer合宿案内サイトは、フレームワークを使わない軽量な静的サイトとして開発されました。レスポンシブデザイン、インタラクティブなUI、実用的な機能を備えながら、シンプルで保守しやすいコード構造を実現しています。ロゴスランド風の温かみのあるデザインと、ユーザビリティを重視した設計により、参加者にとって使いやすい情報提供サイトとなっています。

