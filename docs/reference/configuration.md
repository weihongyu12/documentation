---
sidebar_position: 4
toc_min_heading_level: 2
toc_max_heading_level: 5
---

# 参考配置

import TOCInline from '@theme/TOCInline';

<TOCInline toc={toc} />

## package.json

```json
{
  "scripts": {
    "start": "node scripts/start.js",
    "build": "node scripts/build.js",
    "test": "node scripts/test.js",
    "lint": "npm run lint:js && npm run lint:css",
    "lint:js": "eslint ./src/**/*.{js,jsx,ts,tsx}",
    "lint:css": "stylelint ./src/**/*.{css,scss,jsx,tsx}",
    "format": "npm run format:js && npm run format:css",
    "format:js": "npm run lint:js -- --fix",
    "format:css": "npm run lint:css -- --fix",
    "styleguidist": "styleguidist server",
    "styleguidist:build": "styleguidist build",
    "changelog": "conventional-changelog -p angular -i CHANGELOG.md -s",
    "analyze": "source-map-explorer 'build/static/js/*.js'"
  },
  "lint-staged": {
    "src/**/*.{js,jsx,ts,tsx,json,css,scss}": ["npm run format", "git add"]
  },
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged",
      "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
    }
  }
}
```

## Vue & Webpack

:::tip
- [https://next.cli.vuejs.org/zh/config/](https://next.cli.vuejs.org/zh/config/)
- [https://webpack.js.org/configuration/](https://webpack.js.org/configuration/)
:::

### Preload/Prefetch 配置

(TODO)

### Brotli & Gzip 预压缩配置

```js
// vue.config.js

const { defineConfig } = require('@vue/cli-service');
// $ npm install compression-webpack-plugin --save-dev
const CompressionPlugin = require('compression-webpack-plugin');

module.exports = defineConfig({
  configureWebpack: (config) => {
    const basePlugins = [];
    let productionPlugins = [];

    if (process.env.NODE_ENV === 'production') {
      productionPlugins = [
        // brotli 预压缩
        new CompressionPlugin({
          filename: '[path][base].br[query]',
          algorithm: 'brotliCompress',
          test: /\.(html|js|css|svg|ico|xml|json|wasm|eot|otf|ttf|bmp|md)$/,
          compressionOptions: { level: 11 },
          threshold: 10240,
          minRatio: 0.8,
        }),
        // gzip 预压缩
        new CompressionPlugin({
          filename: '[path][base].gz[query]',
          algorithm: 'gzip',
          test: /\.(html|js|css|svg|ico|xml|json|wasm|eot|otf|ttf|bmp|md)$/,
          compressionOptions: { level: 9 },
          threshold: 10240,
          minRatio: 0.8,
        }),
      ];
    }

    return {
      plugins: [
        ...basePlugins,
        ...productionPlugins,
      ],
    };
  },
});
```

### Crossorigin & SRI 配置

```js
// vue.config.js

const { defineConfig } = require('@vue/cli-service');

module.exports = defineConfig({
  crossorigin: 'anonymous',
  integrity: true,
});
```

### Imagemin 图片压缩配置

```js
// vue.config.js

const { defineConfig } = require('@vue/cli-service');
// npm install image-minimizer-webpack-plugin imagemin --save-dev
//
// 无损压缩（推荐）：
// npm install imagemin-gifsicle imagemin-jpegtran imagemin-optipng imagemin-svgo --save-dev
//
// 有损压缩：
// npm install imagemin-gifsicle imagemin-mozjpeg imagemin-pngquant imagemin-svgo --save-dev
//
// WebP格式转化（推荐）：
// npm install imagemin-webp --save-dev
const ImageMinimizerPlugin = require('image-minimizer-webpack-plugin');

module.exports = defineConfig({
  configureWebpack: (config) => {
    return {
      optimization: {
        minimizer: [
          new ImageMinimizerPlugin({
            minimizer: {
              implementation: ImageMinimizerPlugin.imageminMinify,
              options: {
                // 使用自定义选项进行无损压缩优化
                plugins: [
                  ['gifsicle', { optimizationLevel: 3, interlaced: true }],
                  ['jpegtran', { progressive: true }],
                  ['optipng', { optimizationLevel: 7 }],
                  // Svgo configuration here https://github.com/svg/svgo#configuration
                  [
                    'svgo',
                    {
                      plugins: [
                        {
                          name: 'preset-default',
                          params: {
                            overrides: {
                              removeViewBox: false,
                              addAttributesToSVGElement: {
                                params: {
                                  attributes: [
                                    { xmlns: 'http://www.w3.org/2000/svg' },
                                  ],
                                },
                              },
                            },
                          },
                        },
                      ],
                    },
                  ],
                ],
              },
            },
            generator: [
              {
                // 可以使用“?as=webp”生成器，生成 WebP 图片格式
                preset: 'webp',
                implementation: ImageMinimizerPlugin.imageminGenerate,
                options: {
                  plugins: [['imagemin-webp', { quality: 100, lossless: true }]],
                },
              },
            ],
          }),
        ],
      },
    };
  },
});
```

## Babel

:::tip
- [https://babeljs.io/docs/en/config-files](https://babeljs.io/docs/en/config-files)
- [https://next.cli.vuejs.org/zh/config/#transpiledependencies](https://next.cli.vuejs.org/zh/config/#transpiledependencies)
:::

```js
// vue.config.js

const { defineConfig } = require('@vue/cli-service');

module.exports = defineConfig({
  transpileDependencies: true,
});
```

## Nginx

:::tip
可参考 [HTML5 Boilerplate nginx 配置](https://github.com/h5bp/server-configs-nginx)
:::

:::details 完整版 nginx.conf 配置
```
# For more information on configuration, see:
#   * Official English Documentation: http://nginx.org/en/docs/
#   * Official Russian Documentation: http://nginx.org/ru/docs/

user nginx;
worker_processes auto;
error_log  /var/log/nginx/error.log notice;
pid        /var/run/nginx.pid;

# Load dynamic modules. See /usr/share/doc/nginx/README.dynamic.
# include /usr/share/nginx/modules/*.conf;

load_module /usr/lib/nginx/modules/ngx_http_brotli_filter_module.so;
load_module /usr/lib/nginx/modules/ngx_http_brotli_static_module.so;
load_module /usr/lib/nginx/modules/ngx_http_modsecurity_module.so;

events {
    worker_connections 1024;
}

http {
    server_tokens off;

    charset       utf-8;
    charset_types text/css text/plain text/vnd.wap.wml text/javascript text/markdown text/calendar text/x-component text/vcard text/cache-manifest text/vtt application/json application/manifest+json;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile            on;
    tcp_nopush          on;
    tcp_nodelay         on;
    keepalive_timeout   65;
    types_hash_max_size 2048;

    include             /etc/nginx/mime.types;
    default_type        application/octet-stream;

    # Load modular configuration files from the /etc/nginx/conf.d directory.
    # See https://nginx.org/en/docs/ngx_core_module.html#include
    # for more information.
    include /etc/nginx/conf.d/*.conf;

    set $compression_types
      application/atom+xml
      application/geo+json
      application/javascript
      application/x-javascript
      application/json
      application/ld+json
      application/manifest+json
      application/rdf+xml
      application/rss+xml
      application/vnd.ms-fontobject
      application/wasm
      application/x-web-app-manifest+json
      application/xhtml+xml
      application/xml
      font/eot
      font/otf
      font/ttf
      image/bmp
      image/svg+xml
      image/vnd.microsoft.icon
      image/x-icon
      text/cache-manifest
      text/calendar
      text/css
      text/javascript
      text/markdown
      text/plain
      text/xml
      text/vcard
      text/vnd.rim.location.xloc
      text/vtt
      text/x-component
      text/x-cross-domain-policy;

    map $sent_http_content_type $cache_control {
        default                           "public, immutable, stale-while-revalidate";

        # No content
        ""                                "no-store";

        # Manifest files
        ~*application/manifest\+json      "public";
        ~*text/cache-manifest             ""; # `no-cache` (*)

        # Assets
        ~*image/svg\+xml                  "public, immutable, stale-while-revalidate";

        # Data interchange
        ~*application/(atom|rdf|rss)\+xml "public, stale-while-revalidate";

        # Documents
        ~*text/html                       "private, must-revalidate";
        ~*text/markdown                   "private, must-revalidate";
        ~*text/calendar                   "private, must-revalidate";

        # Data
        ~*json                            ""; # `no-cache` (*)
        ~*xml                             ""; # `no-cache` (*)
    }

    map $sent_http_content_type $expires {
        # Default: Fallback
        default                       1y;

        # Default: No content
        ""                            off;

        # Specific: Assets
        ~*image/svg\+xml              max;
        ~*image/vnd.microsoft.icon    1w;
        ~*image/x-icon                1w;

        # Specific: Manifests
        ~*application/manifest\+json  1w;
        ~*text/cache-manifest         epoch;

        # Specific: Data interchange
        ~*application/atom\+xml       1h;
        ~*application/rdf\+xml        1h;
        ~*application/rss\+xml        1h;

        # Specific: Documents
        ~*text/html                   epoch;
        ~*text/markdown               epoch;
        ~*text/calendar               epoch;

        # Specific: Other
        ~*text/x-cross-domain-policy  1w;

        # Generic: Data
        ~*json                        epoch;
        ~*xml                         epoch;

        # Generic: WebAssembly
        ~*application/wasm            max;

        # Generic: Assets
        ~*application/javascript      max;
        ~*application/x-javascript    max;
        ~*text/javascript             max;
        ~*text/css                    max;

        # Generic: Medias
        ~*audio/                      max;
        ~*image/                      max;
        ~*video/                      max;
        ~*font/                       max;
    }

    map $sent_http_content_type $x_xss_protection {
        ~*text/html "1; mode=block";
    }

    map $sent_http_content_type $x_frame_options {
        ~*text/html DENY;
    }

    map $sent_http_content_type $content_security_policy {
        ~*text/(html|javascript)|application/pdf|xml "default-src 'self' 'https://*.example.com'; base-uri 'none'; form-action 'self'; frame-ancestors 'none'; upgrade-insecure-requests";
    }

    map $sent_http_content_type $permissions_policy {
        ~*text/(html|javascript)|application/pdf|xml "accelerometer=(),autoplay=(),camera=(),display-capture=(),document-domain=(),encrypted-media=(),fullscreen=(),geolocation=(),gyroscope=(),magnetometer=(),microphone=(),midi=(),payment=(),picture-in-picture=(),publickey-credentials-get=(),screen-wake-lock=(),sync-xhr=(self),usb=(),web-share=(),xr-spatial-tracking=()";
    }

    map $sent_http_content_type $referrer_policy {
        ~*text/(css|html|javascript)|application\/pdf|xml "strict-origin-when-cross-origin";
    }

    map $sent_http_content_type $coep_policy {
        ~*text/(html|javascript)|application/pdf|xml "require-corp";
    }

    map $sent_http_content_type $coop_policy {
        ~*text/(html|javascript)|application/pdf|xml "same-origin";
    }

    map $sent_http_content_type $corp_policy {
        ~*text/(html|javascript)|application/pdf|xml "same-origin";
    }

    map $sent_http_content_type $cors {
        # Images
        ~*image/ "*";

        # Web fonts
        ~*font/                         "*";
        ~*application/vnd.ms-fontobject "*";
        ~*application/x-font-ttf        "*";
        ~*application/font-woff         "*";
        ~*application/x-font-woff       "*";
        ~*application/font-woff2        "*";
    }

    open_file_cache          max=1000 inactive=20s;
    open_file_cache_valid    30s;
    open_file_cache_min_uses 2;
    open_file_cache_errors   on;

    brotli_static     on;
    brotli            on;
    brotli_comp_level 11;
    brotli_types      $compression_types;

    gzip_static     on;
    gzip            on;
    gzip_comp_level 9;
    gzip_min_length 256;
    gzip_proxied    any;
    gzip_types      $compression_types;
    gzip_vary       on;

    expires $expires;
    etag    on;

    add_header Cache-Control $cache_control;

    add_header Content-Security-Policy $content_security_policy always;
    add_header Referrer-Policy $referrer_policy always;
    add_header Permissions-Policy $permissions_policy always;
    add_header Cross-Origin-Embedder-Policy $coep_policy always;
    add_header Cross-Origin-Opener-Policy $coop_policy always;
    add_header Cross-Origin-Resource-Policy $corp_policy always;
    add_header X-Content-Type-Options nosniff always;
    add_header X-Frame-Options $x_frame_options always;
    add_header X-XSS-Protection $x_xss_protection always;
    add_header X-Download-Options noopen;

    add_header Access-Control-Allow-Origin $cors;
    add_header Timing-Allow-Origin "*";

    modsecurity            on;
    modsecurity_rules_file /etc/modsecurity.d/modsecurity.conf;

    server {
        listen 80 default_server;
        listen [::]:80 default_server;

        return 301 https://$host$request_uri;
    }

    server {
        listen 443 ssl http2;
        listen [::]:443 ssl http2;
        server_name  _;
        root         /usr/share/nginx/html;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        ssl_certificate     /path/to/signed_cert_plus_intermediates;
        ssl_certificate_key /path/to/private_key;
        ssl_session_timeout 1d;
        ssl_session_cache   shared:MozSSL:10m;  # about 40000 sessions
        ssl_session_tickets off;

        ssl_dhparam /path/to/dhparam; # openssl dhparam -out /etc/nginx/dhparam.pem 2048

        # intermediate configuration
        ssl_protocols             TLSv1.2 TLSv1.3;
        ssl_ciphers               ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384;
        ssl_prefer_server_ciphers off;

        # HSTS (ngx_http_headers_module is required) (63072000 seconds)
        add_header Strict-Transport-Security "max-age=63072000; includeSubDomains; preload" always;

        # OCSP stapling
        ssl_stapling        on;
        ssl_stapling_verify on;

        # verify chain of trust of OCSP response using Root CA and Intermediate certs
        ssl_trusted_certificate /path/to/root_CA_cert_plus_intermediates;

        # replace with the IP address of your resolver
        resolver 127.0.0.1;

        location / {
        }

        location ~* /\.(?!well-known\/) {
            deny all;
        }

        location ~* (?:#.*#|\.(?:bak|conf|dist|fla|in[ci]|log|orig|psd|sh|sql|sw[op])|~)$ {
            deny all;
        }

        error_page 404 /404.html;
            location = /404.html {
        }
    }
}
```
:::

### 伪静态配置

```
# nginx.conf
server {
  location / {
    try_files $uri $uri/ /index.html;
  }
}
```

:::warning
如果使用 History 路由才需要伪静态配置
:::

### 缓存配置

:::tip
- [ngx_http_headers_module](https://nginx.org/en/docs/http/ngx_http_headers_module.html)
- [ngx_http_core_module](https://nginx.org/en/docs/http/ngx_http_core_module.html)
:::

:::tip
- [Cache-Control](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Cache-Control)
- [Expires](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Expires)
- [ETag](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Etag)
:::

```
# nginx.conf
http {
    map $sent_http_content_type $cache_control {
        default                           "public, immutable, stale-while-revalidate";

        # No content
        ""                                "no-store";

        # Manifest files
        ~*application/manifest\+json      "public";
        ~*text/cache-manifest             ""; # `no-cache` (*)

        # Assets
        ~*image/svg\+xml                  "public, immutable, stale-while-revalidate";

        # Data interchange
        ~*application/(atom|rdf|rss)\+xml "public, stale-while-revalidate";

        # Documents
        ~*text/html                       "private, must-revalidate";
        ~*text/markdown                   "private, must-revalidate";
        ~*text/calendar                   "private, must-revalidate";

        # Data
        ~*json                            ""; # `no-cache` (*)
        ~*xml                             ""; # `no-cache` (*)
    }

    map $sent_http_content_type $expires {
        # Default: Fallback
        default                       1y;

        # Default: No content
        ""                            off;

        # Specific: Assets
        ~*image/svg\+xml              max;
        ~*image/vnd.microsoft.icon    1w;
        ~*image/x-icon                1w;

        # Specific: Manifests
        ~*application/manifest\+json  1w;
        ~*text/cache-manifest         epoch;

        # Specific: Data interchange
        ~*application/atom\+xml       1h;
        ~*application/rdf\+xml        1h;
        ~*application/rss\+xml        1h;

        # Specific: Documents
        ~*text/html                   epoch;
        ~*text/markdown               epoch;
        ~*text/calendar               epoch;

        # Specific: Other
        ~*text/x-cross-domain-policy  1w;

        # Generic: Data
        ~*json                        epoch;
        ~*xml                         epoch;

        # Generic: WebAssembly
        ~*application/wasm            max;

        # Generic: Assets
        ~*application/javascript      max;
        ~*application/x-javascript    max;
        ~*text/javascript             max;
        ~*text/css                    max;

        # Generic: Medias
        ~*audio/                      max;
        ~*image/                      max;
        ~*video/                      max;
        ~*font/                       max;
    }

    expires $expires;
    etag    on;

    add_header Cache-Control $cache_control;
}
```

### HTTP/2 配置

:::tip
- [ngx_http_v2_module](https://nginx.org/en/docs/http/ngx_http_v2_module.html)
- [ngx_http_ssl_module](https://nginx.org/en/docs/http/ngx_http_ssl_module.html)
:::

```
# nginx.conf
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;

    ssl_certificate     /path/to/signed_cert_plus_intermediates;
    ssl_certificate_key /path/to/private_key;
    ssl_session_timeout 1d;
    ssl_session_cache   shared:MozSSL:10m;  # about 40000 sessions
    ssl_session_tickets off;

    ssl_dhparam /path/to/dhparam; # openssl dhparam -out /etc/nginx/dhparam.pem 2048

    # intermediate configuration
    ssl_protocols             TLSv1.2 TLSv1.3;
    ssl_ciphers               ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384;
    ssl_prefer_server_ciphers off;

    # HSTS (ngx_http_headers_module is required) (63072000 seconds)
    add_header Strict-Transport-Security "max-age=63072000; includeSubDomains; preload" always;

    # OCSP stapling
    ssl_stapling        on;
    ssl_stapling_verify on;

    # verify chain of trust of OCSP response using Root CA and Intermediate certs
    ssl_trusted_certificate /path/to/root_CA_cert_plus_intermediates;

    # replace with the IP address of your resolver
    resolver 127.0.0.1;
}
```

:::tip
开启 HTTP/2 必须开启 HTTPS，建议 HTTPS 使用 TLS v1.3 协议。

可以参考 [Mozilla SSL 配置生成器](https://ssl-config.mozilla.org/) 生成配置
:::

### Brotli & GZIP 配置

:::tip
- [ngx_brotli](https://github.com/google/ngx_brotli)
- [ngx_http_gzip_module](https://nginx.org/en/docs/http/ngx_http_gzip_module.html)
- [ngx_http_gzip_static_module](https://nginx.org/en/docs/http/ngx_http_gzip_static_module.html)
:::

```
# nginx.conf
load_module /usr/lib/nginx/modules/ngx_http_brotli_filter_module.so;
load_module /usr/lib/nginx/modules/ngx_http_brotli_static_module.so;

http {
  $compression_types
    application/atom+xml
    application/geo+json
    application/javascript
    application/x-javascript
    application/json
    application/ld+json
    application/manifest+json
    application/rdf+xml
    application/rss+xml
    application/vnd.ms-fontobject
    application/wasm
    application/x-web-app-manifest+json
    application/xhtml+xml
    application/xml
    font/eot
    font/otf
    font/ttf
    image/bmp
    image/svg+xml
    image/vnd.microsoft.icon
    image/x-icon
    text/cache-manifest
    text/calendar
    text/css
    text/javascript
    text/markdown
    text/plain
    text/xml
    text/vcard
    text/vnd.rim.location.xloc
    text/vtt
    text/x-component
    text/x-cross-domain-policy;

  brotli_static     on;
  brotli            on;
  brotli_comp_level 11;
  brotli_types      $compression_types;

  gzip_static     on;
  gzip            on;
  gzip_comp_level 9;
  gzip_min_length 256;
  gzip_proxied    any;
  gzip_types      $compression_types;
  gzip_vary       on;
}
```

:::tip
启用 Brotli 应该先安装 [ngx_brotli](https://github.com/google/ngx_brotli) 模块，该模块并非 nginx 官方模块。同时，Brotli 只能在 HTTPS 下运行。
:::

### 安全配置

:::tip
- [Content-Security-Policy](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Security-Policy)
- [Subresource Integrity](https://developer.mozilla.org/zh-CN/docs/Web/Security/Subresource_Integrity)
- [Referrer-Policy](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Referrer-Policy)
- [Permissions-Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Feature-Policy)
- [Access-Control-Allow-Origin](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Allow-Origin)
- [Timing-Allow-Origin](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Timing-Allow-Origin)
- [Cross-Origin-Embedder-Policy](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Cross-Origin-Embedder-Policy)
- [Cross-Origin-Opener-Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cross-Origin-Opener-Policy)
- [Cross-Origin-Resource-Policy](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Cross-Origin-Resource-Policy)
- [X-Content-Type-Options](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/X-Content-Type-Options)
- [X-Frame-Options](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/X-Frame-Options)
- [X-XSS-Protection](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/X-XSS-Protection)
- X-Download-Options
:::

:::tip
- [ModSecurity](https://github.com/SpiderLabs/ModSecurity)
- [ngx_modsecurity](https://github.com/SpiderLabs/ModSecurity-nginx)
:::

```
# nginx.conf
load_module /usr/lib/nginx/modules/ngx_http_modsecurity_module.so;

http {
  server_tokens off;

  modsecurity on;
  modsecurity_rules_file /path/to/modsecurity/modsecurity.conf;

  map $sent_http_content_type $x_xss_protection {
    ~*text/html "1; mode=block";
  }

  map $sent_http_content_type $x_frame_options {
    ~*text/html DENY;
  }

  map $sent_http_content_type $content_security_policy {
    ~*text/(html|javascript)|application/pdf|xml "default-src 'self' 'https://cdn.example.com'; base-uri 'none'; form-action 'self'; frame-ancestors 'none'; upgrade-insecure-requests;";
  }

  map $sent_http_content_type $referrer_policy {
    ~*text/(css|html|javascript)|application\/pdf|xml "strict-origin-when-cross-origin";
  }

  map $sent_http_content_type $permissions_policy {
    ~*text/(html|javascript)|application/pdf|xml "accelerometer=(),autoplay=(),camera=(),display-capture=(),document-domain=(),encrypted-media=(),fullscreen=(),geolocation=(),gyroscope=(),magnetometer=(),microphone=(),midi=(),payment=(),picture-in-picture=(),publickey-credentials-get=(),screen-wake-lock=(),sync-xhr=(self),usb=(),web-share=(),xr-spatial-tracking=()";
  }

  map $sent_http_content_type $cors {
    # Images
    ~*image/                        "*";

    # Web fonts
    ~*font/                         "*";
    ~*application/vnd.ms-fontobject "*";
    ~*application/x-font-ttf        "*";
    ~*application/font-woff         "*";
    ~*application/x-font-woff       "*";
    ~*application/font-woff2        "*";
  }

  map $sent_http_content_type $coep_policy {
    ~*text/(html|javascript)|application/pdf|xml "require-corp";
  }

  map $sent_http_content_type $coop_policy {
    ~*text/(html|javascript)|application/pdf|xml "same-origin";
  }

  map $sent_http_content_type $corp_policy {
    ~*text/(html|javascript)|application/pdf|xml "same-origin";
  }

  add_header Content-Security-Policy $content_security_policy always;
  add_header Referrer-Policy $referrer_policy always;
  add_header Permissions-Policy $permissions_policy always;

  add_header Access-Control-Allow-Origin $cors;
  add_header Timing-Allow-Origin "*";
  add_header Cross-Origin-Embedder-Policy $coep_policy always;
  add_header Cross-Origin-Opener-Policy $coop_policy always;
  add_header Cross-Origin-Resource-Policy $corp_policy always;

  add_header X-Content-Type-Options nosniff always;
  add_header X-Frame-Options $x_frame_options always;
  add_header X-XSS-Protection $x_xss_protection always;
  add_header X-Download-Options noopen;

  server {
    location ~* /\.(?!well-known\/) {
      deny all;
    }

    location ~* (?:#.*#|\.(?:bak|conf|dist|fla|in[ci]|log|orig|psd|sh|sql|sw[op])|~)$ {
      deny all;
    }
  }
}
```

:::tip
[ModSecurity](https://github.com/SpiderLabs/ModSecurity) 是一个开源的、跨平台的Web应用防火墙（WAF），它提供一个 [nginx 模块](https://github.com/SpiderLabs/ModSecurity-nginx)，建议在生产环境使用并使用 [OWASP ModSecurity Core Rule Set](https://coreruleset.org/) 的配置
:::

### 代理配置

:::tip
- [ngx_http_proxy_module](https://nginx.org/en/docs/http/ngx_http_proxy_module.html)
:::

```
# 代理路径、IP、端口，请根据实际情况进行配置
server {
  listen 443;
  server_name example.com www.example.com;
  set $porxy_port 8021;

  location ~ /porxy-path/ {
    proxy_http_version 1.1;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Host $http_host;
    proxy_set_header X-NginX-Proxy true;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
    proxy_pass http://127.0.0.1:$porxy_port$request_uri;
    proxy_redirect off;
  }
}
```

:::warning
尽量使用多域名的部署方式，减少代理的使用
:::

### 其他配置

```
client_body_buffer_size     10K;
client_header_buffer_size   1k;
client_max_body_size        8m;
large_client_header_buffers 4 32k;

limit_zone slimits $binary_remote_addr 5m;
limit_conn slimits 5;

limit_req           zone=ratelimit burst=30 nodelay;
limit_req_log_level warn;
```

## ESLint

:::tip
[https://eslint.org/docs/user-guide/configuring](https://eslint.org/docs/user-guide/configuring)
:::

```js
// .eslintrc.js

module.exports = {
  extends: [
    '@vue/airbnb',
    'plugin:vue/vue3-recommended',
    'plugin:@typescript-eslint/recommended',
    'plugin:no-unsanitized/DOM',
  ],
};
```

## stylelint

:::tip
[https://stylelint.io/user-guide/configure](https://stylelint.io/user-guide/configure)
:::

```js
// stylelint.config.js

// $ npm install stylelint stylelint-config-twbs-bootstrap stylelint-config-recommended-vue postcss-html --save-dev
module.exports = {
  extends: [
    'stylelint-config-twbs-bootstrap',
    'stylelint-config-recommended-vue',
    'stylelint-config-recommended-vue/scss',
  ],
  overrides: [
    {
      files: ['*/**/*.vue'],
      customSyntax: 'postcss-html',
    },
  ],
};
```

```js
// vue.config.js

const { defineConfig } = require('@vue/cli-service');
// $ npm install stylelint-webpack-plugin --save-dev
const StylelintPlugin = require('stylelint-webpack-plugin');

module.exports = defineConfig({
  configureWebpack: (config) => {
    const basePlugins = [
      new StylelintPlugin({
        extensions: ['css', 'scss', 'sass', 'vue'],
      }),
    ];
    let productionPlugins = [];

    if (process.env.NODE_ENV === 'production') {
      // ...
    }

    return {
      plugins: [
        ...basePlugins,
        ...productionPlugins,
      ],
    };
  },
});
```

## browserslist

:::tip
[https://github.com/browserslist/browserslist#browserslistrc](https://github.com/browserslist/browserslist#browserslistrc)
:::

```
# browserslistrc

[production]
last 2 version
> 1%
not dead
not ie < 11
not op_mini all

[development]
last 1 chrome version
last 1 firefox version
last 1 safari version
```

:::tip
支持的浏览器列表可通过运行 `npx browserslist` 查看
:::

## Jest

:::tip
[https://jestjs.io/docs/zh-Hans/configuration](https://jestjs.io/docs/zh-Hans/configuration)

Jest 可使用 CRA 提供的默认配置，如需修改配置可修改 `jest.config.js` 文件
:::

## Commitlint & Conventional Changelog

:::tip
[https://commitlint.js.org/#/reference-configuration](https://commitlint.js.org/#/reference-configuration)
:::

```js
// commitlint.config.js

// $ npm install @commitlint/cli @commitlint/config-angular --save-dev
module.exports = {
  extends: ['@commitlint/config-angular'],
};
```

## Vue Styleguidist

:::warning
截止本文撰写时，Vue Styleguidist 仍不支持 Vue 3
:::

## Docker

### Vue

```dockerfile
# Dockerfile

# 安装依赖和构建
FROM node:16 AS build
WORKDIR /app
COPY configuration /app
RUN npm install
RUN npm ci

# 运行 nginx
FROM nginx:stable AS deploy
COPY --from=build /app/dist/ /usr/share/nginx/html/
COPY --from=build /app/nginx.conf /etc/nginx/nginx.conf
EXPOSE 80
```

:::details 最完整配置（包括 Brotli 和 ModSecurity）
```dockerfile
# Dockerfile

# nginx 使用最新的 stable 版本
ARG NGINX_VERSION="1.20.2"

# 安装依赖和构建
FROM node:16 AS build
WORKDIR /app
COPY . /app
RUN yarn install --frozen-lock
RUN yarn build

# 编译 nginx 模块，运行 nginx
FROM nginx:stable-alpine AS deploy
ARG SSDEEP_VERSION="2.14.1"
## OWASP® ModSecurity Core Rule Set(CRS) 使用最新的 release 版本
ARG OWASP_CRS_VERSION="3.3.2"
## 安装依赖
RUN apk add \
     autoconf \
     automake \
     brotli-dev \
     ca-certificates \
     coreutils \
     curl-dev \
     g++ \
     gcc \
     geoip-dev \
     git \
     libc-dev \
     libmaxminddb-dev \
     libstdc++ \
     libtool \
     libxml2-dev \
     linux-headers \
     lmdb-dev \
     make \
     openssl \
     openssl-dev \
     pkgconfig \
     pcre-dev \
     yajl-dev \
     zlib-dev
## 安装Brotli
RUN git clone https://github.com/google/ngx_brotli.git
RUN cd ngx_brotli && git submodule update --init
## 安装ssdeep
RUN wget --quiet https://github.com/ssdeep-project/ssdeep/releases/download/release-${SSDEEP_VERSION}/ssdeep-${SSDEEP_VERSION}.tar.gz \
    && tar -xvzf ssdeep-${SSDEEP_VERSION}.tar.gz \
    && cd ssdeep-${SSDEEP_VERSION} \
    && ./configure \
    && make \
    && make install
## 安装ModSecurity
RUN git clone https://github.com/SpiderLabs/ModSecurity.git \
    && cd /ModSecurity \
    && ./build.sh \
    && git submodule init \
    && git submodule update \
    && ./configure --with-yajl --with-ssdeep --with-lmdb --with-geoip \
    && make \
    && make install
RUN git clone https://github.com/SpiderLabs/ModSecurity-nginx.git \
    && mkdir -p /etc/modsecurity.d  \
    && cd /etc/modsecurity.d  \
    && wget --quiet https://raw.githubusercontent.com/SpiderLabs/ModSecurity/v3/master/modsecurity.conf-recommended \
    && mv modsecurity.conf-recommended modsecurity-recommended.conf \
    && wget --quiet https://raw.githubusercontent.com/SpiderLabs/ModSecurity/v3/master/unicode.mapping \
    && sed -i 's/SecRuleEngine DetectionOnly/SecRuleEngine On/' modsecurity-recommended.conf \
    && wget --quiet https://github.com/coreruleset/coreruleset/archive/refs/tags/v${OWASP_CRS_VERSION}.tar.gz \
    && mv v${OWASP_CRS_VERSION}.tar.gz owasp-modsecurity-crs.tar.gz \
    && tar -zxvf owasp-modsecurity-crs.tar.gz \
    && mv coreruleset-${OWASP_CRS_VERSION} owasp-modsecurity-crs \
    && mv owasp-modsecurity-crs/crs-setup.conf.example owasp-modsecurity-crs/crs-setup.conf \
    && mv owasp-modsecurity-crs/rules/REQUEST-900-EXCLUSION-RULES-BEFORE-CRS.conf.example owasp-modsecurity-crs/rules/REQUEST-900-EXCLUSION-RULES-BEFORE-CRS.conf \
    && mv owasp-modsecurity-crs/rules/RESPONSE-999-EXCLUSION-RULES-AFTER-CRS.conf.example owasp-modsecurity-crs/rules/RESPONSE-999-EXCLUSION-RULES-AFTER-CRS.conf \
    && touch modsecurity.conf \
    && echo -e "# Include the recommended configuration\nInclude modsecurity-recommended.conf\n# Include OWASP CRS v3 rules\nInclude owasp-modsecurity-crs/crs-setup.conf\nInclude owasp-modsecurity-crs/rules/*.conf" > modsecurity.conf
## 编译模块
RUN wget --quiet https://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz \
    && tar -xzf nginx-${NGINX_VERSION}.tar.gz \
    && cd /nginx-${NGINX_VERSION}  \
    && ./configure \
     --prefix=/etc/nginx \
     --sbin-path=/usr/sbin/nginx \
     --modules-path=/usr/lib/nginx/modules \
     --conf-path=/etc/nginx/nginx.conf \
     --error-log-path=/var/log/nginx/error.log \
     --http-log-path=/var/log/nginx/access.log \
     --pid-path=/var/run/nginx.pid \
     --lock-path=/var/run/nginx.lock \
     --http-client-body-temp-path=/var/cache/nginx/client_temp \
     --http-proxy-temp-path=/var/cache/nginx/proxy_temp \
     --http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp \
     --http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp \
     --http-scgi-temp-path=/var/cache/nginx/scgi_temp \
     --with-perl_modules_path=/usr/lib/perl5/vendor_perl \
     --user=nginx \
     --group=nginx \
     --with-compat \
     --with-file-aio \
     --with-threads \
     --with-http_addition_module \
     --with-http_auth_request_module \
     --with-http_dav_module \
     --with-http_flv_module \
     --with-http_gunzip_module \
     --with-http_gzip_static_module \
     --with-http_mp4_module \
     --with-http_random_index_module \
     --with-http_realip_module \
     --with-http_secure_link_module \
     --with-http_slice_module \
     --with-http_ssl_module \
     --with-http_stub_status_module \
     --with-http_sub_module \
     --with-http_v2_module \
     --with-mail \
     --with-mail_ssl_module \
     --with-stream \
     --with-stream_realip_module \
     --with-stream_ssl_module \
     --with-stream_ssl_preread_module \
     --with-cc-opt='-Os -fomit-frame-pointer -g' \
     --with-ld-opt=-Wl,--as-needed,-O1,--sort-common \
     --add-dynamic-module=/ngx_brotli \
     --add-dynamic-module=/ModSecurity-nginx \
     && make modules
RUN cp /nginx-${NGINX_VERSION}/objs/ngx_http_brotli_filter_module.so /usr/lib/nginx/modules/ \
    && cp /nginx-${NGINX_VERSION}/objs/ngx_http_brotli_static_module.so /usr/lib/nginx/modules/  \
    && cp /nginx-${NGINX_VERSION}/objs/ngx_http_modsecurity_module.so /usr/lib/nginx/modules/
## 部署代码
COPY --from=build /app/docs/.vuepress/dist /usr/share/nginx/html/
COPY --from=build /app/nginx.conf /etc/nginx/nginx.conf
EXPOSE 80
```
:::

### Nuxt.js

```dockerfile
# Dockerfile

# 安装依赖和启动
FROM node:16 AS build
WORKDIR /app
COPY . /app
RUN npm install
RUN npm install pm2 -g
RUN pm2 start
EXPOSE 8000

# 运行 nginx
FROM nginx:stable AS deploy
COPY --from=build /app/nginx.conf /etc/nginx/nginx.conf
EXPOSE 80
```
