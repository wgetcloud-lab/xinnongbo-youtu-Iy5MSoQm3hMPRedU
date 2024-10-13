
plsql是什么：


![](https://img2024.cnblogs.com/blog/2064545/202410/2064545-20241012154410979-1371887509.png)


就是这个，专门操作oracle的一个工具，好用还免费。


创建一个测试表:




```
create table Student(
Id number not null,
Name varchar(20),
Age number,
Grade number,
Gender varchar(2)
)
```


里面的varchar2()是oracle自己专门的字符类型，用就行了。


光标移到表上，右键选择Describe:


![](https://img2024.cnblogs.com/blog/2064545/202410/2064545-20241012154540751-1664803035.png)


现在这些字段都没有说明，不知道是什么意思，给他们都添加说明




```
comment on table Student is '学生表';
comment on column Student.id is 'ID';
comment on column Student.Name is '姓名';
comment on column Student.Age is '年龄';
comment on column Student.Grade is '年纪';
comment on column Student.Gender is '性别';
```


![](https://img2024.cnblogs.com/blog/2064545/202410/2064545-20241012154907922-1236710375.png)


添加一条测试数据


![](https://img2024.cnblogs.com/blog/2064545/202410/2064545-20241012155342520-1999694766.png)


添加多条数据，但是不写insert


![](https://img2024.cnblogs.com/blog/2064545/202410/2064545-20241012155513875-1737581159.png)


在后面输入一个for update，上面的操作栏会显示有可以提交的事务，先不用管，然后现在点击一下下面的锁


![](https://img2024.cnblogs.com/blog/2064545/202410/2064545-20241012155625135-636524609.png)


oracle会生成一个空白行，然后前面带有一个✳，我们先选中我们添加的那一行数据:


![](https://img2024.cnblogs.com/blog/2064545/202410/2064545-20241012155718809-1708552817.png)


然后复制一下，复制以后再选中下一行，不停的粘贴就行了


![](https://img2024.cnblogs.com/blog/2064545/202410/2064545-20241012155933274-2028127749.png)


 然后改一下数据，最后点击一下那个绿色的小勾，再点一下绿色的锁，最后我们去点一下菜单栏的提交事务按钮


![](https://img2024.cnblogs.com/blog/2064545/202410/2064545-20241012160032221-326832792.png)


 执行完毕以后点击查询就可以了：


![](https://img2024.cnblogs.com/blog/2064545/202410/2064545-20241012160159343-1216276166.png)


如果只想执行某一段代码，可以用鼠标选中自己想执行的代码就行了，如图所示，后面的for update就没有执行;


如果想更新某个字段，也可以直接通过上面的步骤操作，有点像在操作excel的感觉；


如果想删除，也和上面的操作类似，只不过是点击的按钮不一样；


![](https://img2024.cnblogs.com/blog/2064545/202410/2064545-20241012161432845-1535927408.png)


执行以后，刘德华就会被删除。


数据的导出：


可以选中行,按住ctrl可以选多行.


![](https://img2024.cnblogs.com/blog/2064545/202410/2064545-20241012160454964-681411761.png)


 在粘贴板上就会把sql语句粘贴进去：


![](https://img2024.cnblogs.com/blog/2064545/202410/2064545-20241012160549467-484258124.png)


删掉多余的，只保留insert部分就可以了。


怎么看我们最开始的建表语句了：


![](https://img2024.cnblogs.com/blog/2064545/202410/2064545-20241012160755280-572813972.png)


点击  view


右下角有一个view sql的按钮，点一下


![](https://img2024.cnblogs.com/blog/2064545/202410/2064545-20241012160859298-1292033070.png)


![](https://img2024.cnblogs.com/blog/2064545/202410/2064545-20241012161032615-1769577908.png)


点进去就可以看到建表语句了，复制出来保存就行了。


暂时只想到这些


下面是一些常用的查询语句




```
select * from student t where instr(t.name, '刘') > 0; --模糊查询

select *
  from student t
 where (t.name = '刘德华' and t.age = '50')
    or t.name = '梁朝伟'; --多个条件的查询

select t.*,
       case
         when t.gender = '男' then
          '帅哥'
         when t.gender = '女' then
          '美女'
         else
          '不知道'
       end p --查询的时候条件判断
  from student t;

select t.*, decode(t.name, '刘德华', '我最喜欢的明星', '明星') -- 判断
  from student t;

select t.*, nvl(t.name, '非主流') from student t; --判断名字是不是空select wm_concat(t.name) from student t --合并多行的某条数据,可以配合group by
```


 QQ技术交流群：332035933；


 


 本博客参考[蓝猫机场](https://fenfang.org)。转载请注明出处！
