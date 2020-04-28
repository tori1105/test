# test
package cn.f.test;

import java.util.Scanner;

import cn.f.Dao.UserDao;
import cn.f.Dao.impl.UserDaoImpl;
import cn.f.game.GuessNumber;
import cn.f.pojo.User;

public class UserTest {
    static Scanner sc = new Scanner(System.in);
    // 多态
    static UserDao ud = new UserDaoImpl();

    public static void main(String[] args) {
        while (true) {
            // 欢迎界面，给出选项
            System.out.println("-------------欢迎光临--------------");
            System.out.println("1.登录");
            System.out.println("2.注册");
            System.out.println("3.退出");
            System.out.println("请输入你的选择：");
            // 键盘录入选择，根据选择做出不同的操作

            // 为了后面录入信息的方便，我所有的数据录入全部用字符接受
            String m = sc.nextLine();
            switch (m) {
            case "1":
                denglu();
                break;
            case "2":
                zhuce();
                break;
            case "3":

            default:
                System.out.println("谢谢使用，欢迎下次再来！");
                System.exit(0);
            }
        }
    }

    public static void denglu() {
        System.out.println("-------------登录界面（请先注册后再登录！）--------------");
        System.out.println("请输入用户名：");
        String n = sc.nextLine();
        System.out.println("请输入密码：");
        String p = sc.nextLine();
        // 调用登录功能
        boolean flag = ud.isLogin(n, p);
        if (flag) {
            System.out.println("登录成功！奖励你玩游戏。");
            System.out.println("你要玩吗？y/n");
            while (true) {
                String r = sc.nextLine();
                if (r.equalsIgnoreCase("y")) {
                    // 玩游戏
                    GuessNumber.strat();
                    System.out.println("是否继续游戏？y/n");
                }else{
                    break;
                }
            }
            System.out.println("谢谢使用，欢迎下次再来！");
            System.exit(0);
        } else {
            System.out.println("用户名或者密码有误，登录失败！");
        }
    }

    public static void zhuce() {
        // 注册界面，请输入用户名和密码
        System.out.println("-------------注册界面--------------");
        System.out.println("请输入用户名：");
        String name = sc.nextLine();
        System.out.println("请输入密码：");
        String mima = sc.nextLine();
        // 把用户名和密码封装到一个对象中
        User user = new User();
        user.setName(name);
        user.setMima(mima);
        // 调用注册功能
        ud.regist(user);
        System.out.println("注册成功！");
    }
}
//以下是添加的登录功能
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
