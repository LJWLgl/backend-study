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

## export

shell翻墙
```shell
export http_proxy=http://127.0.0.1:1087;export https_proxy=http://127.0.0.1:1087;
```



## gh-md-toc

自动生成markdown的目录，请参考[github-markdown-toc](https://github.com/ekalinin/github-markdown-toc)

```shell
# sed '3d' 删除前3行, sed '$d' 删除尾行，sed  's/*/-/g' 替换字符
> gh-md-toc ~/myapps/project/backend-study/README.md | sed '3d' | sed '$d' | sed  's/*/-/g' > ~/temp/3.txt
> open ~/temp/3.txt
```

