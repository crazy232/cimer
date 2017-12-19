### Python执行系统命令方式对比
- os.system

这个方法是直接调用标准C的system() 函数，仅仅在一个子终端运行系统命令，而不能获取命令执行后的返回信息。返回值为执行结果的退出状态码(0,1,2),执行结果为0代表成功

```python
#!/usr/bin/env python
import os
os.system('cat /proc/cpuinfo')
```




- os.popen

该方法不但执行命令，还返回执行后的信息对象,通过管道文件将结果返回，从这个命令获取的值可以继续被调用.函数返回一个file-like的对象，里面的内容是脚本输出的内容(类似echo),明显地，像调用”ls”这样的shell命令，应该使用popen的方法来获得内容.

```shell
#!/usr/bin/env python
import os
output = os.popen('cat /proc/cpuinfo')
print output.read()
# 使用popen 获得ntpd的进程id
os.popen('ps -C ntpd|grep -v CMD|awk '{print $1}').readlines()[0]
```




- commands

该模块返回结果包括标准输出和标准错误，status返回0则代表成功执行

```shell
#!/usr/bin/env python
import commands
(status, output) = commands.getstatusoutput('cat /proc/cpuinfo')
print status,output
```




- subprocess


subprocess通过子进程来执行外部指令，并通过input/output/error管道，获取子进程的执行的返回信息。

> subprocess.call():  执行命令并返回执行状态，其中shell参数为False时，命令需要通过列表方式传入，当shell为True时，可直接传入命令

```python
#!/usr/bin/env python
import subprocess
a = subprocess.call(['df','-hT'], shell=False)
a = subprocess.call('df -hT', shell=True)

```

> subprocess.check_call(): 用法与subprocess.call()类似，区别在于当返回值不为0时，直接抛出异常

```shell
#!/usr/bin/env python
import subprocess
a = subprocess.check_call('df -hT', shell=True)

# 下面这句则会抛出异常
a = subprocess.check_call('dhdjef',shell=True)

```

> subprocess.check_output()：用法与上面两个方法类似，区别是，如果当返回值为0时，直接返回输出结果，如果返回值不为0，直接抛出异常。



> subprocess.Popen(): 在一些复杂场景中，我们需要将一个进程的执行输出作为另一个进程的输入。在另一些场景中，我们需要先进入到某个输入环境，然后再执行一系列的指令等。这个时候我们就需要使用到
>
> 该方法有以下参数：
>
> args：shell命令，可以是字符串，或者序列类型，如list,tuple。
>
> bufsize：缓冲区大小，可不用关心
>
> stdin,stdout,stderr：分别表示程序的标准输入，标准输出及标准错误
>
> shell：与上面方法中用法相同
>
> cwd：用于设置子进程的当前目录
>
> env：用于指定子进程的环境变量。如果env=None，则默认从父进程继承环境变量
>
> universal_newlines：不同系统的的换行符不同，当该参数设定为true时，则表示使用\n作为换行符

```shell
# 示例：在/root目录下创建test目录
a = subprocess.Popen('mkdir test', shell=True, cwd='/root')


# 输出到指定程序
obj = subprocess.Popen(["python"], stdin=subprocess.PIPE, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
obj.stdin.write('print 1 \n')
obj.stdin.write('print 2 \n')
obj.stdin.write('print 3 \n')
obj.stdin.write('print 4 \n')
obj.stdin.close()

cmd_out = obj.stdout.read()
obj.stdout.close()
cmd_error = obj.stderr.read()
obj.stderr.close()

print cmd_out
print cmd_error


# 将一个子进程输出做另一个子进程输入
sub1 = subprocess.Popen(["cat","/etc/passwd"], stdout=subprocess.PIPE)
sub2 = subprocess.Popen(["grep","0:0"], stdin=sub1.stdout, stdout=subprocess.PIPE)
out = sub2.communicate()
```



> sub.poll() 检查子进程状态

> sub.kill() 终止子进程

> sub.send_signal() 向子进程发送信号

> sub.terminate() 终止进程

