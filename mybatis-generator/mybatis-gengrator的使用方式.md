### 下载mysql的连接驱动jar包

**下载地址：**

 https://mvnrepository.com/artifact/mysql/mysql-connector-java 

**注意：请务必根据自己所使用的mysql版本去下载对应的jar**



### 引入maven依赖

```java
<plugin>
        <groupId>org.mybatis.generator</groupId>
        <artifactId>mybatis-generator-maven-plugin</artifactId>
        <version>1.3.7</version>
        <configuration>
          <overwrite>true</overwrite>
        </configuration>
      </plugin>
```



### 创建/修改配置文件(文件名默认为generatorConfig.xml)

`主要是修改路径，和数据库相关的配置`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN" "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<generatorConfiguration>
    
    <!-- 数据库驱动包位置（随便放在哪个文件夹，能访问到就行） -->
    <classPathEntry location="D:\Tool\mysql-connector-java-5.1.6.jar" /><!-- 1 修改点-->
    <context id="DB2Tables" targetRuntime="MyBatis3">
        
        <!--不再追加xml内容-->
        <plugin type="org.mybatis.generator.plugins.UnmergeableXmlMappersPlugin" />

        <commentGenerator>
            <property name="suppressAllComments" value="true" />
        </commentGenerator>
        
        <!-- 数据库链接URL、用户名、密码 -->
        <jdbcConnection driverClass="com.mysql.jdbc.Driver" connectionURL="jdbc:mysql://localhost:3306/authorization?characterEncoding=utf8" userId="root" password="root">  <!-- 2修改点 -->
        </jdbcConnection>
        <javaTypeResolver>
            <property name="forceBigDecimals" value="false" />
        </javaTypeResolver>
        <!-- 生成模型的包名和位置 --> <!-- 3修改点 -->
        <javaModelGenerator targetPackage="com.wjw.model" targetProject="src/main/java">
            <property name="enableSubPackages" value="true" />
            <property name="trimStrings" value="true" />
        </javaModelGenerator>
        <!-- 生成的映射文件包名和位置 --> <!-- 4修改点 -->
        <sqlMapGenerator targetPackage="mappers" targetProject="src/main/resources">
            <property name="enableSubPackages" value="true" />
        </sqlMapGenerator>
        <!-- 生成DAO的包名和位置 --> <!-- 5修改点 -->
        <javaClientGenerator type="XMLMAPPER" targetPackage="com.wjw.dao" targetProject="src/main/java">
            <property name="enableSubPackages" value="true" />
        </javaClientGenerator>
        <!-- 要生成那些表(更改tableName和domainObjectName就可以) --><!-- 6修改点 -->
        <table tableName="sys_user" domainObjectName="SysUser" enableCountByExample="false" enableUpdateByExample="false" enableDeleteByExample="false" enableSelectByExample="false" selectByExampleQueryId="false" />
        <table tableName="sys_dept" domainObjectName="SysDept" enableCountByExample="false" enableUpdateByExample="false" enableDeleteByExample="false" enableSelectByExample="false" selectByExampleQueryId="false" />
        <table tableName="sys_acl" domainObjectName="SysAcl" enableCountByExample="false" enableUpdateByExample="false" enableDeleteByExample="false" enableSelectByExample="false" selectByExampleQueryId="false" />
        <table tableName="sys_acl_module" domainObjectName="SysAclModule" enableCountByExample="false" enableUpdateByExample="false" enableDeleteByExample="false" enableSelectByExample="false" selectByExampleQueryId="false" />
        <table tableName="sys_role" domainObjectName="SysRole" enableCountByExample="false" enableUpdateByExample="false" enableDeleteByExample="false" enableSelectByExample="false" selectByExampleQueryId="false" />
        <table tableName="sys_role_acl" domainObjectName="SysRoleAcl" enableCountByExample="false" enableUpdateByExample="false" enableDeleteByExample="false" enableSelectByExample="false" selectByExampleQueryId="false" />
        <table tableName="sys_role_user" domainObjectName="SysRoleUser" enableCountByExample="false" enableUpdateByExample="false" enableDeleteByExample="false" enableSelectByExample="false" selectByExampleQueryId="false" />
        <table tableName="sys_log" domainObjectName="SysLog" enableCountByExample="false" enableUpdateByExample="false" enableDeleteByExample="false" enableSelectByExample="false" selectByExampleQueryId="false" />
    </context>
</generatorConfiguration>
```



运行命令(IDEA终端Terminal运行如下命令)

`mvn mybatis-generator:generate`