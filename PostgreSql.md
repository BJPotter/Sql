# PostgresSql

### 安装篇

#### PostgresSQL安装

1.安装rpm文件

```shell
yum install https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm  -y
```

2.安装客户端

```shell
yum install postgresql10 -y
```

3.安装服务端

```shell
yum install postgresql10-server  -y
```

4.初始化

```shell
/usr/pgsql-10/bin/postgresql-10-setup initdb
```

5.启动并设置开机自启

```shell
systemctl enable postgresql-10  && systemctl start postgresql-10
```

#### 创建用户和数据库

1.使用postgres用户登录（PostgresSQL安装后会自动创建postgres用户，无密码）

```shell
su - postgres
```

2.登录postgresql数据库

```shell
psql
```

3.创建用户和数据库并授权

```shell
create user test_user with password 'abc123';
create database test_db owner test_user; 
grant all privileges on database test_db to test_user;
```

4.退出psql（输入 \q 再按回车键即可）

#### 开启远程访问

1.修改配置文件监听地址

```shell
echo "listen_addresses = '*'"  >> /var/lib/pgsql/10/data/postgresql.conf
```

2.修改配置文件允许远程访问

```shell
echo "host    all             all             0.0.0.0/0            md5" >> /var/lib/pgs10/data/pg_hba.conf
```

3.重启postgresql服务

```shell
systemctl restart postgresql-10.service
```

#### 开放防火墙

开放5432端口可以远程访问

```shell
firewall-cmd --permanent --add-port=5432/tcp  &&   firewall-cmd --reload
```



