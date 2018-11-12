---
layout: post
title: "设计模式(Design Patterns)"
description: "Design Patterns"
category: JavaKnowledge
tags: [JavaKnowledge]
imagefeature: blog/bg.jpg
comments: true
mathjax: null
featured: false
published: true
---

设计模式(Design Patterns)
===

设计模式`(Design pattern)`是一套被反复使用、多数人知晓的、经过分类编目的、代码设计经验的总结。使用设计模式是为了可重用代码、让代码更容易被他人理解、保证代码可靠性。 
毫无疑问，设计模式于己于他人于系统都是多赢的，设计模式使代码编制真正工程化，设计模式是软件工程的基石，如同大厦的一块块砖石一样。
项目中合理的运用设计模式可以完美的解决很多问题，每种模式在现在中都有相应的原理来与之对应，每一个模式描述了一个在我们周围不断重复发生的问题，以及该问题的核心解决方案，这也是它能被广泛应用的原因。


设计模式的分类
---

总体来说设计模式分为三类:     

- 创建型模式:工厂方法模式、抽象工厂模式、单例模式、建造者模式、原型模式。
- 结构型模式:适配器模式、装饰器模式、代理模式、外观模式、桥接模式、组合模式、享元模式。
- 行为型模式:策略模式、模板方法模式、观察者模式、迭代子模式、责任链模式、命令模式、备忘录模式、状态模式、访问者模式、中介者模式、解释器模式。


设计模式的六大原则
---

- 开闭原则`(Open Close Principle)`             
    开闭原则就是说对扩展开放，对修改关闭。在程序需要进行拓展的时候，不能去修改原有的代码，实现一个热插拔的效果。所以一句话概括就是:
    为了使程序的扩展性好，易于维护和升级。想要达到这样的效果，我们需要使用接口和抽象类，后面的具体设计中我们会提到这点。

- 里氏代换原则`（Liskov Substitution Principle）`        
    里氏代换原则面向对象设计的基本原则之一。 里氏代换原则中说，任何基类可以出现的地方，子类一定可以出现。 `LSP`是继承复用的基石，只有当衍生类可以替换掉基类，
    软件单位的功能不受到影响时，基类才能真正被复用，而衍生类也能够在基类的基础上增加新的行为。
    里氏代换原则是对“开-闭”原则的补充。实现“开-闭”原则的关键步骤就是抽象化。而基类与子类的继承关系就是抽象化的具体实现，所以里氏代换原则是对实现抽象化的具体步骤的规范。

- 依赖倒转原则`（Dependence Inversion Principle）`      
    这个是开闭原则的基础，具体内容：真对接口编程，依赖于抽象而不依赖于具体。

- 接口隔离原则`（Interface Segregation Principle）`        
    这个原则的意思是：使用多个隔离的接口，比使用单个接口要好。还是一个降低类之间的耦合度的意思，从这儿我们看出，其实设计模式就是一个软件的设计思想，
    从大型软件架构出发，为了升级和维护方便。所以上文中多次出现：降低依赖，降低耦合。

- 迪米特法则（最少知道原则）`（Demeter Principle）`        
    为什么叫最少知道原则，就是说：一个实体应当尽量少的与其他实体之间发生相互作用，使得系统功能模块相对独立。

- 合成复用原则`（Composite Reuse Principle）`          
    原则是尽量使用合成/聚合的方式，而不是使用继承。



1.工厂方法模式`(Factory Method)`
---

工厂方法模式分为三种:      

- 普通工厂模式:就是建立一个工厂类，对实现了同一接口的一些类进行实例的创建。

    这里举一个发送邮件和发送短信的例子.      
    
    首先，创建两者的共同接口:   
    ```java
    public interface ISender {
        void send();
    }
    ```
    
    然后分别创建具体的实现类:   
    ```java
    public class MailSender implements ISender {
        @Override
        public void send() {
            System.out.println("mail sender");
        }
    }
    
    public class SmsSender implements ISender {
        @Override
        public void send() {
            System.out.println("sms sender");
        }
    }
    ```
    最后是建立工厂类:    
    ```java
    public class SendFactory {
        public ISender produce(String type) {
            if ("mail".equals(type)) {
                return new MailSender ();
            } else if ("sms".equals(type)) {
                return new SmsSender ();
            } else {
                System.out.println("请输入正确的类型!");
                return null;
            }
        }
    }
    ```

- 多个工厂方法模式:是对普通工厂方法模式的改进，在普通工厂方法模式中，如果传递的字符串出错，则不能正确创建对象，而多个工厂方法模式是提供多个工厂方法，分别创建对象。         

    将上面的代码进行修改，主要修改`SendFactory`就行:   
    ```java
    public class SendFactory {
        public ISender produceMail(){
            return new MailSender();
        }
    
        public ISender produceSms(){
            return new SmsSender();
        }
    }
    ```

- 静态工厂方法模式，将上面的多个工厂方法模式里的方法置为静态的，不需要创建实例，直接调用即可。

    ```java
    public class SendFactory {
        public static ISender produceMail(){
            return new MailSender();
        }
    
        public static ISender produceSms(){
            return new SmsSender();
        }
    }
    ```
    
    测试类:   
    ```java
    ISender sender = SendFactory.produceMail();  
    sender.Send();  
    ```

总体来说，工厂模式适合凡是出现了大量的产品需要创建，并且具有共同的接口时，可以通过工厂方法模式进行创建。在以上的三种模式中，第一种如果传入的字符串有误，不能正确创建对象，第三种相对于第二种，不需要实例化工厂类，所以，大多数情况下，我们会选用第三种——静态工厂方法模式。



2.抽象工厂模式`(Abstract Factory)`
---


工厂方法模式有一个问题就是，类的创建依赖工厂类，也就是说，如果想要拓展程序，必须对工厂类进行修改，这违背了闭包原则，所以，从设计角度考虑，有一定的问题，如何解决？就用到抽象工厂模式，创建多个工厂类，这样一旦需要增加新的功能，直接增加新的工厂类就可以了，不需要修改之前的代码。因为抽象工厂不太好理解，我们先看看图，然后就和代码，就比较容易理解。


还是用上面的例子，只是在工厂类这里需要改一下，提供两个不同的工厂类，他们要实现同一个接口:    

```java
public interface IProvider {  
    public ISender produce();  
}  
```

具体两个工厂类的实现:     

```java
public class SendMailFactory implements IProvider {     
    @Override  
    public ISender produce(){  
        return new MailSender();  
    }  
}  


public class SendSmsFactory implements IProvider{  
    @Override  
    public ISender produce() {  
        return new SmsSender();  
    }  
}  
```

测试类:    

```java
IProvider provider = new SendMailFactory();  
ISender sender = provider.produce();  
sender.Send();  
```

其实这个模式的好处就是，如果你现在想增加一个功能：发送即时信息，则只需做一个实现类，实现`ISender`接口，同时做一个工厂类，实现`IProvider`接口，就`OK`了，无需去改动现成的代码。这样做，拓展性较好！


3.单例模式`(Singleton)`
---


单例模式能保证在一个`JVM`中，该对象只有一个实例存在。

这样的模式有几个好处:      

- 某些类创建比较频繁，对于一些大型的对象，这是一笔很大的系统开销。
- 省去了`new`操作符，降低了系统内存的使用频率，减轻`GC`压力。
- 有些类如交易所的核心交易引擎，控制着交易流程，如果该类可以创建多个的话，系统完全乱了。（比如一个军队出现了多个司令员同时指挥，肯定会乱成一团），所以只有使用单例模式，才能保证核心交易服务器独立控制整个流程。

首先我们写一个简单的单例类：
```java
public class SingleTon {
    private static SingleTon instance = null;
    private SingleTon() {
    }
    public static SingleTon getInstance() {
        if (instance == null) {
            instance = new SingleTon();
        }
        return instance;
    }

    /* 如果该对象被用于序列化，可以保证对象在序列化前后保持一致 */
    public Object readResolve() {
        return instance;
    }
}
```

这个类可以满足基本要求，但是，像这样毫无线程安全保护的类，如果我们把它放入多线程的环境下，肯定就会出现问题了，如何解决？我们首先会想到对`getInstance()`方法加`synchronized`关键字，但是，`synchronized`关键字锁住的是这个对象，这样的用法，在性能上会有所下降，因为每次调用`getInstance()`，都要对对象上锁，事实上，只有在第一次创建对象的时候需要加锁，之后就不需要了，所以，这个地方需要改进。我们改成下面这个:   

```java
public class SingleTon {
    private static SingleTon instance = null;

    private SingleTon() {
    }

    public static SingleTon getInstance() {
        if (instance == null) {
            synchronized (instance) {
                if (instance == null) {
                    instance = new SingleTon();
                }
            }
        }
        return instance;
    }


    /* 如果该对象被用于序列化，可以保证对象在序列化前后保持一致 */
    public Object readResolve() {
        return instance;
    }
}
```

似乎解决了之前提到的问题，将`synchronized`关键字加在了内部，也就是说当调用的时候是不需要加锁的，只有在`instance`为`null`，并创建对象的时候才需要加锁，性能有一定的提升。         但是，这样的情况，还是有可能有问题的，看下面的情况：在`Java`指令中创建对象和赋值操作是分开进行的，也就是说`instance = new Singleton();`语句是分两步执行的。但是JVM并不保证这两个操作的先后顺序，也就是说有可能`JVM`会为新`的Singleton`实例分配空间，然后直接赋值给`instance`成员，然后再去初始化这个`Singleton`实例。这样就可能出错了。     

我们以`A`、`B`两个线程为例:      

- `A、B`线程同时进入了第一个`if`判断
- `A`首先进入`synchronized`块，由于`instance`为`null`，所以它执行`instance = new Singleton();`
- 由于`JVM`内部的优化机制，`JVM`先画出了一些分配给`Singleton`实例的空白内存，并赋值给`instance`成员（注意此时`JVM`没有开始初始化这个实例），然后`A`离开了`synchronized`块。
- `B`进入`synchronized`块，由于`instance`此时不是`null`，因此它马上离开了`synchronized`块并将结果返回给调用该方法的程序。
- 此时`B`线程打算使用`Singleton`实例，却发现它没有被初始化，于是错误发生了。

所以程序还是有可能发生错误，其实程序在运行过程是很复杂的，从这点我们就可以看出，尤其是在写多线程环境下的程序更有难度，有挑战性。我们对该程序做进一步优化:    

```java
public class SingleTon {

    private SingleTon() {
    }

    private static class SingletonFactory {
        private static SingleTon instance = new SingleTon();
    }

    public static SingleTon getInstance() {
        return SingletonFactory.instance;
    }

    public Object readResolve() {
        return getInstance();
    }
}
```

单例模式使用内部类来维护单例的实现，`JVM`内部的机制能够保证当一个类被加载的时候，这个类的加载过程是线程互斥的。这样当我们第一次调用`getInstance()`的时候，`JVM`能够帮我们保证`instance`只被创建一次，并且会保证把赋值给`instance`的内存初始化完毕，这样我们就不用担心上面的问题。同时该方法也只会在第一次调用的时候使用互斥机制，这样就解决了低性能问题。
其实说它完美，也不一定，如果在构造函数中抛出异常，实例将永远得不到创建，也会出错。所以说，十分完美的东西是没有的，我们只能根据实际情况，选择最适合自己应用场景的实现方法。


4.建造者模式`(Builder)`
---


工厂类模式提供的是创建单个类的模式，而建造者模式则是将各种产品集中起来进行管理，用来创建复合对象，所谓复合对象就是指某个类具有不同的属性，其实建造者模式就是前面抽象工厂模式和最后的`Test`测试类结合起来得到的。         

还是前面的例子，一个`ISender`接口，两个实现类`MailSender`和`SmsSender`。最后，建造者类如下:    
```java
public class SenderBuilder {
    private List<ISender> list = new ArrayList<>();
    public void produceMailSender(int count) {
        for (int i = 0; i < count; i++) {
            list.add(new MailSender());
        }
    }

    public void produceSmsSender(int count) {
        for (int i = 0; i < count; i++) {
            list.add(new SmsSender());
        }
    }
}
```

测试类:   
```java
Builder builder = new Builder();  
builder.produceMailSender(10);  
```

建造者模式将很多功能集成到一个类里，这个类可以创造出比较复杂的东西。所以与工程模式的区别就是：工厂模式关注的是创建单个产品，而建造者模式则关注创建符合对象，多个部分。因此，是选择工厂模式还是建造者模式，依实际情况而定。

5.原型模式`(Prototype)`
---

该模式的思想就是将一个对象作为原型，对其进行复制、克隆，产生一个和原对象类似的新对象。本小结会通过对象的复制，进行讲解。在`Java`中，复制对象是通过`clone()`实现的，先创建一个原型类:      

```java
public class Prototype implements Cloneable {
    public Object clone() throws CloneNotSupportedException {
        Prototype proto = (Prototype) super.clone();
        return proto;
    }
}
```

很简单，一个原型类，只需要实现`Cloneable`接口，重写`clone()`方法，此处`clone()`方法可以改成任意的名称，因为`Cloneable`接口是个空接口，你可以任意定义实现类的方法名，如`cloneA`或者`cloneB`，因为此处的重点是`super.clone()`这句话，`super.clone()`调用的是`Object`的`clone()`方法，而在`Object`类中，`clone()`是`native`的。

在这儿，将结合对象的浅复制和深复制来说一下，首先需要了解对象深、浅复制的概念:    

- 浅复制:将一个对象复制后，基本数据类型的变量都会重新创建，而引用类型，指向的还是原对象所指向的。
- 深复制:将一个对象复制后，不论是基本数据类型还有引用类型，都是重新创建的。简单来说，就是深复制进行了完全彻底的复制，而浅复制不彻底。

此处，写一个深浅复制的例子:   

```java
public class Prototype implements Cloneable, Serializable {
    private static final long serialVersionUID = 1L;
    private String string;
    private SerializableObject obj;

    /* 浅复制 */
    public Object clone() throws CloneNotSupportedException {
        Prototype proto = (Prototype) super.clone();
        return proto;
    }

    /* 深复制 */
    public Object deepClone() throws IOException, ClassNotFoundException {
        /* 写入当前对象的二进制流 */
        ByteArrayOutputStream bos = new ByteArrayOutputStream();
        ObjectOutputStream oos = new ObjectOutputStream(bos);
        oos.writeObject(this);

        /* 读出二进制流产生的新对象 */
        ByteArrayInputStream bis = new ByteArrayInputStream(bos.toByteArray());
        ObjectInputStream ois = new ObjectInputStream(bis);
        return ois.readObject();
    }

    public String getString() {
        return string;
    }

    public void setString(String string) {
        this.string = string;
    }

    public SerializableObject getObj() {
        return obj;
    }

    public void setObj(SerializableObject obj) {
        this.obj = obj;
    }
}

class SerializableObject implements Serializable {
    private static final long serialVersionUID = 1L;
}
```

实现深复制，需要采用流的形式读入当前对象的二进制输入，再写出二进制数据对应的对象。


适配器模式`(Adapter)`
---

适配器模式将某个类的接口转换成客户端期望的另一个接口表示，目的是消除由于接口不匹配所造成的类的兼容性问题。

主要分为三类：     

- 类的适配器模式            
    
    核心思想就是：有一个`Source`类，拥有一个方法，待适配，目标接口是`Targetable`，通过`Adapter`类，将`Source`的功能扩展到`Targetable`中。   

    ```java
    public interface Targetable {  
        /* 与原类中的方法相同 */  
	    public void method1();  
	  
	    /* 新类的方法 */  
	    public void method2();  
	}  

	public class Source {  	  
	    public void method1() {  
	        System.out.println("this is original method!");  
	    }  
	}  

	public class Adapter extends Source implements Targetable {  
	    @Override  
	    public void method2() {  
	        System.out.println("this is the targetable method!");  
	    }  
	} 

	public class AdapterTest {  
	    public static void main(String[] args) {  
	        Targetable target = new Adapter();  
	        target.method1();  
	        target.method2();  
	    }  
	}

	输出结果是:    
	this is original method!
	this is the targetable method!
    ```

    `Adapter`类继承`Source`类，实现`Targetable`接口,这样`Targetable`接口的实现类就具有了`Source`类的功能。

- 对象的适配器模式                

    基本思路和类的适配器模式相同，只是将`Adapter`类作修改，这次不继承`Source`类，而是持有`Source`类的实例，以达到解决兼容性的问题。   

    只修改上面的`Adapter`类就可以了。   

    ```java
	public class Adapter implements Targetable {  
	    private Source source;  
	    public Adapter(Source source){  
	        super();  
	        this.source = source;  
	    }  
	    @Override  
	    public void method2() {  
	        System.out.println("this is the targetable method!");  
	    }  
	  
	    @Override  
	    public void method1() {  
	        source.method1();  
	    }  
	} 

	public class AdapterTest {  
	    public static void main(String[] args) {  
	        Source source = new Source();  
	        Targetable target = new Wrapper(source);  
	        target.method1();  
	        target.method2();  
	    }  
	}  
    ```
    输出结果和上面的一样，只是适配器的方法不同。


- 接口的适配器模式

    有时我们写的一个接口中有多个抽象方法，当我们写该接口的实现类时，必须实现该接口的所有方法，这明显有时比较浪费，因为并不是所有的方法都是我们需要的，
    有时只需要某一些，此处为了解决这个问题，我们引入了接口的适配器模式，借助于一个抽象类，该抽象类实现了该接口，实现了所有的方法，
    而我们不和原始的接口打交道，只和该抽象类取得联系，所以我们写一个类，继承该抽象类，重写我们需要的方法就行。例如`Android ListView`中的`Adapter`就是这样设计的。 

    ```java
	public interface ISourceable {  
	    public void method1();  
	    public void method2();  
	    public void method3();  
	    public void method4();  
	    public void method5();  
	    public void method6();  
	}

	public abstract class BaseAdapter implements ISourceable{  
        public void method1() {

        }
	    public void method2() {
        		
        }
	    public void method3() {
        		
        }
	    public void method4() {
        		
        }
	    public void method5() {
        		
        }
	    public void method6() {
        		
        }
	}

	public class ListAdapter extends BaseAdapter {  
		// 不用全部实现方法，只需要实现自己需要的就可以了
	    public void method4(){  
	        System.out.println("the sourceable interface's first Sub1!");  
	    }  
	}  
    ```


总结一下三种适配器模式的应用场景:     

- 类的适配器模式:当希望将一个类转换成满足另一个新接口的类时，可以使用类的适配器模式，创建一个新类，继承原有的类，实现新的接口即可。
- 对象的适配器模式:当希望将一个对象转换成满足另一个新接口的对象时，可以创建一个`Adapter`类，持有原类的一个实例，在`Adapter`类的方法中，调用实例的方法就行。
- 接口的适配器模式:当不希望实现一个接口中所有的方法时，可以创建一个抽象类`Adapter`，实现所有方法，我们写别的类的时候，继承抽象类即可。


装饰模式`(Decorator)`
---

装饰模式就是给一个对象增加一些新的功能，而且是动态的，要求装饰对象和被装饰对象实现同一个接口，装饰对象持有被装饰对象的实例。     

`Source`类是被装饰类，`Decorator`类是一个装饰类，可以为`Source`类动态的添加一些功能，代码如下:    

```java
public interface ISourceable {  
    public void method();  
} 

public class Source implements ISourceable {  
    @Override  
    public void method() {  
        System.out.println("the original method!");  
    }  
} 
public class Decorator implements ISourceable {   
    private ISourceable source;        
    public Decorator(ISourceable source){  
        super();  
        this.source = source;  
    }  
    @Override  
    public void method() {  
        System.out.println("before decorator!");  
        source.method();  
        System.out.println("after decorator!");  
    }  
}
public class DecoratorTest {  
   public static void main(String[] args) {  
        ISourceable source = new Source();  
        ISourceable obj = new Decorator(source);  
        obj.method();  
    }  
}  

输出:       
before decorator!
the original method!
after decorator!
```

装饰器模式的应用场景:      

- 需要扩展一个类的功能。
- 动态的为一个对象增加功能，而且还能动态撤销。（继承不能做到这一点，继承的功能是静态的，不能动态增删）

缺点：产生过多相似的对象，不易排错！


代理模式`(Proxy)`
---

代理模式就是多一个代理类出来，替原对象进行一些操作，比如我们在租房子的时候回去找中介，为什么呢？因为你对该地区房屋的信息掌握的不够全面，希望找一个更熟悉的人去帮你做，此处的代理就是这个意思。再如我们有的时候打官司，我们需要请律师，因为律师在法律方面有专长，可以替我们进行操作，表达我们的想法。也就是说把专业事情交给专业的人来做。    

代理按照代理的创建时期，可以分为两种:     

- 静态代理:由程序员创建代理类或特定工具自动生成源代码再对其编译。在程序运行前代理类的`.class`文件就已经存在了。   
- 动态代理:在程序运行时运用反射机制动态创建而成。     

静态代理是在编译时就将接口、实现类、代理类一股脑儿全部手动完成，但如果我们需要很多的代理，每一个都这么手动的去创建实属浪费时间，而且会有大量的重复代码，此时我们就可以采用动态代理，动态代理可以在程序运行期间根据需要动态的创建代理类及其实例，来完成具体的功能，主要用的是`JAVA`的反射机制。


下面用静态代理的示例:     
```java
public interface ISourceable {  
    public void method();  
} 

public class Source implements ISourceable {  
    @Override  
    public void method() {  
        System.out.println("the original method!");  
    }  
} 
public class Proxy implements ISourceable {  
    private Source source;  
    public Proxy(){  
        super();  
        this.source = new Source();  
    }  
    @Override  
    public void method() {  
        before();  
        source.method();  
        atfer();  
    }  
    private void atfer() {  
        System.out.println("after proxy!");  
    }  
    private void before() {  
        System.out.println("before proxy!");  
    }  
}  

public class ProxyTest {  
    public static void main(String[] args) {  
        Sourceable source = new Proxy();  
        source.method();  
    }  
}  

输出：    
before proxy!
the original method!
after proxy!
```

代理模式可以有效的将具体的实现与调用方进行解耦，通过面向接口进行编码完全将具体的实现隐藏在内部。
代理模式的应用场景，如果已有的方法在使用的时候需要对原有的方法进行改进，此时有两种办法：    

- 修改原有的方法来适应。这样违反了“对扩展开放，对修改关闭”的原则。
- 就是采用一个代理类调用原有的方法，且对产生的结果进行控制。这种方法就是代理模式。

使用代理模式，可以将功能划分的更加清晰，有助于后期维护！

动态代理的优缺点:    
- 优点:代理使客户端不需要知道实现类是什么，怎么做的，而客户端只需知道代理即可（解耦合）。 
- 缺点:      
    - 代理类和委托类实现了相同的接口，代理类通过委托类实现了相同的方法。这样就出现了大量的代码重复。如果接口增加一个方法，除了所有实现类需要实现这个方法外，所有代理类也需要实现此方法。增加了代码维护的复杂度。
    - 代理对象只服务于一种类型的对象，如果要服务多类型的对象。势必要为每一种对象都进行代理，静态代理在程序规模稍大时就无法胜任了
    
即静态代理类只能为特定的接口`(Service)`服务。如想要为多个接口服务则需要建立很多个代理类。


动态代理的思维模式与之前的一般模式是一样的，也是面向接口进行编码，创建代理类将具体类隐藏解耦，不同之处在于代理类的创建时机不同，动态代理需要在运行时因需实时创建。

动态代理示例:    

```java
//动态代理类只能代理接口（不支持抽象类），代理类都需要实现InvocationHandler类，实现invoke方法。该invoke方法就是调用被代理接口的所有方法时需要调用的，该invoke方法返回的值是被代理接口的一个实现类  
public class DynamicProxy implements InvocationHandler {
　　private Object object;//用于接收具体实现类的实例对象
　　//使用带参数的构造器来传递具体实现类的对象
　　public DynamicProxy(Object obj){
　　　　this.object = obj;
　　}
　　@Override
　　public Object invoke(Object proxy, Method method, Object[] args)throws Throwable {
　　　　System.out.println("前置内容");
　　　　method.invoke(object, args);
　　　　System.out.println("后置内容");
　　　　return null;
　　}
}

测试类:   

public static void main(String[] args) {
    ISourceable source = new Source();
    InvocationHandler h = new DynamicProxy(source);
    ISourceable proxy = (ISourceable) Proxy.newProxyInstance(ISourceable.class.getClassLoader(), new Class[]{ISourceable.class}, h);
    proxy.method();
}
```


动态代理与静态代理相比较，最大的好处是接口中声明的所有方法都被转移到调用处理器一个集中的方法中处理`(InvocationHandler.invoke)`。这样，在接口方法数量比较多的时候，我们可以进行灵活处理，而不需要像静态代理那样每一个方法进行中转。而且动态代理的应用使我们的类职责更加单一，复用性更强

代理对象就是把被代理对象包装一层，在其内部做一些额外的工作，比如用户需要上facebook,而普通网络无法直接访问，网络代理帮助用户先翻墙，然后再访问facebook。这就是代理的作用了。

纵观静态代理与动态代理，它们都能实现相同的功能，而我们看从静态代理到动态代理的这个过程，我们会发现其实动态代理只是对类做了进一步抽象和封装，使其复用性和易用性得到进一步提升而这不仅仅符合了面向对象的设计理念，其中还有AOP的身影，这也提供给我们对类抽象的一种参考。关于动态代理与AOP的关系，个人觉得AOP是一种思想，而动态代理是一种AOP思想的实现！

外观模式`(Facade)`
---


外观模式是为了解决类与类之家的依赖关系的，像`spring`一样，可以将类和类之间的关系配置到配置文件中，而外观模式就是将他们的关系放在一个`Facade`类中，降低了类类之间的耦合度，该模式中没有涉及到接口。     

下面以计算机启动过程为例:   
```java
public class CPU {  
    public void startup(){  
        System.out.println("cpu startup!");  
    }  
      
    public void shutdown(){  
        System.out.println("cpu shutdown!");  
    }  
} 

public class Memory {  
    public void startup(){  
        System.out.println("memory startup!");  
    }  
      
    public void shutdown(){  
        System.out.println("memory shutdown!");  
    }  
} 

public class Disk {  
    public void startup(){  
        System.out.println("disk startup!");  
    }  
      
    public void shutdown(){  
        System.out.println("disk shutdown!");  
    }  
}  

public class Computer {  
    private CPU cpu;  
    private Memory memory;  
    private Disk disk;  
      
    public Computer(){  
        cpu = new CPU();  
        memory = new Memory();  
        disk = new Disk();  
    }  
      
    public void startup(){  
        System.out.println("start the computer!");  
        cpu.startup();  
        memory.startup();  
        disk.startup();  
        System.out.println("start computer finished!");  
    }  
      
    public void shutdown(){  
        System.out.println("begin to close the computer!");  
        cpu.shutdown();  
        memory.shutdown();  
        disk.shutdown();  
        System.out.println("computer closed!");  
    }  
}  

public class User {  
    public static void main(String[] args) {  
        Computer computer = new Computer();  
        computer.startup();  
        computer.shutdown();  
    }  
}  

输出：

start the computer!
cpu startup!
memory startup!
disk startup!
start computer finished!
begin to close the computer!
cpu shutdown!
memory shutdown!
disk shutdown!
computer closed!
```

如果我们没有`Computer`类，那么`CPU`、`Memory`、`Disk`他们之间将会相互持有实例，产生关系，这样会造成严重的依赖，修改一个类，可能会带来其他类的修改，这不是我们想要看到的，有了`Computer`类，他们之间的关系被放在了`Computer`类里，这样就起到了解耦的作用，这就是外观模式！


桥接模式`(Bridge)`
---


桥接模式就是把事物和其具体实现分开，使他们可以各自独立的变化。       

桥接的用意是：将抽象化与实现化解耦，使得二者可以独立变化，像我们常用的`JDBC`桥`DriverManager`一样，`JDBC`进行连接数据库的时候，在各个数据库之间进行切换，基本不需要动太多的代码，甚至丝毫不用动，原因就是`JDBC`提供统一接口，每个数据库提供各自的实现，用一个叫做数据库驱动的程序来桥接就行了。        

```java
public interface ISourceable {  
    public void method();  
}

public class SourceSub1 implements ISourceable {  
    @Override  
    public void method() {  
        System.out.println("this is the first sub!");  
    }  
} 
public class SourceSub2 implements ISourceable {  
    @Override  
    public void method() {  
        System.out.println("this is the second sub!");  
    }  
}  
```

定义一个桥，持有`ISourceable`的实例:   
```java
public abstract class Bridge {  
    private ISourceable source;  
  
    public void method(){  
        source.method();  
    }  
      
    public ISourceable getSource() {  
        return source;  
    }  
  
    public void setSource(ISourceable source) {  
        this.source = source;  
    }  
}  
public class MyBridge extends Bridge {  
    public void method(){  
    	if (getSource() == null) {
    		return;
    	}
        getSource().method();  
    }  
}  

public class BridgeTest {  
    public static void main(String[] args) {  
        Bridge bridge = new MyBridge();  
        /*调用第一个对象*/  
        Sourceable source1 = new SourceSub1();  
        bridge.setSource(source1);  
        bridge.method();  
          
        /*调用第二个对象*/  
        Sourceable source2 = new SourceSub2();  
        bridge.setSource(source2);  
        bridge.method();  
    }  
}  

输出:    

this is the first sub!
this is the second sub!
```

这样，就通过对`Bridge`类的调用，实现了对接口`ISourceable`的实现类`SourceSub1`和`SourceSub2`的调用。


组合模式`(Composite)`
---

组合模式有时又叫部分-整体模式在处理类似树形结构的问题时比较方便。   

```java
public class TreeNode {
    private String name;
    private TreeNode parent;
    private Vector<TreeNode> children = new Vector<TreeNode>();

    public TreeNode(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public TreeNode getParent() {
        return parent;
    }

    public void setParent(TreeNode parent) {
        this.parent = parent;
    }

    //添加子节点
    public void add(TreeNode node) {
        children.add(node);
    }

    //删除子节点
    public void remove(TreeNode node) {
        children.remove(node);
    }

    //获取子节点
    public Enumeration<TreeNode> getChildren() {
        return children.elements();
    }
}

public class Tree {
    TreeNode root;

    public Tree(String name) {
        root = new TreeNode(name);
    }
}

测试代码: 
public static void main(String[] args) {
    Tree tree = new Tree("A");
    TreeNode nodeB = new TreeNode("B");
    TreeNode nodeC = new TreeNode("C");

    nodeB.add(nodeC);
    tree.root.add(nodeB);
    System.out.println("build the tree finished!");
}
```
使用场景：将多个对象组合在一起进行操作，常用于表示树形结构中，例如二叉树，数等。

享元模式`(Flyweight)`
---

享元模式的主要目的是实现对象的共享，即共享池，当系统中对象多的时候可以减少内存的开销，通常与工厂模式一起使用。

![image](https://raw.githubusercontent.com/CharonChui/Pictures/master/flyweight_1.jpg?raw=true)     

`FlyWeightFactory`负责创建和管理享元单元，当一个客户端请求时，工厂需要检查当前对象池中是否有符合条件的对象，如果有，就返回已经存在的对象，如果没有，则创建一个新对象，`FlyWeight`是超类。一提到共享池，我们很容易联想到`Java`里面的`JDBC`连接池，想想每个连接的特点，我们不难总结出：适用于作共享的一些个对象，他们有一些共有的属性，就拿数据库连接池来说，`url`、`driverClassName`、`username`、`password`及`dbname`，这些属性对于每个连接来说都是一样的，所以就适合用享元模式来处理，建一个工厂类，将上述类似属性作为内部数据，其它的作为外部数据，在方法调用时，当做参数传进来，这样就节省了空间，减少了实例的数量。

下面用数据库连接池的例子:   

![image](https://raw.githubusercontent.com/CharonChui/Pictures/master/flyweight_2.jpg?raw=true)     

```java
public class ConnectionPool {
    private Vector<Connection> pool;
    /*公有属性*/
    private String url = "jdbc:mysql://localhost:3306/test";
    private String username = "root";
    private String password = "root";
    private String driverClassName = "com.mysql.jdbc.Driver";

    private int poolSize = 100;
    Connection conn;

    /*构造方法，做一些初始化工作*/
    private ConnectionPool() {
        pool = new Vector<>(poolSize);
        for (int i = 0; i < poolSize; i++) {
            try {
                Class.forName(driverClassName);
                conn = DriverManager.getConnection(url, username, password);
                pool.add(conn);
            } catch (ClassNotFoundException e) {
                e.printStackTrace();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }

    /* 返回连接到连接池 */
    public synchronized void release() {
        pool.add(conn);
    }

    /* 返回连接池中的一个数据库连接 */
    public synchronized Connection getConnection() {
        if (pool.size() > 0) {
            Connection conn = pool.get(0);
            pool.remove(conn);
            return conn;
        } else {
            return null;
        }
    }
}
```

通过连接池的管理，实现了数据库连接的共享，不需要每一次都重新创建连接，节省了数据库重新创建的开销，提升了系统的性能！


策略模式`(strategy)`
---

策略模式定义了一系列算法，并将每个算法封装起来，使他们可以相互替换，且算法的变化不会影响到使用算法的客户。需要设计一个接口，为一系列实现类提供统一的方法，多个实现类实现该接口，设计一个抽象类（可有可无，属于辅助类），提供辅助函数，关系图如下：


![image](https://raw.githubusercontent.com/CharonChui/Pictures/master/strategy.jpg?raw=true)     

图中`ICalculator`提供了同样的方法，
`AbstractCalculator`是辅助类，提供辅助方法，接下来，依次实现下每个类:    

```java
public interface ICalculator {  
    public int calculate(String exp);  
} 
public abstract class AbstractCalculator {  
      
    public int[] split(String exp,String opt){  
        String array[] = exp.split(opt);  
        int arrayInt[] = new int[2];  
        arrayInt[0] = Integer.parseInt(array[0]);  
        arrayInt[1] = Integer.parseInt(array[1]);  
        return arrayInt;  
    }  
}  

具体的实现类:   
public class Plus extends AbstractCalculator implements ICalculator {  
  
    @Override  
    public int calculate(String exp) {  
        int arrayInt[] = split(exp,"\\+");  
        return arrayInt[0]+arrayInt[1];  
    }  
}  
public class Minus extends AbstractCalculator implements ICalculator {  
  
    @Override  
    public int calculate(String exp) {  
        int arrayInt[] = split(exp,"-");  
        return arrayInt[0]-arrayInt[1];  
    }  
}  
public class Multiply extends AbstractCalculator implements ICalculator {  
  
    @Override  
    public int calculate(String exp) {  
        int arrayInt[] = split(exp,"\\*");  
        return arrayInt[0]*arrayInt[1];  
    }  
}  

测试类:  
public class StrategyTest {  
  
    public static void main(String[] args) {  
        String exp = "2+8";  
        ICalculator cal = new Plus();  
        int result = cal.calculate(exp);  
        System.out.println(result);  
    }  
} 
输出: 
10
```
策略模式的决定权在用户，系统本身提供不同算法的实现，新增或者删除算法，对各种算法做封装。因此，策略模式多用在算法决策系统中，外部用户只需要决定用哪个算法即可

模板方法模式`(Template Method)`
---

一个抽象类中，有一个主方法，再定义1...n个方法，可以是抽象的，也可以是实际的方法，定义一个类，继承该抽象类，重写抽象方法，通过调用抽象类，实现对子类的调用，先看个关系图:   

![image](https://raw.githubusercontent.com/CharonChui/Pictures/master/template.jpg?raw=true)   

就是在`AbstractCalculator`类中定义一个主方法`calculate()`，`calculate()`调用`spilt()`等，`Plus`和`Minus`分别继承`AbstractCalculator`类，通过对`AbstractCalculator`的调用实现对子类的调用，看下面的例子:   

```java
public abstract class AbstractCalculator {  
    /*主方法，实现对本类其它方法的调用*/  
    public final int calculate(String exp,String opt){  
        int array[] = split(exp,opt);  
        return calculate(array[0],array[1]);  
    }  
      
    /*被子类重写的方法*/  
    abstract public int calculate(int num1,int num2);  
      
    public int[] split(String exp,String opt){  
        String array[] = exp.split(opt);  
        int arrayInt[] = new int[2];  
        arrayInt[0] = Integer.parseInt(array[0]);  
        arrayInt[1] = Integer.parseInt(array[1]);  
        return arrayInt;  
    }  
}

public class Plus extends AbstractCalculator {  
  
    @Override  
    public int calculate(int num1,int num2) {  
        return num1 + num2;  
    }  
}  
```

测试类:    

```java
public static void main(String[] args) {  
    String exp = "8+8";  
    AbstractCalculator cal = new Plus();  
    int result = cal.calculate(exp, "\\+");  
    System.out.println(result);  
}  
```


观察者模式`(Observer)`
---

观察者模式很好理解，类似于邮件订阅和`RSS`订阅，当我们浏览一些博客或`wiki`时，经常会看到`RSS`图标，就这的意思是，当你订阅了该文章，如果后续有更新，会及时通知你。简单的说就是当一个对象变化时，其它依赖该对象的对象都会收到通知，并且随着变化！对象之间是一种一对多的关系。

在`Android`中我们常用的`Button.setOnClickListener()`其实就是用的观察者模式。大名鼎鼎的`RxJava`也是基于这种模式。  

观察者:   
```java
public interface Observer {  
    public void update();  
}  

public class Observer1 implements Observer {  
    @Override  
    public void update() {  
        System.out.println("observer1 has received!");  
    }  
} 
public class Observer2 implements Observer {  
    @Override  
    public void update() {  
        System.out.println("observer2 has received!");  
    }  
  
} 
```
被观察者:     
```java
public interface Subject {     
    /*增加观察者*/  
    public void add(Observer observer);  
      
    /*删除观察者*/  
    public void del(Observer observer);  
      
    /*通知所有的观察者*/  
    public void notifyObservers();  
      
    /*自身的操作*/  
    public void operation();  
}  

public abstract class AbstractSubject implements Subject {    
    private Vector<Observer> vector = new Vector<>();  
    @Override  
    public void add(Observer observer) {  
        vector.add(observer);  
    }  
  
    @Override  
    public void del(Observer observer) {  
        vector.remove(observer);  
    }  
  
    @Override  
    public void notifyObservers() {  
        Enumeration<Observer> enumo = vector.elements();  
        while(enumo.hasMoreElements()){  
            enumo.nextElement().update();  
        }  
    }  
}  

public class MySubject extends AbstractSubject { 
    @Override  
    public void operation() {  
        System.out.println("update self!");  
        // 一旦发生了观察者所需要的动作，就需要去通知观察者们
        notifyObservers();  
    }  
  
}  
```

测试类:   

```java
public static void main(String[] args) {  
    Subject sub = new MySubject();  
    sub.add(new Observer1());  
    sub.add(new Observer2());  
      
    sub.operation();  
}  
```

输出:  

```java
update self!
observer1 has received!
observer2 has received!
```


迭代器模式`(Iterator)`
---

迭代器模式就是顺序访问聚集中的对象，一般来说，集合中非常常见，如果对集合类比较熟悉的话，理解本模式会十分轻松。这句话包含两层意思：一是需要遍历的对象，即聚集对象，二是迭代器对象，用于对聚集对象进行遍历访问。

`MyCollection`中定义了集合的一些操作，`MyIterator`中定义了一系列迭代操作，且持有`Collection`实例，我们来看看实现代码:   

```java
public interface Collection {  
    public Iterator iterator();  
      
    /*取得集合元素*/  
    public Object get(int i);  
      
    /*取得集合大小*/  
    public int size();  
}

public interface Iterator {  
    //前移  
    public Object previous();  
      
    //后移  
    public Object next();  
    public boolean hasNext();  
      
    //取得第一个元素  
    public Object first();  
}  
```

具体实现类:   
```java
public class MyCollection implements Collection {  
    public String string[] = {"A","B","C","D","E"};  
    @Override  
    public Iterator iterator() {  
        return new MyIterator(this);  
    }  
  
    @Override  
    public Object get(int i) {  
        return string[i];  
    }  
  
    @Override  
    public int size() {  
        return string.length;  
    }  
}  
public class MyIterator implements Iterator {  
    private Collection collection;  
    private int pos = -1;  
      
    public MyIterator(Collection collection){  
        this.collection = collection;  
    }  
      
    @Override  
    public Object previous() {  
        if(pos > 0){  
            pos--;  
        }  
        return collection.get(pos);  
    }  
  
    @Override  
    public Object next() {  
        if(pos<collection.size()-1){  
            pos++;  
        }  
        return collection.get(pos);  
    }  
  
    @Override  
    public boolean hasNext() {  
        if(pos<collection.size()-1){  
            return true;  
        }else{  
            return false;  
        }  
    }  
  
    @Override  
    public Object first() {  
        pos = 0;  
        return collection.get(pos);  
    }  
}  
```

测试类:   
```java
public static void main(String[] args) {  
    Collection collection = new MyCollection();  
    Iterator it = collection.iterator();  
      
    while(it.hasNext()){  
        System.out.println(it.next());  
    }  
} 
```

输出:  
```
A B C D E
```

责任链模式`(Chain of Responsibility)`
---

有多个对象，每个对象持有对下一个对象的引用，这样就会形成一条链，请求在这条链上传递，直到某一对象决定处理该请求。但是发出者并不清楚到底最终那个对象会处理该请求，所以，责任链模式可以实现，在隐瞒客户端的情况下，对系统进行动态的调整。先看看关系图：

![image](https://raw.githubusercontent.com/CharonChui/Pictures/master/zerenlian.jpg?raw=true)  

`Abstracthandler`类提供了`get`和`set`方法，方便`MyHandler`类设置和修改引用对象，`MyHandler`类是核心，实例化后生成一系列相互持有的对象，构成一条链。

```java
public interface IHandler {  
    public void operator();  
}  

public abstract class AbstractHandler {     
    private IHandler handler;  
  
    public IHandler getHandler() {  
        return handler;  
    }  
  
    public void setHandler(IHandler handler) {  
        this.handler = handler;  
    }  
}  

public class MyHandler extends AbstractHandler implements IHandler {  
    private String name;  
  
    public MyHandler(String name) {  
        this.name = name;  
    }  
  
    @Override  
    public void operator() {  
        System.out.println(name+"deal!");  
        if(getHandler()!=null){  
            getHandler().operator();  
        }  
    }  
}  
```

测试类:    
```java
 public static void main(String[] args) {  
    MyHandler h1 = new MyHandler("h1");  
    MyHandler h2 = new MyHandler("h2");  
    MyHandler h3 = new MyHandler("h3");  

    h1.setHandler(h2);  
    h2.setHandler(h3);  

    h1.operator();  
} 
```

输出:   
```
h1deal!
h2deal!
h3deal!
```
链接上的请求可以是一条链，可以是一个树，还可以是一个环，模式本身不约束这个，需要我们自己去实现，同时，在一个时刻，命令只允许由一个对象传给另一个对象，而不允许传给多个对象。



命令模式`(Command)`
---


命令模式很好理解，举个例子，司令员下令让士兵去干件事情，从整个事情的角度来考虑，司令员的作用是，发出口令，口令经过传递，传到了士兵耳朵里，士兵去执行。这个过程好在，三者相互解耦，任何一方都不用去依赖其他人，只需要做好自己的事儿就行，司令员要的是结果，不会去关注到底士兵是怎么实现的。我们看看关系图：

![image](https://raw.githubusercontent.com/CharonChui/Pictures/master/command.jpg?raw=true)  

`Invoker`是调用者（司令员），`Receiver`是被调用者（士兵），`MyCommand`是命令，实现了`Command`接口，持有接收对象，看实现代码:    

```java
public interface Command {  
    public void exe();  
}  

public class MyCommand implements Command {  
    private Receiver receiver;  
      
    public MyCommand(Receiver receiver) {  
        this.receiver = receiver;  
    }  
  
    @Override  
    public void exe() {  
        receiver.action();  
    }  
} 
public class Receiver {  
    public void action(){  
        System.out.println("command received!");  
    }  
}

public class Invoker {  
    private Command command;  
      
    public Invoker(Command command) {  
        this.command = command;  
    }  
  
    public void action(){  
        command.exe();  
    }  
}  

public static void main(String[] args) {  
    Receiver receiver = new Receiver();  
    Command cmd = new MyCommand(receiver);  
    Invoker invoker = new Invoker(cmd);  
    invoker.action();  
    // 输出:command received!
}  
```

命令模式的目的就是达到命令的发出者和执行者之间解耦，实现请求和执行分开，熟悉`Struts`的同学应该知道，`Struts`其实就是一种将请求和呈现分离的技术，其中必然涉及命令模式的思想！


备忘录模式`(Memento)`
---


主要目的是保存一个对象的某个状态，以便在适当的时候恢复对象，个人觉得叫备份模式更形象些，通俗的讲下：假设有原始类A，A中有各种属性，A可以决定需要备份的属性，备忘录类B是用来存储A的一些内部状态，类C呢，就是一个用来存储备忘录的，且只能存储，不能修改等操作。做个图来分析一下：


![image](https://raw.githubusercontent.com/CharonChui/Pictures/master/memento.jpg?raw=true)  

`Original`类是原始类，里面有需要保存的属性`value`及创建一个备忘录类，用来保存`value`值。`Memento`类是备忘录类，`Storage`类是存储备忘录的类，持有`Memento`类的实例，该模式很好理解。直接看源码：

```java
public class Original {  
    private String value;  
      
    public String getValue() {  
        return value;  
    }  
  
    public void setValue(String value) {  
        this.value = value;  
    }  
  
    public Original(String value) {  
        this.value = value;  
    }  
  
    public Memento createMemento(){  
        return new Memento(value);  
    }  
      
    public void restoreMemento(Memento memento){  
        this.value = memento.getValue();  
    }  
}  

public class Memento {  
    private String value;  
  
    public Memento(String value) {  
        this.value = value;  
    }  
  
    public String getValue() {  
        return value;  
    }  
  
    public void setValue(String value) {  
        this.value = value;  
    }  
} 

public class Storage {  
    private Memento memento;  
      
    public Storage(Memento memento) {  
        this.memento = memento;  
    }  
  
    public Memento getMemento() {  
        return memento;  
    }  
  
    public void setMemento(Memento memento) {  
        this.memento = memento;  
    }  
}  

测试类:    
public static void main(String[] args) {  
    // 创建原始类  
    Original origi = new Original("egg");  

    // 创建备忘录  
    Storage storage = new Storage(origi.createMemento());  

    // 修改原始类的状态  
    System.out.println("初始化状态为：" + origi.getValue());  
    origi.setValue("niu");  
    System.out.println("修改后的状态为：" + origi.getValue());  

    // 回复原始类的状态  
    origi.restoreMemento(storage.getMemento());  
    System.out.println("恢复后的状态为：" + origi.getValue());  
} 

输出：

初始化状态为：egg
修改后的状态为：niu
恢复后的状态为：egg 
```
新建原始类时，`value`被初始化为`egg`，后经过修改，将`value`的值置为`niu`，最后倒数第二行进行恢复状态，结果成功恢复了。其实我觉得这个模式叫“备份-恢复”模式最形象。


状态模式`(State)`
---


核心思想就是:当对象的状态改变时，同时改变其行为，很好理解！就拿QQ来说，有几种状态，在线、隐身、忙碌等，每个状态对应不同的操作，而且你的好友也能看到你的状态，所以，状态模式就两点:       

- 可以通过改变状态来获得不同的行为
- 你的好友能同时看到你的变化


![image](https://raw.githubusercontent.com/CharonChui/Pictures/master/state.jpg?raw=true)  



`State`类是个状态类，`Context`类可以实现切换，我们来看看代码:   

```java
public class State {  
    private String value;  
      
    public String getValue() {  
        return value;  
    }  
  
    public void setValue(String value) {  
        this.value = value;  
    }  
  
    public void method1(){  
        System.out.println("execute the first opt!");  
    }  
      
    public void method2(){  
        System.out.println("execute the second opt!");  
    }  
}  

public class Context {  
    private State state;  
  
    public Context(State state) {  
        this.state = state;  
    }  
  
    public State getState() {  
        return state;  
    }  
  
    public void setState(State state) {  
        this.state = state;  
    }  
  
    public void method() {  
        if (state.getValue().equals("state1")) {  
            state.method1();  
        } else if (state.getValue().equals("state2")) {  
            state.method2();  
        }  
    }  
}  
```

测试类:    

```java
public static void main(String[] args) {      
    State state = new State();  
    Context context = new Context(state);  
      
    //设置第一种状态  
    state.setValue("state1");  
    context.method();  
      
    //设置第二种状态  
    state.setValue("state2");  
    context.method();  
} 

输出:   
execute the first opt!
execute the second opt!
```

根据这个特性，状态模式在日常开发中用的挺多的，尤其是做网站的时候，我们有时希望根据对象的某一属性，区别开他们的一些功能，比如说简单的权限控制等。

访问者模式`(Visitor)`
---


访问者模式把数据结构和作用于结构上的操作解耦合，使得操作集合可相对自由地演化。访问者模式适用于数据结构相对稳定算法又易变化的系统。因为访问者模式使得算法操作增加变得容易。若系统数据结构对象易于变化，经常有新的数据对象增加进来，则不适合使用访问者模式。访问者模式的优点是增加操作很容易，因为增加操作意味着增加新的访问者。访问者模式将有关行为集中到一个访问者对象中，其改变不影响系统数据结构。其缺点就是增加新的数据结构很困难。

简单来说，访问者模式就是一种分离对象数据结构与行为的方法，通过这种分离，可达到为一个被访问者动态添加新的操作而无需做其它的修改的效果。

示例:银行柜台提供的服务和来办业务的人。把银行的服务和业务的办理解耦了。
缺点：如果银行要修改底层业务接口，所有继承接口的类都需要作出修改。不过java8的新特性接口默认方法可以解决这个问题，或者java8之前可以通过接口的适配器模式来解决这个问题。   

```java
	// 银行柜台服务，以后银行要新增业务，只需要新增一个类实现这个接口就可以了。
    public interface Service {
        void accept(Visitor visitor);
    }

    // 来办业务的人，里面可以加上权限控制等等
    static class Visitor {
        public void process(Service service) {
            // 基本业务
            System.out.println("基本业务");
        }

        public void process(Saving service) {
            // 存款
            System.out.println("存款");
        }

        public void process(Draw service) {
            // 提款
            System.out.println("提款");
        }

        public void process(Fund service) {
            System.out.println("基金");
            // 基金
        }
    }

    static class Saving implements Service {
        public void accept(Visitor visitor) {
            visitor.process(this);
        }
    }

    static class Draw implements Service {
        public void accept(Visitor visitor) {
            visitor.process(this);
        }
    }

    static class Fund implements Service {
        public void accept(Visitor visitor) {
            visitor.process(this);
        }
    }

    public static void main(String[] args) {
        Service saving = new Saving();
        Service fund = new Fund();
        Service draw = new Draw();
        Visitor visitor = new Visitor();
        Visitor guweiwei = new Visitor();
        fund.accept(guweiwei);
        saving.accept(visitor);
        fund.accept(visitor);
        draw.accept(visitor);
        // 输出：
        // 基金
        // 存款
        // 基金
        // 提款
    }
}
```

该模式适用场景：如果我们想为一个现有的类增加新功能，不得不考虑几个事情:      

- 新功能会不会与现有功能出现兼容性问题？
- 以后会不会再需要添加?
- 如果类不允许修改代码怎么办？

面对这些问题，最好的解决方法就是使用访问者模式，访问者模式适用于数据结构相对稳定的系统，把数据结构和算法解耦，

中介者模式`(Mediator)`
---


中介者模式也是用来降低类类之间的耦合的，因为如果类类之间有依赖关系的话，不利于功能的拓展和维护，因为只要修改一个对象，其它关联的对象都得进行修改。
如果使用中介者模式，只需关心和`Mediator`类的关系，具体类类之间的关系及调度交给`Mediator`就行，这有点像`spring`容器的作用。




![image](https://raw.githubusercontent.com/CharonChui/Pictures/master/mediator.jpg?raw=true)  

`User`类统一接口，`User1`和`User2`分别是不同的对象，二者之间有关联，如果不采用中介者模式，则需要二者相互持有引用，这样二者的耦合度很高，为了解耦，
引入了`Mediator`类，提供统一接口，`MyMediator`为其实现类，里面持有`User1`和`User2`的实例，用来实现对`User1`和`User2`的控制。

这样`User1`和`User2`两个对象相互独立，他们只需要保持好和`Mediator`之间的关系就行，剩下的全由`MyMediator`类来维护。   

```java
public interface IMediator {  
    public void createMediator();  
    public void workAll();  
}  


public class MyMediator implements IMediator {  
    private User user1;  
    private User user2;  
      
    public User getUser1() {  
        return user1;  
    }  
  
    public User getUser2() {  
        return user2;  
    }  
  
    @Override  
    public void createMediator() {  
        user1 = new User1(this);  
        user2 = new User2(this);  
    }  
  
    @Override  
    public void workAll() {  
        user1.work();  
        user2.work();  
    }  
}  


public abstract class User {        
    private Mediator mediator;  
      
    public Mediator getMediator(){  
        return mediator;  
    }  
      
    public User(Mediator mediator) {  
        this.mediator = mediator;  
    }  
  
    public abstract void work();  
}  

public class User1 extends User {  
    public User1(Mediator mediator){  
        super(mediator);  
    }  
      
    @Override  
    public void work() {  
        System.out.println("user1 exe!");  
    }  
}  

public class User2 extends User {  
    public User2(Mediator mediator){  
        super(mediator);  
    }  
      
    @Override  
    public void work() {  
        System.out.println("user2 exe!");  
    }  
}  
```

测试类:    
```java
public static void main(String[] args) {  
    Mediator mediator = new MyMediator();  
    mediator.createMediator();  
    mediator.workAll();  
    // 输出:   
    // user1 exe!
    // user2 exe!
}  
```


解释器模式`(Interpreter)`
---

解释器模式是我们暂时的最后一讲，一般主要应用在`OOP`开发中的编译器的开发中，所以适用面比较窄。


![image](https://raw.githubusercontent.com/CharonChui/Pictures/master/interpreter.jpg?raw=true)  


`Context`类是一个上下文环境类，`Plus`和`Minus`分别是用来计算的实现，代码如下:   

```java
public interface Expression {  
    public int interpret(Context context);  
}  

public class Plus implements Expression {  
    @Override  
    public int interpret(Context context) {  
        return context.getNum1()+context.getNum2();  
    }  
}  

public class Minus implements Expression {  
    @Override  
    public int interpret(Context context) {  
        return context.getNum1()-context.getNum2();  
    }  
}  

public class Context {  
    private int num1;  
    private int num2;  
      
    public Context(int num1, int num2) {  
        this.num1 = num1;  
        this.num2 = num2;  
    }  
      
    public int getNum1() {  
        return num1;  
    }  
    public void setNum1(int num1) {  
        this.num1 = num1;  
    }  
    public int getNum2() {  
        return num2;  
    }  
    public void setNum2(int num2) {  
        this.num2 = num2;  
    }  
}  
```

测试类:    
```java
public static void main(String[] args) {  
    // 计算9+2-8的值  
    int result = new Minus().interpret((new Context(new Plus()  
            .interpret(new Context(9, 2)), 8)));  
    System.out.println(result);  
    // 输出:3
}  
```
基本就这样，解释器模式用来做各种各样的解释器，如正则表达式等的解释器等等！

		
---
- 邮箱 ：charon.chui@gmail.com  
- Good Luck! 

	