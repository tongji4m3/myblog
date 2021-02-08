---
title: Java基础--常见基础
author: tongji4m3
top: false
cover: false
coverImg: /images/1.jpg
toc: true
mathjax: false
summary: 'Java基础知识,待完善,之后再看的时候会继续补充。'
categories: Java基础
tags:
  - Java基础
abbrlink: e7b0c3c0
date: 2020-03-01 00:00:00
---
1. > int 4字节 (-2的31次方)~(2的31次方-1) 
   >
   > short 2字节
   >
   > long 8字节
   >
   > byte 1字节 (-128~127)
   >
   > float 四字节
   >
   > double 8字节
   >
   > byte 2字节     因为Java采用16位的Unicode字符集
   >
   > boolean 只有两个值,但是大小没精确定义

2. > 0x开头代表十六进制,如:0xCAFE 
   >
   > 0b开头代表二进制数,如:0b1001

3. > ```java
   > System.out.printf("%8.2f",x);
   > //s为字符串，f为浮点数，d为十进制数
   > //用8字符的宽度和小数点后两位的精度打印x
   > ```

4. > Java总是按值调用
	>
	> 如果是基本数据类型,那么值不变
	>
	> 引用数据类型:引用被拷贝,指向的是原对象,所以仍能改变对象值

5. > Object类equals()方法:
	>
	> 底层调用==来实现,判断两个对象是否具有相同的引用
	>
	> 若是比较状态是否相等
	>
	> ```java
	> public boolean equals(Object obj)
	> {
	>     if(this==obj) return true;
	>     if(obj==null) return false;
	>     if(getClass()!=obj.getClass()) return false;
	> 
	>     Person person = (Person) obj;
	>     return Objects.equals(name, person.name) &&
	>         Objects.equals(age, person.age);
	> }
	> 
	> /*
	> Objects.equals():
	> public static boolean equals(Object a, Object b) 
	> {
	>     return (a == b) || (a != null && a.equals(b));
	> }
	> */
	> ```
6. >  Object类hashCode()方法
	>
	>  如果重新定义equals方法,则需要重新定义hashCode()方法
	>
	>  ```java
	>  @Override
	>  public int hashCode()
	>  {
	>      return Objects.hash(name, age);
	>  }
	>  ```

7. > 自动装箱,自动拆箱,在-128,127之间会被包装到固定的对象,会导致
	>
	> ```java
	> Integer a=10;
	> Integer b=10;
	> if(a==b)//结果为true
	> ```

8. > 异常
	>
	> ```java 
	> Throwable 
	>  	Error 非受查异常
	>  	Exception
	>  		IOException等 受查异常
	>  		RuntimeException 非受查异常
	> ```
	>   一个方法必须声明所有可能抛出的受查异常.非受查异常要么不可控制,要么应该避免发生.
    >     	

​	



1. 多态,父类引用指向子类对象.编译看左边,运行看右边.

2. ```java
   SimpleDateFormat dateFormat =
     new SimpleDateFormat("yyyy年MM月dd日");
   Date date = new Date();
   System.out.println(dateFormat.format(date));
   ```

3. ```java
   StringBuilder builder = new StringBuilder("A");
   builder.append("BC");
   String s = builder.toString();
   ```

4. ```java
   Integer.parseInt(string);
   ```

5. ```java
   <? extend E>泛型中必须是本身或者子类
   ```

6. ```java
   Collections.shuffle(poker);
   Collections.sort(poker);
   Collections.addAll(poker, "A", "B");
   ```



1. ```java
   //运行期异常可以不进行异常处理(RuntimeException).抛出异常
   if(s==null)
   {
     throw new NullPointerException("传递对象为空");
   }

   //编译期异常必须进行异常处理
    public static void main(String[] args) 
      throws FileNotFoundException
    {
      throw new FileNotFoundException("aa");
    }

   try{}
   catch (RuntimeException e)
   {
     e.printStackTrace();
   }
   finally{}
   ```

2. ```java
    new Thread()
    {
      @Override
      public void run()
      {
        for (int i = 0; i < 20; i++)
        	System.out.println(i);     
      }
    }.start();
   Thread.sleep(1000);
   ```

3. ```java
   //同步方法 线程安全 锁对象是this
   public synchronized void payTicket(){}

   //等待唤醒机制,实现线程通信
   Object obj = new Object();
   new Thread()
   {
     @Override
     public void run()
     {
       synchronized (obj)
       {
         obj.wait();
       }
     }
   }.start();

   new Thread()
   {
     @Override
     public void run()
     {
       Thread.sleep(5000);
       synchronized (obj)
       {
         obj.notify();
       }
     }
   }.start();
   ```

4. ```java
   //用线程池管理线程
   ExecutorService es = Executors.newFixedThreadPool(2);
   es.submit(
     new Runnable()
     {
       @Override
       public void run()
       {
         System.out.println("AA");
       }
     });
   ```

5. ```java
   /*函数式编程 只要获取结果就行,不注重谁去做
   适合只想传递一段代码的情况
   Lambda表达式
   */
   public interface Cook
   {
       void invokeCooke();
   }
   public class CookImpl
   {
       public static void main(String[] args)
       {
           test(()->
           {
               System.out.println("吃饭了");
           });
       }

       public static void test(Cook cook)
       {
           cook.invokeCooke();
       }
   }

   /*******************带参数的省略写法************************/
   public interface Cook
   {
       int invokeCooke(int a,int b);
   }
   public class CookImpl
   {
       public static void main(String[] args)
       {
           test(12,13,(a,b)-> a+b);
       }

       public static void test(int a,int b,Cook cook)
       {
           int result=cook.invokeCooke(a,b);
           System.out.println(result);
       }
   }
   ```

6. ```java
   //相对路径 相当于当前项目的根目录 //C:\code_home\idea_home\JAVA\DouDiZhu
   File file = new File("DouDiZhu");
   System.out.println(file.getAbsolutePath());
   ```

7. ```java
   //字符流处理中文问题
    FileReader fileReader = new FileReader("D:\\test.txt");
   char[] chars = new char[1024];//读取到chars中
   int len = 0;//len记录每次读取的字符个数
   while((len=fileReader.read(chars))!=-1)
   {
     System.out.println(new String(chars,0,len));
   }
   ```

8. ```java
   //流对象自动关闭,无需手动close
   public static void main(String[] args) 
     throws FileNotFoundException
   {
     try(FileInputStream fileInputStream = 
         new FileInputStream("D:\\00001.jpg");
         FileOutputStream fileOutputStream = 
         new FileOutputStream("D:\\copy.jpg");)
     {
       byte[] bytes = new byte[1024];
       int length;
       while((length=fileInputStream.read(bytes))!=-1)
       {
         fileOutputStream.write(bytes,0,length);
       }
     }
     catch (IOException e)
     {
       e.printStackTrace();
     }
     //fileOutputStream.close();
     //fileInputStream.close();
   }
   ```

9. ```java
   //配置文件加载与存储
   Properties properties = new Properties();
   properties.setProperty("李", "168");
   properties.setProperty("BA", "1688");
   properties.setProperty("CA", "168888");
   properties.store(new FileWriter("D:\\test.txt"),"save data");//存储硬盘中

   Properties properties = new Properties();//加载硬盘中
   properties.load(new FileReader("D:\\test.txt"));
   Set<String> strings = properties.stringPropertyNames();
   for (String string : strings)
   {
     System.out.println(string+" "+properties.getProperty(string));
   }
   //配置文件基本表示类型
   /*
   #save data
   #Wed Feb 05 11:12:12 CST 2020
   李=168
   CA=168888
   BA=1688
   */
   ```

10. ```java
    HashMap<String, String> hashMap = new HashMap<>();
    BufferedReader bufferedReader = 
      new BufferedReader(new FileReader("D:\\test.txt"));
    String line;
    while((line=bufferedReader.readLine())!=null)
    {
      String[] strings = line.split("\\.");
      hashMap.put(strings[0], strings[1]);
    }
    //如果放在上面就会没了
    BufferedWriter bufferedWriter = 
      new BufferedWriter(new FileWriter("D:\\test.txt"));
    for(String key:hashMap.keySet())
    {
      String value = hashMap.get(key);
      line = key + "." + value;
      bufferedWriter.write(line);
      bufferedWriter.newLine();
    }
    bufferedReader.close();
    bufferedWriter.close();
    }
    ```

11. ```java
    idea默认编码UTF-8,win10默认编码GBK
    ```

12. ipconfig  127.0.0.1 localhost 代表自己  

13. 端口号 0-65535  1024之前的端口不能使用

14. 网络端口:80     MySQL:3306      tomcat服务器:8080

15. ```java
    //网络编程
    //客户端
    Socket socket = new Socket("127.0.0.1", 8888);
    OutputStream outputStream = socket.getOutputStream();
    outputStream.write("你好,服务器".getBytes());

    InputStream inputStream = socket.getInputStream();
    byte[] bytes = new byte[1024];
    int len = inputStream.read(bytes);
    System.out.println(new String(bytes,0,len));
    /*******************服务器端*******************/
    ServerSocket serverSocket = new ServerSocket(8888);
    Socket socket = serverSocket.accept();
    InputStream inputStream = socket.getInputStream();
    byte[] bytes = new byte[1024];
    int len = inputStream.read(bytes);
    System.out.println(new String(bytes,0,len));
    socket.getOutputStream().write("收到谢谢".getBytes());

    ```

16. ```java
    //检测是否是函数式接口 有且仅有一个抽象方法
    @FunctionalInterface
    public interface Test
    {
        void test1();
    }
    public class Demo
    {
        public static void main(String[] args)
        {
            show(() -> System.out.println("AA"));
        }

        public static void show(Test myTest)
        {
            myTest.test1();
        }
    }

    ```

17. ```java
    //stream流式模型 相当于对一个list或者数组进行一系列处理,然后对剩下的集合打印或者其他操作
    public static void main(String[] args)
    {
      List<String> list = new ArrayList<>();
      list.add("AAA");
      list.add("AAB");
      list.stream().
        filter(name->name.startsWith("A")).
        filter(name->name.length()==3).
        forEach(name->System.out.println(name));
    }
    ```


    //一种数据类型转换为另外一种
    Stream<String> stream = Stream.of("12", "23", "45");
    Stream<Integer> stream1=stream.map((String name) ->
     {
           return Integer.parseInt(name);
     });
    stream1.forEach(i->System.out.println(i));
    
    Stream<String> stream = Stream.of("12", "23", "45","78");
    System.out.println(stream.limit(3).count());
    ```

18. ```java
    //junit
    //@Before使得所有测试方法先执行该方法
    @Before
    public void init()
    {
      System.out.println("init..");
    }

    @After
    public void close()
    {
      System.out.println("close..");
    }

    @Test
    public void testIt()
    {
      Demo demo = new Demo();
      demo.test(2,3);
    }
    ```

19. ```java
    //三种反射获得方式
    //全类名
    Class.forName("com.tongji.Student");
    Class clazz = Student.class;
    Student student = new Student();
    student.getClass();

    //一个案例
    Properties properties = new Properties();
    InputStream inputStream = ReflectTest.class.getClassLoader().
      getResourceAsStream("com/tongji/test/pro.properties");
    properties.load(inputStream);

    String className = properties.getProperty("className");
    String methodName = properties.getProperty("methodName");
    Class cls = Class.forName(className);
    Object object = cls.newInstance();
    Method method = cls.getMethod(methodName);
    method.invoke(object);
    ```

20. ```java
    @Deprecated  代表方法已经过时
    @SuppressWarnings("all")  抑制警告
    @Override 重写方法
    ```

    







