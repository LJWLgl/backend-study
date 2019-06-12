# 常用shell命令
## awk
多行合并成一行
```bash
awk BEGIN{RS=EOF}'{gsub(/\n/,"");print}' [file]
```
## sed
一行分割成多行
```bash
# mac
echo "a;b" | sed 's/;/\
/g'
```