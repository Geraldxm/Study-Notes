## 概述

- 可扩展标记语言，EXtensible Markup Language
- 标签，有点像 HTML，但是没有预定义标签，需要自定义
- 和 HTML 不同，用于数据的存储和共享，而不是显示
- 可扩展，可以在不中断应用的情况下进行扩展

## XML 树结构

1. 一个例子

```XML
<?xml version="1.0" encoding="UTF-8"?>
<bookstore>
    <book category="COOKING">
        <title lang="en">Everyday Italian</title>
        <author>Giada De Laurentiis</author>
        <year>2005</year>
        <price>30.00</price>
    </book>
    <book category="CHILDREN">
        <title lang="en">Harry Potter</title>
        <author>J K. Rowling</author>
        <year>2005</year>
        <price>29.99</price>
    </book>
    <book category="WEB">
        <title lang="en">Learning XML</title>
        <author>Erik T. Ray</author>
        <year>2003</year>
        <price>39.95</price>
    </book>
</bookstore>
```

1. 与 HTML 语言类似，XML 文档中的元素形成了一棵文档树，注意这个树根的标签也是双标签, `<root>...</root>` 

```XML
<root>
<child>
<subchild>.....</subchild>
</child>
</root>
```

## XML 语法规则

1. XML 必须包含根元素
2. XML 声明，如果存在需要放在文档中的第一行
3. 所有元素必须都有一个关闭标签 `<element>{content}</element>` 
4. 大小写敏感
5. 可以有属性值，必须加引号，如 `<note date="2023/09/05">`
6. 使用实体引用避免歧义，如:

	| \&lt; | < | less than |
	| :---:  | :---: | :---: |
	| \&gt; | > | greater than |
	| \&amp; | & | ampersand |
	| \&apos; | ' | apostrophe |
	| \&quot; | " | quotation mark |

7. 注释为 `<!--> Comment <-->` 
8. 多个连续的空格会被合并为一个，类似 Markdown

## XML 元素

1. XML 元素：指从开始标签到结束标签的部分，包括其他元素、文本、属性或以上的混合
2. XML 命名规则
	- 字母、数字、其他字符
	- 不能以数字或标点开始
	- 不能有 XML 及其大小写变体开头
	- 不能包含空格
3. 命名习惯
	- 避免"-"和"."和":"，“-”会被认为是减去，"."会被认为是属性，“:"会被认为是命名空间。

XML 属性
- 提供元素的额外信息，值必须加引号（单引号或双引号均可，可以交叉使用，可以单引号内部包含双引号，也可以引号使用字符实体）
- 属性不能包含多个值、不能包含树结构、不易扩展，因此尽量使用元素
- id 属性
	- 可以用于标识 XML 元素

## 使用 CSS 显示 XML
- 可以使用 CSS 格式化 XML，加到第二行 `<?xml-stylesheet type="text/css" href="cd_catalog.css"?>`
- 不常用

## 使用 XSLT 显示 XML
- XSLT，EXtensible Sytlesheet Language Transformations
- 在浏览器显示 XML 文件之前，先把其转换为 HTML

## XMLHttpRequest 对象
- 用于在后台和服务器交换数据

```html
	xmlhttp=new XMLHttpRequest();
```

- 把 XML 字符串解析到 XML DOM 对象中

```html
txt="<bookstore><book>";
txt=txt+"<title>Everyday Italian</title>";
txt=txt+"<author>Giada De Laurentiis</author>";
txt=txt+"<year>2005</year>";
txt=txt+"</book></bookstore>";
 
if (window.DOMParser)
{
parser=new DOMParser();
xmlDoc=parser.parseFromString(txt,"text/xml");
}
else // Internet Explorer
{
xmlDoc=new ActiveXObject("Microsoft.XMLDOM");
xmlDoc.async=false;
xmlDoc.loadXML(txt);
}
```

