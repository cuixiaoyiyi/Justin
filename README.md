# Justin
Justin：面向Java程序的单元测试用例自动生成工具

单元测试是保障软件质量的重要手段。
测试生成技术是一种根据被测程序自动生成测试输入/测试用例的方法，它能够减少开发者机械的手工劳动，同时可以应对应用程序快速演化的挑战。
Justin，一个面向Java程序的单元测试用例自动生成工具。
它以Java字节码作为输入，输出符合JUnit规范的测试用例源码，并自动编译执行，提供测试统计报告。
它采取了多种生成策略：随机策略、特殊值策略、基于程序分析的白盒策略、基于注解的业务敏感的生成策略等。
特别地，白盒策略中实现了基于正则表达式的字符串生成方法。
它输出可视化的报告，包含测试统计、异常统计、异常堆栈等信息。实践表明， Justin可以有效检测出软件中的缺陷。


## 使用方式  
JDK 1.8 

1. `cd ./libs`

2. `java -jar Justin.jar --jre "jrePath" --input "inputPath" --output "outputPath"`
   - "jrePath" indicates the jre path in the local jdk.
   - "inputPath" indicates the input class file, note that the jar package under the windows system needs to be decompressed first.
   - "outputPath" indicates the output path of the result.

For more information, you can run `java -jar Justin.jar -h` or `java -jar Justin.jar --help`:

```
<options>      <description>
----------------------------
-h(--help)     help
--jre          local JRE path in JDK
--input        compiled class path under test
--output       output path folder
--maxString    maximum length of string
--minSet       minimum size of set/array
--maxSet       maximum size of set/array
--maxCase      maximum size of cases for each method
--maxTime      maximum generation time for each class
```
## 示例   
以 commons-lang3-3.9.jar 为例

解压得到所有的字节码，目录为 .\commons-lang3-3.9    
执行以下命令
`cd ./libs`
```
java -jar Justin.jar  --jre "xx\\Program Files\\Java\\jre1.8.0.212" --input .\commons-lang3-3.9 --output .\commons-lang3-3.9-outputPath10140942 --maxTime 300

```

###  命令行运行进度条

![Progress](https://github.com/cuixiaoyiyi/Justin/blob/main/Progress.png) 


###  测试报告
全部结果见 commons-lang3-3.9-outputPath10140942.zip  


#####  基本信息 

![Justin-report-commons-lang3-3.9](https://github.com/cuixiaoyiyi/Justin/blob/main/Justin-report-commons-lang3-3.9.jpeg)


#####  异常用例及堆栈页面 
22	**test_matchesPattern_1_99**	org.apache.commons.lang3.Validate	**java.util.regex.PatternSyntaxException**   
测试用例详细信息
```                    
  @Test(timeout = 5000)
  public void test_matchesPattern_1_99() {

      java.lang.CharSequence charSequence4 = new org.apache.commons.lang3.text.StrBuilder();
      java.lang.String string5 = "[0,1]";
      java.lang.String string6 = "^\\w+([-+.]\\w+)*@\\w+([-.]\\w+)*\\.\\w+([-.]\\w+)*$";
      java.lang.Object[] objectArray7 = {};
      org.apache.commons.lang3.Validate.matchesPattern(charSequence4, string5, string6, objectArray7);

  }
```

                
堆栈详细信息
 ```               
test_matchesPattern_1_99(org.apache.commons.lang3.Validate_Test): Illegal repetition
{"key":2 }
java.util.regex.Pattern.error(Pattern.java:1957)
java.util.regex.Pattern.closure(Pattern.java:3159)
java.util.regex.Pattern.sequence(Pattern.java:2136)
java.util.regex.Pattern.expr(Pattern.java:1998)
java.util.regex.Pattern.compile(Pattern.java:1698)
java.util.regex.Pattern.(Pattern.java:1351)
java.util.regex.Pattern.compile(Pattern.java:1028)
java.util.regex.Pattern.matches(Pattern.java:1133)
org.apache.commons.lang3.Validate.matchesPattern(Validate.java:877)
org.apache.commons.lang3.Validate_Test.test_matchesPattern_1_99(Validate_Test.java:1128)
```

如果遇到找不到 JavaCompiler 异常，复制 JDK目录下的tool.jar 至 jre对应的目录下
