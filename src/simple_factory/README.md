2.简单工厂模式（Simple Factory）
=====

简介
----

### 意图
- 调用者与创建者解藕，调用者不需要知道创建细节

### 主要解决
- 调用者实例化对象时的耦合问题

### 何时使用
- 调用者在不同条件会创建不同的实例时

### 注意
- 如果使用简单工厂模式，就需要引进一个简单工厂类，会增加项目复杂度

实现
----

### 实例
- 你，是一个臭打游戏的，想要一个新的 CPU，你不想知道也没必要知道 CPU 是怎么制造的，直接买就得了
- 这时，有一个专门制造 CPU 的工厂，它可以制造很多品种的 CPU，比如 9400F、3700X 等
- 你直接跟工厂的经销商提出需求，他们根据你的需求（每个人需求不同）直接返回一个你需要的 CPU 即可


### 接口
```java
public interface CPU {

    void printInformation();

}
```

### 实现类
```java
public class I3_9100F implements CPU {
    public void printInformation() {
        System.out.println("我是 i3-9100f");
    }
}
```
```java
public class I5_9400F implements CPU {
    public void printInformation() {
        System.out.println("我是 i5-9400f");
    }
}
```
```java
public class I7_9700K implements CPU {
    public void printInformation() {
        System.out.println("我是 i7-9700k");
    }
}
```
```java
public class I9_9900K implements CPU{
    public void printInformation () {
        System.out.println("我是 i9-9900k");
    }
}
```
```java
public class R5_3600 implements CPU {
    public void printInformation() {
        System.out.println("我是 r5-3600");
    }
}
```
```java
public class R5_3700X implements CPU {
    public void printInformation() {
        System.out.println("我是 r5-3700x");
    }
}
```

### 简单工厂类
```java
public class SimpleFactory {

    public static CPU get9100F() {
        return new I3_9100F();
    }

    public static CPU get9400F() {
        return new I5_9400F();
    }

    public static CPU get9700K() {
        return new I7_9700K();
    }

    public static CPU get9900K() {
        return new I9_9900K();
    }

    public static CPU get3600() {
        return new R5_3600();
    }

    public static CPU get3700X() {
        return new R5_3700X();
    }

}
```

### 调用类
在以下实现中，调用者可以根据不同的条件从简单工厂类中获取不同的实例化对象
```java
public class Main {
    public static void main(String[] args) throws IOException {
        CPU cpu = null;

        String str = new BufferedReader(new InputStreamReader(System.in)).readLine();
        if (str.equalsIgnoreCase("9400f")) {
            cpu = SimpleFactory.get9400F();
        } else if (str.equalsIgnoreCase("3700x")) {
            cpu = SimpleFactory.get3700X();
        }

        if (null != cpu) {
            cpu.printInformation();
        } else {
            System.out.println("init error");
        }
    }
}
```