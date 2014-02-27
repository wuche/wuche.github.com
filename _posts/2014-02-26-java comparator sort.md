---
title: java comparator 接口排序实现   
author: wuche  
layout: post  
permalink:  /java-comparator/  
tags:  
  - java 
  - 排序 
  
---    
在web开发过程中，经常要对list进行排序，升序，降序。数据库是mysql的话，直接可以从数据中捞出已经排好序的结果。
这里介绍一种用java实现的排序方法，可以对list中的对象进行排序，非常方便。  
<!--more-->  
对象类。根据person类的name进行排序。
```java   
public class Person {
  
  private String name;
  
  private Integer age;

  public String getName() {
    return name;
  }

  public void setName(String name) {
    this.name = name;
  }

  public Integer getAge() {
    return age;
  }

  public void setAge(Integer age) {
    this.age = age;
  }

  @Override
  public String toString() {
    return "Person [name=" + name + "]";
  }

  /**
   * @param name
   * @param age
   */
  public Person(String name, Integer age) {
    super();
    this.name = name;
    this.age = age;
  }
  
  public Person(){
    
  }

}
  ```       
  排序测试类，继承java的comparator接口。   
  ```java      
public class ComparatorTest implements Comparator<Person>{

  @Override
  public int compare(Person o1, Person o2) {
    // TODO Auto-generated method stub
    return o1.getName().compareTo(o2.getName());
  }
  
  public static void main(String[] args) {
    List<Person> persons = new ArrayList<Person>();
    Person person = new Person("wuche",10);
    Person person2 =new Person("adc",21);
    Person person3 = new Person("zzz",6);
    persons.add(person);
    persons.add(person2);
    persons.add(person3);
    ComparatorTest comTest = new ComparatorTest();
  //  Collections.sort(persons,comTest);(默认是升序)
    Collections.sort(persons,Collections.reverseOrder(comTest)); //降序，用collections.reverseOrder进行反转
    for(Person per : persons){
      System.err.println(per);  
    }

  }

}
  ```  
  根据person的name排序，是按照string的字母顺序。有的时候，需要对数字的大小进行排序。  Comparator 比较器也可以实现。  
  ```java
  public class ComparatorTest implements Comparator<Person>{

  @Override
  public int compare(Person o1, Person o2) {
    // TODO Auto-generated method stub
    return o1.getName().compareTo(o2.getName());
  }

  public static void main(String[] args) {
    List<Person> persons = new ArrayList<Person>();
    Person person = new Person("wuche",10);
    Person person2 =new Person("adc",21);
    Person person3 = new Person("zzz",6);
    persons.add(person);
    persons.add(person2);
    persons.add(person3);
  //  ComparatorTest comTest = new ComparatorTest();
  //  Collections.sort(persons,comTest);
  //  Collections.sort(persons,Collections.reverseOrder(comTest));
        Collections.sort(persons,new AgeComparartor());
    for(Person per : persons){
      System.err.println(per);
    }

  }


}
  class AgeComparartor implements Comparator<Person>{
    @Override
    public int compare(Person person, Person person2) {
        return person.getAge()-person2.getAge();  //To change body of implemented methods use File | Settings | File Templates.
    }
}
  ```   
  输出结果：   
Person [name=zzz]   
Person [name=wuche]  
Person [name=adc]    
如果要倒序呢？很简单，修改下AgeComparator的compare方法，
```java   
    public int compare(Person person, Person person2) {
        return person2.getAge()-person1.getAge();  //To change body of implemented methods use File | Settings | File Templates.
    }
```  
输出结果：  
Person [name=adc]  
Person [name=wuche]  
Person [name=zzz]  