### JDK动态代理解析

#### JDK的动态代理是由JDK的 java.lang.reflect.*包所支持的，实现动态代理需要完成以下步骤:

- #### 编写服务类接口，编写接口实现类，这个实现类是真正的服务提供者

- #### 编写代理类，提供绑定和代理方法

#### JDK 代理的最大缺点就是需要提供接口，MyBatis中的 Mapper就是一个接口，采用的就是JDK 动态代理

#### 服务接口类

```java 
public interface HelloService{
  public void sayHello(String name);
}
```

#### 接口实现类

``` java 
public class HelloServiceImpl implements HelloService{

	public void sayHello(String name) {
		// TODO 自动生成的方法存根
		System.err.println("Hello "+name);
	}

}
```

#### 代理类，代理类必须实现InvocationHandler接口的代理方法，当对象被绑定后，执行方法时就会进入代理方法中

```java
import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;

public class HelloServiceProxy implements InvocationHandler {

	//真实的服务对象
	private Object target;
	
    //绑定委托对象并返回代理类
	public Object bind(Object target){
		this.target=target;
		return Proxy.newProxyInstance(target.getClass().getClassLoader(),
				target.getClass().getInterfaces(), this);
	}
	
  	/*
	*@param proxy   --代理对象
	*@param method  --被调用方法
	*@param args    --被调用方法的参数
  	*/
	public Object invoke(Object proxy, Method method, Object[] args)
			throws Throwable {
		System.out.println("###################JDK Invocation Proxy#################");
		Object result=null;
		System.err.println("before say hello!");
		result=method.invoke(target, args);
		System.err.println("I have said that!");
		return result;
	}
}
```

#### 在此类中，`target.getClass().getClassLoader()`是获得类构造器，`target.getClass().getInterfaces()`是获得代理对象所挂的接口，`this`是指当前的HelloServiceProxy类

#### 整个调用过程就是，服务提供类(helloServiceImpl)提供自身的对象做为参数绑定到代理类后，代理类返回一个代理对象，代理执行代理方法(invoke)，invoke 第一个参数便是代理对象proxy，第二个参数是真正调用的方法，以及第三个参数为调用方法的参数，invoke中调用method完成后返回result

#### 测试类如下

```java
public class HelloServiceMain {

	public static void main(String[] args){

		HelloServiceProxy HelloHandler=new HelloServiceProxy();
		HelloService proxy=(HelloService)HelloHandler.bind(new HelloServiceImpl());
		proxy.sayHello("TOM");
	}
}

```
#### 测试结果
```java
before say hello!
Hello TOM
I have said that!
```

