# Telegram

## 简介
借助Telegram官方文档telethon和申请的api接口，实现群组的自动添加，群组消息的爬取，还有对群组索引机器人提供的全部群组进行爬取。
需要注册账号后申请Telegram bot接口，获取到api id和api hash填入代码的相应未知，第一次运行时需要接收验证码创建连接。
## 群组自动添加
添加目前尚未加入的群组首先要获得群组实体，get_entity方法可以通过群组身份（例如```@Chat_CN```）或者群组url（例如```t.me/pythonzh```） 获取实体，通过创建一个需要添加的群组链接表变可以实现群组的自动添加。
## 群组文本消息及图片消息的爬取
设置需要爬取消息的群组名称，获取迭代列表，可以记录消息时间、发送者和消息内容。对音视频消息的爬取功能会在之后的项目中实现。
群组会为每条消息按时间设置递增的消息id，增量爬取通过与上次爬取结束时的消息id对比来实现。
图片爬取```photos = client.get_messages(group_id, None, filter=InputMessagesFilterPhotos)```通过InputMessagesFilterPhotos过滤器实现，并将图片按群组id-图片id格式存储。
参考[delete-duplicate-files.rb](https://github.com/yeziyezi/scripts/blob/master/delete-duplicate-files.rb)，可以实现去除重复图片。

## 群组索引机器人
群组索引机器人会通过你回复的关键字匹配符合条件的群组名称和url，通过send_message和get_message方法实现交互，用click方法点击下一页获取内容。
通过对这一步获取的url进行整合，可以作为群组自动添加的来源。

