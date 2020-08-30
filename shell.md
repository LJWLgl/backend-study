# 常用shell命令
## awk
**多行合并成一行**
```bash
awk BEGIN{RS=EOF}'{gsub(/\n/,"");print}' [file]
# 先分割，再合并成一行
awk  -F '.'  '{print $4}' 1.txt | awk BEGIN{RS=EOF}'{gsub(/\n/,",");print}'
```
**选取第一列，并以“，”分隔**
```bash
cat res.txt | awk  -F ' ' '{print $1","}' [file]
# 有引号
awk  -F '.' '{print "\""$2"\","}' 111.txt
awk -F ' ' '{printf("%s",$0);}' [file]
```
## sed
**一行分割成多行**
```bash
# mac
echo "a;b" | sed 's/;/\
/g'
```
**行首行尾添加字符**
```bash
# 在每行的头添加字符，比如"HEAD"，命令如下：
sed 's/^/HEAD&/g' [file]
# 在每行的行尾添加字符，比如“TAIL”，命令如下：
sed 's/$/&TAIL/g' [file]
```
## netstat 
查看tcp连接各状态的数量
```bash
netstat -n | awk '/^tcp/ {++S[$NF]} END {for(a in S) print a, S[a]}'
# output
SYN_RECV 2
ESTABLISHED 4
TIME_WAIT 1
```

