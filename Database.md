1. **MySQL 是一种 DBMS 而不是查询语言，SQL 才是查询语言**

2. **为什么 SQL 不区分大小写？**
	+ 因为历史上内存很珍贵，用6位字符集不足以表示52个大小写字母，因此不区分大小写形成习惯后，即便后来有了7位 ASII，还是不区分，不过 SQL 不区分大小写只是默认选择，用户依然可以选择区分大小写
	+ 与 SQL 不同，绝大多数编程语言受 UNIX 和 C 的影响，是区分大小写的

3. **"LIKE + 通配符" 与 "REGEXP + 正则表达式" 有什么关系？**
  	+ "LIKE + 通配符" 匹配的是整个列
  	+ "REGEXP + 正则表达式" 是匹配的列值，只要列值在其中就可以，但也可以匹配整个列，通过定位符"^"和"$"即可

4. **relation 相当于集合，因此对集合的操作也适用于 relation**

5. **select 是选择列，where 用来过滤行**
  	+ 过滤行这一操作可以让 SQL 来完成，也可以让 SQL 返回所有行，然后让应用来自行完成，但后者会因传输荣誉而造成网络资源的浪费，且应用不具备可伸缩性

6. **在文件系统中，数据是面向具体应用的，其特点是只考虑内部的字段间的联系，而不必考虑文件之间的联系。而在数据库系统中，数据是面向系统的，要以最优的方式适应多个应用程序的需求，它不仅要反映记录内部的联系，还要反映记录外部之间的联系，这种联系是以实体集之间的联系来描述的**

7. **笛卡尔积与关系**
	+ 在数据库中，关系用元祖表示，它是笛卡尔积的子集，笛卡尔积可以说是所有关系的总和
	+ 关系就是表，表示关系的形式，关系是表的意义
	+ 关系表并不是简单的二维表，它是一种规范化的表，遵循一系列规范

8. **SQL = Structured Query Language，是基于关系模型的数据库查询语言，SQL 是高度非过程化的，用户只需指出要做什么，而不需要指出怎么做**

9. **数据库管理系统和数据库系统不是同一个概念**
	+ 数据库管理系统(DBMS)介于用户和操作系统之间的程序，它是数据库系统的核心，对下操纵数据库，对上向用户应用和管理员提供接口
	+ 而数据库系统是包含了 DB，DBMS，Users，OS，Manager 等的完整的系统

10. **为什么要独立于文件系统来开发数据库系统？文件系统和数据库系统之间是什么关系？**
	+ 文件系统和数据库系统之间是合作关系，其中，操作系统包含了文件系统，而数据库管理系统则是操作系统之上的一种应用程序
	+ DBMS 可以调用 OS 的文件系统功能来实现，也可以绕过文件系统，自己去调用 I/O 来实现，有些数据库是不用文件系统的

11. 