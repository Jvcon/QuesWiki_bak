# iconv

 iconv是知名的开源跨平台编码转换库，iconv.exe是iconv库在windows下的命令行工具，iconv.exe的一般用法：

```
iconv.exe -f gbk -t utf-8 gbk.txt > utf-8.txt
```

其中 -f gbk 指明转换前的文件编码是gbk，-t utf-8 指明转换后的文件编码是utf-8，gbk.txt 是转换前文件的名称，> utf-8.txt指明把转换结果输出到utf-8.txt文件中。


当我们要转换大量文件时，我们可以结合windows命令和iconv.exe批量编码转换。用法:

for /r  dir_name  %i in (*.txt) do iconv.exe -f GBK -t UTF-8 %i > %~ni_utf8.txt

其中 dir_name 是待转换文件的存放目录，for /r  dir_name  %i in (*.txt) do 命令循环dir_name目录下的所有txt文件，iconv.exe -f GBK -t UTF-8 %i > %~ni_utf8.txt 用于转换每一个txt文件。 