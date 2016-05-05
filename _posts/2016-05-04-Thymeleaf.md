---
layout: post
title:  "Thymeleaf扫盲"
date:   2016-05-04 16:49:00
categories: Thymeleaf
tags: Thymeleaf
excerpt: Thymeleaf是个XML/XHTML/HTML5模板引擎，可以用于Web与非Web应用。
---
* content
{:toc}

>Thymeleaf是个XML/XHTML/HTML5模板引擎，可以用于Web与非Web应用。
>
Thymeleaf的主要目标在于提供一种可被浏览器正确显示的、格式良好的模板创建方式，因此也可以用作静态建模。你可以使用它创建经过验证的XML与HTML模板。相对于编写逻辑或代码，开发者只需将标签属性添加到模板中即可。接下来，这些标签属性就会在DOM（文档对象模型）上执行预先制定好的逻辑。Thymeleaf的可扩展性也非常棒。你可以使用它定义自己的模板属性集合，这样就可以计算自定义表达式并使用自定义逻辑。这意味着Thymeleaf还可以作为模板引擎框架。
>
Thymeleaf的模板还可以用作工作原型，Thymeleaf会在运行期替换掉静态值。例如下面的html文件，当作为静态文件时，product name显示为Red Chair，当运行在容器中并提供product这个对象时，product name的值会自动替换为product.description对应的值。  


1、 bean值替换

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
    <head>
        <title>Thymeleaf tutorial: exercise 2</title>
        <link rel="stylesheet" href="../../../css/main-static.css" th:href="@{/css/main.css}" />
        <meta charset="utf-8" />
    </head>
    <body>
        <h1>Thymeleaf tutorial - Answer for exercise 1: bean values</h1>
        <h2>Product information</h2>
        <dl>
            <dt>Product name</dt>
            <dd th:text="${product.description}">Red Chair</dd>

            <dt>Product price</dt>
            <dd th:text="${product.price}">350</dd>

            <dt>Product available from</dt>
            <dd th:text="${product.availableFrom}">2014-12-01</dd>
        </dl>
    </body>
</html>
```   
2、 简单数据转换（数字，日期）  

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
    <head>
        <title>Thymeleaf tutorial: exercise 2</title>
        <link rel="stylesheet" href="../../../css/main-static.css" th:href="@{/css/main.css}" />
        <meta charset="utf-8" />
    </head>
    <body>
        <h1>Thymeleaf tutorial - Answer for exercise 2: bean values</h1>
        <h2>Product information</h2>
        <dl>
            <dt>Product name</dt>
            <dd th:text="${product.description}">red Chair</dd>

            <dt>Product price</dt>
            <dd th:text="${#numbers.formatDecimal(product.price, 1, 2)}">180</dd>

            <dt>Product available from</dt>
            <dd th:text="${#dates.format(product.availableFrom, 'yyyy-MM-dd')}">2014-12-01</dd>
        </dl>
    </body>
</html>
```  

3、 字符串拼接  

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
    <head>
        <title>Thymeleaf tutorial: exercise 3</title>
        <link rel="stylesheet" href="../../../css/main-static.css" th:href="@{/css/main.css}" />
        <meta charset="utf-8" />
    </head>
    <body>
        <h1>Thymeleaf tutorial - Answer for exercise 3: string concatenation</h1>
        <h2>Product information</h2>
        <dl>
            <dt>Product price</dt>
            <dd th:text="${'$'+product.price}">235</dd>
        </dl>
    </body>
</html>
```  

4、 国际化  

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
 <head>
		 <title th:text="#{tutorial.exercise4}">Thymeleaf tutorial: exercise 4</title>
		 <link rel="stylesheet" href="../../../css/main-static.css" th:href="@{/css/main.css}" />
		 <meta charset="utf-8" />
 </head>
 <body>
		 <h1 th:text="#{tutorial.exercise4}">Thymeleaf tutorial - Solution for exercise 4: internationalization</h1>
		 <h2 th:text="#{product.info}">Product information</h2>
		 <dl>
		 <dt th:text="#{product.name}">Product name</dt>
		 <dd th:text="${product.description}">Red chair</dd>

		 <dt th:text="#{product.price}">Product price</dt>
		 <dd th:text="${#numbers.formatDecimal(product.price, 1, 2)}">350</dd>

		 <dt th:text="#{product.available}">Product available from</dt>
		 <dd th:text="${#dates.format(product.availableFrom, 'dd-MMM-yyyy')}">28-Jun-2013</dd>
		 </dl>
 </body>
</html>
```  

此时html需要相应的配置文件。例如如下配置文件：  

en:  

```text
tutorial.exercise4=Thymeleaf tutorial - exercise 4: internationalization
product.info=Product information
product.name=Product name
product.price=Product price
product.available=Product available from
back=Back
```  

fr:  

```text
tutorial.exercise4=Tutorial De Thymeleaf - exercice 4: l'internationalisation
product.info=Information du produit
product.name=Nom du produit
product.price=Prix du produit
product.available=Produit disponible depuis
back=Revenir
```

5、 转义和非转义文本  

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
    <head>
        <title>Thymeleaf tutorial: exercise 5</title>
        <link rel="stylesheet" href="../../../css/main-static.css" th:href="@{/css/main.css}" />
        <meta charset="utf-8" />
    </head>
    <body>
        <h1>Thymeleaf tutorial - Solution for exercise 5: escaped and unescaped text</h1>
        <div th:text="${html}">
            Some escaped text
        </div>
        <div th:utext="${html}">
            Some unescaped text
        </div>
    </body>
</html>
```

上述两个div分别生成的html代码为  

```html
<div>This is an &lt;em&gt;HTML&lt;/em&gt; text. &lt;b&gt;Enjoy yourself!&lt;/b&gt;</div>
<div>This is an <em>HTML</em> text. <b>Enjoy yourself!</b></div>
```  

6、 迭代  

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
    <head>
        <title>Thymeleaf tutorial: exercise 6</title>
        <link rel="stylesheet" href="../../../css/main-static.css" th:href="@{/css/main.css}" />
        <meta charset="utf-8" />
    </head>
    <body>
        <h1>Thymeleaf tutorial - Answer for exercise 6: iteration</h1>
        <h2>Product list</h2>
        <table>
            <thead>
                <tr>
                    <th>Description</th>
                    <th>Price</th>
                    <th>Available from</th>
                </tr>
            </thead>
            <tbody th:remove="all-but-first">
                <tr th:each="product:${productList}">
                    <td th:text="${product.description}">Red Chair</td>
                    <td th:text="${'$' + #numbers.formatDecimal(product.price, 1, 2)}">$123</td>
                    <td th:text="${#dates.format(product.availableFrom, 'yyyy-MM-dd')}">2014-12-01</td>
                </tr>
                <tr>
                    <td>White table</td>
                    <td>$200</td>
                    <td>15-Jul-2013</td>
                </tr>
                <tr>
                    <td>Reb table</td>
                    <td>$200</td>
                    <td>15-Jul-2013</td>
                </tr>
                <tr>
                    <td>Blue table</td>
                    <td>$200</td>
                    <td>15-Jul-2013</td>
                </tr>
            </tbody>
        </table>
    </body>
</html>
```

7、 迭代统计  

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
    <head>
        <title>Thymeleaf tutorial: exercise 7</title>
        <link rel="stylesheet" href="../../../css/main-static.css" th:href="@{/css/main.css}" />
        <meta charset="utf-8" />
    </head>
    <body>
        <h1>Thymeleaf tutorial - Solution for exercise 7: iteration stats</h1>
        <h2>Product list</h2>
        <table>
            <thead>
                <tr>
                    <th>Index</th>
                    <th>Description</th>
                    <th>Price</th>
                    <th>Available from</th>
                </tr>
            </thead>
            <tbody th:remove="all-but-first">
                <tr th:each="product : ${productList}">
                    <td th:text="${productStat.count}">1</td>
                    <td th:text="${product.description}">Red chair</td>
                    <td th:text="${'$' + #numbers.formatDecimal(product.price, 1, 2)}">$350</td>
                    <td th:text="${#dates.format(product.availableFrom, 'dd-MMM-yyyy')}">28-Jun-2013</td>
                </tr>
                <tr>
                    <td>2</td>
                    <td>White table</td>
                    <td>$200</td>
                    <td>15-Jul-2013</td>
                </tr>
                <tr>
                    <td>3</td>
                    <td>Reb table</td>
                    <td>$200</td>
                    <td>15-Jul-2013</td>
                </tr>
                <tr>
                    <td>4</td>
                    <td>Blue table</td>
                    <td>$200</td>
                    <td>15-Jul-2013</td>
                </tr>
            </tbody>
        </table>
    </body>
</html>
```  

8、 条件判断  

```html  
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
    <head>
        <title>Thymeleaf tutorial: exercise 8</title>
        <link rel="stylesheet" href="../../../css/main-static.css" th:href="@{/css/main.css}" />
        <meta charset="utf-8" />
    </head>
    <body>
        <h1>Thymeleaf tutorial - Answer for exercise 8: conditions</h1>
        <h2>Product list</h2>
        <table>
            <thead>
                <tr>
                    <th>Description</th>
                    <th>Price</th>
                    <th>Available from</th>
                    <th></th>
                </tr>
            </thead>
            <tbody>
                <tr th:each="product : ${productList}">
                    <td th:text="${product.description}">Red chair</td>
                    <td th:text="${'$' + #numbers.formatDecimal(product.price, 1, 2)}">$350</td>
                    <td th:text="${#dates.format(product.availableFrom, 'dd-MMM-yyyy')}">28-Jun-2013</td>
                    <td>
                        <span th:if="${product.price lt 100}" class="offer">Special offer!</span>
                    </td>
                </tr>
            </tbody>
        </table>
    </body>
</html>
```  

9、 更多条件判断  

```html  
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
    <head>
        <title>Thymeleaf tutorial: exercise 9</title>
        <link rel="stylesheet" href="../../../css/main-static.css" th:href="@{/css/main.css}" />
        <meta charset="utf-8" />
    </head>
    <body>
        <h1>Thymeleaf tutorial - Answer for exercise 9: more on conditions</h1>
        <h2>Customer list</h2>
        <table>
            <thead>
                <tr>
                    <th>First name</th>
                    <th>Last name</th>
                    <th>Gender</th>
                    <th>Payment method</th>
                    <th>Balance</th>
                </tr>
            </thead>
            <tbody th:remove="all-but-first">
                <tr th:each="customer : ${customerList}">
                    <td th:text="${customer.firstName}">Peter</td>
                    <td th:text="${customer.lastName}">Jackson</td>
                    <!--
                       Use th:switch for selecting content based on ${customer.gender}.
                       As genre can be null if unknown, better use ${customer.gender?.name()}
                       for obtaining its name.
                    -->
                    <td th:switch="${customer.gender?.name()}">
                        <img th:case="'MALE'" src="../../../images/male.png" th:src="@{/images/male.png}" alt="Male" /> <!-- Use "/images/male.png" image -->
                        <img th:case="'FEMALE'" src="../../../images/female.png" th:src="@{/images/female.png}" alt="Female" /> <!-- Use "/images/female.png" image -->
                        <span th:case="*">Unknown</span>
                    </td>
                    <td>
                        <span th:text="${customer.paymentMethod.description}">Direct debit</span>
                        <!-- Show next message only when paymentMethod is not CREDIT_CARD -->
                        <span th:unless="${customer.paymentMethod.name() == 'CREDIT_CARD'}" class="warn">
                            Payment must be done in the next 4 days
                        </span>
                    </td>
                    <!-- Add class="enhanced" when balance is greater than 10000 -->
                    <td th:class="${customer.balance gt 10000} ? 'enhanced'" th:text="${customer.balance}">350</td>
                </tr>
                <tr>
                    <td>Mary</td>
                    <td>Johanson</td>
                    <td><img src="../../../images/female.png" /></td>
                    <td><span>Credit card</span></td>
                    <td>5000</td>
                </tr>
                <tr>
                    <td>Robert</td>
                    <td>Allen</td>
                    <td><img src="../../../images/male.png" /></td>
                    <td>
                        <span>Credit card</span>
                        <span class="warn">Payment must be done in the next 4 days</span>
                    </td>
                    <td class="enhanced">50000</td>
                </tr>
            </tbody>
        </table>
    </body>
</html>
```  

10、 Spring表达式语言  

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
    <head>
        <title>Thymeleaf tutorial: exercise 10</title>
        <link rel="stylesheet" href="../../../css/main-static.css" th:href="@{/css/main.css}" />
        <meta charset="utf-8" />
    </head>
    <body>
        <h1>Thymeleaf tutorial - Solution for exercise 10: Spring Expression language</h1>

        <h2>Arithmetic expressions</h2>
        <p class="label">Four multiplied by minus six multiplied by minus two module seven:</p>
        <p class="answer" th:text="${4 * -6 * -2 % 7}">123</p>

        <h2>Object navigation</h2>
        <p class="label">Description field of paymentMethod field of the third element of customerList bean:</p>
        <p class="answer" th:text="${customerList[2].paymentMethod.description}">Credit card</p>

        <h2>Object instantiation</h2>
        <p class="label">Current time milliseconds:</p>
        <p class="answer" th:text="${new java.util.Date().getTime()}">22-Jun-2013</p>

        <h2>T operator</h2>
        <p class="label">Random number:</p>
        <p class="answer" th:text="${T(java.lang.Math).random()}">123456</p>
    </body>
</html>
```  

11、 超链接  

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
    <head>
        <title>Thymeleaf tutorial: exercise 11</title>
        <link rel="stylesheet" href="../../../css/main-static.css" th:href="@{/css/main.css}" />
        <meta charset="utf-8" />
    </head>
    <body>
        <h1>Thymeleaf tutorial - Answer for exercise 11: links</h1>
        <h2>Product actions</h2>
        <ul>
            <li><a href="#" th:href="@{/exercise11/product.html(action='view')}">View product</a></li>
            <li><a href="#" th:href="@{/exercise11/product.html(action='edit')}">Edit product</a></li>
        </ul>
    </body>
</html>
```  

12、 表单  

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
    <head>
        <title>Thymeleaf tutorial: exercise 12</title>
        <link rel="stylesheet" href="../../../css/main-static.css" th:href="@{/css/main.css}" />
        <meta charset="utf-8" />
    </head>
    <body>
        <h1>Thymeleaf tutorial - Solution for exercise 12: forms</h1>
        <h2>Customer edition</h2>
        <form action="saveCustomer.html" th:action="@{/exercise12/saveCustomer.html}" th:object="${customer}" method="post">
            <input type="hidden" th:field="*{id}" />

            <label for="firstName">First name:</label>
            <input type="text" th:field="*{firstName}" value="John" />

            <label for="lastName">Last name:</label>
            <input type="text" th:field="*{lastName}" value="Wayne" />

            Genre:
            <div th:each="gender : ${genders}" class="radio">
                <input type="radio" th:value="${gender}" th:field="*{gender}" />
                <label th:for="${#ids.prev('gender')}" th:text="${gender.description}">Male</label>
            </div>
            <div th:remove="all" class="radio">
                <input type="radio" />
                <label>Female</label>
            </div>

            <label for="paymentMethod">Payment method:</label>
            <select th:field="*{paymentMethod}" th:remove="all-but-first">
                <option th:each="paymentMethod : ${paymentMethods}"
                        th:value="${paymentMethod}" th:text="${paymentMethod.description}">Credit card</option>
                <option>Another payment method</option>
                <option>Another payment method</option>
            </select>

            <label for="balance">Balance (dollars):</label>
            <input type="text" th:field="*{balance}" size="10" value="2500" />

            <input type="submit" />
        </form>
    </body>
</html>
```  

13、 内联  

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
    <head>
        <title>Thymeleaf tutorial: exercise 13</title>
        <link rel="stylesheet" href="../../../css/main-static.css" th:href="@{/css/main.css}" />
        <meta charset="utf-8" />
    </head>
    <body>
        <h1>Thymeleaf tutorial - Solution for exercise 13: inlining</h1>
        <h2>Birthday email</h2>
        <form action="#" method="post">
            <label for="body">Message body:</label>
<textarea id="body" name="body" th:inline="text">
Dear [[${customerName}]],

it is our sincere pleasure to congratulate your in your birthday:
    Happy birthday [[${customerName}]]!!!

See you soon, [[${customerName}]].

Regards,
    The Thymeleaf team
</textarea>
            <input type="submit" value="Send mail" />
        </form>
    </body>
</html>
```  

更多资料可以去[官网](http://itutorial.thymeleaf.org/)查看
