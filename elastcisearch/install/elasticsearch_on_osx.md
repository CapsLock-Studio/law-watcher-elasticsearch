Install elasticsearch on OSX
=============================


## Install the correct Java version

要執行 elasticsearch，必須安裝 JAVA

	https://java.com/en/download/mac_download.jsp

point $JAVA_HOME to the Java installation path in your .bash_profile:

	export JAVA_HOME="/Library/Internet Plug-Ins/JavaAppletPlugin.plugin/Contents/Home"


## Install ElasticSearch via homebrew

在 OSX ，可以透過 homebrew 套件管理安裝 ElasticSearch

	brew update
	brew install elasticsearch

	ln -sfv /usr/local/opt/elasticsearch/*.plist ~/Library/LaunchAgents


## Elasticsearch 的啟動與停止

### 自動啟動

使用 launchctl，開機時自動啟動 elasticsearch 

#### run 

	launchctl load ~/Library/LaunchAgents/homebrew.mxcl.elasticsearch.plist

#### stop 

	launchctl unload ~/Library/LaunchAgents/homebrew.mxcl.elasticsearch.plist


### 手動啟動

執行 binary `elasticsearch` 手動啟動 elasticsearch，參數 --config 可指定設定檔檔案路徑

	elasticsearch --config=/usr/local/opt/elasticsearch/config/elasticsearch.yml

### 確認是否已經啟動

elasticsearch API 預設使用主機 port 9200

執行以下指令確認 elasticsearch 運作正常 
	
	curl -X GET http://localhost:9200


## 發生錯誤怎麼辦

elasticsearch 安裝過程中，如果出現這些訊息，可參考這些解決方法

### Path had bad ownership/permissions

	/usr/local/Cellar/elasticsearch/2.1.0_1/homebrew.mxcl.elasticsearch.plist: Path had bad ownership/permissions
	
路徑中的檔案權限不正確，使用 chmod & chown 修改權限，範例如下

	chmod 600 homebrew.mxcl.elasticsearch.plist  
	sudo chown root homebrew.mxcl.elasticsearch.plist
	
### WARNING: launchctl will fail when run under tmux.

在 tmux 的環境下，無法執行 launchctl 命令，結束 tmux 應可順利執行



