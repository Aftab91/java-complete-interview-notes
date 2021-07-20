Annotations
==========

@Autowired
----------

Since version 2.5, Spring provides the @Autowired annotation to discover the beans automatically and inject collaborating beans (other associated dependent beans) into our bean.

By declaring all the beans in Spring Configuration file, Spring container can autowire relationships between collaborating beans. 

After enabling annotation based injection, now we can use @Autowired annotation. @Autowired can be used on following injection points.

1. Constructors
2. Methods
3. Fields and
4. Parameters

and dependencies can be injected using by type OR by name OR by @Qualifier.


In spring there are two types of autowiring. Those are
- **Autowiring by type** : @Autowired by type uses the class type to autowire the spring boot bean class. The bean is autowired based on the type of the variable.
- **Autowiring by name** : For Autowiring by name, the name of the variable is used for the dependency injection. The name of the authoring variable should be the same as the name of the class or the bean name configured in the @Component annotation.

For example,

```java
public interface Shape {
	public void draw();
}

@Component
public class Rectangle implements Shape {
	@Override
	public void draw() {
		System.out.println(">>>>>>>>>>>>>INVOKING THE RECTANGLE INSTANCE<<<<<<<<<<<<<<<<");
	}
}

@Component
public class Circle implements Shape{
	@Override
	public void draw() {
		System.out.println(">>>>>>>>>>>>>INVOKING THE CIRCLE INSTANCE<<<<<<<<<<<<<<<<");
	}
}

```
the shape interface is implemented by two classes Circle and Rectangle. So we can say both are instances of Shape or both shape. It made Rectangle and Circle as spring beans using the annotation @Component. Now let's see how to autowire these beans in another class.

```java
@Component
public class ShapeService {
	@Autowired
	private Shape rectangle;//by name
	
	@Autowired
	private Rectangle myRectangle;//by type

}
```

Here in ShapeService class, it is autowring the shape Rectangle in two ways.
1. Here in the first @Autowiring, the variable rectangle is autowired based on the name of the variable. Here when the spring checks the type of the variable, he can see it is Shape. But there are two shape implementations are there Rectangle and Circle. So spring doesn't get a proper solution for what component need to autowire. Then the spring check the name of the variable(rectangle) and find out any Shape component with the same name is available. Yes…The Rectangle component is available. So the spring will inject the property with rectangle component.
2. In the second @Autowiring, the type of property is Rectangle. So the spring directly injects the Rectangle component to the property myRectangle.


@Inject vs @Autowired
---------------------

| Key       | @Inject                         |@Autowired                       |
|-----------------|-----------------------------------|-----------------|
|  Basic     | It is part of Java CDI(Contexts and Dependency Injection)   |  It is part of Spring framework  |
|  Required   |  It has no required attribute    |  It has required attribute   |
|  Default Scope   |    Default scope of the autowired beans is Singleton    | Default scope of the inject beans is prototype  |
|  Ambiguity  |  In case of ambiguity in beans for injection then @Named qualifier should be added in your code.  |   In case of ambiguity in beans for injection then @Qualifer  qualifier should be added in your code. |
|  Advantage   | It is a part of Java CDI so it is not dependent on any DI framework. It makes your system loosely coupled. | It makes your application tightly coupled with Spring framework. In the future , if you want to move to another DI framework then you need reconfigure your application.  |














For more information:

1. [Spring – @Autowired](https://javabydeveloper.com/tutorial-on-spring-autowired/)
2. [Core Spring Framework Annotations](https://medium.com/javarevisited/core-spring-framework-annotations-300493ba85da)