Elasticsearch 分析與映射
====

# 使用版本

- elasticsearch

	2.3.3  
	主程式

- analysis-ik 

	1.9.3  
	中文分詞器  
	https://github.com/medcl/elasticsearch-analysis-ik
	
- elasticsearch-sql

	2.3.3.0  
	sql > qsl 轉換

## 附註


- ik 字典檔使用繁體版本

- ik 開啟詞庫熱更新

-  

## 選用

- analysis-icu

- analysis-smartcn

	lucene 默認的中文分詞器

- STConvert 1.6.0 
 
 	簡繁轉換
 	https://github.com/medcl/elasticsearch-analysis-stconvert
	
- elasticsearch-carrot2

	聚合搜尋結果（同義詞）  
	https://github.com/medcl/elasticsearch-carrot2
	
- elasticsearch-HQ

	用網頁介面管理 / ES 管理工具
	
## 備存

- elasticsearch-segmentspy

# 分析(analysis)和分析器(analyzer)

## analysis 過程 & analyzer 如何運作

分析是這樣的一個過程

1. 被處理後的結果被稱為詞 (Term)
2. 標準化這些詞，提高他們的可搜尋性

這個工作是分析器完成的。分析器只是以下三個功能的包裝

- character filter 字符過濾器

	過濾不必要字符
	
- tokenizer 分詞器

	分詞標準化

- token filters 標記過濾

	- 停用詞
	- 增加詞


## ES 內建的分析器

- 標準
- 簡單
- 空格
- 語言

## 當分析器被使用

##  plugin 

- analysis-ik (1.6.1)
- carrot2 
- STConvert (1.6.0)

### analysis-ik IK 分析器

讓ES支援中文搜尋

#### 安裝

1. 下載 ik 

		https://github.com/medcl/elasticsearch-analysis-ik

2. install maven

		apt-get install maven
	
		
##### 備忘
		
	apt-cache search -f 

3. compile

	- mvn package 
	- config file
	- 下載 dic (字典檔)  

4. 重新啟動 elasticsearch ，load plugin ik 

5. 熱更新 ik 字典檔


#### 可用分析器, 選項

- analyzer: ik_smart , ik_max_word
- tokenizer: ik_smart , ik_max_word

##### ik_smart

會將文本做最粗粒度的拆分，例如：中華人民共和國國歌拆分成中華人民共和國，國歌

##### ik_max_word

會將文本做最細粒度的拆分，例如：中華人民共和國國歌拆分成中華人民共和國，中華人民，中華，華人，人民共和國，人民，人，民，共和國，共和... 等各種可能的詞彙

#### 測試


### 拼音分詞器

elasticsearch-analysis-pinyin



### STConvert Analysis

簡繁轉換

elasticsearch-analysis-stconvert

- 新增stconvert的charfilter，在中文分词之前先使用本charfilter，避免分词的问题

#### 手動安裝

	mvn clean 
	mvn compile
	mvn package


#### 可用分析器, 選項

analyzers
	
	stconvert,tsconvert,stconvert_keep_both,tsconvert_keep_both

tokenizers

	stconvert,tsconvert,stconvert_keep_both,tsconvert_keep_both

token-filters

	stconvert,tsconvert,stconvert_keep_both,tsconvert_keep_both
	
char_filters

	stconvert,tsconvert

#### 測試

	http://localhost:9200/pipimy_service/_analyze?analyzer=ik&text=北京國際電視台&tokenizer=stconvert&pretty=true

-------------


### 如何在一次查詢中組合 ik 跟 stconvert

自定義一個 analyzer 組合 ik 跟 stconvert，char-filters使用 stconvert，tokenizer使用ik

### 還沒整理好的內容



### 編譯打包法

	git clone https://github.com/medcl/elasticsearch-analysis-ik
	cd elasticsearch-analysis-ik

	mvn clean
	mvn compile
	mvn package

## 內建

analyzer	logical name	description
standard analyzer	standard	standard tokenizer, standard filter, lower case filter, stop filter
simple analyzer	simple	lower case tokenizer
stop analyzer	stop	lower case tokenizer, stop filter
keyword analyzer	keyword	不分词，内容整体作为一个token(not_analyzed)
pattern analyzer	whitespace	正则表达式分词，默认匹配\W+
language analyzers	lang	各种语言
snowball analyzer	snowball	standard tokenizer, standard filter, lower case filter, stop filter, snowball filter
custom analyzer	custom	一个Tokenizer, 零个或多个Token Filter, 零个或多个Char Filter


## tokenizer

tokenizer	logical name	description
standard tokenizer	standard	
edge ngram tokenizer	edgeNGram	
keyword tokenizer	keyword	不分词
letter analyzer	letter	按单词分
lowercase analyzer	lowercase	letter tokenizer, lower case filter
ngram analyzers	nGram	
whitespace analyzer	whitespace	以空格为分隔符拆分
pattern analyzer	pattern	定义分隔符的正则表达式
uax email url analyzer	uax_url_email	不拆分url和email
path hierarchy analyzer	path_hierarchy	处理类似/path/to/somthing样式的字符串



## 安裝什麼

plugin install analysis-smartcn

plugin install analysis-icu

plugin install royrusso/elasticsearch-HQ


web administration tool 
https://github.com/lmenezes/elasticsearch-kopf/tree/v2.1.1


Inquisitor 幫忙了解 & debug your queries in ElasticSearch.


plugin install mapper-attachments
