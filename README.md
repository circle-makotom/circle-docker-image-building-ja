# CircleCI 上で Node.js のアプリを組み込んだ Docker イメージを作成しデプロイするサンプル

CircleCI 上で Node.js のアプリをビルドし, Docker イメージに組み込んだ上で Azure Container Registry に push, Azure App Service が自動でローリング アップデートを実行するというシナリオのサンプルです.

主に `.circleci/config.yml` がみどころです (CircleCI の設定が書き込まれています). 適宜コメントも書いています.

具体例としては Azure で実装していますが, ビルドの部分は ACR に関係なく流用できます (実際にこのサンプルの最終テストは Docker Hub でやっています). デプロイの部分はデプロイ先やデプロイ パターンに合わせてカスタマイズする必要があります.

ビルドのジョブと平行してテストを実行したり静的解析を実行したりすることで, より充実した CI/CD パイプラインにすることができます.

## その他このアプリに依存するポイント

* アプリは TypeScript で書かれている HTTP サーバーです. `58888/tcp` を listen します.
    * `GET / HTTP/1.1` でバージョン番号を返すようコードされているため, デプロイの確認などに便利です.
    * その他にもいくつかの機能があります. 詳細は `src` 配下を御覧ください.
* アプリのビルド, テストには [Yarn](https://yarnpkg.com/) を使う前提です. 詳細は `package.json` をご覧ください.
* ビルドする Docker イメージの定義は `Dockerfile` をご覧ください.
