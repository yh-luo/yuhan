---
date: "2018-11-06T00:58:28+08:00"
title: "Git submodules is hard to do..."
categories:
  - "random"
---

一時心血來潮想要在網頁上加上 Research Gate 的連結，FontAwesome 其實有提供 icon，但不知道為什麼在我的網頁上呈現不出 G，只剩一個黑框框與 R，因此我決定用 [Academicons](https://jpswalsh.github.io/academicons/)提供的 icon。

然後開始了我學習 git 的旅程。
修改的過程蠻容易的，照 Academicons 的說明加上 link 後，改一下 `config.toml` 就可以了。但因為主題是以 `.gitsubmodules` 的方式處理的，需要先 clone subproject 到 project 裡 ([source](https://git-scm.com/book/zh-tw/v1/Git-%E5%B7%A5%E5%85%B7-%E5%AD%90%E6%A8%A1%E7%B5%84-Submodules))：

```bash
# initiate the submodule (i.e., theme)
$ git submodule init
# clone it to local repository
$ git submodule update
```
接下來的過程過於慘烈，總而言之，如果要修改 submodule 裡的檔案的話，因為subproject 裡有自己的 git 資料庫，最好的方法是**切換到 subproject 的資料夾裡進行修改**，再 commit。E.g., 

```bash
# enter the subproject and checkout
$ cd /themes/hugo-coder-1.0/
$ git checkout -b new_change

# do something ...

# commit the changes
$ git add .
$ git commit -m "my awesome new feature"

# merge to the master branch of the subproject
$ git checkout master
$ git merge new_change
```

(?) 由於[Netlify](https://www.netlify.com/) deploy 時會去找 `.submodules` 裡的 URL，我在 github 存了一份自己稍微修改過的hugo-coder 主題，因此需要把修改的部份也 push 到 github。

```bash
# push to the remote repository of submodule
$ git push origin master
```

沒問題之後再切換回主專案並 commit ([source](https://stackoverflow.com/questions/5828324/update-git-submodule-to-latest-commit-on-origin))

```bash
# I'm lazy
$ cd -
# just to make sure that the local subproject is up-to-date
$ git pull
# commit the changes in subprojects and update the local project
$ git add .
$ git commit -m "Pulled down the awesome update"
```

完成！