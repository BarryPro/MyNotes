# SpringMVC

## 一、SpringMVC 常用注解

- @Controller：用于标识是处理器类

- @RequestMapping:请求到处理器功能方法的映射规则（可以映射多个路径用数组）

- @RequestParam：（form,如何传入的参数用可能是空值是要设置默认值否则会出现异常）请求参数到处理器功能处理方法的方法参数上的绑定，还能绑定上传的文件等。

  >  value:参数名字，即入参的请求参数名字，如username表示请求的参数区中的名字为username的参数的值将传入；
  >
  > required:是否必须，默认是true，表示请求中一定要有想应的参数，否则将报404错误码；,required=false表示请求中允许没有名字为username的参数，如果没有默认为null，此处要注意如下几点：
  >
  > 原子类型：例如，int必须有值，否则抛出异常，如果允许空值请使用包装类代替。
  >
  > Boolean包装类类型：默认Boolean.FALSE,其他引用类型默认为null。
  >
  > defaultValue:默认值，表示如果请求中没有同名参数时的默认值，默认值可以是SpEL表达式，如“#{systemProperties['java,vm,version']}”

- @ModelAttribute：请求参数到命令对象的绑定

  > <1>.绑定请求参数到命令对象：放在功能处理方法的形参上时，用于将多个请求参数绑定到一个命令对象，从而化简绑定流程，而且自动暴露为模型数据用于视图页面展示时使用；
  >
  > <2>.暴露表单引用对象为模型数据：放在处理器的一般方法（非功能处理方法）上时，是为表单准备要展示的表单引用对象，如注册时需要选择的所在城市等，而且在执行功能处理方法（@RequestMapping注解的方法）之前，自动添加到模型对象中，用于视图页面展示时使用。 
  >
  > <3>.暴露@RequestMapping方法返回值为模型数据：放在功能处理方法的返回值上时，是暴露功能处理方法的返回值为模型数据，用于视图页面展示使用；

- @SessionAttribute：用于声明session级别存储的属性，方法在处理器类上，通常列出模型属性（如@ModelAttribute）对应的名称，则这些属性会透明的保存到session中。

- @InitBinder：自定义数据绑定注册支持，用于将请求参数转换到命令对象属性的对应类型

- @CookieValue:cookie数据到处理器功能处理方法的方法参数的绑定

  有3个与@RequestParam同的参数
  value 是cookie的名称
  required 为false表示的是请求中没有响应的cookie的值时也不会抛出异常

- @RequestHeader:请求头（header）数据到处理器功能处理方法的方法参数的绑定

- @RequestBody:请求的body体的绑定（通过HttpMessageConverter进行类型转换）

- @ResponseBody:处理器功能处理方法的返回值作为相应体（HttpMessageConverter进行类型转换）

  > ResponseStatus:定义处理器功能处理方法/异常处理器返回的状态码和原因
  >
  > ExceptionHandler:注解式声明异常处理器
  >
  > PathVariable:（超链）(获取路径（URL）上的参数)请求URL中的模板变量部分到处理器功能处理方法的方法参数的绑定，从而支持RESTful（统一资源接口：一个名对应一个方法）架构风格的URL
  >
  > ModelValue:绑定参数到命令对象
  >
  > SessionAttributes:绑定命令对象到session
  >
  > RequestPart:绑定“multipart/data”数据,

## 二、控制反转一个一个类进行写

``` xml
<bean class="com.belong.controller.UserController"></bean>
```

## 三、SpringMVC防止静态页不好使

``` xml
<mvc:default-servlet-handler/>
```

## 四、URL路径映射

### **<1>.普通URL路径映射：一对一的是啥就是啥**

``` java 
eg:
@RequestMapping(value={"/test1","/user/create"});多个URL路径映射到同一个处理器的功能处理方法
@RequestMapping(value="/user/{userId}"):其中的{****}是占位符，请求的URL可以是“/user/123456”或“/user/abce”;
@RequestMapping(value="/user/{userId}/create"):这样也是可以的，请求的URL可以是“/users/123/create”
```

### **<2>.ANT风格：可以使用占位符**

``` java
eg：
@RequestMapping(value="/user/**"):可以匹配“、user/abc/abc”，但是“user/123”将会被URL模板映射中的“/user/{userId}”模式优先映射到
@RequestMapping（value="/product?"）:可以匹配“、product1”或“/producta”，但是不能匹配"/product"或“/productaa”;
@RequestMapping（value="/product*"）：可以匹配"/productabc"或“product”，但是不可以匹配“/product/abc”;
@RequestMapping(value="/product/*"):可以匹配“/product/abc”,但是不匹配“/productabc”;
@RequestMapping(value="/product/**/{productId}"):可以匹配“/product/abc/abc/123”或“/product/123”
<3>.正则风格:Spring3.0开始支持正则表达式风格
eg:
@RequestMapping（vlaue="/product/{categoryCode:\\d+}-{pageNumber:\\d+}"）:可以匹配“/product/123-1”,但是不能匹配“/product/abc-1”
```

## 五、SpringMVC数据绑定

### Model、Map、ModelMap（后端向前端传递数据）之间的关系

![18aac01e87e33118ad3a15f395c31ba6](../../../../var/folders/3b/d9smmxhd7zbfg_fksx3zj7f40000gn/T/WizNote/18e7e899-f37f-441a-9806-bf7ce7337a5e/index_files/18aac01e87e33118ad3a15f395c31ba6.jpg)