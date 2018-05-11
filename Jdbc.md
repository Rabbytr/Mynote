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














d
