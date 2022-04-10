---
title: "Xserver Domain で取得したドメインを使って GitHub Pages でサイトを公開する方法"
date: 2022-04-15T00:45:00+09:00
description: TBD
tags:
  - RESTfulAPI
  - 設計
  - サーバーサイド
---

## はじめに
ブログを公開する方法は様々ありますが、 GitHub Pages を使うことで無料で始めることができます。
無料でブログを公開する場合、`{user_name}.github.io` といったサブドメインをブログのURLに使用することになります。
HTTPSへの対応も自動で行うことができ大変便利なのですが、ひとつ問題があります。
それは、Google AdSense での収益化ができない点です。
Google AdSense ではサブドメインでの申請はできないため、自分でドメインを取得してブログを公開しなければなりません。
この記事では Xserver Domain を使ってドメインを取得し、GitHub Pages のブログにカスタムドメインを設定する方法を紹介します。

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
### ドメインの取得
### DNS と GitHub Pages の設定
### ブログのHTTPS化
ｆ

## まとめ

## 参考記事

## 注釈
