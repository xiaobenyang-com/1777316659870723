# 万智牌卡牌查询服务 

一个基于Model Context Protocol (MCP)的服务端，提供万智牌中文卡牌信息的查询和搜索功能。
A server based on Model Context Protocol (MCP) that provides query and search functions for Chinese card information of Wanzhi brand.## 工具列表 Tool List

本MCP服务封装下列工具，可让模型通过标准化接口调用以下功能。 本MCP服务封装下列工具，可让模型通过标准化接口调用以下功能。

| 工具 Tool   | 描述 Description         |
|-------|--------------------|
| get_card_by_set_and_number | 通过系列代码和收集编号获取单张卡牌。 |
| search_cards | 通过查询字符串搜索卡牌，支持分页和排序。  **查询语法示例:** - `t:creature c:r` (红色生物) - `pow>=5 or mv<2` (力量大于等于5或法术力值小于2) - `o:"draw a card" -c:u` (包含"抓一张牌"的非蓝色牌) - `(t:instant or t:sorcery) mv<=3` (3费或以下的瞬间或法术)  **分页参数:** - `page`: 页码 (整数, 默认 1) - `page_size`: 每页数量 (整数, 默认 20, 最大 100)  **排序参数:** - `order`: 按字段排序，逗号分隔。前缀 `-` 表示降序   (例如: `name`, `-mv`, `name,-rarity`)   默认排序: `name`  **其他参数:** - `unique`: 去重方式 (id, oracle_id, illustration_id) - `priority_chinese`: 是否优先显示中文卡牌 |
| get_sets | 返回所有MTG卡牌系列的完整数据，按发布日期降序排列 |
| get_set | 根据系列代码获取单个系列的详细信息 |
| get_set_cards | 获取特定系列的所有卡牌，支持分页和排序。 |
| hzls | 活字乱刷（使用卡牌图像拼接句子），将输入的文本使用魔法卡牌图像拼接成图片 |


## 检查服务 ## Inspector

工具在线测试： [https://mcp.xiaobenyang.com/inspector/1777316659870723](https://mcp.xiaobenyang.com/inspector/1777316659870723)

Online Tool test [https://mcp.xiaobenyang.com/inspector/1777316659870723](https://mcp.xiaobenyang.com/inspector/1777316659870723)

## 服务配置 MCP Server Config


> #### 如何获取 XBY-APIKEY ？ How to get XBY-APIKEY ?
> 访问小笨羊科技网站 [https://xiaobenyang.com](https://xiaobenyang.com)，注册用户即可获得APIKEY
> Visit XiaoBenYang website [https://xiaobenyang.com](https://xiaobenyang.com), register and get the APIKEY.

### SSE
```json
{
  "mcpServers": {
    "万智牌卡牌查询服务": {
      "headers": {
        "XBY-APIKEY": "<YOUR_XBY_APIKEY>"
      },
      "type": "sse",
      "url": "https://mcp.xiaobenyang.com/1777316659870723/sse"
    }
  }
}
```
### STREAMABLE HTTP
```json
{
  "mcpServers": {
    "万智牌卡牌查询服务": {
      "headers": {
        "XBY-APIKEY": "<YOUR_XBY_APIKEY>"
      },
      "type": "streamable_http",
      "url": "https://mcp.xiaobenyang.com/1777316659870723/mcp"
    }
  }
}
```
### STDIO
```json
{
    "mcpServers": {
        "万智牌卡牌查询服务": {
          "command": "npx",
          "args": [
            "-y",
            "xiaobenyang-mcp"
          ],
          "env": {
            "XBY_APIKEY": "<YOUR_XBY_APIKEY>",
            "mcpId": "1777316659870723",
          },
          "transport": "stdio"
        }
      }
}

```
