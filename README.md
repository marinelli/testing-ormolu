`ormolu` uses the first cabal file it finds. If it finds a cabal file that does not contain the module in consideration, it uses the default values without trying to check for a cabal file in the parent dir. i.e.:

```shell
$ ormolu --debug -i two/app/Main.hs 2>&1 | head -n1
Found .cabal file two/two.cabal, but it did not mention two/app/Main.hs
$ git diff two/app/Main.hs 
diff --git a/two/app/Main.hs b/two/app/Main.hs
index 094b78a..a55d030 100644
--- a/two/app/Main.hs
+++ b/two/app/Main.hs
@@ -1,4 +1,4 @@
 module Main where
 
 main :: IO ()
-main = undefined #undefined
+main = undefined # undefined
$ git restore two/app/Main.hs 
$ rm two/two.cabal
$ ormolu -i two/app/Main.hs
$ git diff two/app/Main.hs
$
```
