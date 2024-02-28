Run `$ pnpm run build` then observe the error [`TypeError: jsxDEV is not a function`](#the-error).

Caused by the commit [835fb71](https://github.com/brillout/reprod_jsxDev-not-a-function/commit/835fb711d3b60eb6e6780afd736176af74f2f72c):

``` diff
// package.json

-   "build": "vite build",
+   "build": "NODE_ENV=development vite build",
```

It seems that setting `NODE_ENV` to any value other than `production` triggers the error. For example, the following triggers the error as well.

``` diff
// package.json

-   "build": "NODE_ENV=development vite build",
+   "build": "NODE_ENV=staging vite build",
```


## The error

```
$ pnpm run build

> @ build /home/rom/tmp/reprod_jsxDev-not-a-function
> NODE_ENV=development vite build

vite v5.0.12 building for production...
✓ 232 modules transformed.
dist/client/_temp_manifest.json                                 3.82 kB │ gzip:   0.68 kB
dist/client/assets/static/logo.2_7Lo9tV.svg                     5.79 kB │ gzip:   2.00 kB
dist/client/assets/static/onPageTransitionEnd.DQ-loHhw.css      1.28 kB │ gzip:   0.68 kB
dist/client/assets/chunks/chunk-S31rFZG_.js                     0.10 kB │ gzip:   0.11 kB
dist/client/assets/chunks/chunk-DTBiLySn.js                     0.30 kB │ gzip:   0.25 kB
dist/client/assets/entries/pages_error.24ur7TnO.js              1.96 kB │ gzip:   0.79 kB
dist/client/assets/entries/pages_star-wars_index.BgKRJwUK.js    3.02 kB │ gzip:   0.89 kB
dist/client/assets/entries/pages_hello.D_GyAr1w.js              3.56 kB │ gzip:   0.98 kB
dist/client/assets/entries/pages_index.D-1hmq6C.js              3.75 kB │ gzip:   1.21 kB
dist/client/assets/entries/entry-client-routing.CR7jc55r.js     6.77 kB │ gzip:   2.17 kB
dist/client/assets/chunks/chunk-DDGTLX6s.js                    11.79 kB │ gzip:   4.82 kB
dist/client/assets/entries/pages_star-wars_-id.zjcaeWSz.js     12.59 kB │ gzip:   4.20 kB
dist/client/assets/entries/pages_markdown.BZ38t9QC.js          14.54 kB │ gzip:   5.67 kB
dist/client/assets/chunks/chunk-yJ7HupB4.js                    55.45 kB │ gzip:  17.92 kB
dist/client/assets/chunks/chunk-CHbEPwtg.js                   330.95 kB │ gzip: 100.19 kB
vite v5.0.12 building SSR bundle for production...
✓ 35 modules transformed.
dist/server/package.json                       0.02 kB
dist/server/importBuild.cjs                    0.28 kB
dist/server/importBuild.mjs                    0.28 kB
dist/server/importBuild.js                     0.28 kB
dist/server/chunks/chunk-Bk6bgc-s.js           0.16 kB
dist/server/chunks/chunk-BChgxANp.js           0.21 kB
dist/server/chunks/chunk-Amq53xga.js           0.46 kB
dist/server/entries/pages_error.mjs            2.29 kB
dist/server/entries/pages_markdown.mjs         2.37 kB
dist/server/entries/pages_star-wars_-id.mjs    3.20 kB
dist/server/entries/pages_index.mjs            3.35 kB
dist/server/entries/pages_hello.mjs            5.42 kB
dist/server/entries/pages_star-wars_index.mjs  6.23 kB
dist/server/entry.mjs                          6.65 kB
dist/server/chunks/chunk-C9xYb7Vv.js           7.81 kB
✓ built in 476ms
vike v0.4.160 pre-rendering HTML...
TypeError: jsxDEV is not a function
    at onRenderHtml (file:///home/rom/tmp/reprod_jsxDev-not-a-function/dist/server/chunks/chunk-C9xYb7Vv.js:195:80)
    at file:///home/rom/tmp/reprod_jsxDev-not-a-function/node_modules/.pnpm/vike@0.4.160_react-streaming@0.3.23_vite@5.0.12/node_modules/vike/dist/esm/node/runtime/renderPage/executeOnRenderHtmlHook.js:15:53
    at file:///home/rom/tmp/reprod_jsxDev-not-a-function/node_modules/.pnpm/vike@0.4.160_react-streaming@0.3.23_vite@5.0.12/node_modules/vike/dist/esm/shared/hooks/executeHook.js:46:31
    at executeHook (file:///home/rom/tmp/reprod_jsxDev-not-a-function/node_modules/.pnpm/vike@0.4.160_react-streaming@0.3.23_vite@5.0.12/node_modules/vike/dist/esm/shared/hooks/executeHook.js:55:7)
    at executeOnRenderHtmlHook (file:///home/rom/tmp/reprod_jsxDev-not-a-function/node_modules/.pnpm/vike@0.4.160_react-streaming@0.3.23_vite@5.0.12/node_modules/vike/dist/esm/node/runtime/renderPage/executeOnRenderHtmlHook.js:15:35)
    at prerenderPage (file:///home/rom/tmp/reprod_jsxDev-not-a-function/node_modules/.pnpm/vike@0.4.160_react-streaming@0.3.23_vite@5.0.12/node_modules/vike/dist/esm/node/runtime/renderPage/renderPageAlreadyRouted.js:80:46)
    at processTicksAndRejections (node:internal/process/task_queues:95:5)
    at file:///home/rom/tmp/reprod_jsxDev-not-a-function/node_modules/.pnpm/vike@0.4.160_react-streaming@0.3.23_vite@5.0.12/node_modules/vike/dist/esm/node/prerender/runPrerender.js:489:19
 ELIFECYCLE  Command failed with exit code 1.
```
