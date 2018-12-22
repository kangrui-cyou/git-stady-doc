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
    //省略get/set
}
```

```java
/*
* JDK动态代理 需实现InvocationHandler接口
*
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