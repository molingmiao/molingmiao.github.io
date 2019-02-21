---
layout: post
title:  "Springboot-mybatis"
categories: Springboot
tags: SpringbootMybatis
author: MLM
---


总结：
1、	新建Gradle项目。
1)	下载和配置Gradle. 
https://gradle.org/install；
在环境变量中配置：Gradle的安装路径\bin
通过 gradle –v 来确认安装成功及有效。
2)	在Eclipse中配置gradle
在Preferences中的Gradle项的Gradle User Home：选择Gradle的安装路径并应用
3)	安装Eclipse Gradle(Buildship)工具插件
在Eclipse的MarketPlace中搜索并安装。
4)	创建一个新的Gradle工程
等下载插件结束就创建成功了。
2、	SpringBoot和Gradle的整合





3、	配置Flyway及~.SQL文件的拟定

4、	通过SQL文件创建对应的Bean及Mapper关系
例如：ProjectBase.java => ProjectBaseMapper.java => ProjectBaseMapper.xml
5、	自定义映射关系JsonbTypeHandler
1.	继承BaseTypeHandler<T>
2.	声明Json要转换成对象。
/**
	 * @param valueType
	 *            把json字符串转换为Java对象时指定的java类类型
	 *
	 */
	public JsonbTypeHandler(Class<T> valueType) {
		this.valueType = valueType;
	   }
3.	重写Base的4个方法
/**
	 * @see org.apache.ibatis.type.BaseTypeHandler#setNonNullParameter(java.sql.PreparedStatement,
	 *      int, java.lang.Object, org.apache.ibatis.type.JdbcType)
	 */
	@Override
	public void setNonNullParameter(PreparedStatement ps, int i, T parameter, JdbcType jdbcType)
			throws SQLException {
		String jsonString = null;
		try {
			jsonString = JsonbTypeHandler.objectMapper.writeValueAsString(parameter);
		}
		catch (JsonProcessingException e) {
			log.error("method: setNonNullParameter, error:" + e.toString());
		}
		ps.setString(i, jsonString);
	}

	/**
	 * @see org.apache.ibatis.type.BaseTypeHandler#getNullableResult(java.sql.ResultSet,
	 *      java.lang.String)
	 */
	@Override
	public T getNullableResult(ResultSet rs, String columnName) throws SQLException {
		return this.string2Object(rs.getString(columnName));
	}

	/**
	 * @see org.apache.ibatis.type.BaseTypeHandler#getNullableResult(java.sql.ResultSet,
	 *      int)
	 */
	@Override
	public T getNullableResult(ResultSet rs, int columnIndex) throws SQLException {
		return this.string2Object(rs.getString(columnIndex));
	}

	/**
	 * @see org.apache.ibatis.type.BaseTypeHandler#getNullableResult(java.sql.CallableStatement,
	 *      int)
	 */
	@Override
	public T getNullableResult(CallableStatement cs, int columnIndex) throws SQLException {
		return this.string2Object(cs.getString(columnIndex));
	}
4.	通过Jackson2ObjectMapperBuilder对象去除时间转换功能后生成的ObjectMapper来进行Json和Object的转换。
	ObjectMapper objectMapper = new Jackson2ObjectMapperBuilder()
			.featuresToDisable(SerializationFeature.WRITE_DATES_AS_TIMESTAMPS).build()
	
6、	创建Service对应的ServiceImpl及Controller

7、	创建pgsql。
连接数据库：
1)C:\devtools\pgsql-10.2-1\bin>psql -U postgres
2)执行命令# select* from pg_user;
3)执行命令# select* from pg_database;
4)创建数据库新用户，如 t0p_p1_admln：
   # CREATE USER t0p_p1_admln WITH PASSWORD 'p0ssw0rd_0dmln';
5)创建用户数据库，如t0pmonoger_db：
   # CREATE DATABASE t0pmonoger_db OWNER t0p_p1_admln;
6)将t0pmonoger_db数据库的所有权限都赋予t0p_p1_admln：
   # GRANT ALL PRIVILEGES ON DATABASE t0pmonoger_db TO t0p_p1_admln;
7)使用命令 \q 退出psql：
   # \q
8)开启远程访问，在所有IP地址上监听，允许远程连接到数据库服务器：
修改postgresql.conf（devtools\pgsql-10.2-1\data）：listening_address: '*'
9)允许任意用户从任意机器上以密码方式访问数据库
   修改pg_hba.conf（devtools\pgsql-10.2-1\data）：
   host    all       all       0.0.0.0/0     password
7、编译加启动：gradlew.bat bootRun。
