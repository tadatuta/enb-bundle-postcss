# enb-bundle-postcss

## Usage

Here a diff to add `enb-bundle-postcss` to [project-stub](https://github.com/bem/project-stub) configuration:

```diff
diff --git a/.enb/make.js b/.enb/make.js
index c98c578..163bf70 100644
--- a/.enb/make.js
+++ b/.enb/make.js
@@ -8,6 +8,7 @@ var techs = {
 
         // css
         stylus: require('enb-stylus/techs/stylus'),
+        postcss: require('enb-bundle-postcss/techs/enb-bundle-postcss'),
 
         // js
         browserJs: require('enb-diverse-js/techs/browser-js'),
@@ -46,11 +47,16 @@ module.exports = function(config) {
 
             // css
             [techs.stylus, {
-                target: '?.css',
+                target: '?.post.css',
                 autoprefixer: {
                     browsers: ['ie >= 10', 'last 2 versions', 'opera 12.1', '> 2%']
                 }
             }],
+            [techs.postcss, {
+                source: '?.post.css',
+                sourcemap: true,
+                plugins: [require('lost')()]
+            }],
 
             // bemtree
             // [techs.bemtree, { devMode: process.env.BEMTREE_ENV === 'development' }],
diff --git a/package.json b/package.json
index 23e6677..1290e2f 100644
--- a/package.json
+++ b/package.json
@@ -21,7 +21,9 @@
     "enb-borschik": "^2.0.0",
     "enb-diverse-js": "^0.1.0",
     "enb-modules": "^0.2.0",
+    "enb-bundle-postcss": "tadatuta/enb-bundle-postcss",
     "enb-stylus": "^2.0.0",
+    "lost": "^6.5.0",
     "ym": "^0.1.2"
   },
   "scripts": {
```
