# Blog

基于 Hugo 的个人博客，使用自定义 `paper` 主题并部署到 Vercel。

## 本地预览

需要 Hugo `0.139.0` 或兼容版本。

```sh
hugo server -D
```

## 构建

```sh
hugo --minify
```

Vercel 部署时会通过 `VERCEL_PROJECT_PRODUCTION_URL` 自动设置 `baseURL`。如果使用自定义域名，建议在 Vercel 环境变量中设置：

```sh
HUGO_BASEURL=https://your-domain.example/
```
