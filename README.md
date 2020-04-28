package com.yyq.dao;
 
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
 
import com.yyq.entity.Student;
import com.yyq.util.Conn;
 
public class StudentDao {
	private Connection con = null;
	private PreparedStatement pst = null;
	
	public StudentDao() {
		con =Conn.getConnection();
	}
	
	//编写登录验证方法valiUser()
	public boolean valiUser(Student user){
		try{
			pst = con.prepareStatement("select * from user where username=? and pwd=?");
			pst.setString(1, user.getUserName());
			pst.setString(2, user.getPwd());
			ResultSet rs =pst.executeQuery();
			if(rs.next()){
				return true;
			}else{
				return false;
			}
		}catch(Exception e){
			e.printStackTrace();
			return false;
		}
	}
}
