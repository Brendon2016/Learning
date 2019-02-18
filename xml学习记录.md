# XML文件结构  
xml文件区分大小写。
xml文件是结构化数据存储的，相当于一个xml文件就是一个结构体数据，因此只能有一个根元素和众多子元素。以下则为结构体翻译成xml的例子
C/C++
```
struct debug_settings
{
    std::string m_file;               // log filename
    int m_level;                      // debug level
    std::set<std::string> m_modules;  // modules where logging is enabled
    void load(const std::string &filename);
    void save(const std::string &filename);
};
```
XML
```
<debug>
    <filename>debug.log</filename>
    <modules>
        <module>Finance</module>
        <module>Admin</module>
        <module>HR</module>
    </modules>
    <level>2</level>
</debug>
```
# XML文件构成
- 文档声明
```
<strong><?xml version="1.0" encoding="utf-8" standalone="yes" ?>   //文档声明一共三个参数，分别为版本、字符编码、独立。可以一个都不写，其中utf-8和GB2312支持中文
```
- 元素  
即结构体中的变量，书写形式为：
```
<变量名>值</变量名>
```
- 属性
- 注释
- CDATA区、特殊字符
- 处理指令
- 命名空间
