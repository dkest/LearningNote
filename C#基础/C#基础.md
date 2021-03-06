### 虚方法和抽象方法

###### 虚方法

* 用virtual修饰的方法叫虚方法
* 虚方法可以在子类中通过override关键字来重写
* 常见的虚方法：ToString()  Equals()



###### 抽象方法

* 抽象类与抽象方法由abstract修饰

* abstract的使用注意

  > * 抽象方法没有方法体
  > * 抽象成员只能存在于抽象类中
  > * 抽象类可以由非抽象成员
  > * 抽象类的派生类必须实现抽象方法体
  > * 抽象类只能用作基类，无法实例化



##### 比较

| 虚方法              | 抽象方法           |
| ------------------- | ------------------ |
| 用 virtual 修饰     | 用 abstract 修饰   |
| 要有方法体          | 不允许由方法体     |
| 可以被子类 override | 必须被子类override |
| 除了密封类都可以写  | 只能在抽象类中     |



### 抽象类和接口

###### 抽象类
抽象类是特殊的类，只是不能被实例化；除此以外，具有类的其他特性；
重要的是抽象类可以包括抽象方法，这是普通类所不能的。
抽象方法只能声明于抽象类中，且不包含任何实现，派生类必须覆盖它们。
另外，抽象类可以派生自一个抽象类，可以覆盖基类的抽象方法也可以不覆盖，如果不覆盖，则其派生类必须覆盖它们。

###### 接口
接口除了可以包含方法之外，还可以包含属性、索引器、事件，而且这些成员都被定义为公有的。除此之外，不能包含任何其他的成员，例如：常量、域、构造函数、析构函数、静态成员。

###### 相同点
1）都可以被继承。
2）不能被实例化。
3）自身不提供实现代码。
4）派生类必须实现未实现的方法。

###### 不同点
1）抽象基类可以定义字段、属性、方法实现。接口只能定义属性、索引器、事件、和方法声明，不能包含字段。
2）接口可以被多重实现，抽象类只能被单一继承。
3）一个类一次可以实现若干个接口，但是只能扩展一个父类。
4）抽象类实现的具体方法默认为虚的，但实现接口的类中的接口方法默认为非虚的，不过你也可以声明为虚的。
5）抽象类实现了 OOP 中的一个原则，把可变的与不可变的分离。抽象类和接口就是定义为不可变的，而把可变的交给子类去实现。
6）好的接口定义应该是具有专一功能性的，而不是多功能的，否则造成接口污染。如果一个类只是实现了这个接口的中一个功能，而不得不去实现接口中的其它方法，就叫接口污染。