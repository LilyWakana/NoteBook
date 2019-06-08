### 分词
对文本进行分词，可以使用开元库jieba等等。应该提供数据冗余、自定义词库等等。

也要对当前知识库进行分词

词库=知识库 + 自定义词库 + （用户输入）
### tf-idf
- 可以使用scikit进行tf-idf的计算，计算用户的输入的词语的tf-idf

预处理
- 对知识库的每条记录计算tf-idf

### simhash
- 使用tf-idf作为用户输入词汇的simhash的权重
- 计算输入的simhash

预处理
- 计算每条记录的simhash


### 检索
计算输入的simhash和知识库的每条记录的simhash进行比较，返回距离最小的记录


### 归一化
- 人工创建一批问题，并打上问题类别标签
- 计算每类问题的t-i的标准特征向量

- 计算用户输入的问题的特征向量
- 判断和标准类别的相似性，最高值作为最终类别

- 根据类别分析槽位词


### 返回答案




### 其他
- 定时对计算词库进行分词，并计算这些词的idf（可以缓存）
- 定时计算知识库的每条记录的simhash特征



## 调研
### 语音识别
- 英文语音识别 https://github.com/Uberi/speech_recognition/blob/master/examples/audio_transcribe.py
	- 提供不同的识别接口:
		- sphinx
		- google
		- google cloud
		- wit.ai
		- 等等

### 分词语音转文字
