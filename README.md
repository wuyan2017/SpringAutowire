# Spring Autowire example

The easiest way to autowire a bean is by using the @Autowire annotation, to avoid the xml configuration. It can be used to autowire a bean on the setter method, on a constructor or a field.

Using this as a starting point
https://examples.javacodegeeks.com/enterprise-java/spring/beans-spring/spring-autowire-example/

## Auto-Wiring using applicationContext.xml

**Color.java** will be the **bean** that we will use to **autowire** in all possible ways. It is a class that represents the color of an animal. It has two attributes, the **baseColor** and **textureColoe**.

* Auto-Wiring ‘no’ : It is the **default mode** that includes no autowiring. Bean references must be defined via a **ref element**.
````xml
    <bean id="cat" class="Cat">
        <property name="name" value="cat"/>
        <property name="color" ref="color"/>
    </bean>
````
* Auto-Wiring ‘byName’ : Autowiring by **property name**. Spring looks for a bean with the same name as the property that needs to be autowired. 
````xml
    <bean id="dog" class="Dog" autowire="byName">
        <property name="name" value="dog" />
    </bean>
````
  * In this case the class Dog has a private declaration of "Color".
````java
    private Color color;
````
* Auto-Wiring ‘byType’ : Allows a property to be autowired.
```xml
    <bean id="elephant" class="Elephant" autowire="byType">
        <property name="name" value="elephant" />
    </bean>
```
  * So the same line of code, in a different class, is used to do the auto-wiring?
````java
    private Color color;
````
* Auto-Wiring ‘constructor’ : Analogous to byType, but applies to constructor arguments. 
````xml
    <bean id="frog" class="Frog" autowire="constructor">
        <property name="name" value="frog" />
    </bean>
````
  * The ctor
  ````java
    public Frog(Color color){
        this.color= color;
    }
````
## Auto-Wiring with @Autowired annotation

All code below from the Tiger class.  Had to add default ctor to Tiger class.

* Setter method - example 1
````java
    @Autowired
    public void setColor(Color color) {
        this.color = color;
    }
````
* Constructor - example 2
````java
    @Autowired
    public Tiger(Color color) {
        this.color = color;
    }
````
* Field - example 3
````java
    @Autowired
    private Color color;
````
* Dependency checking (skipping this one for now)

* @Qualifier annotation - not working, colors not changing
````xml
    <bean id="differentColors" class="Color">
        <property name="baseColor" value="yellow" />
        <property name="textureColor" value="black" />
    </bean>
````
````java
    @Autowired
    @Qualifier("differentColors")
    private Color color;
````
