elasticsearch on laravel 
=========================
簡介 elasticsearch on laravel 

# PHP API

以下套件皆遵循 [Elasticsearch PHP API](https://www.elastic.co/guide/en/elasticsearch/client/php-api/current/index.html)

## Elasticsearch PHP Client

- [elasticsearch-php](https://github.com/elastic/elasticsearch-php)  
*官方版本*


- [Elastica](https://github.com/ruflin/Elastica)  
能使用 image, attement 等 plugin 


## Elasticsearch for Laravel

- [laravel-elasticsearch](https://github.com/shift31/laravel-elasticsearch)  
能在 laravel 裡面使用 Es 操作

## 教學

http://blog.madewithlove.be/post/integrating-elasticsearch-with-your-laravel-app/


# Eloquent ORM + Elasticsearch

Elasticsearch for Eloquent Laravel Models

## package

[larasearch](https://github.com/iverberk/larasearch)

[Elasticquent](https://github.com/elasticquent/Elasticquent)

[Elasticquent - Laravel 5](https://github.com/mustafaaloko/elasticquent5)

## 教學

http://fullstackstanley.com/read/simple-search-with-laravel-and-elasticsearch

# JDBC importer for Elasticsearch

[elasticsearch-jdbc](https://github.com/jprante/elasticsearch-jdbc)

匯入 MySQL 到 elasticsearch


# 參考資料

[Managing Relations Inside Elasticsearch](https://www.elastic.co/blog/managing-relations-inside-elasticsearch)


# 我應該要知道些什麼

- 安裝 elasticsearch
- 設定 laravel eloquent ORM 與 elasticsearch mapper,  document index
- es 直接抓 mysql 的資料


1. 清楚了解架構
2. 各個 service 跟 package 的用途
3. 什麼時候該做什麼事情

## 實作情境

需求，行為，實作

### 開放部分資料表的資料給 user 做關鍵字查詢

- 需求

	a api interface for pipimy query store, product,
	
		curl -X GET /api/search?d=keyword

- 行為

	- 定義哪些欄位要給查詢
	- 根據 es api 分類的 data type，設定好這些欄位的 mapping type 作為 properties
	- 在 middleware, 觸發 events 為 before database insert, update (特定資料表) 做 putMapping
	- create a command allAllToIndex() 
	
- 實作

	- mapping 
	
		- index name : pipimy_service  
		- type name : products
		- field 
		
	


### 分析 & 探勘資交易紀錄，找到趨勢,統計,摘要或異常

### 比價平台

### analytics/business-intelligence

# 實作

## 安裝 elasticsearch 

## 開 branch feature/elasticsearch

### install package 

	composer require aloko/elasticquent5 
	
### adding the service provider 

### publishing the config file

### Adding it to models

- product



1. set mapping properties in your model
2. set a custom index name, 

	example : twitter
	
	pipimy_service

3. set a Custom Type Name, 預設值是 models name


----------------------------------
以下是尚未整理的內容
------------------------------


	composer require spatie/searchindex

```
{
	"require": {
		"elasticsearch/elasticsearch": "^1.3"
	}
}
```


目標: 

1. install Elasticsearch server

		curl -X GET 'http://localhost:9200'
	
2. Elasticsearch 支援 mysql

		JDBC importer for Elasticsearch
		
3. Elasticsearch client (Elasticsearch-PHP)

4. Search with Laravel and ElasticSearch

