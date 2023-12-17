FROM node:18 AS base
CMD [ "bash" ]

# Build
FROM base AS test-and-build
COPY . /workspace
# RUN npm ci && npm run buildするためにディレクトリを移動
WORKDIR /workspace
ARG REACT_APP_API_SERVER
# npm install より厳密に依存関係を保持できる
RUN npm ci && npm run test && npm run build

# Hosting in nginx
FROM nginx:latest AS production
# nignxのお作法
# /var/wwwの中のリソースをHTTPサーバーとしてwebに公開する
COPY --from=test-and-build /workspace/build /var/www
COPY nginx.conf /etc/nignx/conf.d/default.conf
