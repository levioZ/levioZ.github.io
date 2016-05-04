---
layout: post
title:  "使用Spring的Validator接口进行校验"
date:   2016-05-03 15:09:00
categories: spring
tags: java spring Validator
author: eli
excerpt: 你可以使用Spring提供的validator接口进行对象的校验。Validator接口与Errors协同工作，在Spring做校验的时候，它会将所有的校验错误汇总到Errors对象中去。
---
* content
{:toc}

你可以使用Spring提供的validator接口进行对象的校验。Validator接口与Errors协同工作，在Spring做校验的时候，它会将所有的校验错误汇总到Errors对象中去。  

来看这个简单的数据对象：

```java
public class Person {

  private String name;
  private int age;

  // the usual getters and setters...
}
```  

实现org.springframework.validation.Validator接口中的两个方法，我们将为对Person类加上校验行为：  

* supports(Class)：表示这个Validator是否支持该Class的实例?
* validate(Object, org.springframework.validation.Errors)：对提供的对象进行校验，并将校验的错误注册到传入的Errors 对象中。  

实现一个Validator也比较简单，尤其是当你学会了Spring所提供的ValidationUtils以后。我们一起来看一下如何才能创建一个校验器。  

```java
public class PersonValidator implements Validator {

    /**
    * This Validator validates just Person instances
    */
    public boolean supports(Class clazz) {
        return Person.class.equals(clazz);
    }

    public void validate(Object obj, Errors e) {
        ValidationUtils.rejectIfEmpty(e, "name", "name.empty");
        Person p = (Person) obj;
        if (p.getAge() < 0) {
            e.rejectValue("age", "negativevalue");
        } else if (p.getAge() > 110) {
            e.rejectValue("age", "too.darn.old");
        }
    }
}
```   

如你所见，我们使用了ValidationUtils中的一个静态方法rejectIfEmpty(..)来对name属性进行校验，假若'name'属性是 null 或者空字符串的话，就拒绝验证通过 。请参照ValidationUtils相关的JavaDoc，查看一下除了例子中介绍过的之外其他的一些功能。
对复杂对象来说，实现Validator类来验证其内置的属性类当然也是可行的，但是为每个内置类的示例实现Validator可能是个更好的主意。关于这样的一个'rich'这样的例子是Customer类，它包含两个String属性(first name 和second name)，还有一个复杂的Address对象。Address对象可能独立于Customer对象，因此独立实现了一个AddressValidator。假若你希望你的CustomerValidator重用AddressValidator内部的逻辑，但是又不想通过拷贝粘贴来实现，你可以在你的CustomerValidator中依赖注入AddressValidator对象，或者创建一个。然后这样用：  

```java

public class CustomerValidator implements Validator {

   private final Validator addressValidator;

   public CustomerValidator(Validator addressValidator) {
      if (addressValidator == null) {
          throw new IllegalArgumentException("The supplied [Validator] is required and must not be null.");
      }
      if (!addressValidator.supports(Address.class)) {
          throw new IllegalArgumentException(
            "The supplied [Validator] must support the validation of [Address] instances.");
      }
      this.addressValidator = addressValidator;
   }

    /**
    * This Validator validates Customer instances, and any subclasses of Customer too
    */
   public boolean supports(Class clazz) {
      return Customer.class.isAssignableFrom(clazz);
   }

   public void validate(Object target, Errors errors) {
      ValidationUtils.rejectIfEmptyOrWhitespace(errors, "firstName", "field.required");
      ValidationUtils.rejectIfEmptyOrWhitespace(errors, "surname", "field.required");
      Customer customer = (Customer) target;
      try {
          errors.pushNestedPath("address");
          ValidationUtils.invokeValidator(this.addressValidator, customer.getAddress(), errors);
      } finally {
          errors.popNestedPath();
      }
   }
}  
```  

验证错误会被报告到传来的Errors对象中。在Spring Web MVC中，你可以使用<spring:bind/>标签来检查错误信息，当然你也可以自行处理错误。可以在它的Javadoc中找到它提供的方法的描述。
