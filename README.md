# Jetsプロジェクトの開始

`jets new demo-ruby-jets --mode api`
`jets g scaffold post title:string`
database.ymlと.envを編集
`jets db:create`
`jets db:migrate`

`jets c`
Post.create(title: 'my first post')

`jets s`
http://127.0.0.1:8888/postsにアクセスし、JSONのレスポンスが返ってくることを確認



# RDSとの接続

AWSコンソールにログインし、IAMポリシーとIAMユーザを作成
参考：https://www.takayasugiyama.com/entry/2020/06/13/070000#%E3%83%9D%E3%83%AA%E3%82%B7%E3%83%BC%E3%81%A8%E3%83%A6%E3%83%BC%E3%82%B6%E3%83%BC%E3%81%AE%E4%BD%9C%E6%88%90

IAMユーザのアクセスキーを発行し、AWS CLIに設定

RDSを作成
RDSのセキュリティグループを追加
インバウンドルール：TCP 3306 マイIP

RDSへの接続設定
config.function.vpc_config
database.yml
.env

ローカルからRDSへの接続確認
```bash
JETS_ENV=production jets db:create db:migrate
JETS_ENV=production jets s
```
http://localhost:8888/posts





# トラブルシューティング

```bash
Signature expired: 20230723T044619Z is now earlier than 20230729T011204Z (20230729T012704Z - 15 min.) (Aws::STS::Errors::SignatureDoesNotMatch)
```

WindowsOSでWSL2を使用していると、スリープ時に時計が止まってしまい、AWSの時計と差異があるとエラーになる

```bash
sudo ntpdate ntp.nict.jp
```
ntpで日本時間を設定しなおす
