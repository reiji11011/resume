# 外国人留学生に特化したインターン求人媒体

## 参画期間
2017年10月～2018年3月

## 担当業務
・1人エンジニアとしてプロダクトの0→1を担当  
・技術選定、要件定義、デザイン、設計、開発  

## プロジェクトの背景
・外国人留学生数は2015年以降毎年3万人のペースで増加し、2018年には29万人を突破。  
・日本で働きたい留学生は全体の約64%だが、国内就職率は36%に留まる。  
・日本政府は2020年までに留学生受入れ30万人を目指す「留学生30万人計画」を発表。  
・政府は「日本再興戦略改訂2016」において外国人留学生の国内就職率を3割から5割へ向上させることを閣議決定。  

***留学生は年々増加しているにも関わらず、日本での就労が上手くいっていない現状。  
さらに、日本の人手不足は明白であり、国も注力している領域の1つである。***  

![スクリーンショット 2021-01-15 1 47 18](https://user-images.githubusercontent.com/22842524/104621802-d796bb00-56d3-11eb-90a7-8dd20464d34b.png)
  
出典：[「外国人留学生在籍状況調査」及び「日本人の海外留学者数」等について](https://www.mext.go.jp/a_menu/koutou/ryugaku/__icsFiles/afieldfile/2019/01/18/1412692_1.pdf)  
参考：[人手不足なのに｢外国人留学生｣は就職難だ](https://toyokeizai.net/articles/-/233419)  

## 課題と解決策
・外国人受け入れの課題は「言語」「受け入れ体制（評価制度）」がある。  
・まずは、受け入れのハードルを下げ、受け入れの基準値をつくろう！ということでインターンサイトの着想へと進む。  

# プロジェクト概要
## チームメンバー
社内のメンバーは社長と自分の2名でスタート。  
社長はビジネスサイド全般を担当し、自分は開発責任者として開発全般を担当。  

業務委託のエンジニアをリファラルで採用し、開発チームは計3名体制で取り組む。

会社：2名  
開発チーム：社内1名、社外2名  

## 開発の責務
・最低限のデモプロダクトを作成し、営業活動を開始する。

# 自分の貢献

## ミニマム構成なAWS（EC2＋RDS）
事業の検証フェーズであるため安く、シンプルな構成を目指しました。  
そのため、障害耐性、冗長化、負荷分散、オートスケーリングは非対応となっています。  

![AWS2](https://user-images.githubusercontent.com/22842524/104798883-c81b8d00-580d-11eb-834b-f09c0a099862.png)

### Single-AZ
・本来はMulti-AZで冗長的な構成にすることにより、障害対応やバックアップ体制を取るのが一般的かと思いますが、利用料金が2倍になるため今回は実装しませんでした。  
障害対応：  
バックアップ対応：  

### 1台のEC2にELBの導入
・1台のEC2ですがELBを導入しました。下記点をメリットとして感じたためです。
- ACMの無料SSL証明書が利用でき、自動更新で管理できる。
- 「ELBのヘルチェック+CloudWatchアラーム」を利用したwebサーバーの死活監視。
- システム負荷が高くなった場合にスケールアップだけではなくスケールアウトを考慮した拡張性。

### Nginx + Unicorn + Capistrano3
Nginx、Unicornの構築を行いました。  
また、デプロイの一連の流れが地味に工数を取るためCapistrano3での自動化を行いました。  

## 開発体制の構築
1人エンジニアの開発の中で、自分の技術力・経験値の少なさは「セキュリティリスク、開発のアンチパターンの実装、技術的負債」などのリスクを抱えていました。  
また、根性では乗り越えることが出来ないバグの壁にもぶつかり、開発スピード向上を考えると対策を打つ必要がありました。

### 開発メンターの巻き込み
開発スピードを考えた時に、立ちはだかったのがバグです。バグに関して社内では相談する相手がいないため、詰まったら一生詰まる状況でした。  
そのため、外部で相談できる人を見つけるべく下記に取り組みました。  
- エンジニアのシェアハウスに住む。
- もくもく会への参加。
- インターン先（株式会社div）でのエンジニアとの交流。
積極的に外部との交流を行うことによって、常時3名以上に相談ができる状況をつくりました。  
今思い出しても、当時相談に乗っていただいた方々には感謝してもしきれません。  

### 業務委託でのエンジニア採用
開発スケジュールに対してメンバーのリソースが足りていなかったため、業務委託のメンバーの採用、契約締結を行いました。  
SNSツールや知り合いの紹介経由で2名の採用に成功をしました。（自分経由は1名採用）  

### 約30冊の書籍購入
知識・経験値を埋めるために書籍を大量購入しました。  
技術書は高いので一気に貯金が減り、ひもじい生活へと突入しました。  

## プロトタイピングツールを使った要件の擦り合せ
モックはProttにて作成し、手書きに比べてより具体的にイメージを擦り合せできる体制をつくりました。  

デザインは既存のサービスを3つベンチマークとして選定し、抽象化して模倣することにより1からデザインをつくる工数を抑えました。  
また、webデザインの4原則を意識してデザインを作成しました。  
