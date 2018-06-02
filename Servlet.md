### Servlet 生命周期
* #### 构造函数
* #### 初始化init
* #### doGet or doPost
* #### 销毁destroy

### 返回编码
* #### 设置格式为text/json  
* #### response.setContentType("text/json");
* #### 设置字符集为'UTF-8'
* #### response.setCharacterEncoding("UTF-8");

### 跳转
* #### 重定向 resp.sendRedirect(url)
* #### 请求转发： getRequestDispatcher(path).forward(request,response)
* #### 请求包含： getRequestDispatcher(path).include(request,response)

### 表单post&get
* #### 得到单个请求参数： req.getParameter(arg0_name)
* #### 得到参数数组：req.getParameterValues(arg0_name)

> ##### 可以用doPost调用doGet

### Cookie&Session
```
//设置Cookie
Cookie cookie = new Cookie(key,value);
cookie.setMaxAge(time);
resp.addCookie(cookie);
//获取Cookie
Cookie[] Cookies = req.getCookies();

//设置Session
HttpSession session = req.getSession();
session.setAttribute(key, value);
String value = session.getAttribute(key);
```

### Servlet共享变量
* ##### 1.ServletContext
作用域为整个Web容器
* ##### 2.HttpSession
作用域为一次会话
* ##### 3.HttpServletRequest
作用域为一次请求
