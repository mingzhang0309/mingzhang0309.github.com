---
layout: post
title: java annotation
description: 学习GUAVA过程中遇到了很多的annotation，本文记录java annotation相关知识
category: blog
---

## java annotation常见作用
<ul>
    <li>生成文档。这是最常见的，也是java 最早提供的注解。常用的有@see @param @return 等</li>
    <li>跟踪代码依赖性，实现替代配置文件功能。比较常见的是spring 2.5 开始的基于注解配置。作用就是减少配置。现在的框架基本都使用了这种配置来减少配置文件的数量。</li>
    <li>在编译时进行格式检查。如@override 放在方法前，如果你这个方法并不是覆盖了超类方法，则编译时就能检查出。</li>
</ul>


## 四个元注解
四个元注解分别是：@Target,@Retention,@Documented,@Inherited ，再次强调下元注解是java API提供，是专门用来定义注解的注解

### @Target
@Target 表示该注解用于什么地方，可能的值在枚举类 ElemenetType 中，包括：
          ElemenetType.CONSTRUCTOR 构造器声明
          ElemenetType.FIELD 域声明（包括 enum 实例）
          ElemenetType.LOCAL_VARIABLE 局部变量声明
          ElemenetType.METHOD 方法声明
          ElemenetType.PACKAGE 包声明
          ElemenetType.PARAMETER 参数声明
          ElemenetType.TYPE 类，接口（包括注解类型）或enum声明 

### @Retention
@Retention 表示在什么级别保存该注解信息。可选的参数值在枚举类型 RetentionPolicy 中，包括：
          RetentionPolicy.SOURCE 注解将被编译器丢弃
          RetentionPolicy.CLASS 注解在class文件中可用，但会被VM丢弃
          RetentionPolicy.RUNTIME VM将在运行期也保留注释，因此可以通过反射机制读取注解的信息。 

### @Documented
@Documented 将此注解包含在 javadoc 中 ，它代表着此注解会被javadoc工具提取成文档。在doc文档中的内容会因为此注解的信息内容不同而不同。相当与@see,@param 等。

### @Inherited
在您定义注解后并使用于程序代码上时，预设上父类别中的注解并不会被继承至子类别中，您可以在定义注解时加上java.lang.annotation.Inherited 限定的Annotation，这让您定义的Annotation型别被继承下来。

## 代码
代码来自[宁静致远][]
### Author.java
{% highlight java %}
package com.ming.annotation;

import java.lang.annotation.Documented;
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

/**
 * 定义作者信息，name和group
 * 
 * @author ming
 * 
 */
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
@Documented
public @interface Author {

	String name();

	String group();
}

{% endhighlight %}
### Description.java
{% highlight java %}
package com.ming.annotation;
/**
 * 
 */
import java.lang.annotation.Documented;
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;
/**
 * @author ming
 * 
 *         定义描述信息 value
 */
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
@Documented
public @interface Description {
	String value();
}
{% endhighlight %}
### Utility.java
{% highlight java %}
package com.ming.annotation;
@Description(value = "这是一个有用的工具类")
public class Utility {
	@Author(name = "ming", group = "com.ming")
	public String work() {
		return "work over!";
	}
}
{% endhighlight %}
### AnalysisAnnotation.java
{% highlight java %}
package com.ming.annotation;

import java.lang.reflect.Method;

public class AnalysisAnnotation {
	/**
	 * 在运行时分析处理annotation类型的信息
	 * 
	 * 
	 */
	public static void main(String[] args) {
		try {
			// 通过运行时反射API获得annotation信息
			Class rt_class = Class.forName("com.ming.annotation.Utility");
			Method[] methods = rt_class.getMethods();

			boolean flag = rt_class.isAnnotationPresent(Description.class);

			if (flag) {
				Description description = (Description) rt_class
						.getAnnotation(Description.class);
				System.out.println("Utility's Description--->"
						+ description.value());
				for (Method method : methods) {
					if (method.isAnnotationPresent(Author.class)) {
						Author author = (Author) method
								.getAnnotation(Author.class);
						System.out.println("Utility's Author--->"
								+ author.name() + " from " + author.group());

					}
				}
			}

		} catch (ClassNotFoundException e) {
			e.printStackTrace();
		}
	}

}
{% endhighlight %}


## 相关资料
[ELmentType.PACKAGE][] 关于注解用于包中的说明，package-info.java 作用及用法详解

[GUAVA annotation][] GUAVA中的注解

[java annotation][] java 注解

## 总结
注解在应用级开发中应用的比较少，这里主要是在看GUAVA源码中遇到了一些问题记录与此，关于具体注解的应用到了公司再慢慢研究。

[GUAVA annotation]:    http://www.cnblogs.com/zemliu/p/3311276.html "GUAVA annotation"
[zhangming]:    http://mingzhang0309.github.com  "zhangming"
[ELmentType.PACKAGE]:    http://www.tmser.com/?post=36&page=1 "ELmentType.PACKAGE"
[宁静致远]:    http://www.cnblogs.com/mandroid/archive/2011/07/18/2109829.html "宁静致远"
[java annotation]:    http://blog.csdn.net/lifetragedy/article/details/7394910 "java annotation"
