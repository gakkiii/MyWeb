

#### 概述

有一些时候我们需要对某一个方法进行修改,希望它能在执行的时候能够有一些功能增强,但是又因为权限问题并不能直接修改方法的源代码,这时就有3种方法进行操作:

1. 继承:通过子类继承父类的方式重写父类的方法来完成功能的增强`继承可不能乱用!`
2. 装饰者设计模式`麻烦`
3. 动态代理`这里提供模板供以后参考`

```java
动态代理普通模板:
模板参与对象:
	有被增强需求的对象		a
	该对象所属类				Aa
	该对象要被增强的方法		m()
    代理对象				da
        
代码:
	final Aa a = ...;
		
	//这里要做一个强转
	Aa da = (Aa)Proxy.newProxyInstance(
        a.getClass().getClassLoader(),a.getClass().getInterfaces(),new InvocationHandler() 
        {			
            public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                if("m".equals(method.getName())) {		//判断,如果是要增强的方法就开始增强
                    //这里是方法增强/修改的代码
                    //调用原方法:	method.invoke(a, 参数列表);
                }
                //如果不是要增强的方法就调用原来的方法
                method.invoke(a,参数列表);
            }
		}
	);

//使用增强后的方法
da.m();


```



