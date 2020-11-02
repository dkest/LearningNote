抽象类和接口的区别
===========
      LayoutInflater.inflate()这个方法，大家一定很熟悉——在给fragment添加布局文件，或者在RecyclerView

的Adapter中为item添加布局时，都会用到。inflate()这个方法需要最多三个参数：resource，root，以及

attachToRoot。参考源码，就知道了这里的resource是你具体要添加的那个布局文件，root是布局的根参数，

那么attachToRoot是什么意思呢？什么时候为true，什么时候为false？


三个参数的关系
-----------

    1）抽象类可以提供成员方法的实现细节，而接口中只能存在public abstract方法；
    2）抽象类中的成员变量可以是各种类型的，而接口中的成员变量只能是public static final类型的；
    
    3）接口中不能含有静态代码块以及静态方法，而抽象类可以有静态代码块和静态方法；
    
    4）一个类只能继承一个抽象类，而一个类却可以实现多个接口。
    
    
2.设计层面上的区
---------------


