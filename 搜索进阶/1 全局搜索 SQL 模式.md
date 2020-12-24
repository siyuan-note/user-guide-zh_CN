## `blocks` 表
{: id="20201117103851-l9cahuc"}

该表用于存储内容块数据。
{: id="20201222212031-yor7l6v"}

|  字段 | 类型 | 说明                                      |
| --------: | :------: | --------------------------------------------- |
|      id |  text  | 内容块 ID                                |
|     box |  text  | 笔记本名                                |
|    path |  text  | 内容块所在文档路径                 |
| tree_id |  text  | 抽象语法树 ID，和根节点 ID 相同 |
| content |  text  | 内容块 Markdown                          |
|    type |  text  | 内容块类型                             |
|    time |  text  | 日期时间                                |
{: id="20201222212031-jnbrj51"}

示例：
{: id="20201222212031-vil9r7k"}

```sql
SELECT * FROM blocks WHERE content LIKE '%内容块%'
```
{: id="20201222212031-fk6aspl"}

`type` 内容块类型值列表请参考((20201224091608-s8dzhjc "这里"))。
{: id="20201222212031-tghln16"}

## 默认查询条件
{: id="20201222212031-sltqve6"}

* {: id="20201222212031-sn1prwa"}如果不指定 `type` 列，则默认会加上 `type = p`，即只查询段落块
* {: id="20201222212031-tfte2r9"}如果不指定 `LIMIT`，则最多只返回前 32 条结果
{: id="20201222212031-njp0qkt"}


{: id="20201222093044-rx4zjoy" type="doc"}
