# 爬虫类使用方法
* 安装需要的python库`pip install -r requirements.txt`
* 修改`config.ini`文件里面的mongoDB和redis配置
* 运行`nohup python main.py > log.log 2>&1 &`
* nohup启动后，爬虫会以守护进程的方式运行
## Mongo数据
### 分区数据
对于每一个分区，都有一个collection，名字对应
* comprehensive: 综合热榜
* national_original: 国创相关
* anime: 动漫
* music: 音乐
* dancing: 舞蹈
* games: 游戏
* knowledge: 知识
* technology: 科技
* sports: 运动
* fashion: 时尚
* fun: 娱乐
* movies: 影视
* origin: 原创
* rookie: 新人
每一个分区的数据包含：
* title: 视频名
* onwerName: 作者名
* views: 播放量
* comments: 评论数
* favorites: 收藏数
* likes: 点赞数
* coins: 投币数
* shares: 分享数
* pubLocation: 发布地点
* uploadTime: 发布时间
* duration: 视频时长
* bvid: bvid
* rank: 在当前分区的排名
* rcmdReason: 推荐理由（仅综合热榜有）
### 分区弹幕
对于每一个分区的弹幕，所在是collection的名字是分区名后面加Comments。如comprehensive分区的弹幕是comprehensiveComments
弹幕包含三种数据：
* content: 弹幕内容
* videoTime: 在视频里面出现的时间（相对于视频时间）
* videoRealTime: 在视频里面出现的时间（相对于真实世界的时间）
时间都使用时间戳表示
## Redis数据
### 情感分析
redis里面存储了情感趋势。set里面有多个key，这个key是时间，value对应有positive，negative和neutral三种的值，表示每一个时间段内三种情感的数量
### 点赞投币趋势
redis里面存储量点赞投币其实。哈希表里面有多个key，这个key是排名，value对应有coins，likes和favorites三种的值，表示每一个排名的投币、点赞和收藏数量。