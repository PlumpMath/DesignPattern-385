# DesignPattern
该工程基于jdk 8，maven，junit 4，用单元测试讨论详细的设计模式

## 示例进度
- 单例示例全面讨论完毕 2016-12-13
- 工厂模式讨论完毕
	工厂方法没做示例，我将工厂方法模式看成是抽象工厂模式的特例，就省去示例了
	2016-12-14
- 门面模式讨论完毕  2016-12-15

## 代码包目录
### com.shineoxygen.designpattern.creational 
creational design pattern围绕对象创建的设计模式
- 单例模式
- 工厂模式(及抽象工厂模式)

### com.shineoxygen.designpattern.structural
structural design pattern，围绕对象间结构的设计模式
具体有：
- 组合模式
- 门面模式
- 装饰者模式
- 代理模式
- 适配器模式

### com.shineoxygen.designpattern.behavioral
behavioral design pattern，围绕对象行为的设计模式
- 模板方法模式
- 责任链模式
- 观察者模式
- 策略模式
- 命令模式
 
##  关键点
### 单例模式
单例实现必须包括如下条件：<br>
1. 静态的私有单例变量
2. 私有的构造器
3. 返回单例的静态方法

单例实现的比较如下：   <br>
- 饿汉式单例实现	<br>
	单例类初始化时，实例化单例，初始化耗时长的话，则性能不好
	不能处理异常，因为单例为类加载时变量就赋值了
	线程安全
- 静态块单例实现<br>
	单例类初始化时，实例化单例
	可处理异常（catch异常）
	线程安全
- 懒汉式单例实现
	使用时才实例化单例
	可处理异常
	线程不安全
- 线程安全单例实现
	使用时才实例化单例
	可处理异常
	线程安全
- 双重null检查的线程安全单例实现
	使用时才实例化单例
	可处理异常
	线程安全
	双重null检查，性能提升（单例一旦实例化后，有的线程不会像单个null检查那样被锁在外面，而是直接返回单例，提升性能）
- 静态内部类单例实现
	使用时才实例化单例，内部类都是使用时初始化
	可处理异常
	线程安全，变量为static final修改，一直唯一
	此种写法最推荐，简洁易理解
- 反射技术破坏单例唯一性
	反射技术可创建多个单例，从而破坏单例唯一性
- 枚举类单例实现
	枚举是全局唯一的，保证了单例的唯一性
	类初始化时，就实例化单例
	线程安全
	防止反射技术破坏
- 序列化中的单例实现
	分布式环境中，序列化一个单例，而每次反序列化都是生成一个新实例，不满足单例的唯一性
	解决：考虑到无论是实现Serializable接口，或是Externalizable接口
			  当从I/O流中读取对象时，readResolve()方法都会被调用到
			  只要添加返回单例的readResolve方法则能保证反序列化的唯一性
			  至于序列化的单例，可参考上述单例实现方式来做加上readResovle方法

	推荐使用静态内部类实现单例模式，大部分场景够用也简洁

### 工厂模式
- 简单工厂
	将对象的创建封装起来，通过传入类型来返回对应的对象
	从这个角度来说，任何对对象创建过程封装的方式我都理解为工厂模式
- 抽象工厂
	工厂中的工厂
	抽象工厂类下有若干具体工厂类，每个具体工厂类生成对应的对象（可以有多个生成方法，生成不同对象，如跑车工厂为具体工厂类，生成宝马跑车、卡迪拉克跑车、劳斯莱斯跑车，其他具体工厂类生成商务车，对应一个产品族）
- 工厂方法
	我理解为抽象工厂的一个特例，不过具体工厂类生产一个对象，即仅有一个产品，而不是一套产品族

### 门面模式
- 门面模式更像客户端应用的帮助类，未对客户端隐藏子系统接口，是否使用门面模式依赖于客户端代码
- 不管何种开发目的，都可使用门面模式，通常当接口数量变多，系统变得复杂时使用
- 子系统接口不感知门面类，也不应该有门面类的引用
- 门面模式应该应用于类似的接口，提供单个接口好过多个类似的接口，使客户端关注范围由原有的多个接口缩小到单个接口，提升效率
- 工厂模式搭配门面模式适用时，能提供更好的接口给客户端
