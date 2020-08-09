# Redmine

## 設定

| 項目 | 値 |  
|:-----|:-----|
| ベースAMI | Bitnami Redmine 4.1.1-3 on Debian 10 | 
| EC2インスタンス名 | webbilling-redmine | 
| 管理者ユーザ | user | 
| 管理者パスワード | H7afaGJt6lVg | 
| EC2ユーザ | bitnami | 
| ssh接続 | `ssh -i ~/.ssh/webbilling-ec2.pem bitnami@<ipアドレス>` | 
| コンフィグファイル | /opt/bitnami/apps/redmine/htdocs/config/configuration.yml | 
| SES SMTPサーバ | email-smtp.ap-northeast-1.amazonaws.com | 
| SES SMTPユーザ | AKIAZ2BRXOD7J63RIPER | 
| SES SMTPパスワード | BB5zsLLC1dKhLNwec9Ca8uzVO21uqx3ifGsYecrNTA0l | 

## ログの参照

1. Redmineログ 
```bash
journalctl -u bjournalctl bitnami
``` 

1. アクセスログ
```bash
tail -f /opt/bitnami/apache2/logs/access_log
``` 

## 再起動

```bash
sudo systemctl restart bitnami
``` 

