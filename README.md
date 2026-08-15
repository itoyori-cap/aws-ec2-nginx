# AWS EC2 + Nginx 構築記録

## 概要
AWS上にEC2インスタンスを構築し、NginxをインストールしてWebページを公開しました。

## 構成図
[インターネット] → [VPC] → [パブリックサブネット] → [EC2 (t3.micro)]
↓
[Nginx :80]

## 環境情報

| 項目 | 値 |
|---|---|
| Region | us-east-1 |
| Instance Type | t3.micro |
| AMI | Amazon Linux 2023 |
| Web Server | Nginx |
| Public IP | 54.90.95.221 |

## セキュリティグループ（インバウンド）

| タイプ | ポート | ソース | 用途 |
|---|---|---|---|
| SSH | 22 | 0.0.0.0/0 | サーバー管理 |
| HTTP | 80 | 0.0.0.0/0 | Webアクセス |

## 構築手順

### 1. EC2インスタンスの起動
- AWSマネジメントコンソール → EC2 → インスタンスを起動
- AMI: Amazon Linux 2023
- Instance Type: t3.micro
- キーペア: my-key.pem（RSA, .pem形式）
- セキュリティグループ: SSH(22), HTTP(80) を許可

### 2. SSH接続
```bash
ssh -i ~/.ssh/my-key.pem ec2-user@54.90.95.221
3. Nginxのインストールと起

### 3. Nginxのインストールと起動
sudo dnf install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx

### 4. カスタムページの配置
sudo nano /usr/share/nginx/html/index.html
# （オリジナルHTMLを記述）

### 5. アクセス確認
ブラウザで http://54.90.95.221 にアクセス
トラブルシューティング



問題
原因
解決方法



SSH接続できない
セキュリティグループからSSHルールが消えていた
インバウンドルールにSSH(22)を追加


Nginxが見つからない
Amazon Linux 2023のパッケージ名の問題
sudo dnf install nginx -y で解決


変更したページが反映されない
ブラウザキャッシュ
Ctrl + F5 で強制再読み込み

今後の課題

 Elastic IPの付与（IPアドレスの固定）
 HTTPS対応（Let's Encrypt）
 S3との連携（静的アセットの配置）

作成日
2026年8月15日
