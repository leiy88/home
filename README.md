---
title: Java泛型
tags: Java,Generic,泛型
grammar_cjkRuby: true
---
## 为什么要有泛型？
### 没有泛型时存在的问题
1. 参数无法任意化
2. 集合弱类型
### 使用泛型的目的
1. 参数任意化
2. 类型安全
3. 消除强制类型转换
4. 运行时异常提前为编译时异常

## 定义
>　　泛型，即“参数化类型”。提到参数，最熟悉的就是定义方法时有形参，然后调用此方法时传递实参。
>　　泛型就是将类型由原来的具体的类型参数化，类似于方法中的变量参数，此时类型也定义成参数形式（可以称之为类型形参），然后在使用/调用时传入具体的类型（类型实参）。例如：List\<E\>中，E就是类型形参，当实例化成List\<String\>时，String就是传入的类型实参。
>　　JDK 1.5之后，用\<\>（diamond）来表示泛型

## 使用
### 泛型类
### 泛型接口
### 泛型方法

## Bound
### 上界
泛型参数在具体化时最大可以使用的类型，比如T extends Number
那么在具体化T的时候，他可以是Number或Number的子类，最大就是Number
### 下界
相反，最小类型，比如T super Integer
那么具体化T时，可以使Integer以及它的父类Number和Object，最小是Integer
### PECS原则

## Wildcard

## 泛型擦除
### 泛型擦除带来的问题

## 协变(covariant)与逆变(contravariant)
```java?linenums
Object[] objs = new String[3];
List<Number> list = new ArrayList<Integer>();
public void foo(List<? extends Number> list){
	list.add(new Integer(1));
}

public void bar(List<? super Number> list){
	Number number = list.get(0);
}
```
数组是协变的
令f(A)=A[]，容易证明数组是协变的：
String≤Object 
Object[] objs = new String[] ==> f(String)≤ f(Object)
泛型时不变的
f(A)=List\<A\>
List\<Integer\>跟List\<Number\>即f(Integer)跟f(Number)并没有什么关系
由于泛型的不变性，导致List\<Number\>中无法放入Integer类型的元素，违背了里氏替换原则

为了让泛型可以协变，加入了通配符
？ extends实现协变
List<? extends Number> list = new ArrayList\<Integer\>();
？ super实现逆变
List<? super Number> list = new ArrayList\<Object\>();

