# multietch

Squarespace export

## (Re)running the export

We run `mirror.sh` **three times** because Squarespace is finicky and tries to deny access randomly. `wget` will ignore files that have already been retrieved in the subsequent rounds.

One quick way to check if all files are there is to look at the `etching-` files; there should be 23. A complete list of all files (excluding third-party domain page assets) can be found on the [sitemap](https://www.multietch.com/sitemap.xml).

```sh
rm -rf docs && mkdir docs && mkdir docs/files && mkdir docs/files/assets
./mirror.sh && ./mirror.sh && ./mirror.sh
./copy.sh
./rewrite.sh
```

My regexfu failed me when combined with `sed` and its many (nonstandard) (annoying) idiosyncrases. So then we need to do manual find and replace across the 'docs' files:

| From | To |
|------|----|
|href="../static1.squarespace.com|href="/files|
|src="../static1.squarespace.com|src="/files|
|href="../images.squarespace-cdn.com|href="/files|
|src="../images.squarespace-cdn.com|src="/files|
|href="../assets.squarespace.com|href="/files/assets|
|src="../assets.squarespace.com|src="/files/assets|
