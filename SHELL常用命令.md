## Linux 日常命令



1. 不换行输出

   ```
   echo -n "hello word"
   ```

2. 输出变量

   ```
   HOSTNAME=$(hostname)
   echo "$HOSTNAME,${HOSTNAME}abc"
   ```

3. 按行读取文件到数组中

   ```
   #userlist.txt
   mapfile -t users < userlist.txt
   
   ```

4. 数组

   ```
   # 遍历数组
   # 按元素遍历
   for user in ${users[@]};do
   	echo $user
   done
   
   # 按索引号遍历
   for i in ${!users[@]};do
   	user=${users[$i]}
   	echo "$i,$user"
   done
   
   ```

5. 字符串分割数组

   ```
   str='user01,user02,user03'
   IFS=',' read -ra arr <<< $str
   for item in ${arr[@]};do
   	echo $item
   done
   
   login="root@rtian.domain.com"
   IFS='@' read -r user host <<< $login
   echo "user:$user,host:$host"
   ```

6. 下载文件，重命名

   ```
   wget -qO newfile https://abc.domain.com/oldfile
   # -q 静默执行
   
   
   curl -fso newfile https://abc.domain.com/oldfile
   # -f 不显示错误信息
   # -s 静默执行
   
   # 带头信息访问
   header='Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36'
   curl -H $header -fso newfile https://abc.domain.com/oldfile
   ```

7. 判断语句

   ```
   # 判断是否为空 
   test=''
   [[ -z "$test"  ]] && echo "空" || echo "不空"
   
   # 判断非空
   [[ -n "$test" ]]
   
   # 判断文件是否存在
   [[ -e $filename ]]
   
   ```

8. Shell 特殊变量及其含义

| 变量      | 含义                                                         |
| --------- | ------------------------------------------------------------ |
| $0        | 当前脚本的文件名。                                           |
| $n（n≥1） | 传递给脚本或函数的参数。n 是一个数字，表示第几个参数。例如，第一个参数是 $1，第二个参数是 $2。 |
| $#        | 传递给脚本或函数的参数个数。                                 |
| $*        | 传递给脚本或函数的所有参数。                                 |
| $@        | 传递给脚本或函数的所有参数。当被双引号`" "`包含时，$@ 与 $* 稍有不同，我们将在《[Shell $*和$@的区别](https://c.biancheng.net/view/vip_4559.html)》一节中详细讲解。 |
| $?        | 上个命令的退出状态，或函数的返回值，我们将在《[Shell $?](https://c.biancheng.net/view/808.html)》一节中详细讲解。 |
| $$        | 当前 Shell 进程 ID。对于 Shell 脚本，就是这些脚本所在的进程 ID。 |

9. 字符串

   1) 由单引号`' '`包围的字符串：

      - 任何字符都会原样输出，在其中使用变量是无效的。

      - 字符串中不能出现单引号，即使对单引号进行转义也不行。

   2) 由双引号`" "`包围的字符串：

      - 如果其中包含了某个变量，那么该变量会被解析（得到该变量的值），而不是原样输出。

      - 字符串中可以出现双引号，只要它被转义了就行。

   3) 不被引号包围的字符串

      - 不被引号包围的字符串中出现变量时也会被解析，这一点和双引号`" "`包围的字符串一样。

      - 字符串中不能出现空格，否则空格后边的字符串会作为其他变量或者命令解析。

10. 字符串的截取

    1) 使用 # 号截取右边字符

    ```bash
    #${string#*chars}
    url="http://c.biancheng.net/index.html"
    echo ${url#*:}
    #结果为//c.biancheng.net/index.html
    
    ```

    

    1) 使用 % 截取左边字符

11. 函数

```bash
function abc(){
	echo $1
}
# 调用时后面跟参数
bash abc "hello word"
```

12 . 查找当前目录下包含“abcd”的文件

```
grep -l "abcd" *
#删除所有查询到的文件
grep -l 'abcd' * | xargs rm -v
```

