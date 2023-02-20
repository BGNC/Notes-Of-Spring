# Notes-Of-Spring


### Nedir?

Spring Framework, Java tabanlı uygulamalar geliştirmek ve bağımlılık yönetimi için kullanılır.
Yaklaşık 20 modülü olduğu için Core Container, AOP, Data Access, Web gibi modüllerden oluşur.

Spring platformunda yer alan, [[Spring Boot]], Spring Data, Spring MVC, Spring Batch, Spring Security gibi projelerin temelinde Spring framework yer alır.

Spring Framework
- Core Container
	- spring-core
	- spring-beans
	- spring-context
	- spring-expression
- Web (MVC / Remoting)
	- Web
	- Servlet
	- Portlet
	- Struts
- Data Access / Integration
	- JDBC
	- ORM (JPA interface, Hibernate implementation)
	- OXM
	- JMS
	- Transactions
- AOP
- Aspects

- - -

#### IoC (Inversion of Control) Container nedir

Sınıflardan nesne oluşturmak, oluşan nesnelerin ihyitaç duyduğu nesneleri bağlamak ve yönetmek için kullanılan prensip ve desenlerin bir araya geldiği araçlardır.

IoC Container araçları genellikle şağıdaki prensip ve desenleri kullanır: 

IoC Container Framework
- IoC (Inversion of Control) Tasarım prensibi
	- Factory Pattern
	- Dependency Injection
		- Constructor Injection
		- Setter Injection
		- Interface Injection
	- Strategy Pattern
	- Service Locator Pattern
	- Template Method Pattern
- DIP (Dependency Inversion Prenciple) Tasarım Prensibi

#TODO bu patternleri not et
not: inversion = tersine çevirme #eng

Not: Tasarım prensipleri (DRY, SOLID, SoC, KISS, YAGNI) uyulması gereken kuralları belirtirken, tasarım desenleri bu kuralların uygulamalarıdır. 

Spring framework, IoC prensibini uygulamak için genellikle Dependency Injection tasarım desenini kullanır. 

#### IoC (Inversion of Control) Nedir?
Bir sınıf (A) içerisinde kullanılan sınıfların (B,C..) başka bir yöntemle (Constructor, Factory vb..) oluşturulması, dahil edilmesi ve kontrol edilmesine IoC denir. 

```java
public class A {
	private B b;
	
	public A(){
		b = new B(); // dependency
	}
}

public class B {
	public void print(){
		System.out.println("onur");
	}
}
```

Sınıf A içerisinde **new** keywordü ile başka bir sınıfı kullanması, A'nın B'ye bağımlı olmasına neden olur.

Bu bağımlılığın sınıftan (A'dan) alınarak başka bir sınıfa verilmesi, kontrolün tersine çevrilmesi, IoC olarak adlandırılır. 

Bu işlemin yapılması için Factory, DI, Strategy, Service Locator, Template method gibi design patterns kullanılır.

```java
public class ObjectFactory{
	public static B getB(){
		return new B();
	}
}

public class A {
	private B b;
	
	public A(){
		b = ObjectFactory.getB();
	}

	public void print(){
		b.print();
	}
}
```

İhtiyaca göre ObjectFactory düzenlenir, A classını ellemeye pek gerek olmaz.

- - -

#### Dependency Injection Nedir?

Bir sınıfın içinde kullanılacak sınıfların constructor veya method ile sınıfa atanmasıdır.

```java
public class A {
	private B b;

	public A(B b){ // constructor
		this.b = b;
	}

	public void setB(B b){ // method
		this.b = b;
	}
}
```

- - -

#### Dependency Inversion Prenciple Nedir?
Bir sınıfın, başka bir sınıfı doğrudan kullanması yerine abstract class veya interface üzerinden kullanılmasına denir.

Sınıfların birbirini doğrudan kullanması, sınıflar arasında tight coupled sıkı bağ olmasına neden olur.

Sınıfları doğrudan kullanmak yerine soyut sınıf veya arayüzler kullanmak değişikliğin daha kolay yönetilmesini sağlar. 

İhtiyaç duyulan sınıfların oluşturulması, yönetilmesi, Spring framework içinde yer alan **Core Container** kullanılarak yapılır.

Spring framework bu işlemleri yaparken design principles, design patterns, Java Reflection #TODO , Java Annotation gibi yapıları kullanır.
#TODO  todo reflection ve annotation yusuf sezer


Spring framework sınıfları **bean** olarak adlandırılır ve XML'de bean etiketi ile tanımlanır.

IoC Container, BeanFactory arayüzü ile sağlanır.
Oluşturulan nesneler Singleton yani her sınıf için sadece bir nesne oluşturulacaktır.
