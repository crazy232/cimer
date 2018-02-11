### freemarker语法

- 取值

```shell
String str = "hello world";
int var = 1;
boolean boo = true;
String str2 = null;

String获取：<font color="red"> ${str} </font><br>
int获取：<font color="red"> ${var} </font><br>
boolean获取：<font color="red"> ${boo?string("yes","no")} </font>
null获取：<font color="red"> ${str2!"默认"} </font><br>   <!--${str!"默认"}即为有值时正常显示，无值显示默认-->
```


```shell
# 封装对象取值
# 现有对象User[name, age]
name获取：<font color="red"> ${User.name} </font><br>
age获取：<font color="red"> ${User.age} </font><br>
```


```shell
# 日期对象取值
 java.sql.Date date = new Date().getTime();
 java.sql.Date time = new Date().getTime();
 java.sql.Date datetime = new Date().getTime();
 
 date获取：<font color="red"> ${date?string('yyyy-MM-dd')} </font><br>
 time获取：<font color="red"> ${date?string('HH:mm:ss')} </font><br>
 datetime获取：<font color="red"> ${date?string('yyyy-MM-dd HH:mm:ss')} </font><br>
```

```shell
# html转义
# ${var?html}
在后台文件中封装变量Menu[ name, model ]
Menu m = new Menu(); 
m.setName(" freemarker ");
m.setModel("<font color = 'red'>我只是个菜单</font>");
# 在页面中获取变量：
	非转义获取：<font color="red"> ${m.model} </font><br>
	转义获取： ${m.model?html} </font><br>
 	展示结果：
		非转义获取：我只是个菜单
 		转义获取：<font color = 'red'>我只是个菜单</font>
```

```shell
# 页面定义变量，计算赋值
<#assign num=100 />
num获取：<font color="red"> ${num)} </font><br>
计算结果：<font color="red"> ${num * 10} </font><br>
```

```shell
# List集合取值
<#list  list集合  as  item> 
	 ${item} <br/>
	 ${item!} <br/>
</#list>
```

```shell
# Map类型取值
<#list map?keys as key>
${key}:${map[key]}
</#list>
```

- if-else

```shell
 <#assign age = 20 /><br>
<#if age == 18>
      <font color="red"> age = 18</font>
<#else>
      <font color="red"> age != 18</font>
</#if>

<#assign age = 20 /><br>
<#if age &gt; 18>
      <font color="red">青年</font>
<#elseif age == 18>
      <font color="red"> 成年</font>
<#else>
      <font color="red"> 少年</font>
</#if>
```

- switch

```shell
<#switch var="星期一">
<#case "星期一">
     油焖大虾
<#break>
<#case "星期二">
      炸酱面
<#break>
<#default>
     肯德基
</#switch>
```

