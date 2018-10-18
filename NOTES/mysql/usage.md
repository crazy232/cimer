#### MYSQL 常用语句

- 新增用户，并给权限

```shell
create user 'user'@'%' identified by 'password';
grant all on *.* to 'sapiens'@'%';
flush privileges;
```

- 禁止root用户远程登录

```shell
delete from user where user="root" and host!="localhost";
flush privileges;
```

