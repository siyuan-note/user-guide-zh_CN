## `blocks` 表
{: id="20201117103851-l9cahuc"}

该表用于存储内容块数据。

|   字段 | 类型 | 说明                                      |
| -------: | :-----: | ------------------------------------------- |
|       id | integer | 自增主键                                |
| block_id |  text  | 内容块 ID                                |
|      box |  text  | 笔记本名                                |
|     path |  text  | 内容块所在文档路径                 |
|  tree_id |  text  | 抽象语法树 ID，和根节点 ID 相同 |
|  content |  text  | 内容块 Markdown                          |
|     type |  text  | 内容块类型                             |

示例：

```sql
SELECT * FROM blocks WHERE content LIKE '%内容块%'
```

`type` 内容块类型值列表：

* `NodeDocument` 文档块
* `NodeHeading` 标题块
* `NodeParagraph` 段落块
* `NodeList` 列表块
* `NodeListItem` 列表项块
* `NodeMathBlock` 数学公式块
* `NodeCodeBlock` 代码块
* `NodeBlockquote` 块引用块
* `NodeTable` 表格块
* `NodeSuperBlock` 超级块

## 默认查询条件

* 如果不指定 `type` 列，则默认会加上 `type = NodeParagraph`，即只查询段落块
* 如果不指定 `LIMIT`，则最多只返回前 32 条结果


{: id="20201222093044-rx4zjoy" type="doc"}
