# Zscaler-Tips
Zscalerに関する主な製品、機能、技術についてまとめていきます。

## Zscalerについて

https://www.zscaler.jp/  
Gartner社のマジッククワドラント　2020年SWG(Secure Web Gateway)部門で唯一のリーダーを獲得

## Zscalerのサービス

[ZIA(Zscaler Internet Access)](https://www.zscaler.jp/products/zscaler-internet-access)・・・Secure Web Gateway製品でありクラウドでの出口対策機能を提供  

[ZPA(Zscaler Private Access)](https://www.zscaler.jp/products/zscaler-private-access)・・・Identity Aware Proxy製品であり安全なリモートアクセス機能を提供  

## エージェントソフト(Client Connector)対応端末

| OS | 対応可否 |
| ------------- | ------------- |
| Windows  | ○  |
| Mac  | ○  |
| iOS  | ○  |
| Android  | ○  |

詳細はこちらを参照　　
https://www.zscaler.jp/products/zscaler-client-connector

## SAML対応状況

Zscalerは管理者画面およびユーザ利用にてSAML SSOが利用可能

※2021年2月時点での対応可能idP
+ Active Directoryフェデレーションサービス（AD FS）
+ Azure Active Directory（Azure AD）
+ CAシングルサインオン（CA SSO）
+ グーグルアプリ
+ Okta
+ OneLogin
+ PingFederate

参考ドキュメント  https://help.zscaler.com/zia/configuring-saml

## ZIA (Zscaler Internet Access)

主要なキャリアがバックボーンとして採用しているサービスでもあり、インフラ基盤や低遅延通信などはどのSWGよりも強い部分だと感じています。  

詳しくは[サイトHP](https://www.zscaler.jp/products/zscaler-internet-access)を見ていただきたいのですが、機能としては以下を提供しています。  

+ セキュアWebゲートウェイ
+ クラウドファイアウォール
+ Cloud IPS
+ Cloud Sandbox
+ クラウドアクセスセキュリティブローカ（CASB：Cloud Access Security Broker）
+ Cloud DLP
+ クラウドアプリケーションコントロール
+ 帯域幅コントロール
+ クラウドブラウザ分離（アイソレーション）
+ クラウドセキュリティポスチャ管理（CSPM）

## ZPA (Zscaler Private Access)

企業のオンプレ環境、AWS、Azure上に連携用のVMを立て、外部から安全な通信をアプリケーションレベルで実現出来ます。

ポイントは、リモートアクセス製品にも関わらず連携用のVMを外部に公開せずにリモートアクセス出来る点だと思います。  
（TCP443ポートの外部向け通信のみ）

こういったIAP製品で良いと思う点は、SSL-VPN製品と比べて動作するレイヤが異なり必要な通信のみをアプリケーションレベルで許可する仕様ということです。

仮にリモートワークで使用している端末がウィルス感染し、企業のオンプレ環境に対してポートスキャンを仕掛けられた場合、SSL-VPNはL3、L4レベルの通信が通ってしまうので開放状況が分かってしまうのですが、IAP製品の場合はTLS1.2のトンネルのためレイヤが異なりポートスキャンに対しては何も反応を返すことはありません。

また、ポリシーの構造として、「誰が」「どのデバイスが」「どのネットワークで」など定義することが出来ますので、ゼロトラスト アーキテクチャ実現のためのコンポーネントとして重要な役割を担う製品です。

なお、OktaやAzureADなどのIDaaS製品と組み合わせが必須となる製品となりますのでご注意ください。
