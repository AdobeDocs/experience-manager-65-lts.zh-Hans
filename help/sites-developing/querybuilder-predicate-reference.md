---
title: 查询生成器谓词参考
description: 查询生成器API的完整谓词引用。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Developing,Search,Query Builder
role: Developer
exl-id: c044d541-24d6-4975-9b38-6a4317a16358
source-git-commit: a85b54d5a7c3b00f95f439941a390dcfee883187
workflow-type: tm+mt
source-wordcount: '2291'
ht-degree: 1%

---

# 查询生成器谓词参考{#query-builder-predicate-reference}

>[!CAUTION]
>
>本页上的信息并非详尽无遗。
>
>有关完整信息，请参阅Query Builder Debugger控制台上&#x200B;**可用谓词**&#x200B;下的列表；例如，位于：
>* [http://localhost:4502/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)
>
>例如，请参阅：
>
>* [http://localhost:4502/system/console/services？filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29](http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29)

## 常规 {#general}

* [根](#root)
* [组](#group)
* [orderby](#orderby)

## 谓词 {#predicates}

* [布尔属性](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [contentfragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [dateComparison](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [日期范围](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
* [排除路径](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [全文](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [hasPermission](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [语言](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [mainasset](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [memberOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [节点名称](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [notexpired](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [路径](/help/sites-developing/querybuilder-predicate-reference.md#path)
* [属性](/help/sites-developing/querybuilder-predicate-reference.md#property)
* [rangeproperty](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [相对日期范围](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [savedquery](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [相似](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [标记](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [tagid](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [类型](/help/sites-developing/querybuilder-predicate-reference.md#type)

### `boolproperty` {#boolproperty}

匹配JCR BOOLEAN属性。 仅接受值“`true`”和“`false`”。 如果设置为“`false`”，则当该属性的值为“`false`”或根本不存在时，该属性将匹配。 用于检查仅在启用时设置的布尔标记。

继承的“`operation`”参数没有意义。

它支持彩块化提取。 为每个`true`或`false`值提供存储段，但仅适用于现有属性。

#### 属性 {#properties}

* **布尔属性**
属性的相对路径，例如`myFeatureEnabled`或`jcr:content/myFeatureEnabled`。

* **值**
要检查属性“`true`”或“`false`”的值。

### `contentfragment` {#contentfragment}

将结果限制为内容片段。

它不支持筛选。

它不支持彩块化提取。

#### 属性 {#properties-1}

* **contentfragment**
它可以与任何值一起使用来检查内容片段。

### `dateComparison` {#datecomparison}

将两个JCR DATE属性相互进行比较。 您可以测试它们是否相等、不相等、大于或大于或等于。

仅限过滤的谓词，不能使用搜索索引。

#### 属性 {#properties-2}

* **属性1**

  第一个日期属性的路径。

* **属性2**

  指向第二个日期属性的路径。

* **操作**

  “`equals`”表示完全匹配，“`!=`”表示不相等比较，“`greater`”表示属性1大于属性2，“`>=`”表示属性1大于或等于属性2。 默认值为“ `equals`”。

### `daterange` {#daterange}

将JCR DATE属性与日期和时间间隔匹配。 使用ISO8601
日期和时间格式(`YYYY-MM-DDTHH:mm:ss.SSSZ`)，并允许部分呈现，如`YYYY-MM-DD`。 或者，时间戳可以按UTC时区(UNIX®时间格式)提供自1970年以来的毫秒数。

您可以查找介于两个时间戳之间的任何内容，比给定日期更新或更早的任何内容，也可以选择介于包含时间间隔和打开时间间隔之间的内容。

它支持彩块化提取。 提供存储桶“今天”、“本周”、“本月”、“最近3个月”、“今年”、“去年”和“比去年早”。

它不支持筛选。

#### 属性 {#properties-3}

* **属性**

  `DATE`属性的相对路径，例如`jcr:lastModified`。

* **下限**

  用于检查属性（例如，`2014-10-01`）的日期下限。

* **lowerOperation**

  “`>`”（较新）或“`>=`”（在或较新）适用于`lowerBound`。 默认值为“`>`”。

* **上限**

  检查属性的上限，例如`2014-10-01T12:15:00`。

* **upperOperation**

  “`<`”（较旧）或“`<=`”（等于或较旧）适用于`upperBound`。 默认值为“`<`”。

* **时区**

  未作为ISO-8601日期字符串提供时要使用的时区ID。 默认值是系统的默认时区。

### `excludepaths` {#excludepaths}

从结果中排除路径与正则表达式匹配的节点。

仅限过滤的谓词，不能使用搜索索引。

它不支持彩块化提取。

#### 属性 {#properties-4}

* **排除路径**

  正则表达式与结果路径匹配，不包括结果中的匹配路径。

### `fulltext` {#fulltext}

搜索全文索引中的术语。

它不支持筛选。

它不支持彩块化提取。

#### 属性 {#properties-5}

* **全文**

  全文搜索词。

* **relPath**

  在属性或子节点中搜索的相对路径。 此属性是可选的。

### `group` {#group}

允许生成嵌套条件。 组可以包含嵌套的组。 查询生成器查询中的所有内容都隐式位于根组中，该组也可以有`p.or`和`p.not`参数。

将两个属性中的一个与值匹配的示例：

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

概念上`(1_property`或`2_property)`。

嵌套组示例：

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

在&#x200B;**中的页面或**&#x200B;中的资产中搜索术语“`/content/geometrixx/en`管理`/content/dam/geometrixx`”。

概念`fulltext AND ( (path AND type) OR (path AND type) )`。 此类OR连接需要良好的索引来提高性能。

#### 属性 {#properties-6}

* **p.或**

  如果设置为“`true`”，则组中只有一个谓词必须匹配。 默认为“`false`”，表示所有规则必须匹配

* **p.not**

  如果设置为“`true`”，则它会使组无效（默认为“`false`”）。

* **&lt;谓词>**

  添加嵌套谓词。

* **N_&lt;谓词>**

  同时添加多个嵌套谓词，如`1_property, 2_property, ...`。

### hasPermission {#haspermission}

将结果限制为当前会话具有指定[JCR权限的项目。](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

仅限过滤的谓词，不能使用搜索索引。 它不支持彩块化提取。

#### 属性 {#properties-7}

* **hasPermission**

  当前用户会话必须全部具有相关节点的逗号分隔JCR权限。 例如，`jcr:write`，`jcr:modifyAccessControl`。

### `language` {#language}

查找采用特定语言的CQ页面。 这会查看页面语言属性和页面路径，后者通常包括顶级网站结构中的语言或区域设置。

仅限过滤的谓词，不能使用搜索索引。

它支持彩块化提取。 为每个唯一的语言代码提供存储段。

#### 属性 {#properties-8}

* **语言**

  ISO语言代码，例如“`de`”。

### `mainasset` {#mainasset}

检查节点是否是DAM主资产而不是子资产。 基本上，每个节点不在“子资产”节点内。 不检查`dam:Asset`节点类型。 要使用此谓词，请设置“`mainasset=true`”或“`mainasset=false`”，没有其他属性。

仅限过滤的谓词，不能使用搜索索引。

它支持彩块化提取，并为主资源和子资源提供两个分段。

#### 属性 {#properties-9}

* **mainasset**

  布尔值，主资产为“`true`”，子资产为“`false`”。

### memberOf {#memberof}

查找属于特定[sling资源集合](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/resource/collection/ResourceCollection.html)成员的项。

仅限过滤的谓词，不能使用搜索索引。 它不支持彩块化提取。

#### 属性 {#properties-10}

* **memberOf**

  Sling资源集合的路径。

### `nodename` {#nodename}

匹配JCR节点名称。

它支持彩块化提取。 为每个唯一的节点名称（文件名）提供存储段。

#### 属性 {#properties-11}

* **节点名称**

  允许使用通配符的节点名称模式： `*` =任何或不包含字符，`?` =任何字符，`[abc]` =仅包含括号中的字符。

### `notexpired` {#notexpired}

通过检查JCR DATE属性是否大于或等于当前服务器时间匹配项。 可用于检查“`expiresAt`”之类的日期属性，并限制为仅包含尚未过期(`notexpired=true`)或已过期(`notexpired=false`)的属性。

它不支持筛选。

它与日期范围谓词一样，支持Facet提取。

#### 属性 {#properties-12}

* **notexpired**

  布尔值，“`true`”表示尚未过期（日期在将来或相等），“`false`”表示已过期（日期在过去）（必需）。

* **属性**

  要检查的`DATE`属性的相对路径（必需）。

### `orderby` {#orderby}

允许对结果进行排序。 如果需要按多个属性排序，则必须使用数字前缀（如`1_orderby=first`、`2_oderby=second`）多次添加此谓词。

#### 属性 {#properties-13}

* **orderby**

  JCR属性名称由前导@指示，例如，`@jcr:lastModified`或`@jcr:content/jcr:title`，或者查询中的另一个谓词，例如，要排序的`2_property`。

* **排序**

  排序方向，按降序排列“`desc`”或按升序排列“`asc`”（默认）。

* **案例**

  如果设置为`ignore`，排序将不区分大小写，这意味着“a”在“B”之前；如果为空或省略，排序将区分大小写，这意味着“B”在“a”之前

### `path` {#path}

在给定路径内搜索。

它不支持彩块化提取。

#### 属性 {#properties-14}

* **path**

  路径模式。 当`exact=false`（默认）时，搜索与指定路径下的整个子树匹配 — 类似于XPath中的`//*`附加，但不包括基本路径本身。 当`exact=true`时，搜索仅与精确路径匹配，其中可包含`*`通配符。 如果设置了`self`，则搜索将包括基节点及其整个子树。


* **精确**

  如果`exact`为true （开），则确切的路径必须匹配，但它可以包含简单通配符(`*`)，这些通配符与名称匹配，但不匹配“`/`”；如果为false（默认），则包含所有后代（可选）。

* **平面**

  仅搜索直接子项（如在`/*`中附加“`xpath`”）（仅在“`exact`”不为true或可选时使用）。

* **self**

  搜索子树，但包含作为路径指定的基础节点（无通配符）。

### `property` {#property}

匹配JCR属性及其值。

它支持彩块化提取。 为结果中的每个唯一属性值提供存储段。

#### 属性 {#properties-15}

* **属性**

  属性的相对路径，例如`jcr:title`。

* **值**

  要检查属性的值；遵循JCR属性类型到字符串的转换。

* **N_value**

  使用`1_value`、`2_value`、...检查多个值（默认情况下与`OR`以及`AND` if and=true组合）（从5.3开始）。

* **和**

  设置为true可将多个值(`N_value`)与AND（从5.3开始）组合。

* **操作**

  使用`equals`进行完全匹配（默认），使用`unequals`进行不等式比较。 使用`like`应用可选的`jcr:like` XPath函数。 使用`not`表示无匹配项（例如，XPath中的`not(@prop)`）；在这种情况下，将忽略`value`参数。 使用`exists`检查属性是否存在： `true` （默认）需要该属性，`false`等同于`not`。

* **深度**

  属性和相对路径可以存在的通配符级别数。 例如，`property=size depth=2`检查节点和大小、节点/&amp;amp；ast；/size以及节点/&amp;amp；ast；/&amp;amp；ast；/size。

### `rangeproperty` {#rangeproperty}

将JCR属性与时间间隔匹配。 适用于线性类型的属性，如`LONG`、`DOUBLE`和`DECIMAL`。 对于`DATE`，请参阅已优化日期格式输入的日期范围谓词。

您可以定义下限和上限，也可以只定义其中一个。 也可以分别为下限和上限指定操作（例如，“小于”或“小于或等于”）。

它不支持彩块化提取。

#### 属性 {#properties-16}

* **属性**

  属性的相对路径。

* **下限**

  检查属性的下限。

* **lowerOperation**

  “`>`”（默认）或“`>=`”适用于`lowerValue`

* **上限**

  检查属性的上限。

* **upperOperation**

  “`<`”（默认）或“`<=`”适用于`lowerValue`

* **decimal**

  如果检查的属性为Decimal类型，则为“`true`”

### `relativedaterange` {#relativedaterange}

使用相对于当前服务器时间的时间偏移量将`JCR DATE`属性与日期和时间间隔匹配。 您可以使用毫秒值或bugzilla语法`lowerBound`指定`upperBound`和`1s 2m 3h 4d 5w 6M 7y`。 带有“`-`”的前缀，表示当前时间之前的负偏移。 如果仅指定`lowerBound`或`upperBound`，则另一个将默认为0，即当前时间。

例如：

* `upperBound=1h` （没有任何`lowerBound`）将在下一小时选择任何内容
* `lowerBound=-1d` （没有任何`upperBound`）将选择过去24小时内的任何内容
* `lowerBound=-6M`和`upperBound=-3M`将选择6个月到3个月之前的任何内容
* `lowerBound=-1500`和`upperBound=5500`将选择过去1500毫秒到未来5500毫秒之间的任何时间
* `lowerBound=1d`和`upperBound=2d`将选择后天的任何内容

它不考虑闰年，所有月份都是30天。

它不支持筛选。

它与日期范围谓词一样，支持Facet提取。

#### 属性 {#properties-17}

* **上限**

  以毫秒为单位的上限日期或相对于当前服务器时间的`1s 2m 3h 4d 5w 6M 7y`（1秒、2分钟、3小时、4天、5周、6个月、7年），使用“ — ”表示负偏移。

* **下限**

  以毫秒为单位或相对于当前服务器时间的`1s 2m 3h 4d 5w 6M 7y`（1秒、2分钟、3小时、4天、5周、6个月、7年）为下限，使用“ — ”表示负偏移。

### `root` {#root}

根谓词组。 它支持组的所有功能，并允许您设置全局查询参数。

名称“root”从未在查询中使用，它是隐式的。

#### 属性 {#properties-18}

* **p.offset**

  指示结果页面开始的数字，即要跳过的项目数。

* **p.limit**

  表示页面大小的数字。

* **p.guessTotal**

  为避免计算完整结果总计的成本，请不要计算所有匹配项。 相反，设置总计的最大值，以将其计数为（例如，`1000`），以便为用户提供较小结果的大致大小和确切总计。 或将其设置为`true`以仅计数到所需的最小值： `p.offset + p.limit`。


* **p.excerpt**

  如果设置为“`true`”，则在结果中包含全文摘录。

* **p.hits**

  （仅适用于JSON servlet）选择点击作为JSON写入的方式，并使用这些标准点击（可通过ResultHitWriter服务扩展）：

   * **简单**：

     最小项目，如`path`、`title`、`lastmodified`、`excerpt`（如果已设置）。

   * **完整**：

     结果将呈现为每个节点的Sling JSON，其中`jcr:path`显示点击路径。 默认情况下，响应仅包含节点的直接属性；使用`p.nodedepth=N`包含更深入的内容，其中`0`返回整个子树。 设置`p.acls=true`以包含每个项目的当前会话的JCR权限(`create` = `add_node`，`modify` = `set_property`，`delete` = `remove`)。


   * **选择性**：

     响应仅包括`p.properties`中列出的属性，该属性是以空格分隔的相对路径列表（在URL中使用`+`）。 如果相对路径的深度大于1，则输出会将其嵌套为子对象。 特殊`jcr:path`属性始终包含点击路径。


### `savedquery` {#savedquery}

它包含持久查询生成器查询的所有谓词作为子组谓词添加到当前查询中。

它不会运行额外的查询，但会扩展当前查询。

可以使用`QueryBuilder#storeQuery()`以编程方式保留查询。 格式可以是多行字符串属性，也可以是以Java™属性格式将查询作为文本文件包含的`nt:file`节点。

它不支持为已保存查询的谓词进行Facet提取。

#### 属性 {#properties-19}

* **savedquery**

  已保存查询的路径（字符串属性或`nt:file`节点）。

### `similar` {#similar}

使用JCR XPath的`rep:similar()`进行相似性搜索。

它不支持筛选。 它不支持彩块化提取。

#### 属性 {#properties-20}

* **相似**
要查找相似节点的节点的绝对路径。

* **本地**
子节点或当前节点的`.`的相对路径（可选，默认为“`.`”）。

### `tag` {#tag}

通过指定标记标题路径，搜索使用一个或多个标记标记的内容。

它支持彩块化提取。 使用每个唯一标记的当前标记标题路径为其提供存储段。

#### 属性 {#properties-21}

* **标记**

  要查找的标记标题路径，例如“资产属性：方向/横向”。

* **N_value**

  使用`1_value`、`2_value`、...检查多个标记（默认情况下与`OR`相结合，如果为`AND`且为true）（从5.6开始）。

* **属性**

  要查看的属性（或属性的相对路径）（默认为“`cq:tags`”）

### `tagid` {#tagid}

通过指定标记ID来搜索使用一个或多个标记标记的内容。

它支持彩块化提取。 使用每个唯一标记的当前标记ID为其提供存储段。

#### 属性 {#properties-22}

* **tagid**

  标记ID，以便您可以查找，例如&quot; `properties:orientation/landscape`&quot;。

* **N_value**

  使用`1_value`、`2_value`、...检查多个`tagids`（默认情况下与`OR`组合，如果为`AND`且为true）（从5.6开始）。

* **属性**

  要查看的属性（或属性的相对路径）（默认为“`cq:tags`”）。

### `tagsearch` {#tagsearch}

通过指定关键字，搜索带有一个或多个标记的内容。 首先搜索其标题中包含这些关键字的标记，然后将结果限制为仅包含标记的项目。

它不支持彩块化提取。

#### 属性 {#Properties-1}

* **tagsearch**

  要在标记标题中搜索的关键字。

* **属性**

  要查看的属性（或属性的相对路径）（默认`cq:tags`）。

* **lang**

  仅搜索特定本地化的标记标题（例如，`de`）。

* **所有**

  （布尔）搜索整个标记全文，即所有标题、描述等。 优先于“l `ang`”。

### `type` {#type}

将结果限制到特定的JCR节点类型（主节点类型或mixin类型），并查找该节点类型的子类型。 存储库搜索索引必须涵盖节点类型才能有效执行。

它支持彩块化提取。 为结果中的每个唯一类型提供存储段。

#### 属性 {#Properties-2}

* **类型**

  要搜索的节点类型或mixin名称，例如`cq:Page`。
