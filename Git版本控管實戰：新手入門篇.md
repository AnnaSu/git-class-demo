

### Git版本控管實戰：新手入門篇筆記:

[課程連結](http://miniasp.kktix.cc/events/dct-104001)

##GIT 課程-學習目標

1. 建立正確觀念，怎麼做版控。

2. 多使用工具做版控，可以節省時間。

3. 講解分支與合併


***

##重要名詞解釋


###版本控管Version Control

- 完整記錄文件變化過程
	
- 查詢歷史記錄，復原變更，比對差異，標記版本，變更追蹤

	>(回朔變更的歷程，找出此檔案使用者的記錄，上一個編輯的是誰？)

- 多人版控的協同作業，分支合併，版控流程，發行管理（如何解決衝突？某一個branch 是用來發行的，此branch具有權限，會自動觸發ci的機制，自動建置自動發佈到測試機，正式機也可以，優點是減少人員疏失，有做流程控管，使用多條branch，由專人做審核，確認之後就可以自動發佈到測試機上）


###工作區Workspace

- 頻繁異動的開發目錄

###儲存庫Repository 

- 本地

不做分支合併就會無法管理 在分析版本歷史過程中，從版本線圖就可以看出發生什麼事

遠端 https://bitbucket.org/

***

##版本控管的種類
- 僅本地

	- 資料夾版控
	>使用copy/paste的儲存依據-完整保存
	- RCS (Revision Control System)
	>使用diff工具-差異保存
	
- 集中式版本控管 
>優點是很容易做權限控管，把檔案都集中在一起，可以鎖定或合併，壞處是 每一次commit 都要連線，每次看log都要有網路，速度會很慢，有網路才能做一次commit，變更追蹤就沒有這麼好，例如改了三個功能，十個檔案，就不能批次做commit，無法提交新版本，無法在本地端查詢歷史記錄，只會傳遞差異的部分，而且還會壓縮，所以速度非常快

	- CVS
	>使用copy/paste的儲存依據-完整保存
	- SVN	
	>使用diff工具-差異保存

- 分散式版本控管 
>誰在什麼時間點 建了什麼版本 做了什麼修改，合併也是
>還是需要一個共同儲存的地方，例如：github，稱為遠端儲存庫，第一次clone下來，會完整備份到本地儲存庫，完整複製回來，檔案會很大，但速度會很快，因為commit不需要上網，最後再做pull（會做差異比對，確認遠端儲存庫是否有最新檔案，如果有，就做差異比對並更新）和push就好，可以在本地端建立離線版本和離線記錄，缺點是無法鎖定和權限控管，例如某個檔案鎖定大家都不能改，因為git 檔案都下載下來了，當然都不能改，所有東西在本地端了，是開放的，所以無法鎖定檔案。

如果不小心commit重要的帳號密碼？

如何使用dropbox做版控？把dropbox當做你自己的github

	- CVS
	>使用copy/paste的儲存依據-完整保存
	- SVN	
	>使用diff工具-差異保存
	
***

##安裝git工具

- git for windows
- tortoiseGit

##開始使用git工具

- 設定環境變數
	>git config --global user.name "你的姓名"
	>git config --global user.email "你的信箱"
	
	寫log規則，能寫多少就寫多少，寫越多越好
	

##DEMO

### 01 開始使用 Git 用戶端工具 ( 設定環境變數 )

<<設定 user.name 與 user.email>>

```
git config --global user.name "你的姓名"
git config --global user.email "你的Email"

git config --global user.name "Anna Su"
git config --global user.email "newstory0113@gmail.com"

```

<<個別儲存庫設定不同的 user.name 與 user.email>>
在另外一個儲存庫，可以覆蓋掉姓名和信箱的設定檔

```
git config --local user.name "你的姓名"
git config --local user.email "你的Email"

```

實際上這些設定會寫到 .git/config設定檔裡。


<<設定 alias>>

```
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.sts "status -s"
git config --global alias.br branch
git config --global alias.re remote
git config --global alias.di diff
git config --global alias.type "cat-file -t"
git config --global alias.dump "cat-file -p"
git config --global alias.lo "log --oneline"
git config --global alias.ll "log --pretty=format:'%h %ad | %s%d [%Cgreen%an%Creset]' --graph --date=short"
git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset %ad |%C(yellow)%d%Creset %s %Cgreen(%cr)%Creset' --abbrev-commit --date=short"
git config --global core.editor notepad.exe
git config --global core.autocrlf true
git config --global help.autocorrect 1

```

<<變更預設編輯器>>

```
git config --global core.editor notepad.exe

```

### 02 建立工作區 (Workspace) 與本地儲存庫 (Local Repository)

<<建立工作區>>

- demo 建立一個空的儲存庫，

```
mkdir p1
cd p1
git init
echo %time% > time.txt
git add .
git status
git commit跳出notpad
輸入commit訊息 儲存再關閉
```

<<建立本地儲存庫>>

```
mkdir p1
cd p1
git init
echo test > test.txt
git status
git add .
git status
git commit -m "Initial commit"
git log
```


### 03 複製遠端儲存庫 (Remote Repository) 並建立工作區

git clone https://github.com/github/gitignore.git

透過clone 複製一個遠端資料庫的檔案

copy to clipboard

<<複製儲存庫>>

```
git clone https://github.com/github/gitignore.git

```




###04 從GitHub 建立新的遠端儲存庫 (Remote Repository)、複製回來 (clone)、建立版本 (commit)、推送上去 (push)

####複製回來 (clone)

```
git clone https://github.com/AnnaSu/git-class-demo.git
```

####暫存檔案 (add)
>加入暫存後，狀態會從Changes not staged for commit變成Changes to be committed

```
git add . or git add 檔案名稱
```

####建立版本 (commit)

```
git commit -m "git notes"
```

####推送上去 (push)

git remote add remote名稱 remote網址

例如：

```
git remote add git-class-demo-remote https://github.com/AnnaSu/git-class-demo.git
```

查看remote列表，確定已正確被加入遠端位置

```
git remote
```

git push -u origin（remote名稱） master（目前branch名稱）


例如:

```
git push git-class-demo-remote master
```



Remote origin 代表原本clone的位置
但如果原本clone的位置沒有權限，可以push到另外一個自己的repo

### 05 將本地儲存庫推送到一個遠端儲存庫，並設定 origin 遠端儲存庫位置與設定遠端追蹤分支



### 06 將本地儲存庫推送到一個已經有版本的遠端儲存庫 (需先 pull 合併後再 push 上去)

***
pull 遠端有本地沒有，無法push的時候要做pull
push 本地有遠端沒有

如果兩種情況都存在，就要先pull先更新再進行push進行合併。




