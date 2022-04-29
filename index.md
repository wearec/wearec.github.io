#刘江晨的blog
#关键字

####一、this关键字

#####this关键字用法1：==this.属性名==

***解决成员变量与局部变量名称冲突的问题***
  *当一个类的属性（成员变量）名与访问该属性的方法参数名相同时，==则需要使用 this 关键字来访问类中的属性，即引用当前类的实例变量，即this关键字来区分局部变量和实例变量==，以区分类的属性和方法中的参数。*

```java{.line-numbers}
public class Teacher {
    private String name;    // 教师名称
    private double salary;    // 工资
    private int age;    // 年龄
}
// 创建构造方法，为上面的3个属性赋初始值
public Teacher(String name,double salary,int age) {
    this.name = name;    // 设置教师名称
    this.salary = salary;    // 设置教师工资
    this.age = age;    // 设置教师年龄
}
public static void main(String[] args) {
    Teacher teacher = new Teacher("王刚",5000.0,45);
    System.out.println("教师信息如下：");
    System.out.println("教师名称："+teacher.name+"\n教师工资："+teacher.salary+"\n教师年龄："+teacher.age);
}
//输出结果
教师信息如下
教师名称：王刚
教师工资：5000.0
教师年龄：45
```

*this.name表示当前对象具有的变量name.等号右边的name表示通过参数传递过来的值。*

#####this关键字用法2：==this.方法名(参数)==

***让类中一个方法访问类中的另一个方法和变量***
*this 可以代表任何对象，当 this 出现在某个方法体中时，它所代表的对象是不确定的，但它的类型是确定的，它所代表的只能是当前类的实例。只有当这个方法被调用时，它所代表的对象才被确定下来，==谁在调用这个方法，this 就代表谁。==*

```java{.line-numbers}
// 定义一个run()方法，run()方法需要借助jump()方法
//
public class sports{
    String shoes;
    static String water;
public void run() {
    // 使用this引用调用run()方法的对象
    this.jump();
    this.shoes;
    sports.water;
    System.out.println("正在执行run方法");
    }
}
```

大部分时候，一个方法访问该类中定义的其他方法、成员变量时加不加 this 前缀的效果是完全一样的。

```java{.line-numbers}
public void run() {
    jump();
    shoes;
    water;
    System.out.println("正在执行run方法");
}
```

* 注意：对于 static 修饰的方法而言，可以使用类来直接调用该方法，如果在 static 修饰的方法中使用 this 关键字，则这个关键字就无法指向合适的对象。
* 所以，==static 修饰的方法中不能使用 this 引用==。
* Java 语法规定，==静态成员不能直接访问非静态成员==。

#####this关键字用法3：==this()访问构造方法==

* this()不能再普通方法中使用，只能再构造方法中使用
* 在构造方法中使用时，必须是第一条语句
* 括号内可以有参数，有参数表明调用指定的构造方法

```java{.line-numbers}
public class this3_person {
        int age;
        String name;
        int sex;
        String job;
        public this3_person(int age, String name, int sex){
            this.age=age;
            this.name=name;
            this.sex=sex;
        }
        public this3_person(int age, String name, int sex, String job) {
            this(age, name, sex);
            this.job = job;
        }
void display(){
    System.out.println(age+name+sex+job);
    }
}
```

test类

```java{.line-numbers}
public class this3_test {
    public static void main(String[] args) {
        this3_person pe=new this3_person(2,"张三",0);
        this3_person per=new this3_person(3,"李四",1);
pe.display();
per.display();

    }
}
```

**注意：this括号内的参数必须与成员变量的参数一致，不可自定义，而构造方法内的参数可以自定义**

####二、static关键字

* *static修饰的成员变量称为静态变量（类变量），修饰的方法称为静态方法（类方法），统称为静态成员，归整个类所有*
* *static修饰的方法或变量不需要依赖与对象来访问，可直接访问（输入方法名）或通过类名来访问。*

#####静态变量

* 在类中定义静态的属性（成员变量），在 main() 方法中可以直接访问，也可以通过类名访问，还可以通过类的实例对象来访问。
* 在类的内部，可以在任何方法内直接访问静态变量。
* 在其他类中，可以通过类名访问该类中的静态变量。

```java{.line-numbers}
public class static_person {
    public static String name="a";
    public static void main(String[] args) {
    String age="b";
        System.out.println(name+age);//直接访问name
        System.out.println(static_person.name+age);//通过 类名访问
        static_person s=new static_person();
        System.out.println(s.name);//通过类的实例去访
        }
    }
```

#####静态方法

见第二节 方法

####三、final关键字

* final修饰变量，表示变量的值不可改变，即称为常量
* final修饰方法，表示方法不可被重写
* final修饰类，表示该类不可被继承

#####final修饰变量

* final 修饰的变量不能被赋值这种说法是错误的，严格的说法是，final 修饰的变量不可被改变，一旦获得了初始值，该 final 变量的值就不能被重新赋值。
* 使用 final 修饰的引用类型变量不能被重新赋值，但可以改变引用类型变量所引用对象的内容。例如一个数组名Arr所引用的数组对象，final 修饰后的 Arr 变量不能被重新赋值，但 Arr 所引用数组的数组元素可以被改变。

#####final 修饰方法

* final 修饰的方法仅仅是不能被重写，并不是不能被重载。
* 如果子类中定义一个与父类 private方法有相同方法名、相同形参列表、相同返回值类型的方法，也不是方法重写，只是重新定义了一个新方法。因此，即使使用 final 修饰一个 private 访问权限的方法，依然可以在其子类中定义与该方法具有相同方法名、相同形参列表、相同返回值类型的方法。

####四、super关键字

#####super调用父类构造方法

* 子类不继承父类的构造方法，如果子类想使用父类的构造方法，必须在子类的构造方法中使用关键字super表示
* super语句要放在第一行，在子类构造方法中，第一条语句默认调用父类的构造方法，不写super()代表默认调用父类的无参构造方法。如果父类只有有参构造方法而没有无参构造方法时，必须写一个带相应参数的super(参数列表)；

```java{.line-numbers}
public class super1_student {
    int number;
    String name;
    super1_student(int number,String name){
        this.number=number;
        this.name=name;
    }
    public int getnumber(){
        return number;//上述第七行已经获得number的值
    }
    public String getname(){
        return name;//上述第八行已经获得name的值。
    }
    }
 class universtudent extends super1_student{
    int age;//子类新增的属性
    universtudent(int number,String name,int age){
        super(number,name);
    }
    public int getage(){
        return age;
    }
}
```

主函数

```java{.line-numbers}
public class super1_test {
    public static void main(String[] args) {
        universtudent liu=new universtudent(111,"jc",11);
        int number=liu.getnumber();
        String name=liu.getname();
        int age=liu.getage();
        System.out.println("liu的学号，姓名，年龄是"+number+name+age);
    }
}
```

#####super访调用成员方法和属性

*super访问父类的成员与this关键字相似。不过super访问的是子类的父类*
==当父类的属性名和子类的属性名或父类的方法名和子类的方法明显相同时需要用super进行调用==

* super.member(member是父类的成员)
* 不需放在第一行

```java{.line-numbers}
class Person {
    void message() {
        System.out.println("This is person class");
    }
}

class Student extends Person {
    void message() {
        System.out.println("This is student class");
    }

    void display() {
        message();
        super.message();
    }
}

class Test {
    public static void main(String args[]) {
        Student s = new Student();
        s.display();
    }
}
```

####五、instanceof关键字

* 用于判断一个对象是否为一个类（或接口、抽象类、父类）的实例
* 格式：boolean result = obj instanceof Class
  * 返回值为true or false
  * Class 表示一个类或接口
  * obj 是 class 类（或接口）的实例或者子类实例
