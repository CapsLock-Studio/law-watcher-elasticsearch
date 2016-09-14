結巴斷詞系統建造與環境
------------------

jieba rpc server & client 

# jieba rpc server 

- python 3.4+

## 安裝

### Ubuntu

正服, 測試伺服器環境

#### 測服相關路徑

`/var/www/servicetest02.pipimy.com.tw/seg/jiebarpc`
`/usr/local/lib/python3.4/dist-packages`

#### 自動安裝

使用 pip3 安裝

	pip3 install jieba-rpc

如果沒有 pip3 可用，要先裝以下：

	apt-get install python3-pip
	
### mac

開發用測試環境

#### 自動安裝

	pip3 install jieba-rpc 
	
#### 半自動安裝

#### 手動安裝

## 啟動

	python3 -m jiebarpc localhost:8888
	
## 測試

	python3 client.py 青青河邊草
	
** 測試用程式 client.py 放在海洋的盡頭，去找吧！ **


## 設為 service 

## jieba rpc client 

- php extension msgpack 

## 安裝

### Ubuntu 

	apt-get install php5-msgpack

reload php-fpm 

	service php5-fpm reload
	
檢查是否已經支援

	<?php phpinfo();?>
	
console 環境下

	php -i | grep msgpack 
	
### mac 

	brew install php55-msgpack
	
** 視你使用的 php 版本做調整 **

# Protocol 規格


