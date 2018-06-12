# 项目分析总结

## 架构

架构是蚂蚁金服的sofa2简化版架构,根据郑哥口述,sofa2架构如下:

- common
  - util
- core
  - mapper
  - model
- biz
  - manager
  - service
  - fac
- web
- test

- common 层协助各个层次的架构进行自己的逻辑处理
  - 比如提供各个层次需要的工具类
  - 进行全局的异常处理
  - 设置错误信息
  - 等等
- core 层是核心层
  - 功能类似于ssm架构中的dao层
  - mapper类似于ssm中的mapper,但是其中只有对单表的操作,多个表的操作在service中体现
  - model类似于ssm中的pojo
- biz负责业务处理
  - manager负责连接不同的service
  - service类似于ssm中的service层
  - fac负责调用其他模块中的功能,以及进行一些非http层面的交互
- web曾负责http请求的处理
  - 相当于ssm中的controller,其中的Api即类似于servlet
- test用于放置junit单元测试类

---

### 注意

- 在进行多表联查的时候,不通过join语句进行连接查询,而是通过service的业务处理的方式来实现多个表中数据的调用
  - 如果是mapper层级的多表联查,在单个service中进行处理即可
  - 如果是service层级的多表联查,则需要调用manager进行处理
- 在本项目中,由于是单模块开发,所以没有模块间的调用,同时也没有用到非表层面的数据连接查询,所以也没有使用manager,
- 于是将service上调一级架构,省略了biz
- src/resources/benchmark.ftl 是.doc文档转换成.xml之后再转换而成的,通过该ftl可以生成.doc文档
- 后台只负责业务逻辑,不负责页面逻辑,也就是说,页面跳转之类的东西都交由前段通过js实现,这种可以实现程序的前后端的松耦合性

---

## export war

1. 打开 pom 注释 spring-boot-starter-tomcat

2. 修改 application.properties log 级别

---

## next version

- SpringBoot 升级至 2.x
- excel 格式下载
  - POI 方式提供下载 docx 和 xlsx 文件
- 历史查询
- 德育录入公式修改
- 数字东林批量导入