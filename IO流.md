---


## File类

---

```java
public class FileDemo {
    public static void main(String[] args) {
        //File构造函数演示
        String pathName = "e:\\test\\Hello.java";
        File f1 = new File(pathName);//将Test22文件封装成File对象。注意；有可以封装不存在文件或者文件夹，变成对象。
        System.out.println(f1);

        File f2 = new File("e:\\test","Hello.java");
        System.out.println(f2);

        //将parent封装成file对象。
        File dir = new File("e:\\test");
        File f3 = new File(dir,"Hello.java");
        System.out.println(f3);
    }
}


    //e:\test\Hello.java
    //e:\test\Hello.java
    //e:\test\Hello.java
```
```java
    public class FileMethodDemo {
    	public static void main(String[] args) {
    		//创建文件对象
    		File file = new File("Test22.java");
    		//获取文件的绝对路径，即全路径
    		String absPath = file.getAbsolutePath();
    		//File中封装的路径是什么获取到的就是什么。
    		String path = file.getPath();
    		//获取文件名称
    		String filename = file.getName();
    		//获取文件大小
    		long size = file.length();
    		
    		System.out.println("absPath="+absPath);
    		System.out.println("path="+path);
    		System.out.println("filename="+filename);
    		System.out.println("size="+size);
    	}
    }
    
    //absPath=D:\code\BigData\designPattern\Test22.java
    //path=Test22.java
    //filename=Test22.java
    //size=0
```
```java
    public class FileMethodDemo2 {
    	public static void main(String[] args) throws IOException {
    		// 对文件或者文件加进行操作。
    		File file = new File("e:\\file.txt");
    		// 创建文件，如果文件不存在，创建 true 。 如果文件存在，则不创建 false。 如果路径错误，IOException。
    		boolean b1 = file.createNewFile();
    		System.out.println("b1=" + b1);
    		//-----------删除文件操作-------注意：不去回收站。慎用------
    		 boolean b2 = file.delete();
    		 System.out.println("b2="+b2);
    
    		//-----------需要判断文件是否存在------------
    		 boolean b3 = file.exists();
    		 System.out.println("b3="+b3);
    
    		//-----------对目录操作 创建，删除，判断------------
    		File dir = new File("e:\\abc");
    		//mkdir()创建单个目录。//dir.mkdirs();创建多级目录
    		boolean b4 = dir.mkdir();
    		System.out.println("b4="+b4);
    		//删除目录时，如果目录中有内容，无法直接删除。
    		boolean b5 = dir.delete();
    		//只有将目录中的内容都删除后，保证该目录为空。这时这个目录才可以删除。
    		System.out.println("b5=" + b5);
    
    		//-----------判断文件，目录------------
    		File f = new File("e:\\javahaha");// 要判断是否是文件还是目录，必须先判断存在。
    		// f.mkdir();//f.createNewFile();
    		System.out.println(f.isFile());
    		System.out.println(f.isDirectory());
    	}
    }
    
                //b1=true
                //b2=true
                //b3=false
                //b4=true
                //b5=true
                //false
                //false
```
文件过滤器
```java
public class FileDemo2 {
    public static void main(String[] args) {
        //获取扩展名为.java所有文件
        //创建File对象
        File file = new File("E:\\test");
        //获取指定扩展名的文件,由于要对所有文件进行扩展名筛选，因此调用方法需要传递过滤器
        File[] files = file.listFiles(new MyFileFilter());
        //遍历获取到的所有符合条件的文件
        for (File f : files) {
            System.out.println(f);
        }
    }
}


//定义类实现文件名称FilenameFilter过滤器
class MyFileFilter implements FilenameFilter{
    public boolean accept(File dir, String name) {
        return name.endsWith(".java");
    }
}

```


## 字节流

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650781041156-1dac993d-c5fa-4c42-b9fc-5a37cdb4713b.png#clientId=ua080b6b1-c287-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=707&id=u4f5d9a4c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=707&originWidth=988&originalType=binary&ratio=1&rotation=0&showTitle=false&size=78138&status=done&style=none&taskId=ud7e66384-a674-48ca-859e-e6505b2cd70&title=&width=988)

- 数据写出到文件
```java
public static void main(String[] args) throws IOException {
    		//创建存储数据的文件。
    		File file = new File("E:\\file.txt");
    		//创建一个用于操作文件的字节输出流对象。一创建就必须明确数据存储目的地。
    		//输出流目的是文件，会自动创建。如果文件存在，则覆盖。
    		FileOutputStream fos = new FileOutputStream(file);
    		//调用父类中的write方法。
    		byte[] data = "abcde".getBytes();
    		fos.write(data);
    		//关闭流资源。
    		fos.close();
    	}


```
追加数据
```java
public static void main(String[] args) throws Exception {
    		File file = new File("E:\\file.txt");
    		FileOutputStream fos = new FileOutputStream(file, true);
    		String str = "\r\n"+"HelloIO";
    		fos.write(str.getBytes());
    		fos.close();
    	}

```

- 读入文件数据
```java
public class FileInputStreamDemo {
    public static void main(String[] args) throws IOException {
        File file = new File("E:\\file.txt");
        //创建一个字节输入流对象,必须明确数据源，其实就是创建字节读取流和数据源相关联。
        FileInputStream fis = new FileInputStream(file);
        //读取数据。使用 read();一次读一个字节。
        int ch = 0;
        while((ch=fis.read())!=-1){
            System.out.println("ch="+(char)ch);		
        }
        // 关闭资源。
        fis.close();
    }
}

```
一次读多个
```java
public class FileInputStreamDemo2 {
    public static void main(String[] args) throws IOException {
        /*
         * 演示第二个读取方法， read(byte[]);
         */
        File file = new File("E:\\file.txt");
        // 创建一个字节输入流对象,必须明确数据源，其实就是创建字节读取流和数据源相关联。
        FileInputStream fis = new FileInputStream(file);		
        //创建一个字节数组。
        byte[] buf = new byte[1024];//长度可以定义成1024的整数倍。		
        int len = 0;
        while((len=fis.read(buf))!=-1){
            System.out.println(new String(buf,0,len));
        }
        fis.close();
    }
}
```

- 复制图片
```java
public static void main(String[] args) throws Exception{
    //1,明确源和目的。
    File srcFile = new File("E:\\vuepress\\myblog\\docs\\.vuepress\\public\\images\\66.ico");
    File destFile = new File("E:\\vuepress\\myblog\\docs\\.vuepress\\public\\images\\66copy1.ico");

    //2,明确字节流 输入流和源相关联，输出流和目的关联。
    FileInputStream fis = new FileInputStream(srcFile);
    FileOutputStream fos = new FileOutputStream(destFile);

    //3, 使用输入流的读取方法读取字节，并将字节写入到目的中。
    //定义一个缓冲区。
    byte[] buf = new byte[1024];
    int len = 0;
    while ((len = fis.read(buf)) != -1) {
        fos.write(buf, 0, len);// 将数组中的指定长度的数据写入到输出流中。
    }
    //4,关闭资源。
    fos.close();
    fis.close();
}
```




## 字符流

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650781061347-c3f6705f-4b34-4518-a38a-7af22bef6e11.png#clientId=ua080b6b1-c287-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=877&id=u4fa1cbff&margin=%5Bobject%20Object%5D&name=image.png&originHeight=877&originWidth=975&originalType=binary&ratio=1&rotation=0&showTitle=false&size=126391&status=done&style=none&taskId=u63a39790-9a76-4bfa-aec3-2f2225e3b06&title=&width=975)

- FileReader
```java
 
    public static void main(String[] args) throws IOException {
        //给文件中写中文
        writeText();
        //读取文件中的中文
        readText();
    }	
    //读取中文
    public static void readText() throws IOException {
        FileReader fr = new FileReader("E:\\test\\a.txt");
        int ch = 0;
        while((ch = fr.read())!=-1){
            //输出的字符对应的编码值
            System.out.println(ch);
            //输出字符本身
            System.out.println((char)ch);
        }
    }
    //写中文
    public static void writeText() throws IOException {
        FileOutputStream fos = new FileOutputStream("E:\\test\\a.txt");
        fos.write("林子很大".getBytes());
        fos.close();
    }

        //26519
        //林
        //23376
        //子
        //24456
        //很
        //22823
        //大

```

- FileWriter
```java
public class FileWriterDemo {
    public static void main(String[] args) throws IOException {
        //演示FileWriter 用于操作文件的便捷类。
        FileWriter fw = new FileWriter("E：\\text\\fw.txt");
        fw.write("你好,六脉神剑");//这些文字都要先编码。都写入到了流的缓冲区中。
        fw.flush();//刷新
        fw.close();// 关闭之前需要刷新它
    }
}
```

## 转换流

---

### OutputStreamWriter（字节 to 字符）

---

```java
public static void writeC() throws Exception {
    //创建与文件关联的字节输出流对象
    FileOutputStream fos = new FileOutputStream("c:\\c.txt");
    //创建可以把字符转成字节的转换流对象，并指定编码
    OutputStreamWriter osw = new OutputStreamWriter(fos,"utf-8");
    //调用转换流，把文字写出去，其实是写到转换流的缓冲区中
    osw.write("六脉神剑");//写入缓冲区。
    osw.close();
}


```

### InputStreamReader（字节 to 字符）

---

```java

    public static void main(String[] args) throws IOException {
        //演示字节转字符流的转换流
        readC();
    }
    public static void readC() throws IOException{
        //创建读取文件的字节流对象
        InputStream in = new FileInputStream("E:\\c.txt");
        //创建转换流对象 
        //InputStreamReader isr = new InputStreamReader(in);这样创建对象，会用本地默认码表读取，将会发生错误解码的错误
        InputStreamReader isr = new InputStreamReader(in,"utf-8");
        //使用转换流去读字节流中的字节
        int ch = 0;
        while((ch = isr.read())!=-1){
            System.out.println((char)ch);
        }
        //关闭流
        isr.close();
    }

```


## 缓冲流

---


### BufferedOutputStream

---

```java

public static void main(String[] args) throws IOException {

    //写数据到文件的方法
    write();
}

/*
 * 写数据到文件的方法
 * 1,创建流
 * 2，写数据
 * 3，关闭流
 */
private static void write() throws IOException {
    //创建基本的字节输出流
    FileOutputStream fileOut = new FileOutputStream("abc.txt");
    //使用高效的流，把基本的流进行封装，实现速度的提升
    BufferedOutputStream out = new BufferedOutputStream(fileOut);
    //2，写数据
    out.write("hello".getBytes());
    //3，关闭流
    out.close();
}
```
### BufferedInputStream

---

```java
/*
 * 从文件中读取数据
 * 1,创建缓冲流对象
 * 2，读数据，打印
 * 3，关闭
 */
private static void read() throws IOException {
    //1,创建缓冲流对象
    FileInputStream fileIn = new FileInputStream("abc.txt");
    //把基本的流包装成高效的流
    BufferedInputStream in = new BufferedInputStream(fileIn);
    //2，读数据
    int ch = -1;
    while ( (ch = in.read()) != -1 ) {
        //打印
        System.out.print((char)ch);
    }
    //3，关闭
    in.close();
}
```
对比
```java
方式1： 采用基本的流，一次一个字节的方式复制	共耗时 224613毫秒
方式2： 采用基本的流，一个多个字节的方式赋值	共耗时     327毫秒
方式3： 采用高效的流，一次一个字节的方式复制	共耗时    2047毫秒
方式4： 采用高效的流，一个多个字节的方式赋值	共耗时      96毫秒
```

### BufferedWriter

---

```java
/*
 * BufferedWriter 字符缓冲输出流
 * 方法
 * 	public void newLine()写入一个行分隔符
 * 
 * 需求： 通过缓冲输出流写入数据到文件
 * 分析：
 * 	1，创建流对象
 * 	2，写数据
 * 	3，关闭流
 * 
 */
    public static void main(String[] args) throws IOException {
        //创建流
        //基本字符输出流
        FileWriter fileOut = new FileWriter("file.txt");
        //把基本的流进行包装
        BufferedWriter out = new BufferedWriter(fileOut);
        //2，写数据
        for (int i=0; i<5; i++) {
            out.write("hello");
            out.newLine();
        }
        //3,关闭流
        out.close();
    }

```

### BufferedReader

---

```java
/*
 * BufferedReader 字符缓冲输入流
 * 
 * 方法：
 * 	String readLine() 
 * 需求：从文件中读取数据，并显示数据
 */

public static void main(String[] args) throws IOException {
    //1,创建流
    BufferedReader in = new BufferedReader(new FileReader("file.txt"));
    //2，读数据
    //一次一个字符
    //一次一个字符数组
    //一次读取文本中一行的字符串内容
    String line = null;
    while( (line = in.readLine()) != null ){
        System.out.println(line);
    }

    //3,关闭流
    in.close();
}
```
