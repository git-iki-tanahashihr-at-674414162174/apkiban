# AWS 検証環境情報

## INDEX

1. [準備](#準備)
1. [bastionへの接続](#bastionへの接続)
1. [CodeComit](#CodeComit)
1. [Oracleへの接続](#Oracleへの接続)
1. [SES](#SES)
1. [AmazonConnect](#AmazonConnect)
1. [KMS](#KMS)

## 準備

### google authentiatorのインストール

iOS, Android端末に`google authentiator`をインストールしておく。

## AWSアカウントへのMFA追加

MFA用のQRコードをメールで送付するので`google authentiator`に読み込ませておいてください。


## bastionへの接続

1. 以下のQRコードを`google authentiator`に読み込ませておく
![](images/qr.png)

1. `git bash`などからssh 接続（`putty`などから接続する場合、鍵の場所を指定してください）
```bash
ssh -i ~/.ssh/bastion-user.pem bastion-user@54.250.84.194
```
	- `.bashrc`に`alias ssh='ssh -o ServerAliveInterval=60'`を書いておくとSSHのセッションが切れることを防止できます。

1. `google authentiator`に表示されたPINを入力する
```bash
Verification code:
```

1. 踏み台からworkサーバへの接続  
```bash
ssh -i ~/.ssh/developer.pem developer@172.17.1.231
```
	- 踏み台での作業は、ホームディレクトリの下に「kondoukta」や「sugiyamasi」などの自分用のディレクトリを作成して作業してください。
	- IPアドレスは変わることがあるため、ログインできない場合は、AWSのマネコンのEC2画面で`webbilling-work`サーバのローカルIPアドレスを確認して下さい。

## CodeComit

### リポジトリ

| リポジトリ | 用途 | URL | 
|:-----|:-----|:-----|
| webbilling | コード管理 | https://git-codecommit.ap-northeast-1.amazonaws.com/v1/repos/webbilling |
| webbilling-doc | ドキュメント管理 | https://git-codecommit.ap-northeast-1.amazonaws.com/v1/repos/webbilling-doc |
| webbilling-exeo | コード管理 | https://git-codecommit.ap-northeast-1.amazonaws.com/v1/repos/webbilling-exeo |
| webbilling-exeo-doc | ドキュメント管理 | https://git-codecommit.ap-northeast-1.amazonaws.com/v1/repos/webbilling-exeo-doc |
| webbilling-iki | コード管理 | https://git-codecommit.ap-northeast-1.amazonaws.com/v1/repos/webbilling-iki |
| webbilling-iki-doc | ドキュメント管理 | https://git-codecommit.ap-northeast-1.amazonaws.com/v1/repos/webbilling-iki-doc |

### gitリポジトリのクローン  

```bash
git clone <上記のURL>
```
プロンプトでID/PWが求められるので、`****_codecommit_credentials.csv`中の`User Name`と`Password`を入力して下さい。

## Oracleへの接続

### 設定情報

| 項目 | 値 | 
|:-----|:-----|
| エンドポイント | webbillng-db.cyqckoqjqzte.ap-northeast-1.rds.amazonaws.com |
| ポート | 1521 |
| SID | ORCL |
| ユーザID | admin |
| パスワード | webbillng-oracle |

### DBへの接続

```bash
sqlplus admin@webbillng-db.cyqckoqjqzte.ap-northeast-1.rds.amazonaws.com:1521/ORCL
```

## SES

| 項目 | 値 | 
|:-----|:-----|
| ドメイン | nttd-m-finance.com |
| SPF設定 | "v=spf1 include:amazonses.com -all" |
| DKIM設定 | なし |
| 制限解除 | 未解除 ※ |

※ 送信制限の解除をしていないため、メールの送信テストをする場合は、SESの画面から「Verify a New Email Address」で送信先のメールアドレスを登録する必要があります。

## AmazonConnect

| 項目 | 値 | 
|:-----|:-----|
| インスタンス | webbilling |
| アクセス URL | https://webbilling.awsapps.com/connect/home |
| 電話番号 | +81 50-3183-0461 |
| 管理者ユーザ | admin |
| 管理者パスワード | 48B2ZbudJ8FK |

## KMS

| 項目 | 値 | 
|:-----|:-----|
| CMK | 024fd067-1361-48da-8f89-f7d8694c80f9 |
| Data Key ID | arn:aws:kms:ap-northeast-1:674414162174:key/024fd067-1361-48da-8f89-f7d8694c80f9 |
