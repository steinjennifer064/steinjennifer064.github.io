ChatGPT 近期以其强大的对话和信息整合能力风靡全网，能够写代码、改论文、讲故事，几乎无所不能。这让人不禁产生一个大胆的想法：能否利用 ChatGPT 的对话模型，将微信打造成一个智能机器人？这样不仅可以在与好友对话中提供意想不到的回应，还能提升工作效率。

本项目基于 ChatGPT 的微信聊天机器人，通过 [OpenAI](https://bit.ly/bewildcard) 接口生成对话内容，并使用 [ItChat](https://github.com/littlecodersh/ItChat) 实现微信消息的接收和自动回复。

---

## 简介

### 已实现特性

- **文本对话**：接收私聊及群组中的微信消息，使用 ChatGPT 生成回复内容，完成自动回复。
- **规则定制化**：支持私聊中按指定规则触发自动回复，支持对群组设置自动回复白名单。
- **多账号支持**：支持多微信账号同时运行。
- **图片生成**：支持根据描述生成图片，并自动发送至个人聊天或群聊。

---

## 更新日志

- **2022.12.19**：引入 [ItChat-UOS](https://github.com/why2lyj/ItChat-UOS) 替换 ItChat，解决网页微信登录问题，并兼容 Python 3.9。
- **2022.12.18**：支持根据描述生成图片并发送，OpenAI 版本需大于 0.25.0。
- **2022.12.17**：从原方案切换为调用 OpenAI 官方 API，提升稳定性和响应速度，但暂不支持上下文记忆的对话。

---

## 快速开始

### 准备

#### 1. 注册 OpenAI 账号

前往 [OpenAI 注册页面](https://bit.ly/bewildcard) 创建账号，并在 [API 管理页面](https://beta.openai.com/account/api-keys) 创建一个 API Key。保存该 Key，后续需要在项目中配置。

> 项目中使用的对话模型为 `davinci`，计费方式为每 1k 字（包含请求和回复）消耗 $0.02，图片生成每张消耗 $0.016。新账号有 $18 免费额度，使用完后可更换邮箱重新注册。

#### 2. 运行环境

支持 Linux、MacOS、Windows 系统（可在 Linux 服务器上长期运行），同时要求安装 Python（版本需在 3.7.1~3.9.X 之间，Linux 环境建议使用 3.7.X）。

1. 克隆项目代码：

   bash
   git clone https://github.com/zhayujie/chatgpt-on-wechat
   cd chatgpt-on-wechat/
   

2. 安装所需核心依赖：

   bash
   pip3 install itchat-uos==1.5.0.dev0
   pip3 install openai==0.25.0
   

---

### 配置

配置文件模板位于项目根目录的 `config-template.json` 中，需复制该模板创建最终生效的 `config.json` 文件：

bash
cp config-template.json config.json


然后在 `config.json` 中填入自定义配置，各配置项含义如下：

json
{
  "open_ai_api_key": "YOUR API KEY",                           // 填入上面创建的 OpenAI API KEY
  "single_chat_prefix": ["bot", "@bot"],                      // 私聊时文本需要包含该前缀才能触发机器人回复
  "single_chat_reply_prefix": "[bot] ",                       // 私聊时自动回复的前缀，用于区分真人
  "group_chat_prefix": ["@bot"],                              // 群聊时包含该前缀则会触发机器人回复
  "group_name_white_list": ["ChatGPT测试群", "ChatGPT测试群2"], // 开启自动回复的群名称列表
  "image_create_prefix": ["画", "看", "找"]                    // 开启图片回复的前缀
}


**配置说明**：

- 私聊中，需要以 `bot` 或 `@bot` 为开头的内容触发机器人，对应配置项 `single_chat_prefix`；机器人回复的内容会以 `[bot]` 作为前缀，用于区分真人。
- 群组聊天中，群名称需配置在 `group_name_white_list` 中才能开启群聊自动回复。默认情况下，只要被 @ 就会触发机器人自动回复，或者检测到以 `@bot` 开头的内容。
- 图像生成需满足触发条件外，还需要额外的关键词，对应配置项 `image_create_prefix`。
- 关于 OpenAI 对话及图片接口的参数配置（内容自由度、回复字数限制、图片大小等），可参考 [对话接口文档](https://beta.openai.com/docs/api-reference/completions) 和 [图像接口文档](https://beta.openai.com/docs/api-reference/completions)，直接在项目代码 `bot/openai/open_ai_bot.py` 中调整。

---

### 运行

1. 如果是本地调试，直接在项目根目录下执行：

   bash
   python3 app.py
   

   终端输出二维码后，使用微信扫码。当输出 "Start auto replying" 时，表示自动回复程序已成功运行（注意：用于登录的微信需完成实名认证）。

2. 如果是服务器部署，则使用 `nohup` 命令在后台运行：

   bash
   touch nohup.out                                   # 首次运行需新建日志文件                     
   nohup python3 app.py & tail -f nohup.out          # 后台运行程序并输出日志
   

   同样在扫码后，程序即可成功运行于服务器后台。

---

👉 [WildCard | 一分钟注册，轻松订阅海外线上服务](https://bit.ly/bewildcard)