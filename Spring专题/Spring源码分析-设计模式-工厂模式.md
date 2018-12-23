##***Spring源码分析 - 设计模式 - 工厂模式***

## **什么是工厂模式？**

* 工厂模式是用来实例化对象的，替代new操作，统一化，值关注结果
* 解耦

## **工厂模式的种类**

* 简单工厂（Simple Factory）

  * 也就是写一个函数或者类方法来构造对象

  ```java
  /*
  * 汽车接口 汽车需要满足一定标准才能上路
  */
  public interface Car{
      public String carName();
  }
  ```

  ```java
  /*
  * 汽车实例
  */
  public Aodi implements Car{
      @Override
      public String carName(){
          return "奥迪"；
      }
  }
  ```

  ```java
  /*
  * 简单工厂 或者你可以用switch写  没啥区别
  * 可是这个工厂太牛逼了 啥都能干 不实际 不专业
  * 那么全栈工程师真的存在么  只不过是一群学跳舞的猴子  没意义
  */
  public class SimpleCarFactory{
      public Car getCarByName(String carName){
          if("奥迪".equals(carName)){
              return new Aodi();
          }else{
              return null;
          }
      }
  }
  ```

  ```java
  public class SimpleCarFactoryTest{
      @test
      public void test1{
          SimpleCarFactory sf = new SimpleCarFactory();
      	Aodi aodi = (Aodi)sf.getCarByName("奥迪");
      }
  }
  ```

* 工厂方法模式（Factory Method）

  * 工厂老大 一个接口 所有的工厂需要按照大厂的标准来执行
  * 具体工厂 大厂的实现类 它含有具体的业务逻辑

  ```java
  /*
  * 汽车接口 汽车需要满足一定标准才能上路
  */
  public interface Car{
      public String carName();
  }
  ```

  ```java
  /*
  * 汽车实例
  */
  public Aodi implements Car{
      @Override
      public String carName(){
          return "奥迪"；
      }
  }
  ```

  ```java
  /*
  * 工厂接口 定义了所有工厂的执行标准
  */
  public intergace Faction{
      Car getCar();
  }
  ```

  ```java
  /*
  * 具体的产品工程 按标准生产
  */
  public class AodiFactory implemrnt Factory{
      @Override
      public Car getCar(){
          return new Aodi();
      }
  }
  ```

  ```java
  public class FactoryTest{
      @test
      public void test1{
      	//各个产品的生产商都拥有各自的产品
          Factory factory = new AodiFactory();
          Aodi aodi = (Aodi)factory.getCar();
      }
  }
  ```

* 抽象工厂模式

  * 抽象工厂：定义产品
  * 具体工厂：生产具体产品

  ```java
  /*
  * 汽车接口 汽车需要满足一定标准才能上路
  */
  public interface Car{
      public String carName();
  }
  ```

  ```java
  /*
  * 汽车实例
  */
  public Aodi implements Car{
      @Override
      public String carName(){
          return "奥迪"；
      }
  }
  ```

  ```java
  /*
  * 抽象工厂模式 用户的主入口
  */
  public abstract class AbstractFactory{
      //可添加一些公共的逻辑  方便管理
      
      /*
      * 抽象工厂指定标准 由car工厂去自己实现
      */
      public abstract Car getAodi();
  }
  ```

  ```java
  /*
  * car 工厂
  */
  public CarFactory extends AbstractFactory{  
      @Override
      public Car getAodi(){
          return new Aodi();
      }
  }
  ```

  ```java
  public class AbstractFactoryTest{
      @test
      public void test1{
      	//对于用户而言只有选择权  只需求去买奥迪 不管别的
          AbstractFactory factory = new CarFactory();
          Aodi aodi = factory.getAodi();
      }
  }
  ```

