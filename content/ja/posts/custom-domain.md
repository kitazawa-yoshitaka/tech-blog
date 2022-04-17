---
title: "Xserver Domain で取得したドメインを使って GitHub Pages で HTTPS に対応したサイトを公開する方法"
date: 2022-04-17T21:30:00+09:00
description: Xserver Domain を使ってドメインを取得し、GitHub Pages のブログにカスタムドメインを設定する方法を紹介します。また、 HTTPS に対応するために Xserver SSL を使用して Let's Encrypt の証明書を取得します。
tags:
  - GitHub Pages
  - ブログ作成
  - Xserver
  - HTTPS
meta_image: images/card/custom-domain.png
image: images/card/custom-domain.png
---

## はじめに
ブログを公開する方法は様々ありますが、 GitHub Pages を使うことで無料で始めることができます。
無料でブログを公開する場合、`{user_name}.github.io` といったサブドメインをブログのURLに使用することになります。HTTPSへの対応も自動で行うことができ大変便利なのですが、ひとつ問題があります。
それは、Google AdSense での収益化ができない点です。Google AdSense はサブドメインでの申請はできないため、自分で取得したドメインを使ってブログを公開しなければなりません。
この記事では Xserver Domain を使ってドメインを取得し、GitHub Pages のブログにカスタムドメインを設定する方法を紹介します。
ちなみに、このブログも Xserver Domain で取得したドメインを使用して、GihHub Pages でサイトを公開しています。

### 想定読者
GitHub Pages を使ってブログを公開しようとしている人
github.io ドメインでブログを公開している人

## Xserver Domain とは
まずは [Xserver Domain](https://www.xdomain.ne.jp/)について紹介します。
Xserver Domain は独自ドメインを取得することができるサービスで、2022年4月現在 `.com` ドメインを1年間1円で使用する事ができます。（2年目以降の更新料は1298円（税込））
よく比較対象になる[お名前.com](https://www.onamae.com/)は `.com` ドメインの初回1年間は1円で使用できますが、2年目以降の更新料は1,408円となっていて、 Xserver Domain の方が少々お安くなります。
また、ドメインを取得すると Whois にドメイン管理者の情報を公開しなくてはなりません。
個人情報を全世界に公開することに抵抗がある方は、[Whoisの代行公開サービス](https://www.xserver.ne.jp/manual/man_member_setting_whois.php)を使うことで Whois 公開情報を Xserver.inc 名義に設定することができます。
Xserverではこれを無料で利用することができます。
お名前.comの[Whois情報公開代行](https://www.onamae.com/service/d-regist/option.html)では年間1,078円かかります。
私は費用を抑えることを優先して考えたため、Xserver Domain を使用してドメインを取得することにしました。

## ドメイン取得から設定まで
まずはドメインの取得を行います。
その後、DNS や GitHub Pages の設定変更を行い、最後に HTTPS 通信に対応するための証明書作成を行います。
面倒な部分もありますが、手順通りに設定をすることで独自ドメインでサイトを公開し、 HTTPS にも対応できるようになります。
HTTPS 化することでセキュリティの向上だけでなく、 Google の検索順位の優遇などのメリットもありますので、 HTTPS に対応できるようにしておくことをお勧めします。

### ドメインの取得
1. [Xserver Domain](https://www.xdomain.ne.jp/)のサイトで取得したいドメイン名を入力してドメインの空きを確認してください。
後の更新料金や汎用性を考えると `.com` ドメインがおすすめです。
希望するドメインが空いていることを確認できたら画面の指示に従って、アカウント登録とお支払いを行いドメインを取得してください。
1. [Xserver Domain の管理ページ](https://secure.xserver.ne.jp/xapanel/xdomain/index)にログインして、取得したドメインが表示されていることを確認してください。
1. 次に `Whois情報設定` のタブをクリックして、Whois代理公開設定を `ON` にします。
これで自分自身の個人情報を世界に公開することなく、Xserver 側が代理で Whois に情報を公開してくれます。
{{< img src="/images/posts/custom-domain/Whois.png" alt="Whois image" width="700px" position="center" >}}
1. 最後にネームサーバーの設定を行います。
`ネームサーバー設定` のタブをクリックして、ドメイン適用先サービスを `Xserver Domain` にして画面の指示通りに登録してください。
GitHub Pages でページを公開する場合、 Xserver のレンタルサーバーなどは使用しないためドメインのみの利用となります。
{{< img src="/images/posts/custom-domain/NameServer.png" alt="Name server image" width="700px" position="center" >}}
これで ドメインの取得と初期設定は完了です。

### DNS の設定
1. 新しく取得したドメインに来た通信を GitHub Pages に向けるため、DNSレコードの設定を登録します。
`DMSレコード設定` のタブをクリックして、 `DNSレコード設定を追加する` をクリックしてください。
{{< img src="/images/posts/custom-domain/Domain1.png" alt="Name server image" width="700px" position="center" >}}

以下の種別 `A` と `AAAA` のレコードをDNSに追加します。ホスト名と優先度は特に入力する必要はありません。
{{< boxmd >}}
Aレコード  
- 185.199.108.153
- 185.199.109.153
- 185.199.110.153
- 185.199.111.153
{{< /boxmd >}}
{{< boxmd >}}
AAAAレコード
- 2606:50c0:8000::153
- 2606:50c0:8001::153
- 2606:50c0:8002::153
- 2606:50c0:8003::153
{{< /boxmd >}}

最終的には以下の画像のようになっていればOKです。
※ 詳細は[GitHub Pages カスタムドメインの設定](https://docs.github.com/ja/enterprise-cloud@latest/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)の `Apexドメインを設定する` に記載されています。
{{< img src="/images/posts/custom-domain/Domain2.png" alt="Name server image" width="700px" position="center" >}}
これで DNS の設定は完了です。

### HTTPS に対応するための証明書の取得と設定
1. 無料で証明書を発行するために [Xserver SSL](https://ssl.xdomain.ne.jp/) のアカウントを作成し、SSL証明書の申し込みを行います。
ブログであれば証明書のブランドは `Let's Encrypt` で問題ありません。無料ではじめられますので、まずはこれで良いと思います。
1. 指示通りに進めていくと証明書発行時の認証方法を選択する画面になります。 `DNS認証` を選択して、表示されたレコードを Xserver Domain の DSNに登録してください。
{{< img src="/images/posts/custom-domain/DNSCertification.png" alt="Name server image" width="700px" position="center" >}}
1. DNS に CNAME レコードを追加して、 www サブドメインを利用できるようにします。
Xserver Domain の DNS に 下記のレコードを登録してください。
※ 詳細は[GitHub Pages カスタムドメインの設定](https://docs.github.com/ja/enterprise-cloud@latest/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)の `Apexドメインとwwwサブドメイン付きのドメインの設定` に記載されています。
{{< boxmd >}}
- ホスト名： www.取得したホスト名
- 種別： CNAME
- 内容： あなたのGitHubアカウント名.github.io
- 優先度： 入力不要
{{< /boxmd >}}
1. 最後に GitHub Pages 側に設定を行い、取得したドメインでサイトにアクセスできるようにします。
GitHub Pages を設定している GitHub リポジトリにアクセスし、Setting、Pages をクリックしてください。
Custom domain に取得したドメインを入力し、 アクティブになるまで数分待ち時間が発生します。
画面上部のステータスが緑になったら、Enforce HTTPS にチェックを付けます。
{{< img src="/images/posts/custom-domain/GitHubSetting.png" alt="Name server image" width="700px" position="center" >}}

これでサイトを Xservr Domain で取得したドメインで公開し、HTTPSにも対応した状態になりました。
実際にサイトにアクセスして正しく表示されることを確認してください。

## まとめ
GitHub Pages で公開するサイトを独自ドメインをつかって HTTPS で公開する方法を記載しました。
Xserver Domain や Xserver SSL を使ってドメイン取得や証明書取得をする方法について、中々記事が見つからなかったので自分で記事を書いてみました。
この方法で実現することで格安でサイトを公開することができます。
専門知識が必要なところなので悩んでいる方がいましたら参考になると幸いです。
