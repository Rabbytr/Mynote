## java Jdbc
```
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;
···
try{
  Class.forName("com.mysql.jdbc.Driver");
  String url = "jdbc:mysql://localhost:3306/" + "db1";
  Connection conn = DriverManager.getConnection(url, "root", "123456");
  Statement state = conn.createStatement();
  System.out.print("Success");
  String sql = "select * from users order by id desc";
  ResultSet result = state.executeQuery(sql);
  System.out.println(result==null);
  while (result.next()) {
    System.out.println(result.getInt(1));
  }   
  }catch (Exception e) {
    System.out.print(e);
  }
```  

## ResultSet
* #### -next()  
返回boolean类型，判断是否有数据  

## PreparedStatement
```
String sql = "select * from table where id = ?";
PreparedStatement pstmt = conn.prepareStatement(sql);
pstmt.setInt(1, n);
pstmt.executeUpdate();
```
* 修改数据使用: pstmt.executeUpdate();
* 查询数据使用: pstmt.executeQuery();

## DBUtils
* QueryRunner qr = new QueryRunner(myDBUtil.getDataSource());
* #### 插入-删除-修改：qr.update(sql,params)
* #### 批量参数：qr.batch(sql, params[]);
* #### 查询：qr.query(sql,new ArrayHandler(),params)

* ### ResultSetHandler接口
**ArrayHandler()**：把结果集中的第一行数据转成对象数组（存入Object[]）    
```
String sql = "select * from user where phonenumber = ?";
User user = qr.query(sql,new BeanHandler<User>(User.class),"10086");
```
**ArrayListHandler()**：把结果集中的每一行数据都转成一个对象数组，再存放到List中。  
**BeanHandler(Class<T> type)**：将结果集中的第一行数据封装到一个对应的JavaBean实例中  
**ColumnListHandler(String columnName/int columnIndex)**：将结果集中某一列的数据存放到List中。  
**MapHandler()**：将结果集中的第一行数据封装到一个Map里，key是列名，value就是对应的值。  
**MapListHandler()**：将结果集中的每一行数据都封装到一个Map里，然后再将所有的Map存放到List中。  
**KeyedHandler(String columnName)**：将结果集每一行数据保存到一个“小”map中,key为列名，value该列的值，再将所有“小”map对象保存到一个“大”map中 ， “大”map中的key为指定列，value为“小”map对象  
**ScalarHandler(int columnIndex)**：通常用来保存只有一行一列的结果集
> 数据库中的表**列名**与Bean类中**属性**名称一致  
