# Peer Review Check List 
## DRAFT Version

## Functionality -- Функциональность
*simple, reusable and maintainable manner -- простота, переиспользование и возможность поддержки*

**SOLID design principle -- принципы проектирования архитектуры**
- Single Responsibility Principle -- класс создан для выполнения единственной задачи и не пытается решить одновременно несколько различных;
- Open/closed principle -- классы, модули, функции могут быть расширены без изменения их кода;
- Liskov substitution principle -- используемые классом и его методами объекты могут быть заменены их подтипами (например, метод возвращает List\<Integer>, который можно заменить подтипом - ArrayList\<Integer>);
- Interface segregation principle -- использованию общего универсального интерфейса отдается предпочтение отдельным специализированным;
- Dependency inversion principle -- зависимости построены на абстракциях и не зависят от деталей.


**DRY - Don’t Repeat Yourself -- код не содержит повторов и дублирующих фрагментов**<br>
**KISS - Keep It Short and Simple -- решения простые и короткие**

**OO concepts -- Принципы ООП**
- Abstraction -- отделение деталей для получения возможности сосредоточиться на главных особенностях объекта;
- Polymorphism -- использование общего интерфейса для обработки данных разных типов;
- Inheritance -- образование новых классов на основе использования(наследования) существующих;
- Encapsulation -- объект включает данные и методы их обработки, доступ к которым осуществляется не напрямую, а через заданный интерфейс (открытые поля и методы).

These principles and concepts are all about accomplishing “Low coupling” and “High cohesion“ --  Соблюдение перечисленных мер направлено на снижение взаимной зависимости и повышение качества связей между программными модулями.

**Apply functional programming paradigm where it makes more sense -- Функциональное программирование используйте там, где его применение имеет смысл.**

## Clean code -- Чистый код
1. Use of descriptive and meaningful variable, method and class names as opposed to relying too much on comments.
Использование описательных и имеющих значение имен для переменных, методов и классов в противовес чрезмерной зависимости от комментариев.
*E.g. calculateGst(BigDecimal amount), BalanceLoader.java, etc.
Bad: List list;
Good: List<String> users;*

2. Class and functions should be small and focus on doing one thing. No duplication of code. -- Класс и функции должны быть маленькими и фокусироваться на решении одной задачи.
Без дублирования кода.
*E.g. CustomerDao.java for data access logic only -- только логика доступа к данным, Customer.java for domain object -- объект предметной области, 
CustomerService.java for business logic -- бизнес-логика, and CustomerValidator.java for validating input fields -- проверка правильности вводимых данных, etc.
Similarly, separate functions like processSalary(String customerCode) will invoke other sub functions with meaningful names like 
evaluateBonus(String customerCode), evaluateLeaveLoading(String customerCode), etc 
-- аналогично функции типа посчитатьЗарплату(String кодПользователя) должны вызывать другие подзадачи со значимыми названиями 
вроде посчитатьБонус(String кодПользователя), посчитатьОтпускные(String кодПользователя)*

3. Functions should not take too many input parameters. -- функции не должны принимать слишком много параметров </br>
*Bad: processOrder(String customerCode, String customerName, String deliveryAddress, BigDecimal unitPrice, int quantity, BigDecimal discountPercentage); </br>
Good: processOrder(CustomerDetail customer, OrderDetail order);* </br>
where CustomerDetail is a value object with attributes like customerCode, customerName, etc. -- тут несколько атрибутов объединены в один объект

4. Use a standard code formatting template.	Share the template across the development team. 
-- Используйте стандартные шаблоны форматирования кода, используйте их вместе всей командой разработчиков.
Declare the variables with the smallest possible scope.	For example, if a variable “tmp” is used only inside a loop, then declare it inside the loop, and not outside.
-- Насколько возможно ограничивайте область объявления переменных. К примеру, если переменная “tmp” используетя только внутри цикла, объвляйте ее внутри цикла, а не снаружи.
Don’t preserve or create variables that you don’t use again. -- Не создавайте и не храните переменные, которые не будут повторно использованы.
*E.g. instead of -- вместо этого: boolean removed = myItems.remove(item); return removed; 
Do: -- сделайте так: return myItems.remove(item);*

5. Omit needless and commented out code. No System.out.println statements either.	You have source control for the history. 
Use proper logging frameworks like slf4j and logback for logging.
-- Избегайте ненужного и закоментированного кода. Никакой печати в консоль. Для истории существует система управления исходным кодом. Используйте для сохранения логов
специальные фреймворки.

## Fundamentals
6. Make a class final and the object immutable where possible.	Immutable classes are inherently thread-safe and more secured. 
For example, the Java String class is immutable and declared as final.
7. Minimize the accessibility of the packages, classes and its members like methods and variables.	E.g. private, protected, default, and public access modifiers.
Code to interface as opposed to implementation.	Bad: ArrayList<String> names = new ArrayList<String>();
Good: List<String> names = new ArrayList<String>();
8. Use right data types.	For example, use BigDecimal instead of floating point variables like float or double for monetary values. 
9. Use enums instead of int constants.
10. Avoid finalizers and properly override equals, hashCode, and toString methods.	The equals and hashCode contract must be correctly implemented to prevent hard to debug defects.
11. Write fail-fast code by validating the input parameters.	
12. Apply design by contract.
13. Return an empty collection or throw an exception as opposed to returning a null. Also, be aware of the implicit autoboxing and unboxing gotchas. 
NullpointerException is one of the most common exceptions in Java.

## Key Areas like Security, Exception Handling, Performance, Memory/Resource leaks, Concurrency, etc
### Security.
14. Don’t log sensitive data.	 
15. Clearly document security related information.
16. Sanitize user inputs.
17. Favor immutable objects.
18. Use Prepared statements as opposed to ordinary statements.	 Security to prevent SQL injection attack.
19. Release resources (Streams, Connections, etc).	 Security to prevent denial of service attack (DoS) and resource leak issues.
20. Don’t let sensitive information like file paths, server names, host names, etc escape via exceptions.	Security and Exception Handling.
21. Follow proper security best practices like SSL (one-way, two-way, etc), encrypting sensitive data, authentication/authorization, etc.
22. Use exceptions as opposed to return codes.	Exception Handling.
23. Don’t ignore or suppress exceptions. Standardize the use of checked and unchecked exceptions. Throw exceptions early and catch them late.	Exception Handling.
24. Write thread-safe code with proper synchronization and use of immutable objects. Also, document thread-safety.	Concurrency.
25. Keep synchronization section small and favor the use of the new concurrency libraries to prevent excessive synchronization.	Concurrency and Performance.
26. Reuse objects via flyweight design pattern.	Performance.
27. Presence of long lived objects like ThreadLocal and static variables holding references to lots of short lived objects.	Memory Leak and Performance
28. Badly constructed SQL, REGEX, etc.	Performance. E.g. Cartesian joins in SQL and back tracking regular expressions.
29. Inefficient Java coding and algorithms in frequently executed methods leading to death by thousand cuts.	Performance

## Other general programming
30. Favor using well proven frameworks and libraries as opposed to reinventing the wheel by writing your own.	
*E.g. Apache commons libraries, Google Gauva libraries, Spring libraries, XML/JSON libraries, etc.
31. Presence of JUnit and JBehave test cases. Check the test coverage and quality of the unit tests with proper mock objects to be able to easily maintain and run independently/repeatedly.
32. Test only a unit of code at a time (e.g. one function).
33. Unit tests must be independent of each other. They should run independendtly.
34. Set up should not be too complicated.
35. Mockout external states and services that you are not asserting. For example, retrieving data from a database.
36. Avoid unneccessary assertions.
37. Start with functions that have the fewest dependencies, and work your way up.
38. Write unit tests for negative scenarios like throwing exceptions, negative values, null values, etc.
39. Don’t have try/catch inside unit tests. Use throws Exception statement in test case declaration itself.
40. Don’t have any System.out.println(…..)
41. Ensure that the unit tests are written properly.	Don’t write unit tests for the sake of writing one.
42. Presence of hard coded config values. Externalize configuration data in a .properties file. Sensitive information like password must be encrypted.
43. Presence and implementation of non functional requirements like archiving, auditing, and purging data and application monitoring where required. It is easy to ignore these

<p> ![picture alt](https://lostechies.com/derickbailey/files/2011/03/SOLID_6EC97F9C.jpg)
![picture alt](https://lostechies.com/derickbailey/files/2011/03/SingleResponsibilityPrinciple2_71060858.jpg) 
![picture alt](https://lostechies.com/derickbailey/files/2011/03/OpenClosedPrinciple2_2C596E17.jpg)
![picture alt](https://lostechies.com/derickbailey/files/2011/03/LiskovSubtitutionPrinciple_52BB5162.jpg)
![picture alt](https://lostechies.com/derickbailey/files/2011/03/InterfaceSegregationPrinciple_60216468.jpg)
![picture alt](https://lostechies.com/derickbailey/files/2011/03/DependencyInversionPrinciple_0278F9E2.jpg)
</p>
