# 这里是刘江晨的其中一个java基础学习blog
## 面向对象编程三大特性

#### 封装

* 封装的特点：只能通过规定的方法访问数据。
  隐藏类的实例细节，方便修改和实现。
* 封装的具体实践步骤
  * 修改属性的可见性来限制对属性的访问，一般设为 private。
  * 为每个属性创建一对赋值（setter）方法和取值（getter）方法，一般设为 public，用于属性的读写
  * 在赋值和取值方法中，加入属性控制语句（对属性值的合法性进行判断）。

```java{.line-numbers}
public class Employee {
    private String name; // 姓名
    private int age; // 年龄
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        // 对年龄进行限制
        if (age < 18 || age > 40) {
            System.out.println("年龄必须在18到40之间！");
            this.age = 20; // 默认年龄
        } else {
            this.age = age;
        }
    }
```

```java{.line-numbers}
public class EmployeeTest {
    public static void main(String[] args) {
        Employee people = new Employee();
        people.setName("王丽丽");
        people.setAge(35);
        System.out.println("姓名：" + people.getName());
        System.out.println("年龄：" + people.getAge());
    }
}
```

*输出结果
姓名：王丽丽
年龄：35*

#### 继承

* 定义：在已经存在类的基础上进行扩展，从而产生新的类。已经存在的类称为父类、基类或超类，而新产生的类称为子类或派生类。在子类中，不仅包含父类的属性和方法，还可以增加新的属性和方法。
* 格式：修饰符 子类 extends 父类{类的主体}
* 只允许一个类直接继承另一个类，即==子类只能有一个直接父类，但可以有多个间接父类==，extends 关键字后面只能有一个类名。
  ==*如下演示方法的继承与重写*==

```java{.line-numbers}
public class father {
    double A(int x,int y){
        return x+y;
    }
    double B(int m,int n){
        return m*n;
    }
}

class son extends father {
    double A(int x,int y){
        return x+2*y;
    }
}
```

主函数

```java{.line-numbers}
public class test {
    public static void main(String[] args) {
        son s=new son();
        System.out.println(s.A(1,2));

    }
}

```

*输出结果5.0*

#### 多态

==补充：对象类型转换==
*这里的类型转换是指存在继承关系的类型转换*

##### 向上转型

父类引用指向子类对象

* 格式：父类类名 对象名=new 子类类名。
* 向上转型就是把子类对象直接赋给父类引用，不用强制转换。
* 使用向上转型可以调用父类类型中的所有成员，不能调用子类类型中特有成员，最终运行效果看子类的具体实现

```java{.line-numbers}
class Car {
    public void run() {
        System.out.println("这是父类run()方法");
    }
}

public class Benz extends Car {
    public void run() {
        System.out.println("这是Benz的run()方法");

    }

    public void price() {
        System.out.println("Benz:800000$");
    }

    public static void main(String[] args) {
        Car car = new Benz();//向上转型
        car.run();
       //car.price();程序报错
    }
}

```

*当调用price方法时，程序就会报错*

此处进行的是向上转型，虽然car对象指向子类，但是==子类进行了向上转型，就失去了调用父类中没有的方法的权力，只能调用父类中存在的方法，==

***

##### 向下转型

子类对象指向父类引用
格式 ；子类名 =new 父类名()

* 向下转型必须进行强制类型转换
  * 父类引用指向的对象一定是该子类对象
  * 引入运算符instanceof来判断，判断成功后再进行强制转换

```java{.line-numbers}
  Animal animal = new Cat();
if (animal instanceof Cat) {
    Cat cat = (Cat) animal; // 向下转型
    ...
}
```
***
***

* 多态的定义：==多态是同一个行为具有多个不同表现形式或形态的能力。==
* 多态的分类：多态分为编译时多态和运行时多态。
  * 其中编译时多态是静态的，主要是指方法的重载，它是根据参数列表的不同来区分不同的方法。通过编译之后会变成两个不同的方法，在运行时谈不上多态。
  * 而运行时多态是动态的，它是通过动态绑定来实现的，也就是大家通常所说的多态性。
* 多态存在的==必要==条件：继承、重写和向上转型。
  * 继承：在多态中必须存在有继承关系的子类和父类。
  * 重写：子类对父类中某些方法进行重新定义，在调用这些方法时就会调用子类的方法。
  * 向上转型：在多态中需要将子类的引用赋给父类对象，只有这样该引用才既能可以调用父类的方法，又能调用子类的方法。
* 多态的实现方式(==充要==)：
  * 方法重写
  * 接口
  * 抽象类和抽象方法

```java{.line-numbers}

```
