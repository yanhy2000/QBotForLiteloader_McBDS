# QBotForLiteloader 简介

本插件用于在Liteloader加载下在MCBDS服务端内使用QQ群Bot（频道Bot暂未开发）

Bot框架采用[oicq](https://github.com/takayama-lily/oicq),目前使用[Liteloader](https://github.com/LiteLDev/LiteLoaderBDS)加载本插件，推荐使用版本>=2.9.0

> 近期事情多比较忙，如有建议或bug反馈可提issue，尽可能抽空维护

## v0.0.6 更新说明
0. 无Liteloader API更新，兼容Liteloader>=2.7.1，Readme已更新
1. 修复 密码登陆滑块验证时提交无法ticket与sms
2. 调整 监听事件与调用api逻辑顺序以优化性能
3. 修复 二维码登陆卡控制台及无输入
4. 修复 自定义聊天\指令前缀仅支持单字符问题
5. 增加 配置文件版本与初始配置验证
6. 增加 管理员可私聊机器人执行指令
7. 增加 配置文件可修改消息格式
8. 更新开发环境：Liteloader=2.9.0 BDS=1.19.51

## 功能
1. 群聊聊天内容转发至服聊(可全部转发或者自定义前缀转发）
2. BDS服务器聊天转发至Q群
3. Bot管理员可在群内发出指令至BDS控制台（自定义操作指令前缀）
4. 群内查服指令，可查询本机或者其他服（可自定义指令内容）
5. （正在开发）查询服务器系统相关状态

# 使用环境
- Liteloader >=2.7.1
- BDS >=1.19.30

# 使用方法
- 配置一个 Liteloader>=2.7.1 版本的BDS服务端(过程请参考[Liteloader安装](https://github.com/LiteLDev/LiteLoaderBDS/blob/main/README_zh-cn.md#-%E5%AE%89%E8%A3%85))
- 下载本项目中[Release](https://github.com/yanhy2000/QBotForLiteloader/releases)的最新版本插件，后缀为.llplugin格式
- 将插件放置在 BDS根目录/plugins 文件夹内，不需要改名以及其他操作
- 启动服务端，会自动进行插件初始化安装，等待开服完成后再手动关服
- 打开文件夹 BDS根目录/plugins/QBot ,打开*config.json*配置文件，对照下方详解进行修改，其中高级配置文件*Advanced_Config.json*无需修改，高级配置文件后续会更新详解
- 保存后重新开服，开服完成后自动进入登录模式，如扫码登陆异常请切换其他方式

# 配置文件说明
*机器人管理员与群管理员不同，前者需要在配置文件手动设置*

第一次启动本插件会由Liteloader自动装载相关依赖，且插件会生成配置文件在*BDS/plugins/QBot*内，您需要修改**Config.json**文件内相关内容，详解如下：

```
{
	"useQQGroup": false,//默认为禁用，使用群机器人时请启用，设置为true
	"qq": {
		"my_group": 123123,//群号（目前只开放这一个，多群等后续开放）
		"admin": [//机器人管理员，可在群内发指令到后台
			123123,
			123123456
		],
		"account": 123123,//机器人账号
		"password": ""//不填写密码则为扫码
	}
	"bds": {
		"ServerChat": true,//是否开启服务器聊天转发至群
		"chat_prefix": "chat",//玩家从群内发聊天信息至BDS的前缀(例 "chat 你好")
		"QQChat": 2,//群聊设置，0=群-x-服;  1=群(全部聊天)->-服 (图片等会简化为[图片]等传输);	2=群(带前缀的聊天)->-服
		"ServerEvent": true,//是否转发服务器事件，目前的事件有：玩家进出服
		"group_cmd": true//是否开启机器人管理员在群内发指令到BDS后台
		"private_cmd": true, //管理员私聊机器人执行指令
		"cmd_prefix": "cmd",//(仅单字符)机器人管理员从群内向BDS发指令的前缀 (例 "cmd whitelist add player")
		"motd": true,//是否开启群聊内全部人使用查服的权限（功能含查本机和查其他服，例如"查服","查服 a.abc.com 19132"，端口可不输入）
		"motd_cmd": "查服",//群内使用查服指令的前缀，可以用符号、文字、数字等，如"查服" "查服 server.com" "查服 server.com 19132"
	},
	server: {
		ip: "localhost",//目前用于查询服务器时设置本机ip，后续可能用于多服联动
		port: 19132,//同上
	},
	"format": {
		"ServerChat": "<{name}> {msg}",  // 服聊 -> 群聊
		"QQChat": "§2[QQ]{name}> {msg}",//群聊 -> 服聊
		"ServerEvent_leave": "玩家 <{name}> 离开服务器",
		"ServerEvent_join": "玩家 <{name}> 进入服务器",
		"cmd_error": "指令错误: {cmd_err}",
		"cmd_succ": "指令输出:{cmd_out}"
	},
	"config_version": 0.6 //版本，请勿手动修改
}
```

# TODO

- （√）增加可自定义修改聊天转发格式
- 增加插件功能，将机器人常用api与服务端常用api规范并引出

> 本项目只要有人用，就会一直维护下去~

高级设置不需要修改，涉及到群机器人设置，默认使用apad设备...

### 更多内容待补充，本插件正在开发中...
