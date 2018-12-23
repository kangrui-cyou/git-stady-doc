##***Spring源码分析 - 设计模式 - 单例模式***

## **概念**

* 保证从系统启动到系统停止，全过程只会产生一个实例。

## **穷举**

* 配置文件
* 每个人的个体

## **代码演示**

```java
/*
*	懒汉式单例，在第一次调用的时候实例化
*/
public class Singleton1{
    //1构造私有
    private Singleton1(){}
    //2:声明静态变量保存单例的引用
    private static Singleton1 single = null;
    //3：通过一个静态的方法获取单例引用
    //不安全
    public static Singleton1 getSingleton1(){
        if(single == null){
            single = new Singleton1();
        }
        return single;
    }
}
```

```java
/*
*	懒汉式单例，在第一次调用的时候实例化
*   并保证线程安全
*/
public class Singleton2{
    //1构造私有
    private Singleton2(){}
    //2:声明静态变量保存单例的引用
    private static Singleton2 single = null;
    //3：通过一个静态的方法获取单例引用
    // 为了保证多线程环境下的正确访问，给方法上加同步锁保证线程安全
    // 可是这样新能低下，并行变串行，浪费资源
    public static synchronized Singleton2 getSingleton2(){
        if(single == null){
            single = new Singleton2();
        }
        return single;
    }
}
```

```java
/*
*	懒汉式单例，双重锁检查
*/
public class Singleton3{
    //1构造私有
    private Singleton3(){}
    //2:声明静态变量保存单例的引用
    private volatile static Singleton3 single = null;
    //3：通过一个静态的方法获取单例引用
    // 为了保证多线程环境下的正确访问，双重锁检查
    public static  Singleton3 getSingleton3(){
        if(single == null){
            synchronized(Singleton3.class){
                if(single == null){
                    single = new Singleton3();
                }   
            }
        }
        return single;
    }
}
```

```
/*
* 懒汉式静态内部类
* 这种写法即解决了安全，又解决了性能
*/
public class Singletin4{
    //1:先声明一个静态内部类
    //private私有保证别人不能修改   static保证全局唯一
    private static class LazyHolder{
        private static final Singletin4 INSTANCE = new Singletin4();
    }
    
 	//2:将构造方法私有
    private Singletin4(){}
    
    //3:提供静态方法获取实例 
    //final确保别人不能覆盖该方法
    public static final Singletin4 getSingletin4(){
    	//方法中的逻辑是在用户调用的时候才执行的，内存也是在调用的时候分配
        return LazyHolder.INSTANCE;
    }
}
```

```java
/*
* 饿汉式单例 类初始化时就创建 
*/
public class Singletin5{
	//私有构造
    private Singletin5(){}
    //声明静态变量 在类初始化的时候就初始化变量 天生的安全
    private static final Singletin5 single = new Singletin5();
    //开放静态方法 获取实例
    public static Singletin5 grtSingletin5(){
        return new Singletin5();
    }
}
```

```java
/*
* 类名注册 去容器里面取
*/
public class Singletin6{
    private static Map<String,Singletin6> map = new HashMap<>();
    static{
        Singletin6 singletin = new Singletin6();
        map.put(singletin.getClass(),singletin);
    }
    protected Singletin6(){}
    //静态工厂方法，返回实例
    public static Singletin6 getSingletin6(String name){
        if(name == null){
            name = Singletin6.class.getName();
        }
        if(map.get(name)==null){
            try{
                map.get(name,(Singletin6)Class.forName(name).newInstance());
            }catch(Exception e){
                e.printStaskTrace();
            }
        }
        return map.get(name);
    }
}
```

```
还有一种  枚举~
```



