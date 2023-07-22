`jets new demo-ruby-jets --mode api`
`jets g scaffold post title:string`
database.ymlと.envを編集
`jets db:create`
`jets db:migrate`

`jets c`
Post.create(title: 'my first post')

`jets s`
http://127.0.0.1:8888/postsにアクセスし、JSONのレスポンスが返ってくることを確認
