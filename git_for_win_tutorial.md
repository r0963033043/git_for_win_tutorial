# Git for Windows
#### 參考：
安裝：https://gitbook.tw/chapters/environment/install-git-in-windows.html
快捷鍵：https://juejin.im/post/5bd5a08cf265da0add520772

新增環境變數：https://www.itread01.com/p/912692.html
設定sudo:https://www.itread01.com/content/1548980665.html
設定make:

git bash 設定:https://github.com/xnng/my-git-bash


## 教學步驟
- [ ] Step1：到官網下載git並安裝
  1. https://git-scm.com/download/win
  2. 一路按下一步按到底
  3. 安裝完就可在任意處按右鍵點選```git bash```開始使用

- [ ] Step2：設定快速鍵(Ctrl+Alt+T)開啟```git bash```
  1. 按```win鍵```搜尋```Git Bash```，點選```開啟檔案位置```
  2. 右鍵點選```Git Bash```，點選```屬性```
  3. 設置快捷鍵，輸入```Ctrl+Alt+T``` 

- [ ] Step3：解決快捷鍵延遲問題
問題：按下快捷建終端會延遲3秒才打開，是某些版本的windows上普遍存在的bug
解決方法：禁用服務```SysMain```
  1. 按```win鍵```搜尋```服務```並打開
  2. 找到並按右鍵點選```SysMain```，選擇```停用```

- [ ] Step4：新增sudo指令到環境變數
問題：windows沒有sudo指令
解決方法：自己寫一個執行在Windows系統的sudo命令工具
＊＊＊未完成
  1. 新建文字檔```sudo.vbs```，複製以下文字到檔案
```vbs=
'ShellExecute 方法

'作用: 用於執行一個程式或指令碼。

'語法
'      .ShellExecute "application", "parameters", "dir", "verb", window
'      .ShellExecute 'some program.exe', '"some parameters with spaces"', , "runas", 1

'關鍵字
'   application   要執行的程式或指令碼名稱
'   parameters    執行程式或指令碼所需的引數
'   dir           工作路徑，若未指定則使用當前路徑
'   verb          要執行的動作 (值可以是 runas/open/edit/print)
'                   runas 動作通常用於提升許可權
'   window        程式或指令碼執行時的視窗樣式 (normal=1, hide=0, 2=Min, 3=max, 4=restore, 5=current, 7=min/inactive, 10=default)


Set UAC = CreateObject("Shell.Application")
Set Shell = CreateObject("WScript.Shell")
If WScript.Arguments.count<1 Then
    WScript.echo "語法:  sudo <command> [args]"
ElseIf WScript.Arguments.count=1 Then
    UAC.ShellExecute WScript.arguments(0), "", "", "runas", 1
'    WScript.Sleep 1500
'    Dim ret
'    ret = Shell.Appactivate("使用者賬戶控制")
'    If ret = true Then
'        Shell.sendkeys "%y"        
'    Else
'        WScript.echo "自動獲取管理員許可權失敗，請手動確認。"
'    End If
Else
    Dim ucCount
    Dim args
    args = NULL
    For ucCount=1 To (WScript.Arguments.count-1) Step 1
        args = args & " " & WScript.Arguments(ucCount)
    Next
    UAC.ShellExecute WScript.arguments(0), args, "", "runas", 5
End If
```
  
  2. 開啟```檔案```，右鍵點選```主機```，點選```內容```
  3. 左邊點選```進階???```，（在```進階```）點選```環境變數```，在```系統變數```裡雙擊```path```，點選```新增```
  4. 將```sudo.vbs```所在路徑新增到環境變數


- [ ] Step5：修改預設、新增工具--字體、主題、tmux
使用套件：https://github.com/xnng/my-git-bash
  1. 開啟```git bash```下載套件：
```bash
$ git clone https://github.com/xnng/my-git-bash.git
$ cd my-git-bash
```
  2. 安裝字體
解決unicode亂碼問題。執行後，將字體文件拖放進字體庫
```bash
$ start c://Windows//Fonts && start %cd%/fonts
```
  3. 安裝主題
```bash
$ sudo cp .minttyrc ~ && cp git-prompt.sh /etc/profile.d
```
  4. 安裝tmux
```bash
$ sudo cp tmux/bin/* /usr/bin && cp tmux/share/* /usr/share -r
$ echo -e "setw -g mouse\nset-option -g mouse on" > ~/.tmux.conf
```



- [ ] Step6：

