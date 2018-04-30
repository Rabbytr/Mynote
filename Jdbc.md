## java Jdbc
```
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;
...
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
