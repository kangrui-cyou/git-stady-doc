##***Spring源码分析 - 设计模式 - 委派模式***

## **什么是委派模式？**

* 两个角色：受托人、委托人
* 持有委托人的引用
* 关心的是结果

## 代码实现

```java
/*
* 某一个功能的接口
*/
public interface ITarget{
    public void doing(String command);
}
```

```java
/*
* 具体的功能实现者  被委派者
*/
public class UserA impements ITarget{
    @Override
    public void doing(String command){
        System.out.pring("祥哥在肯吃肯吃的"+command)
    }
}
```

```java
/*
* 委派者
*/
public class Leader implements ITarget{
    private Map<String,ITarget> targets = new HashMap<>();
    public Leader(){
        targets.put("写代码"，new UserA());
    }
    
    //项目经理自己不干活
    public void doing(String command){
        targets.get(command).doing(command);
    }
}
```

```java
/*
* 委派的核心：分发、调度、派遣
* 就是静态代理和策略模式的一种特殊组合
*/
public class test{
    @Test
    public void test{
        new Leader().doing("写代码");
    }
}
```

