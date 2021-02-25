# 安裝RabbitMQ Server

* 	下載 Erlang 安裝後設定環境變數ERLANG_HOME和PATH
https://medium.com/@mybaseball52/install-rabbitmq-on-win-10-a039d48e1c80

*	打開PowerShel，先安裝chocolatey
指令:
```Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))```
安裝完後可輸入choco -? 確認是否有安裝成功

*	安裝RabbitMQ
指令: choco install rabbitmq
安裝成功後可到背景程式確認RabbitMQ是否有正確執行（或重新開機後確認）
![](https://i.imgur.com/M7Fa7fK.png)


*	打開CMD，到RabbitMQ Server資料夾裡面的sbin
Cd “C:\Program Files\RabbitMQ Server\rabbitmq_server-3.8.5\sbin”
指令:  rabbitmq-plugins enable rabbitmq_management
成功之後就可以使用http://localhost:15672/  來管理RabbitMQ Server
*	進入http://localhost:15672/ 
帳號:guest 密碼:guest
進入之後建議先到Admin tab新增user
 ![](https://i.imgur.com/uE62CKv.png)
新增之後點擊剛剛的user name ，設定權限，然後把guest刪除
 ![](https://i.imgur.com/pGwKLyD.png)

*	新增防火牆TCP PORT 5672和15672，若是VM則需新增VM的Inbound security rules
*	在別台電腦輸入 http://{ip}:15672 確認是否成功連線
