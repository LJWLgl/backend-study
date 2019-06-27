# 常用shell命令
## awk
**多行合并成一行**
```bash
awk BEGIN{RS=EOF}'{gsub(/\n/,"");print}' [file]
```
**选取第一列，并以“，”分隔**
```bash
cat res.txt | awk  -F ' ' '{print $1","}' [file]
```
## sed
一行分割成多行
```bash
# mac
echo "a;b" | sed 's/;/\
/g'
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

