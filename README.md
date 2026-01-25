# anki-prompt

最初的提示词来自：[mcp工具使用分享：anki-mcp 自动对知识进行制卡](https://linux.do/t/topic/554270)

优化点：

1. 只对有效知识制卡，没有考核价值（毕竟我的主要需求就是这个，可以自行修改）的就不制卡；
2. 脱离上下文的例子不制卡。针对把资料中的例子也单独拿出来制卡且没有上下文的情况；
3. 美化排版。没有经过排版的内容不容易阅读，挤在一堆，后面测试了一下发现我用的mcp server是支持直接使用HTML标签排版的，所以在提示词里面要求LLM使用基本的HTML标签进行语义化标记，避免内联样式（style属性设置样式），样式由卡片模板来提供。这样在保证无卡片模板的情况下也可以正常阅读，且节省token，后续还能随时替换卡片模板修改样式。
4. 添加“答案”、“解释”、“助记”字段，方便翻面之后学习。

## 工具

以下是我使用的工具，供参考：

- LLM：深度求索的deepseek-reasoner
- mcp client：Cherry Studio v1.7.13，配置如下

```JSON
{
  "mcpServers": {
    "anki": {
      "name": "anki",
      "description": "",
      "baseUrl": "",
      "command": "node",
      "args": [
        "E:\\\\01_Projects\\\\Code\\\\AI\\\\MCP\\\\anki\\\\build\\\\index.js"
      ],
      "env": {},
      "isActive": true,
      "type": "stdio"
    }
  }
}
```
- mcp server：[CamdenClark/anki-mcp-server](https://github.com/CamdenClark/anki-mcp-server)   这个mcp server还支持添加tag，挺好用的。
- anki：版本 25.09.2 (3890e12c)
- anki插件：[AnkiConnect](https://ankiweb.net/shared/info/2055492159)。因为百度输入法占用了其默认端口8765，所以我在插件设置里面改了端口，在本地的mcp server的源代码里也改了改接着重新build，就可以绕开了。

