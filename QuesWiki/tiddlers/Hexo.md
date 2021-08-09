Hexo

## 安装hexo

```
npm install hexo-cli -g
```

## 初始化hexo

```
hexo init
```

## 安装组件

```
npm install hexo-deployer-git --save
npm install https://github.com/CodeFalling/hexo-asset-image --save
```

## 安装主题

## 利用Github Action自动部署

```yaml
name: HEXO CI

on: 
  push:
    branches: nhexo

jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [10.x]

    steps:
      - uses: actions/checkout@v1
        with:
          ref: nhexo

      - name: Use Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v1
        with:
          node-version: ${{ matrix.node-version }}

      - name: Configuration environment
        env:
          HEXO_DEPLOY_PRI: ${{secrets.HEXO_DEPLOY_PRI}}
        run: |
          mkdir -p ~/.ssh/
          echo "$HEXO_DEPLOY_PRI" > ~/.ssh/id_rsa
          chmod 600 ~/.ssh/id_rsa
          ssh-keyscan github.com >> ~/.ssh/known_hosts
          git config --global user.name 'Jvcon'
          git config --global user.email 'Jvcon@users.noreply.github.com'
          npm i -g hexo-cli
          npm i
          npm install hexo-wordcount --save
          npm install hexo-generator-json-content --save
          npm install hexo-generator-feed --save
          npm install hexo-generator-sitemap --save
          npm install hexo-translate-title --save

      - name: Deploy hexo
        run: |
          hexo g -d

```