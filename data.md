<b>数据库结构如下</b>

Log表，日志表

    字段        类型	        含义
    uid         bigint(20)	    主键，自增
    appuid	    varchar(50)	    APP的ID，应用的ID
    theday	    varchar(30)	    数据产生的日期，比如2013-03-15
    thehour	    varchar(10)	    数据产生的小时，比如1~23之间任意数值
    userip      varchar(300)    用户的IP
    thewho	    varchar(100)    用户的UID，比如d2a3724e-d621-3939-96c3-c8192b255b7a
    cuid        varchar(10)	    推广人的ID


App表，应用列表

    字段        类型            含义
    uid         bigint(20)	    主键，非自增，保持唯一性
    appname	    varchar(50)	    APP的名称
    theday	    varchar(30)	    数据产生的日期，比如2013-03-15
    
Marketing表，推广人员列表

    字段        类型            含义
    uid         bigint(20)      主键，非自增，保持唯一性
    cname	    varchar(50)	    APP的名称
    theday	    varchar(30)	    数据产生的日期，比如2013-03-15


<b>Log表数据截图如下</b>
![部分数据](https://raw.github.com/clean315/clean01/master/pics/09.png)


<b>推广人的使用场景</b>

+我要查，最近几天，所有应用，下载的总量

+我要查，最近几天，不同的应用，下载的总量

+我要查，最近几天，所有应用，新增的下载量，也就是用户量（用户用thewho来进行唯一标识）

+我要查，最近几天，不同的应用，新增的下载量，也就是用户量

+我要查，当天，所有应用，下载的总量

+我要查，当天，不同的应用，下载的总量
