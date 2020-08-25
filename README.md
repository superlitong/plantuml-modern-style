# 引言

我们通常会使用visio或者Edraw画流程图或者时序图等，但是你有没有觉得每次修改都要花大量时间调整线与文字的位置？又或者多人协同写一个设计文档，画出来的图风格也是千奇百怪？这篇文章就是要教会你解放双手，通过VSCode中PlantUML插件画各种类图/流程图/时序图等，我们会先讲安装步骤，然后再介绍使用PlantUML的高阶技巧。

# 什么是PlantUML
 
PlantUML是一个支持快速绘制的开源项目。其定义了一套完整的语言用于实现UML关系图的描述。并基于强大的graphviz图形渲染库进行UML图的生成。绘制的UML图还可以导出为图片，以及通用的矢量SVG格式文件。
 
如以下代码，可实现时序图

```
@startuml example
Alice -> Bob: Authentication Request
Bob --> Alice: Authentication Response
 
Alice -> Bob: Another authentication Request
Alice <-- Bob: another authentication Response
@enduml
```

![时序图](hexample-origin.png)

PlantUML可以使用在线的版本https://www.planttext.com/，也可以使用编辑器VSCode安装插件，以下介绍安装教程。
 
# Windows系统下VSCode安装PlantUML插件
 
1.前置需求
- Java
- graphviz
- VSCode
 
2.安装java并为其配置环境变量,java/javac检测是否成功
- 变量名：JAVA_HOME
- 变量值：C:\Program Files (x86)\Java\jdk1.8.0_91        // 要根据自己的实际路径配置
- 变量名：CLASSPATH
- 变量值：.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;         //记得前面有个"."
- 变量名：Path
- 变量值：%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;
 
3.安装graphviz并配置环境变量，dot -version 检测是否成功
- 变量名：GRAPHVIZ_DOT
- 变量值：C:\Program Files (x86)\Graphviz 2.28\bin\dot.exe        // 要根据自己的实际路径配置
 
4.在VSCode中直接搜索，并安装PlantUML插件
- VSCode可以在官网上下载，并安装。安装完成后，在软件左上角搜索PlantUML关键字，安装插件。并在“设置-扩展-PlantUML配置”里，Java可执行文件位置填写：C:\Java\jdk13\bin\java.exe    // 要根据自己的实际路径配置
- 打开UML文件，按ALT + D 即可实时预览UML图
 
5、标签用法参考：http://plantuml.com/zh/commons
 
# 高阶技能

有没有觉得PlantUML默认画出来的图，是60年代的风格？如果想要画出现代风格的图，可参考sample文件夹中的示例代码。（本项目中的libs和部分示例代码来源于项目https://github.com/xuanye/plantuml-style-c4.git）
 
接下来，以上面的例子为例，修改源代码如下：

```
@startuml example
 
' 加载库文件，使新风格生效
!include ../libs/core.puml
 
' 设置成草图风格[可选]
skinparam backgroundColor #EEEBDC
skinparam handwritten true
center footer <font color=red>Warning:</font> Created for discussion, needs to be validated
 
' 设置红色箭头[可选]
RED_ARROW
 
Alice -> Bob: Authentication Request
Bob --> Alice: Authentication Response
 
Alice -> Bob: Another authentication Request
Alice <-- Bob: another authentication Response
@enduml
```

这样画出来的效果就是这样的：

![时序图](example.png)

有没有觉得一下子从60年代回到了2020呢？
