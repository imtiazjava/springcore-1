 #SpringIOC Application
 
 1.Test.java
 package com.bms.beans;

import java.util.Iterator;
import java.util.List;
import java.util.Map;
import java.util.Set;

public class Test {
	int id;
	String name;
	double salary;

	int arr[];
	String s[];

	Employee emp;
	Employee e[];

	List<Employee> list;
	Set<Employee> set;
	Map<Integer, String> map;

	public void setId(int id) {
		this.id = id;
	}

	public void setName(String name) {
		this.name = name;
	}

	public void setSalary(double salary) {
		this.salary = salary;
	}

	public void setArr(int[] arr) {
		this.arr = arr;
	}

	public void setS(String[] s) {
		this.s = s;
	}

	public void setEmp(Employee emp) {
		this.emp = emp;
	}

	public void setE(Employee[] e) {
		this.e = e;
	}

	public void setList(List<Employee> list) {
		this.list = list;
	}

	public void setSet(Set<Employee> set) {
		this.set = set;
	}

	public void setMap(Map<Integer, String> map) {
		this.map = map;
	}

	public void print() {
		System.out.println(this.id);
		System.out.println(this.name);
		System.out.println(this.salary);
		for (int i : arr) {
			System.out.println(i);
		}
		for (String ss : s) {
			System.out.println(ss);
		}
		System.out.println(e.toString());
		for (Employee ee : e) {
			System.out.println(ee.toString());
		}

		list.forEach(s -> System.out.println(s));
		set.forEach(s -> System.out.println(s));
		Set ss = map.entrySet();
		Iterator it = ss.iterator();
		while (it.hasNext()) {
			System.out.println(it.next());
		}
	}
}


2.Employee.java
package com.bms.beans;

public class Employee {
int id;
String name;
public void setId(int id) {
	this.id = id;
}
public void setName(String name) {
	this.name = name;
}
@Override
public String toString() {
	return "Employee [id=" + id + ", name=" + name + "]";
}




}

3.ClientCode
package com.bms.beans;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class ClientCode {

	public static void main(String[] args) {
		
	ApplicationContext context = new ClassPathXmlApplicationContext("spring.xml");
	Test ref = context.getBean("test",Test.class);
	ref.print();

	}

}

4.spring.xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<beans xmlns="http://www.springframework.org/schema/beans"
 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 xmlns:context="http://www.springframework.org/schema/context"	
xsi:schemaLocation="http://www.springframework.org/schema/beans
 http://www.springframework.org/schema/beans/spring-beans-4.3.xsd
 http://www.springframework.org/schema/context
 http://www.springframework.org/schema/context/spring-context-4.3.xsd">
<context:property-placeholder location="classpath:mydata.properties"/>

<bean id="e1" class="com.bms.beans.Employee">
	<property name="id" value="${id}"/>
	<property name="name" value="${name}"/>
</bean>
<bean id="e2" class="com.bms.beans.Employee">
	<property name="id" value="${id1}"/>
	<property name="name" value="${name1}"/>
</bean>



<bean id="test" class="com.bms.beans.Test" scope="singleton">
	<property name="id" value="1001"/>
	<property name="name" value="ss"/>
	<property name="salary" value="45000.00"/>
	<property name="arr">
			<list>
				<value>1</value>
				<value>2</value>
				<value>3</value>
				
			</list>
	</property>
	<property name="s">
		<list>
			<value>india</value>
			<value>palestan</value>
			<value>turkey</value>
		</list>
	</property>
	
	<property name="emp" ref="e1"/>
	<property name="e">
		<list>
			<ref bean="e1"/>
			<ref bean="e2"/>
			
		</list>
	</property>
	
	
	<property name="list">
			<list>
					<ref bean="e1"/>
					<ref bean="e2"/>
				
			</list>
	</property>
	
	<property name="set">
			<set>
					<ref bean="e1"/>
					<ref bean="e2"/>
				
			</set>
	</property>
	
	<property name="map">
			<map>
				<entry key="1001" value="lux"/>
				<entry key="1002" value="santoor"/>
				<entry key="1003" value="xxx"/>
			</map>
	</property>
	
	
</bean>
</beans>

5.mydata.properties
id=1001
name=raju
id1=1002
name1=sunil
