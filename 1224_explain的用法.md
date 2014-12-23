##explain的用法
###用于解释命令是显示mysql是如何的使用索引来来处理select语句及连接表。从而可以写出更好的索引和写出更好的优化语句来进行查询；
####使用语句 explain select * from testtable where id = 9;
--
#### 会出现以下的语句提示：id selectType table type possible_key key key_len ref rows extra
--
###解释如下：
###table : 显示当前语句要执行的表名
--
####type :最重要的一列，显示链接使用了何种类型，从最好到最差的类型依次为:const、eq_reg、ref、range、index 、all 
####possible_key:显示可能用在当前表中的索引，为空的话表示没有，可以为相关的域选择一个合适的语句
####key:实际用的索引，很少的情况下mysql会选择优化不足的sql语句
####key_len:使用的索引的长度，默认的情况下越短越好
####ref:显示索引的那一列被使用了，如果可能的话是一个常数
####rows:mysql 返回必须或者实际要检查的行数
####Extra:解析查询额外的信
