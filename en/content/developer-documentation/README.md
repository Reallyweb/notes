# Developer documentation/开发者文档

> Developer documentation/开发者文档

## 项目：

名称：  
full-stack Studies & Notes/全栈笔记  
   时间：  
2017-02-12  ---  
   参与人员：  
[limbobark](https://github.com/limbobark),[740641444](https://github.com/740641444),[c2017](https://github.com/c2017),[likaiweb](https://github.com/likaiweb),[zhangcuiZC](https://github.com/zhangcuiZC),[雨落花香溢漫天](https://github.com/MrQingman)

## 文件夹结构

/-------------------  
  \|--- assets/  所有引用格式资源\(eg:image.jpg\)  
  \|--- js/      库 \(eg:jquery-1.12.2.min.js\)   js文件  
  \|--- css/     样式 \(public.css\)  css文件  
  \|--- content/
  \|--- --- content/Module name folder 各模块文件夹  
  \|--- --- --- content/Module name folder/son Module name folder 子模块文件夹  
  \|--- --- --- content/Module name folder/son Module name.md 子模块文档  
  \|--- --- content/Module name.md 各模块说明文档  
  \|--- --- content/Document name.md 未分类文档

## 规范

文档的文件名不得含有空格。

文件名必须使用半角字符，不得使用全角字符。这也意味着，中文不能用于文件名。

```
错误： 名词解释.md

正确： glossary.md
```

文件名建议只使用小写字母，不使用大写字母。

```
错误：TroubleShooting.md

正确：troubleshooting.md 
```

为了醒目，某些说明文件的文件名，可以使用大写字母，比如`README`、`LICENSE`。

文件名包含多个单词时，单词之间建议使用半角的连词线（`-`）分隔。

```
不佳：advanced_usage.md

正确：advanced-usage.md
```

合作愉快！

