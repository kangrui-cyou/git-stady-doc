## ***Spring源码分析 - 设计模式 - 代理模式***

### **什么是代理模式？**

* 代理模式是给某一个对象提供一个代理对象，并由代理对象控制原对象的引用
* 字节码重组
* 这样的好处是可以再目标对象实现的基础上，添加额外功能，也就是扩展了目标对象的功能

## **穷举**

* 中介
* 黄牛
* 媒婆

## **特点**

* 两个角色：代理对象和被代理对象
* 只注重过程，被代理对象必须要做，而自己没时间或者做不好的事
* 代理对象必须拿到被代理对象的身份，也就是引用

## **代码实现**

* jdk

```java
/*
* Person 接口
*/
public interface Person{
    public void findLove();//寻求真爱
}
```

```java
/*
* Person 实例化对象
*/
public class ZhangXiang implemments Person{
    private String sex = "男";
    private String name = "张祥";
    
    @Override
    public void findLove(){
        System.out.print("我叫"+this.name+"性别"+this.sex);
        System.out.print("找对象的条件是"+"肤白貌美大长腿！");
    }
    //省略get/set/构造
}
```

```java
/*
* JDK动态代理 需实现InvocationHandler接口
* 媒婆 
*/
public calss JDKMeiPo implements InvocationHandler{
    
    //被代理人的引用作为一个成员变量进行保存
    private Person target;
    
    //获取被代理人的个人资料 参数为Person接口
    public Object getInstance(Person target) throws Exception{
        this.target = target;
        //被代理对象的class
        Class clazz = target.getClass();
        //需要三个参数 被代理对象的类类型  被代理对象的接口类类型 当前对象
        //也就决定了为什么jdk代理基于接口实现  
        //该方法执行完成以后会自动生成代理对象，并之心 invoke方法
        return Proxy.newProxyInstance(
          clazz.getClassLoader(),
          clazz.getInsterfaces(),
          this);
    }
    
    @Override
    publilc Object invoke(Object proxy,Method,Object[] args){
        //是不是类似前置 后置 环绕 异常 
        System.out.print("我是媒婆，我要给你找对象了~");
        method.invode(this,target,args);//执行原始方法
        System.out.print("找完了，能不能成就看你自己了");
    	return null;    
    }
}
```

```java
/*
* 测试类
*/
public class TestFindLove{
    //自己找对象  找的慢  没资源
    @Test
    public void testZiJiZhao{
        ZhangXiang zx = new ZhangXiang();
        zx.findLove();
    }
    
    //jdk 动态代理测试  可以在没有生成代码对象之前和在生成代理对象之后查看类类型是否发生变化
    @Test
    public void JDKMeiPo(){
        /*原理
        *1：拿到被代理对象的引用
        *2：JDK重新生成一个类，同时实现我们给代理对象实现的接口
        *3：把代理对象的引用也拿到
        *4：重新动态生成一个class字节码
        *5：动态编译
        */
        Person obj = (Person) new JDKMeiPo().getInstance(new ZhangXiang());
        obj.findLove();
    }
    
}
```

* cglib

```java
/*
* 被代理类
*/
public class ZhangXiang{
    private String sex = "男";
    private String name = "张祥";
    
    public void findLove(){
        System.out.print("我叫"+this.name+"性别"+this.sex);
        System.out.print("找对象的条件是"+"肤白貌美大长腿！");
    }
    //省略get/set/构造
}
```

```java
/*
* 代理类将被代理类作为自己的父类
*
*/
public class CGLIBMeiPo implements MethidInterceptor{
    
    //该方法用于生成动态代理类
    public Object getInterceptor(Class clazz)throws Exception{
        Enhancer enhancer = new Enhancer();
        //把父类设置为谁？
        //这一步就是告诉cglib，生成的子类需要继承那个类
        enhancer.setSuperclass(clazz);
        //设置回调
        enhancer.setCallback(this);
        //第一步：生成源代码
        //第二步：编译成class文件
        //第三步：加载到JVM中，并返回代理对象
        return enhancer.create();
    }
    
    //同样是做了字节码重一件事 
    //对于使用api的用户来说是无感知的（悄悄地给你搞了一个儿子你还不知道）
    @Override
    public Object intercept(Object obj,Method method,Object[] args,MethodProxy proxy) throws Exception{
        System.out.print("我是CGLIB媒婆，我要给你找对象了~");
        
        //Super就是原始被代理对象  
        proxy.invokeSuper(obj,args);
        //proxy.invoke(obj,args);//这样会死循环  调取的是动态代理为你生成的子类的方法
        
        return null;
    }
    
}
```

```java
/*
* 测试类
*/
public class TestFindLove{
    //自己找对象  找的慢  没资源
    @Test
    public void testZiJiZhao{
        ZhangXiang zx = new ZhangXiang();
        zx.findLove();
    }
    
    @Test
    public void CGLIBmeipo(){
        /*原理
        *1：CGLIB的动态代理是通过生成一个被代理对象的子类，然后重写父类的方法
        *2：生成以后的对象可以强制转换为被代理对象
        *3：子类的引用赋值给父类
        */
        ZhangXiang obj = (ZhangXiang) new CGLIBMeiPo().getInstance(ZhangXiang.class;
        obj.findLove();
    }
    
}
```



### **两种代理的对比**

*  JDK

  * jdk的动态代理是通过接口进行强制转换的
  * 生成以后的代理对象，可以强制转换为接口

*  CGLIB

  * CGLIB的动态代理是通过生成一个被代理的对象的子类，然后重写费用类的方法
  * 生成以后的对象，可以强制转换为被代理对象
  * 子类引用赋值给父类
