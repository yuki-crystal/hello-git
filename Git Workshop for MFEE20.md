---
title: Git Workshop for MFEE20
tags: iii-mfee20
description: Git Workshop for iii MFEE20
version: 20210918
---



#中壢前端班-賴老師筆記

---

## 任務 0: Why git?

github, gitlab, bitbucket,...

git 是什麼？「分散式」版本控制


版本？
- 每次更新的檔案
- 每一次的更改
- 每次更新的紀錄

多存一份再改

![](https://i.imgur.com/wXfqx1l.png)

Linus Torvalds

作業系統: Linux --> 1991? 22 歲 Unix
    Ubuntu, CentOS, RedHat,....

git：大約 10~14 天

「最新版本？」
「兩個版本之間的差異？」
「什麼功能是誰寫的？」
「什麼功能是在什麼時候寫的？」
「什麼功能是什麼時候拿掉的？誰拿掉的？」
「沒有負擔做很多功能測試」

---

## 任務 1: 安裝 git

確認電腦裡是否有安裝過 git:

```bash=
git --version
```


沒有安裝過的到 https://git-scm.com/download/win 下載安裝檔

windows:
https://gitbook.tw/chapters/environment/install-git-in-windows.html

提示: 安裝路徑中不要有中文字，容易出錯。

git 版本更新 https://blog.poychang.net/git-update-to-latest-version/

---

## 任務 2: 設定環境變數

```bash=
$ git config --global user.name "''" "ashleylai"
$ git config --global user.email "ashleylai58@gmail.com"

# 確認設定的內容
$ git config --list

```

其實設定檔是存在 ~/.gitconfig 這個檔案

--- 

## 任務 3: 建立 repo

repository (存儲庫) --> repo

每一個專案的進度(版本)都是獨立控管

initial

在要被控管的專案底下，輸入這個指令
```bash=
$ git init
```

會在這個 hello-git 內建立了 .git 檔案夾，之後所有關於 git 管理的資訊都會存在這個檔案夾。

Q. 如果 hello-git 這個檔案夾(專案) 不想再被 git 管理了？
A: 直接把整個 .git 檔案夾刪掉 `rm -r .git`

![](https://i.imgur.com/iYbhwu4.png)

暫存區: 放準備要提交的檔案 (這一次要 commit 的)

---

## 任務 4: 在 repo 中新增、修改、刪除檔案

```bash=
# 查看 git 的狀態
$ git status

# 把檔案加入
$ git add test.txt

# 提交這次的修改
$ git commit -m "正確填寫這次 commit 的資訊"

# 檢視這次修改的差異
$ git diff

# 已經加入過的檔案，又有修改的話，一樣要再 add 一次，才可以 commit
$ git add test.txt
$ git commit -m "xxxx"
# 針對已經加入過的檔案，可以直接用以下指令提交
$ git commit -am "xxxxx"

# 可以「反悔」加入暫存區
$ git restore --staged login.html

# 反悔剛剛的修改
$ git restore login.html

# 讓檔案回到某個特定版本
$ git checkout <commit> test.txt

# 讓檔案回復到前兩個版本
$ git checkout HEAD~2 test.txt
# 回到現在版本
$ git checkout HEAD
```

練習：在 hello-git 建立至少兩個檔案，編輯他們，建立出至少三個 commit log 來。


`git log` 相關指令
```bash=
# 查看提交紀錄
$ git log

# 查看特定檔案的紀錄
$ git log <file>

# 查看檔案修改細節
$ git log -p a.txt

# 可以搜尋關鍵字
$ git log --grep="delete"

# 查看內容是誰編寫的
$ git blame test.txt
```


寫寫程式.. 當你覺得完成了一個功能
登入功能: html, Javascript, CSS

- 當他 html 做好表單、按鈕 -> 提交一次
- 有的人是全部做完才提交

「團隊一致性」
 
有修改、改到你覺得應該要提交
git status


練習
1. 把檔案從暫存區中移出
修改兩個檔案，把這個檔案都加入暫存區
```bash=
$ git add <file1>
$ git add <file2>

$ git status 
# 暫存區應該要有兩個檔案

# 把檔案從暫存區中移出
$ git restore --staged <file1>

$ git status
```

2. 反悔修改
```bash=
$ git restore <file1>
```

```bash=
# 從 git 中刪除檔案
$ git rm <file>

# 如果是在硬碟中刪除了檔案 (rm)
$ git restore <file>
```

---

## 任務 5: 建立分支與合併

分支 branch

預設分支: master / main

BLM運動 master -> slave

master server - slave server

把 git 預設分支改成 main
```bash=
$ nano ~/.gitconfig      
```

```
[init]
        defaultBranch = main
```

如果 hello-git 是 master 的同學可以執行以下指令把主分支改成叫 main：
```bash=
$ git branch -m master main
```


分支指令：

```bash=
# 檢視分支
$ git branch

# * 是標注你所在的分支

# 建立分支 
$ git branch <branch-name>

# 切換分支
$ git switch <branch-name>

```

### merge

情境:
分支 main: 主分支
分支 feature-login: 這是用開發 login 功能的

當我們把 login 功能完成後，必須把這個 login 分支「merge」回主分支去

```bash=
$ git switch main

$ git merge feature-login

# 如果兩個分支有提交過同一個檔案的修改，那就有可能發生衝突 confict
# 就只能人工修改，可能需要跟同事討論
# 解完衝突之後，就要再 commit 一次
```

login merge 進去 main

當發 pull request 的時候，有衝突，要求開發的人回到自己的電腦，
把 main merge 進去 login 一次，再 push 一次這個 login。


==9/18 作業==

- 練習基本 linux 指令
- 複習任務五以前的 git 指令
- 自己完成任務 6

--- 

## 任務 6: 建立 Github 帳號



--- 

## 任務 7: 建立 github repo

1. 在 github 上建立一個 github repo

```bash=
git remote add origin git@github.com:azole/hello-git.git
```
- remote: 遠端
- add: 增加
- origin: 是這個遠端的名字，可以不要叫做 origin，但我建議不要改
- git@github.com:azole/hello-git.git: 就是那個遠端 repo 的網址

```bash=
git push -u origin main
```
push: 推送程式碼到遠端去，而且是推到 origin 這個遠端，要推送的分支是 main

---

## 任務 8: 撰寫 readme

https://markdown.tw/

使用 Markdown 語法撰寫 readme 檔案
- 介紹專案
- 解釋專案怎麼安裝
- 解釋專案怎麼使用
- ...


--- 

## 任務 9: 了解 git flow

要合併分支，會在 github 發 pull request，請另外一個同事幫忙做 code review。

- 測試看看要合併的這個分支功能是否正常
    - 測試哪些情境？
    - 開發工程師的產出是程式碼
- coding style 有沒有符合我們團隊的規範
- 看看這次的程式有沒有什麼可能的問題，例如效能問題



![](https://i.imgur.com/rV7GdFn.png)

--- 

頻率
嚴重程度

首頁: 有一個錯字... 頻率高、不太嚴重

購物車結帳的按鈕，100 個人裡面有一個人按結帳按鈕會失敗: 頻率不高、蠻嚴重

頻率高、又很嚴重 ---> 優先權
嚴重的、比頻率


我要做什麼事、然後我已經做什麼了、我預期應該要看到什麼、但是我看到了什麼


---

## 補充

### 參考資料

- [Git 10 週年，Linux 之父談他是怎麼在 10 天內開發完成](https://buzzorange.com/techorange/2015/04/09/linus-torvalds-talked-about-git/)
- [22 歲開發出 Linux 的 FullStack 天才：Linus Torvalds 的故事](https://www.techapple.com/archives/19224)


- [Git 與 Github 版本控制基本指令與操作入門教學](https://blog.techbridge.cc/2018/01/17/learning-programming-and-coding-with-python-git-and-github-tutorial/)

### git alias

nano ~/.gitconfig

貼上以下這段

```
[alias]
	co = checkout
	br = branch
	ci = commit
	st = status
        lg = log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cd) %C(bold blue)<%an>%Creset' --abbrev-commit --date=iso
	l = log --oneline --graph
        la = log --all --oneline --decorate --graph
```

### 常用的終端機指令

```bash
. 現在的檔案夾位置
.. 上一層案夾
~ 我的目錄，就是目前這個「使用者的目錄」，像是 /Users/aaa 之類的
```

/User/xxx 
/C/Users/iii_student

```bash=
# 回到使用者目錄或是 home 目錄
cd ~
# 回到上一層
cd .. 
```

參數的意義，不同指令會不一樣，但通常會是這樣
-a ==> all   全部
-f ==> force 強制

| Windows | MacOS/Linux | 說明 |
| -------- | -------- | -------- |
| cd     | cd     | 切換目錄 change directory    |
| cd     | pwd     | 顯示目前所在路徑     |
| dir     | ls     | 列出目前檔案夾的檔案列表  list   |
| mkdir     | mkdir     | 建立新的檔案夾  make dir   |
| copy     | cp     | 複製檔案   copy  |
| move     | mv     | 移動檔案   move  |
| del     | rm     | 刪除檔案    remove |
| cls     | clear     | 清除畫面上的內容     |
| cat     | cat     | 印出檔案內容     |

```bash=
# 建立 hello-git 檔案夾
mkdir hello-git
# 進入 hello-git 檔案夾
cd hello-git
# 建立檔案 test.txt
touch test.txt

ls
# 列出全部檔案（列出隱藏檔）
ls -a   
# 以完整格式列出檔案
ls -l
# 以完整格式列出所有的檔案
ls -al

# 檢視檔案內容
cat test.txt
```

nano 

ctrl+x => y => enter

