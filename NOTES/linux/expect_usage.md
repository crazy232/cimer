### 使用 expect 脚本进行命令的自动交互

#### 当在shell脚本或者dockerfile中执行的命令需要交互时会产生错误，此时可以使用expect工具，可以编写 expect脚本 

```shell
#!/usr/bin/expect                      #告诉系统执行的是expect脚本
spawn mysql -uroot -p -e "select @@sql_mode;"       #执行此命令时需输入mysql密码
expect "Enter password:"                #判断遇到的交互提示信息
send "\n"                               #判断成功，则输出回车
expect eof                              #脚本结束
```



