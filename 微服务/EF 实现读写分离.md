### EF Core 如何优雅的实现读写分离



**前言**

​		我们都知道当单库遇到性能瓶颈的时候，读写分离是首要的优化手段之一。因为绝大多数系统的读的比例远高于写的比例，并且大量耗时的读操作容易引起锁表导致数据无法写入，这时读写分离就显得格外重要了。

​		EF Core如何通过代码实现读写分离，我们可以搜索到很多的案例。总结起来的一种方法是注册一个 `DbContextFactory`,读操作注入 `ReadDbContext` ,写操作注入 `WriteDbContext` ; 另外一种就是动态修改数据库连接。

​		无论以上那种方法，实现简单粗暴的读写分离功能也不复杂。如果是需要实现从库状态监测（从库宕机）、主备自动切换（主库宕机）、从库灵活的复杂均衡配置、耗时查询的SQL语句路由到指定的从库、指定一些特定的表不需要读写分离（如，基础数据表）等等，随着系统数据的增加，以后还会设计到分片（分库和分表），分片以后优惠设计到分布式事务，以上这些如果通过业务代码去实现，那需要费太多男子且稳定性是个大问题。

​		有没有更优雅的解决方案？中间件或许是个不错的选择。EF Core 也一样可以很好实现基于中间件实现读写分离。



**为什么要使用中间件**

- 读写分离采用客户端直连方案（C# 代码直接实现），因为少了一层中间件转发，查询性能可能会稍微好一点。但是这种方案，由于要了解后端的部署细节，所以在出现主备切换、数据库迁移等操作的时候，客户端都需要感知到，并且需要调整数据库连接信息。如果通过中间件转发，客户端不需要关注后端细节、连接维护、主从切换等工作，这些都有中间件来完成。这样就可以让业务端更关注业务逻辑的开发。
- 绝大部分生产项目，性能的瓶颈都在数据库。实现读写分离是解决性能瓶颈的首要手段之一。然而当读写分离还不能解决时，接下来手段就是分片（分库、分表）。数据被分到多个分片数据库后，应用如果需要读取数据，就要需要处理多个数据源的数据。如果没有数据库中间件，那么应用将直接面对分片集群，数据源切换、事务处理、数据聚合都需要应用直接处理，原本该是专注于业务的应用，将会花大量的工作来处理分片后的问题，最重要的是每个应用处理将是完全的重复造轮子。所以有了数据库中间件，应用只需要集中与业务处理，大量的通用的数据聚合，事务，数据源切换都由中间件来处理。
- 国内各大厂、各个云平台都有自己的数据库中间件。



**几款免费开源的中间件**

​		目前社区比较成熟的、免费开源的且还在维护的中间件有  `mycat`、`shardingsphere-proxy`、`proxysql`、`maxscale`。



**EFCore生成maxscale的Hint**

​		读写分离必须要部署集群，基于maxscale中间件实现，还需要安装 maxsale。

- [mariadb基于GTID主从复制搭建](https://github.com/AlphaYu/Adnc/tree/master/doc/mariadb)

- [maxscale安装](https://github.com/AlphaYu/Adnc/tree/master/doc/maxscale)

  

  EFCore的TagWith是什么请参考[官方文档](https://docs.microsoft.com/en-us/ef/core/querying/tags)。





[参考文章](https://www.cnblogs.com/alphayu/p/14241406.html)

