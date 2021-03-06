## 江苏大学自动健康打卡项目
> selenium自动化 模拟人工打卡
### 主要流程：
1. 设置谷歌浏览器
2. 身份认证登录
3. 填写健康表单
4. 发送邮件通知

### 核心技术点：
##### 验证码识别：身份认证登录时需要填写验证码
解决方案：调用百度OCR，识别验证码
##### 邮箱通知：将打卡结果反馈给用户
解决方案：调用SMTP服务，利用网易邮箱实现
##### 服务器部署：将项目部署在linux服务器上以实现定时效果
解决方案：租用阿里云主机，利用crontab和bash脚本实现

### 项目文件介绍：
- data -- 存放屏幕截图和处理后的验证码图片
- results -- 存放打卡信息，json格式
- AipOcr.py -- 百度OCR应用服务
- chromedriver.exe -- chrome浏览器驱动文件(需要根据chrome版本进行替换)
- crontab -- crontab配置文件，部署linux服务器时使用，用于启动定时任务
- HealthPunch.sh -- bash脚本文件，部署linux服务器时使用，用于激活conda环境
- Mail.py -- 调用SMTP服务给用户发送邮件通知
- main.py -- 主程序，控制项目整体的运行
- README.md -- 项目说明文件 
- requirements.txt -- pip包列表
- Settings.py -- 项目设置文件，包括所有有关信息的设置，如综合服务门户登录账号密码等
- VerCode.py -- 识别验证码，主要内容为截取验证码图片并调用AipOcr.py

### 如何拿来用？
##### Windows本地部署

- pip下载安装对应的包，参考requirements.txt
- 下载chrome浏览器和对应版本的驱动(chromedriver.exe)，放至项目目录下，替换原有的驱动文件
- 申请百度OCR应用服务，替换Settings.py中的对应设置项
- 开通邮箱的SMTP服务，获取邮箱授权码等
- 填写Settings.py中的综合服务门户登录信息和其它各类信息
> 注意：
>
> 在windows端调试时，若已经注释掉headless指令,启用chrome界面，则需要将系统显示设置中的缩放调成100%，否则selenium截图时会出现验证码位置不匹配的情况
>
> 本项目默认用户至少已经打了1次卡，填写健康表单时只填写温度等每次打卡必须重新填写的信息。若用户1次卡也没打过，打卡表单没有地址等信息，则会引发报错 

##### Linux服务器部署

- 租用一台服务器或使用树莓派并配置 virtualenv 环境
- 下载并安装chrome浏览器和对应版本的linux驱动
- 修改HealthPunch.sh和crontab文件

### 欢迎与我交流：
> 作者邮箱：Amoza.light@gmail.com
>
> 免责声明：这只是一个编程实践的小项目，希望我不会被校领导请去喝茶