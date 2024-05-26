# 基本的なコマンドについて学ぶ
# FROM , COPY , RUN , CMD , WORKDIR , ENV , USER

# ベースとなるDockerImageを指定。公式で提供されているImageを使用するのが一般的。
# ベースイメージとも言う。
FROM node

# Docker内で使用する環境変数を定義
ENV NODE_ENV=production

# コマンドを実行する際に基準とするディレクトリの指定。
# 存在しないディレクトリを指定すると自動で作成される。デフォルトだと/が設定されているため、最悪の場合既存のディレクトリを上書きしてコンテナを起動できなくなってしまうので注意。
WORKDIR /scripts

# Docker内へホストのファイルやディレクトリをコピー。
# 第一引数はホスト側のディレクトリ。第二引数はDocker側のディレクトリを指定。
# 下記の場合、ホスト側はdocker buildで指定したディレクトリ、Docker側はWORKDIRで指定したディレクトリを参照
COPY . .

# Docker内でコマンドを実行。
# コンテナへ依存するライブラリやパッケージのインストール、ユーザーの設定などを記述する
RUN npm install \
 && groupadd app \
 && useradd -g app -m app \
 && mv /root/.config /home/app/ \
 && chown -R app:app /scripts /home/app/.config

#  DockerImageの起動時にログインするユーザーの指定。
# デフォルトではrootのため、セキュリティの観点から別のユーザーを指定すべき。
USER app

# 起動時にデフォルトで実行されるコマンドの定義。
CMD ["npm", "start"]