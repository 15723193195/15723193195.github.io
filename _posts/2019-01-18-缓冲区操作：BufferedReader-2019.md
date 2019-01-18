---
layout:     post                    # 使用的布局（不需要改）
title:      缓冲区操作：BufferedReader            # 标题 
subtitle:         					#副标题   
date:       2019-01-18              # 时间
author:     XHN                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - java基础
---

如果说想在把所有的输入数据放在一起了，一次性读取出来，那么这个时候肯定就能够避免中文问题了，而这一操作就必须依靠缓冲区操作流完成。对于缓冲区的读取在IO包中定义了两种类：BufferedInputStream，BufferedReader，但是考虑到本次操作有中文的问题，肯定使用BufferedReader类完成操作。下面就需要观察一下BufferedReader类的继承结构，构造方法，操作方法：

| **继承结构：** | java.lang.Object<br>java.io.Reader<br>java.io.BuffereedReader |
| --- | --- |
| **构造方法：** | public BuffereedReader( **Reader in** ) |
| **读取操作：** | public String readLine() throws IOException |


实际上之所以不使用BufferedInputStream而使用BufferedReader类的另外一个原因在于BufferedReader类有一个方法可以读取一行数据，而这个方法BufferedInputStream类没有。

在BufferedReader类之中的readLine()方法返回的是String数据，而一旦返回的数据类型是String就非常方便：

- String类之中有大量的方法供用户操作；
- String类可以直接使用正则验证其格式；
- String类可以向基本数据类型或日期型进行转型操作。

范例：使用BufferedReader进行数据读取

	package cn.mldn.test;
	import java.io.BufferedReader;
	import java.io.InputStreamReader;
	import java.io.Reader;
	import java.io.CharArrayReader;
	import java.io.InputStream;
	import java.io.OutputStream;
	public class SystemTest {
		public static void main(String[] args) throws Exception {
			// TODO 自动生成的方法存根
			InputStream input =System.in;
			System.out.println("请输入：");
			//BufferedReader构造接收Reader对象，InputStreamReader对象向上转型称为BufferedReader对象,InputStreamReader构造接收InputStream对象，System.in是InputStream对象
			BufferedReader buf=new BufferedReader(
					new InputStreamReader(System.in));
			String str=buf.readLine();
			System.out.println(str);
		}
	}
	请输入：
	邸田贵
	邸田贵

此时输入的数据不再存在长度的限制了，并且可以方便的进行中文数据的输入。

范例：对输入的数据进行验证，现在要求一个用户由键盘输入一个数字，而后进行数字的乘法运算，如果用户输入的不是数字则需要提醒用户重新输入

	package cn.mldn.test;
	import java.io.BufferedReader;
	import java.io.InputStreamReader;
	import java.io.Reader;
	import java.io.InputStream;
	public class SystemTest {
		public static void main(String[] args) throws Exception {
			// TODO 自动生成的方法存根
			InputStream input =System.in;
			
			//BufferedReader构造接收Reader对象，InputStreamReader对象向上转型称为BufferedReader对象,InputStreamReader构造接收InputStream对象，System.in是InputStream
			BufferedReader buf=new BufferedReader(
					new InputStreamReader(System.in));
			boolean flag=true;
			while(flag){
				System.out.println("请输入数字：");
				String str=buf.readLine();
				if(str.matches("\\d+")){
					
					int num=Integer.valueOf(str);
					System.out.println(num*num);
					flag=false;
				}else{
					System.out.println("请重新输入");
				}
			}
		}
	}
	请输入数字：
	qw
	请重新输入
	请输入数字：
	12
	144

通过本程序只是希望提醒，如果要想使用BufferedReader多次输入数据的话，重复调用readLine()方法即可。
