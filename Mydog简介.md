# 配置文件 /mydog-test/src/main/resources/generatorConfig.xml 说明：
```
<?xml version="1.0" encoding="UTF-8" ?>
<generatorConfiguration> 
  <!-- 配置mysql驱动，这里可以配置多个地址，开发时候有时候在公司，有时候在家里，经常要改这个地址，所以改成可以配置多个，如果配置的文件路径找不到，会自动忽略，如果一个都未加载，链接数据库会提示找不到驱动-->
  <classPathEntry location="D:/JAVA/apache-maven/repo/mysql/mysql-connector-java/5.1.37/mysql-connector-java-5.1.37.jar,E:/JAVA/mvn/repo/mysql/mysql-connector-java/5.1.37/mysql-connector-java-5.1.37.jar"/>  
  <context id="my">
    <!-- 保留配置，暂时未使用 -->
    <commentGenerator> 
      <property name="suppressDate" value="false"/>  
      <property name="suppressComment" value="true"/> 
    </commentGenerator>
    
    <!-- 自定义属性，可以将这些属性 模版中生成，只用 直接是${autoer},暂时不支持带小数点的属性 --> 
    <properties>
    	<property name="author" value="Mycat Mydog"/>
    </properties>
    <!-- 数据库链接，暂时只支持Mysql，后续会支持 sqlserver，oracle 等主流数据库 -->
    <jdbcConnection driverClass="com.mysql.jdbc.Driver" connectionUrl="jdbc:mysql://127.0.0.1:3306/test" username="root" password="123456"/>
    
    <!-- 配置生成的文件
	      生成java类：
	      model 为 javaModel 类， 类名 table节点的domainObjectName属性值
	      mappping 生成Mapping 注解接口
	      dao 生成dao
          controller 生成控制器
          daoImpl 生成接口实现
          
       生成其他扩展名文件：
           举例说明，只写xml生成文件名为: model名.xml
          写Mapper.xml 生成文件名为: model名Mapper.xml
     -->  
    <generators>
      <generator type="model" tmplate="/templates/model1.tfl" targetPackage="com.hpgary.auto.model" root="com.hpgary.model.BaseModel"/>
      <generator type="mappping" tmplate="/templates/mapping1.ftl"  targetPackage="com.hpgary.auto.mapping" root="com.hpgary.dao.BaseDaoMybatis"/>
      <generator type="service" targetPackage="com.hpgary.auto.service" root="com.hpgary.service.BaseService"/>
      <generator type="Mapper.xml" tmplate="/templates/mapperXml1.ftl" targetPackage="com.hpgary.auto.mapper" />
    </generators>
    <!---
    	 配置生成的表
    	   tableName 表名
    	   domainObjectName 对应生成的类名
    	   name: 模版名称
     -->
	<tables>
	    <table tableName="users" domainObjectName="Users" name="系统用户管理"  />
    </tables> 
  </context> 
</generatorConfiguration>
```
# 导入说明 mydog-test/pom.xml 
（特别注意，尚未上传 maven仓库，所以直接写这个肯定是下载不成功的,需要下载项目源码）
```
<plugins>
	<plugin>
		<groupId>io.mycat</groupId>
		<version>0.5</version>
		<artifactId>mydog-core</artifactId>
		<configuration>
                        <!-- mvn启动精简参数 -->
			<goalPrefix>mydog-core</goalPrefix>
                         /*配置文件 generatorConfig.xml 所在位置*/
			<configXml>src/main/resources/generatorConfig.xml</configXml>
		</configuration>
	</plugin>
</plugins>
```

# 运行
```
cd mydog-test 
mvn mydog-core:touch
```
最后欢迎使用者贡献模版，提供maven项目，最好提供一个完整项目，实现一个基本的增删改查功能<br/>
联系人：Gary<br/>
email:hpgary@qq.com