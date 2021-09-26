# 使用nginx部署多个vue项目
1.设置路由路径
```
new Router({
  mode: 'history',
  base: 'cms', //配置前端路由基础路径
  routes: []
})
```
2.设置打包后项目的相对路径
```
//webpack中
  assetsPublicPath=‘cms’
//vue-cli中
  publicPath=‘cms’
```
3.nginx配置
```
server {
  listen       80;
  server_name  localhost;
  location /app {
    alias /usr/www/app/;
    index  index.html index.htm;
    try_files $uri /app/index.html;
    index  index.html;
  }
  location /cms {
    alias /usr/www/cms/;
    index  index.html index.htm;
    try_files $uri /cms/index.html;
    index  index.html;
  }
  location /api {
    proxy_pass http://127.0.0.1:8018;
  }
}
```
