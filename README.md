<%@ page language="java" import="java.util.*" pageEncoding="utf-8"%>
<%@ page import="java.sql.*"%>
<html>
  <head>
    <title>My JSP 'uc.jsp' starting page</title>
  </head>
  
  <body>
    <%
    	String name=request.getParameter("yonghu");
    			//接收參數，大多數接收參數的方法
    	name=new String(name.getBytes("ISO-8859-1"),"utf-8");
    	//處理參數中文亂碼
    	String pwd=request.getParameter("mima");
    	
    	String url="jdbc:mysql://localhost:3306/test";
    	
    	String driverClass="com.mysql.jdbc.Driver";
    	String username="root";
    	String password="159459";
    	Class.forName(driverClass);
    	Connection conn=DriverManager.getConnection(url,username,password);
    	
    	Statement stmt=conn.createStatement();
    	ResultSet rs=stmt.executeQuery("select * from tb_asd");
    	int flag=1;
    	while(rs.next())
    	{
    		String sqlname=rs.getString("name");
    		String sqlpwd=rs.getString("pwd");
    		if(name.equals(sqlname)&&pwd.equals(sqlpwd))
    		{
    			out.print("通过验证！");
    			flag=0;
    			break;
    		}
    	}
    	rs.close();
    	stmt.close();
    	conn.close();
    	if(flag==1)
    	{
    		out.print("登陆失败，2秒后转至登录页面！");
    		response.setHeader("refresh","2;url=login.jsp");
    		//頁面停留
    	}
     %>
  </body>
</html>
