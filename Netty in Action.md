---

> tree /F 输出某个文件夹下的所有目录和文件

```java
itstack-demo-netty-1-00
└── src
    ├── main
    │   └── java
    │       └── org.itstack.demo.netty
    │           ├── aio
    │           │   ├── client
    │           │   │   ├── AioClient.java
    │           │   │   └── AioClientHandler.java	
    │           │   ├── server
    │           │   │   ├── AioServer.java
    │           │   │   ├── AioServerChannelInitializer.java
    │           │   │   └── AioServerHandler.java
    │           │   ├── ChannelAdapter.java
    │           │   ├── ChannelHandler.java
    │           │   └── ChannelInitializer.java	
    │           ├── bio
    │           │   ├── client
    │           │   │   ├── BioClient.java
    │           │   │   └── BioClientHandler.java	
    │           │   ├── server
    │           │   │   ├── BioServer.java
    │           │   │   └── BioServerHandler.java
    │           │   ├── ChannelAdapter.java
    │           │   └── ChannelHandler.java	
    │           └── nio
    │               ├── client
    │               │   ├── NioClient.java
    │               │   └── NioClientHandler.java	
    │               ├── server
    │               │   ├── NioServer.java
    │               │   └── NioServerHandler.java
    │               ├── ChannelAdapter.java
    │               └── ChannelHandler.java	
    └── test
         └── java
             └── org.itstack.demo.test
                 └── ApiTest.java
```


## Chapter 1 Netty and Java NIO APIS

---

主要内容

- netty架构
- 为什么我们需要NIO
- 阻塞 vs 非阻塞
- 已知的JDK的NIO问题和Netty的解决方案

Netty api is asynchronous-netty是异步的

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650884728694-318a9380-ed87-45e8-a345-5fb235d843ab.png#clientId=ua8641013-0a0a-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=384&id=u76a46a3f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=384&originWidth=570&originalType=binary&ratio=1&rotation=0&showTitle=false&size=195590&status=done&style=none&taskId=u70ac61cf-9075-4245-9d4f-217807dc1d9&title=&width=570)

实现同步

- Callback
- Futures
```java
ExecutorServce executor = Executors.newCachedThreadPool()
Runnable task1 = new Runnable(){
    @override
    public void run() {
        doSomeHeavyWork();
    }
}

Runnable task2 = new Runnable(){
    @override
    public void run() {
        doSomeHeavyWorkWithResult();
    }
}


Future<？> future1 = executor.submit(task1);
Future<Integer> future2 = executor.submit(task2);
while (!future1.isDone() || !future2.isDone()){
    ...
    // do something else
    ...
}
```


### Blocking IO
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650887292437-c59183ff-224a-48bf-aa5d-dc97ead77382.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=260&id=u8d47ee58&margin=%5Bobject%20Object%5D&name=image.png&originHeight=325&originWidth=623&originalType=binary&ratio=1&rotation=0&showTitle=false&size=48779&status=done&style=none&taskId=u048d0ceb-7042-492b-8872-28d4588e883&title=&width=498.4)
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.net.ServerSocket;
import java.net.Socket;

public class PlainEchoServer {
  public static void serve(int port) throws IOException {
    final ServerSocket socket = new ServerSocket(port);
    try {
      while (true) {
        final Socket clientSocket = socket.accept();
        System.out.println("Accept connect from " + clientSocket);
        new Thread(new Runnable() {
          @Override
          public void run() {
            // TODO Auto-generated method stub
            try {
              BufferedReader reader = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
              PrintWriter writer = new PrintWriter(clientSocket.getOutputStream(), true);
              while (true) {
                writer.println(reader.readLine());
                writer.flush();
              }

            } catch (IOException e) {
              e.printStackTrace();
              try {
                clientSocket.close();
              } catch (IOException ex) {

              }
            }

          }
        }).start();
      }

    } catch (Exception e) {
      e.printStackTrace();
    }
  }
  public static void main(String[] args) {
    try{
      PlainEchoServer.serve(3309);
    }catch(IOException e){

    }
  }
}
```
> telnet 127.0.0.1 3309, 可以用来测试连接

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650888129010-6e469fc3-c73c-4d05-969a-e6ab9a80e380.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=138&id=ud14cea6b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=173&originWidth=222&originalType=binary&ratio=1&rotation=0&showTitle=false&size=2924&status=done&style=none&taskId=u9366e482-a818-4af8-b042-b0a56610b54&title=&width=177.6)



### Non-blocking IO
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650887320928-bcd1ff7e-9598-41c0-8b58-f87c2a97f8b3.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=388&id=u382055e2&margin=%5Bobject%20Object%5D&name=image.png&originHeight=485&originWidth=533&originalType=binary&ratio=1&rotation=0&showTitle=false&size=46637&status=done&style=none&taskId=u9f0abf0d-98aa-47a6-9737-4de754c890c&title=&width=426.4)



---



## 黑马Netty

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650889214166-6e62eb14-1f95-48f5-99f0-953f00d839b6.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=337&id=u0e53c2b4&margin=%5Bobject%20Object%5D&name=image.png&originHeight=421&originWidth=1189&originalType=binary&ratio=1&rotation=0&showTitle=false&size=502966&status=done&style=none&taskId=u2a110eec-c4fa-45f0-ac3d-cb42c010b67&title=&width=951.2)


## NIO基础

---


#### Channel 

---

- FileChannnel
- DatagramChannel(UDP)
- SocketChannel(TCP )
- ServerSocketChannel(TCP)


#### Buffer

---

- ByteBuffer

-MappedByteBuffer
-DirectByteBuffer
-HeapByteBuffer

- ShortBuffer

...


#### Selector

---

多线程版

- 内存占用高
- 线程上下文切换成本高
- 只适合连接数较少

线程池版

- 阻塞模式下，线程仅能处理一个socket连接
- 仅适合短连接场景

Selector版
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650890132141-4a247f98-4c1c-4fd8-a101-9c43860425fe.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=292&id=ue76c5e58&margin=%5Bobject%20Object%5D&name=image.png&originHeight=365&originWidth=563&originalType=binary&ratio=1&rotation=0&showTitle=false&size=103444&status=done&style=none&taskId=ua52f58a9-a3c2-43f3-a9ca-67a9971f936&title=&width=450.4)



## ByteBuffer

---

netty-demo

- pom
```java
<dependencies>
        <dependency>
            <groupId>io.netty</groupId>
            <artifactId>netty-all</artifactId>
            <version>4.1.39.Final</version>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.16.18</version>
        </dependency>
        <dependency>
            <groupId>com.google.code.gson</groupId>
            <artifactId>gson</artifactId>
            <version>2.8.5</version>
        </dependency>
        <dependency>
            <groupId>com.google.guava</groupId>
            <artifactId>guava</artifactId>
            <version>19.0</version>
        </dependency>
        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
            <version>1.2.3</version>
        </dependency>

    </dependencies>
```

- 测试
```java
package com.meehom.netty.c1;

import lombok.extern.slf4j.Slf4j;

import java.io.FileInputStream;
import java.io.IOException;
import java.nio.ByteBuffer;
import java.nio.channels.FileChannel;

/**
 * @author meehom
 * @data 2022/4/25 - 20:44
 */
@Slf4j
public class TestByteBuffer {
	public static void main(String[] args) {
		// FileChannel
		// 1. 输入输出流 2.RandomAccessFile
		try {
			FileChannel channel = new FileInputStream("netty-demo/data.txt").getChannel();
			// 准备缓冲区
			ByteBuffer buffer = ByteBuffer.allocate(10);
			while (true) {
				// 读取数据， 向buffer中写
				int len = channel.read(buffer);
				log.debug("读取到的字节{}", len);
				if (len == -1){
					break;
				}
				// 打印Buffer内同
				buffer.flip(); // 切换到读模式
				while (buffer.hasRemaining()){
					byte b = buffer.get();
					//System.out.println((char) b);
					log.debug("实际字节{}", (char) b);
				}

				// 切换成写模式
				buffer.clear();
			}

		} catch (IOException e) {
			e.printStackTrace();
		}
	}
}
```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650892234173-ad4705cc-1630-43dc-a55a-5b3ec51b61ba.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=249&id=uccccc2b0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=311&originWidth=592&originalType=binary&ratio=1&rotation=0&showTitle=false&size=167463&status=done&style=none&taskId=ufa7d5dba-1ac4-4553-86dd-48a06dd5f7c&title=&width=473.6)

### ByteBuffer结构

- capacity
- position
- limit

##### flip
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650892362458-993150ce-bfda-486f-b356-2c8b5fd6b381.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=466&id=u26fed223&margin=%5Bobject%20Object%5D&name=image.png&originHeight=582&originWidth=1062&originalType=binary&ratio=1&rotation=0&showTitle=false&size=218410&status=done&style=none&taskId=ue6516362-7726-4c50-befe-3a2b93278bf&title=&width=849.6)


##### clear
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650892463825-99cadb6f-1037-43c4-bed2-d2bba25e79b6.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=516&id=u916f7b25&margin=%5Bobject%20Object%5D&name=image.png&originHeight=645&originWidth=994&originalType=binary&ratio=1&rotation=0&showTitle=false&size=188155&status=done&style=none&taskId=ue44c2f2c-42ce-4291-9230-e9690fcce8f&title=&width=795.2)

##### compact
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650892490165-268fe477-7cd6-455f-abcb-b60c9f5affb6.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=287&id=u80738438&margin=%5Bobject%20Object%5D&name=image.png&originHeight=359&originWidth=1134&originalType=binary&ratio=1&rotation=0&showTitle=false&size=253019&status=done&style=none&taskId=u55b9c253-ba7b-428f-adc1-49c6f37ebf3&title=&width=907.2)


### ByteBuffer工具类
```java
package com.meehom.netty.c1;

import java.nio.ByteBuffer;

import io.netty.util.internal.MathUtil;
import io.netty.util.internal.StringUtil;
import io.netty.util.internal.MathUtil.*;


/**
 * @author Panwen Chen
 * @date 2021/4/12 15:59
 */
public class ByteBufferUtil {
	private static final char[] BYTE2CHAR = new char[256];
	private static final char[] HEXDUMP_TABLE = new char[256 * 4];
	private static final String[] HEXPADDING = new String[16];
	private static final String[] HEXDUMP_ROWPREFIXES = new String[65536 >>> 4];
	private static final String[] BYTE2HEX = new String[256];
	private static final String[] BYTEPADDING = new String[16];

	static {
		final char[] DIGITS = "0123456789abcdef".toCharArray();
		for (int i = 0; i < 256; i++) {
			HEXDUMP_TABLE[i << 1] = DIGITS[i >>> 4 & 0x0F];
			HEXDUMP_TABLE[(i << 1) + 1] = DIGITS[i & 0x0F];
		}

		int i;

		// Generate the lookup table for hex dump paddings
		for (i = 0; i < HEXPADDING.length; i++) {
			int padding = HEXPADDING.length - i;
			StringBuilder buf = new StringBuilder(padding * 3);
			for (int j = 0; j < padding; j++) {
				buf.append("   ");
			}
			HEXPADDING[i] = buf.toString();
		}

		// Generate the lookup table for the start-offset header in each row (up to 64KiB).
		for (i = 0; i < HEXDUMP_ROWPREFIXES.length; i++) {
			StringBuilder buf = new StringBuilder(12);
			buf.append(StringUtil.NEWLINE);
			buf.append(Long.toHexString(i << 4 & 0xFFFFFFFFL | 0x100000000L));
			buf.setCharAt(buf.length() - 9, '|');
			buf.append('|');
			HEXDUMP_ROWPREFIXES[i] = buf.toString();
		}

		// Generate the lookup table for byte-to-hex-dump conversion
		for (i = 0; i < BYTE2HEX.length; i++) {
			BYTE2HEX[i] = ' ' + StringUtil.byteToHexStringPadded(i);
		}

		// Generate the lookup table for byte dump paddings
		for (i = 0; i < BYTEPADDING.length; i++) {
			int padding = BYTEPADDING.length - i;
			StringBuilder buf = new StringBuilder(padding);
			for (int j = 0; j < padding; j++) {
				buf.append(' ');
			}
			BYTEPADDING[i] = buf.toString();
		}

		// Generate the lookup table for byte-to-char conversion
		for (i = 0; i < BYTE2CHAR.length; i++) {
			if (i <= 0x1f || i >= 0x7f) {
				BYTE2CHAR[i] = '.';
			} else {
				BYTE2CHAR[i] = (char) i;
			}
		}
	}

	/**
	 * 打印所有内容
	 * @param buffer
	 */
	public static void debugAll(ByteBuffer buffer) {
		int oldlimit = buffer.limit();
		buffer.limit(buffer.capacity());
		StringBuilder origin = new StringBuilder(256);
		appendPrettyHexDump(origin, buffer, 0, buffer.capacity());
		System.out.println("+--------+-------------------- all ------------------------+----------------+");
		System.out.printf("position: [%d], limit: [%d]\n", buffer.position(), oldlimit);
		System.out.println(origin);
		buffer.limit(oldlimit);
	}

	/**
	 * 打印可读取内容
	 * @param buffer
	 */
	public static void debugRead(ByteBuffer buffer) {
		StringBuilder builder = new StringBuilder(256);
		appendPrettyHexDump(builder, buffer, buffer.position(), buffer.limit() - buffer.position());
		System.out.println("+--------+-------------------- read -----------------------+----------------+");
		System.out.printf("position: [%d], limit: [%d]\n", buffer.position(), buffer.limit());
		System.out.println(builder);
	}

	private static void appendPrettyHexDump(StringBuilder dump, ByteBuffer buf, int offset, int length) {
		if (MathUtil.isOutOfBounds(offset, length, buf.capacity())) {
			throw new IndexOutOfBoundsException(
					"expected: " + "0 <= offset(" + offset + ") <= offset + length(" + length
							+ ") <= " + "buf.capacity(" + buf.capacity() + ')');
		}
		if (length == 0) {
			return;
		}
		dump.append(
				"         +-------------------------------------------------+" +
						StringUtil.NEWLINE + "         |  0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f |" +
						StringUtil.NEWLINE + "+--------+-------------------------------------------------+----------------+");

		final int startIndex = offset;
		final int fullRows = length >>> 4;
		final int remainder = length & 0xF;

		// Dump the rows which have 16 bytes.
		for (int row = 0; row < fullRows; row++) {
			int rowStartIndex = (row << 4) + startIndex;

			// Per-row prefix.
			appendHexDumpRowPrefix(dump, row, rowStartIndex);

			// Hex dump
			int rowEndIndex = rowStartIndex + 16;
			for (int j = rowStartIndex; j < rowEndIndex; j++) {
				dump.append(BYTE2HEX[getUnsignedByte(buf, j)]);
			}
			dump.append(" |");

			// ASCII dump
			for (int j = rowStartIndex; j < rowEndIndex; j++) {
				dump.append(BYTE2CHAR[getUnsignedByte(buf, j)]);
			}
			dump.append('|');
		}

		// Dump the last row which has less than 16 bytes.
		if (remainder != 0) {
			int rowStartIndex = (fullRows << 4) + startIndex;
			appendHexDumpRowPrefix(dump, fullRows, rowStartIndex);

			// Hex dump
			int rowEndIndex = rowStartIndex + remainder;
			for (int j = rowStartIndex; j < rowEndIndex; j++) {
				dump.append(BYTE2HEX[getUnsignedByte(buf, j)]);
			}
			dump.append(HEXPADDING[remainder]);
			dump.append(" |");

			// Ascii dump
			for (int j = rowStartIndex; j < rowEndIndex; j++) {
				dump.append(BYTE2CHAR[getUnsignedByte(buf, j)]);
			}
			dump.append(BYTEPADDING[remainder]);
			dump.append('|');
		}

		dump.append(StringUtil.NEWLINE +
				"+--------+-------------------------------------------------+----------------+");
	}

	private static void appendHexDumpRowPrefix(StringBuilder dump, int row, int rowStartIndex) {
		if (row < HEXDUMP_ROWPREFIXES.length) {
			dump.append(HEXDUMP_ROWPREFIXES[row]);
		} else {
			dump.append(StringUtil.NEWLINE);
			dump.append(Long.toHexString(rowStartIndex & 0xFFFFFFFFL | 0x100000000L));
			dump.setCharAt(dump.length() - 9, '|');
			dump.append('|');
		}
	}

	public static short getUnsignedByte(ByteBuffer buffer, int index) {
		return (short) (buffer.get(index) & 0xFF);
	}
}

```

- 测试
```java
public class TestByteBufferReadWriter {
	public static void main(String[] args) {
		ByteBuffer buffer = ByteBuffer.allocate(10);
		buffer.put((byte) 0x61);//a
		debugAll(buffer);
	}
}
```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650892974121-04c7ec01-168c-47c1-a64a-4bd2dbddcbcf.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=193&id=u7308f51c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=241&originWidth=1430&originalType=binary&ratio=1&rotation=0&showTitle=false&size=22351&status=done&style=none&taskId=u2b976a0e-e4c8-4afa-b168-fd90c599d89&title=&width=1144)



### ByteBuffer其他常用方法

---

- ByteBuffer.allocate()

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650893178010-f6193a5c-dd32-47f0-b313-1cb9aa586a2a.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=254&id=u3dc293b9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=317&originWidth=850&originalType=binary&ratio=1&rotation=0&showTitle=false&size=192736&status=done&style=none&taskId=u67dc5d96-3c10-400c-a30a-51b29183230&title=&width=680)

- 堆内存，读写效率低，受到GC影响
- 直接内存（系统内存），读写效率高（少一次拷贝）, 不会受到GC影响，分配效率低，且可能导致内存泄漏

- ByteBuffer.put()
- channel.read(bytebuffer)
- channel.write(bytebuffer)
- bytebuffer.get()

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650893481173-b1001db4-c1b6-4f2d-9d94-f8205e917b67.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=186&id=u2b72bbd8&margin=%5Bobject%20Object%5D&name=image.png&originHeight=233&originWidth=1229&originalType=binary&ratio=1&rotation=0&showTitle=false&size=145082&status=done&style=none&taskId=u8faa9f26-0a92-43fb-bd88-c27d0a694d6&title=&width=983.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650893653797-b6419d81-f5ab-42db-811a-c0a2f72fa4dd.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=270&id=u3b6b11c6&margin=%5Bobject%20Object%5D&name=image.png&originHeight=338&originWidth=881&originalType=binary&ratio=1&rotation=0&showTitle=false&size=255623&status=done&style=none&taskId=uc04133ad-a4a9-4e06-a112-4dffbe78fae&title=&width=704.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650893681822-a6fca421-1075-4407-b6be-5d250f19d25c.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=94&id=u42a6a07f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=117&originWidth=628&originalType=binary&ratio=1&rotation=0&showTitle=false&size=52189&status=done&style=none&taskId=u734d0d4b-1622-4ea8-985c-221f3a5ef92&title=&width=502.4)


### 字符串和ByteBuffer的转换

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650893891012-f31c4424-1361-4e4d-ac8d-ad9c7a253db1.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=363&id=ueff991b1&margin=%5Bobject%20Object%5D&name=image.png&originHeight=454&originWidth=882&originalType=binary&ratio=1&rotation=0&showTitle=false&size=240066&status=done&style=none&taskId=u63b6a3f9-ad35-4a1c-a3b9-ab89ec7d7c1&title=&width=705.6)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650893953266-966244b8-af8d-4ff5-944e-b152b36e097f.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=177&id=ufc733646&margin=%5Bobject%20Object%5D&name=image.png&originHeight=221&originWidth=798&originalType=binary&ratio=1&rotation=0&showTitle=false&size=143300&status=done&style=none&taskId=uc95d3573-bc6e-4321-bf5c-8fdff7580c5&title=&width=638.4)

### Scattering Reads

---

分散读取
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650894076936-188c50dc-6f43-4c2a-8865-55f1032f7180.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=435&id=u37d6ef13&margin=%5Bobject%20Object%5D&name=image.png&originHeight=544&originWidth=1200&originalType=binary&ratio=1&rotation=0&showTitle=false&size=287444&status=done&style=none&taskId=u2be6acf5-520e-49bd-b756-ac9e541af34&title=&width=960)
集中写入
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650894165646-c013dda8-ed45-461d-bb51-3ecbcef1d610.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=305&id=udef81deb&margin=%5Bobject%20Object%5D&name=image.png&originHeight=381&originWidth=1181&originalType=binary&ratio=1&rotation=0&showTitle=false&size=287947&status=done&style=none&taskId=ubd1ba9a1-99f5-4231-b276-c247a302ddd&title=&width=944.8)

### 粘包和半包分析

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650894257360-285fd804-005b-4220-84a1-eb90992eaf36.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=319&id=u534a1de7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=399&originWidth=859&originalType=binary&ratio=1&rotation=0&showTitle=false&size=219436&status=done&style=none&taskId=ua4b72510-0995-4fa4-8080-b8580f96057&title=&width=687.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650894671377-dd212bcd-8713-41e9-b10b-02fe927a6cf3.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=682&id=ucfef2d1a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=852&originWidth=1058&originalType=binary&ratio=1&rotation=0&showTitle=false&size=480161&status=done&style=none&taskId=u38008b87-50ad-4823-9659-3ec6917b51d&title=&width=846.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650894699975-895746b7-ae6f-4f29-9ade-a69803ff9e1a.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=424&id=u8b135686&margin=%5Bobject%20Object%5D&name=image.png&originHeight=530&originWidth=930&originalType=binary&ratio=1&rotation=0&showTitle=false&size=341792&status=done&style=none&taskId=ua35c8e31-8c84-4608-b2a8-a3686a43320&title=&width=744)


## 文件编程
> FileChannel只工作在阻塞模式下

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650894839785-ec2f9388-a0f0-48c1-a89d-29e2c999e427.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=249&id=u6fe18695&margin=%5Bobject%20Object%5D&name=image.png&originHeight=311&originWidth=1111&originalType=binary&ratio=1&rotation=0&showTitle=false&size=232977&status=done&style=none&taskId=u3f165ba9-5333-4a79-bc2c-c770b05f677&title=&width=888.8)

### TransferTo（效率比文件输入输出流高）

---

> bug: 文件最多传输2g数据

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650895056205-13e07f5a-69f3-498d-9282-fd1d6c440306.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=295&id=u322babb3&margin=%5Bobject%20Object%5D&name=image.png&originHeight=369&originWidth=1019&originalType=binary&ratio=1&rotation=0&showTitle=false&size=221914&status=done&style=none&taskId=u3131ef99-d99b-4af7-9a8f-4240d1e34dc&title=&width=815.2)
文件大于2g改进
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650895228847-1074c003-4dd5-4027-9978-5bdee5854f74.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=454&id=ud8ad0369&margin=%5Bobject%20Object%5D&name=image.png&originHeight=567&originWidth=1071&originalType=binary&ratio=1&rotation=0&showTitle=false&size=307578&status=done&style=none&taskId=ue567ec64-826f-42ec-a6cc-c4524dadb9e&title=&width=856.8)

### Path

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650895352114-31730305-7129-42ed-887e-65853b6b1f94.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=448&id=u406e9182&margin=%5Bobject%20Object%5D&name=image.png&originHeight=560&originWidth=1178&originalType=binary&ratio=1&rotation=0&showTitle=false&size=177344&status=done&style=none&taskId=u16150134-07d1-4079-8f21-6f4429390fc&title=&width=942.4)

### Files

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650895401784-0a5fc4e0-0b66-437f-bfd0-6c6c1d01421b.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=518&id=u08f393c7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=648&originWidth=872&originalType=binary&ratio=1&rotation=0&showTitle=false&size=305387&status=done&style=none&taskId=u3f72b106-3400-45f0-9495-52e552e0f88&title=&width=697.6)


### WalkFile

---

- 遍历目录和文件

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650895623207-947dd7c7-4044-4f4d-bf27-5d5d12804b96.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=586&id=u69639bfa&margin=%5Bobject%20Object%5D&name=image.png&originHeight=732&originWidth=1301&originalType=binary&ratio=1&rotation=0&showTitle=false&size=550137&status=done&style=none&taskId=u4c3d5366-451e-4ba2-bd58-c00603e39d5&title=&width=1040.8)

- 删除文件夹和目录

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650895854976-d92e6c1b-754c-44a6-bdaa-d0237bed4c18.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=502&id=uf0290d32&margin=%5Bobject%20Object%5D&name=image.png&originHeight=627&originWidth=1254&originalType=binary&ratio=1&rotation=0&showTitle=false&size=410408&status=done&style=none&taskId=u4de6480e-26de-498d-9788-1fd9e397a8c&title=&width=1003.2)

- 拷贝多级目录

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650896034305-c63fdbe9-3efd-49d4-95db-8c9bf40a43ba.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=573&id=uaf43f740&margin=%5Bobject%20Object%5D&name=image.png&originHeight=716&originWidth=897&originalType=binary&ratio=1&rotation=0&showTitle=false&size=350410&status=done&style=none&taskId=u8bc1c3f5-b904-49be-860e-e26d5468b3e&title=&width=717.6)


## 网络编程

---

### 阻塞

- server

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650896350357-f028693a-e2fd-4cb2-9b94-33d60b3f58a5.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=627&id=u5c7d2d4d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=784&originWidth=879&originalType=binary&ratio=1&rotation=0&showTitle=false&size=378424&status=done&style=none&taskId=u9688c724-0cb4-4c8a-aeb9-f27443f7823&title=&width=703.2)

- client

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650896494350-178fad2a-8101-41e2-af17-ee672facea31.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=210&id=u418b6534&margin=%5Bobject%20Object%5D&name=image.png&originHeight=262&originWidth=867&originalType=binary&ratio=1&rotation=0&showTitle=false&size=158390&status=done&style=none&taskId=u5807786e-2349-462b-b233-01c97513699&title=&width=693.6)

- 细节（accept与read都是阻塞方法）

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650896684342-d30dbbe3-8656-4b7e-a27a-0126e46f5878.png#clientId=u9e948f9d-d465-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=357&id=u72c48d04&margin=%5Bobject%20Object%5D&name=image.png&originHeight=446&originWidth=736&originalType=binary&ratio=1&rotation=0&showTitle=false&size=280440&status=done&style=none&taskId=uce855de6-f243-4cff-b9e0-1747531a256&title=&width=588.8)
阻塞住就不能干别的事情：

- 如果一个客户端连接完了，发送信息完了，服务器会出在等待连接状态，然后这个客户端继续发送数据也会阻塞，必须等第二个连接完成后才能处理数据
- 单线程处理多个连接问题很大

### 非阻塞

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650897231812-1f78d29c-71c8-4803-9df8-2bdcdb122edc.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=726&id=u0be73ea5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=907&originWidth=1218&originalType=binary&ratio=1&rotation=0&showTitle=false&size=568690&status=done&style=none&taskId=u6186b358-61dc-441f-ae30-9dd40df85f1&title=&width=974.4)
线程一直转，非常忙碌


### Selector

---

事件类型

- accept--服务器连接请求出发
- connect--客户端连接建立后触发
- read--可读事件
- write--可写事件

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650897989397-49e93404-62b2-4e53-82b6-ef15eeb59e3f.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=699&id=u9cb60c3d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=874&originWidth=966&originalType=binary&ratio=1&rotation=0&showTitle=false&size=518053&status=done&style=none&taskId=u10e3c1f6-48c5-466d-b94d-766217de913&title=&width=772.8)
selector事件未处理时不会阻塞


read
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650898331542-2f5f8d43-ee5f-4d9f-8f9b-ff03438f19a3.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=684&id=ub57ef67e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=855&originWidth=1111&originalType=binary&ratio=1&rotation=0&showTitle=false&size=660937&status=done&style=none&taskId=uef873652-c4d1-485c-9c69-6f328924189&title=&width=888.8)
有报错
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650898558244-e1139f2c-4d62-4d66-8561-714489fec42b.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=309&id=ue098b186&margin=%5Bobject%20Object%5D&name=image.png&originHeight=386&originWidth=884&originalType=binary&ratio=1&rotation=0&showTitle=false&size=156367&status=done&style=none&taskId=u84a064e8-c3b0-450e-9fb2-6ba2beb75ca&title=&width=707.2)
处理完key需要手动移除这个key
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650898628479-00ba659a-a2ad-435c-940c-cb63e7c5eba2.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=417&id=ub23f5b1b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=521&originWidth=851&originalType=binary&ratio=1&rotation=0&showTitle=false&size=389611&status=done&style=none&taskId=uc897a67c-ee89-4e15-9dc7-2b915549a2b&title=&width=680.8)
处理客户端正常断开和异常断开
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650898824030-3bf6d31e-46bc-4686-b76d-77d169209f7f.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=429&id=u0df7347f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=536&originWidth=1202&originalType=binary&ratio=1&rotation=0&showTitle=false&size=328610&status=done&style=none&taskId=ub6cb3c6e-9485-422a-9482-ec7358e8077&title=&width=961.6)


消息边界问题

- 固定消息长度
- 分隔符
- LTV格式，长度(L)+类型(T)+内容(V)

以上粘包分包处理，如果单个消息长度大于bytebuffer，则需要扩容

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650899339301-6ead4058-4b14-46e9-aa9c-263bd7c3bd48.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=521&id=u6e362e53&margin=%5Bobject%20Object%5D&name=image.png&originHeight=651&originWidth=1169&originalType=binary&ratio=1&rotation=0&showTitle=false&size=210551&status=done&style=none&taskId=ufac1dde9-3c45-44e6-909d-159f362a510&title=&width=935.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650899540342-ef095d30-142b-49a6-b30e-f49b679a66e9.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=561&id=u15e53006&margin=%5Bobject%20Object%5D&name=image.png&originHeight=701&originWidth=1070&originalType=binary&ratio=1&rotation=0&showTitle=false&size=500740&status=done&style=none&taskId=uf4939219-a488-43a3-a96d-013c67de444&title=&width=856)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650899659636-8e52f04a-764f-40c3-92ab-531638a475eb.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=359&id=uf622f177&margin=%5Bobject%20Object%5D&name=image.png&originHeight=449&originWidth=1189&originalType=binary&ratio=1&rotation=0&showTitle=false&size=493275&status=done&style=none&taskId=u4c3c5b17-f58b-4c73-aec8-4ae749a6646&title=&width=951.2)


write方法
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650899802470-7f94fb27-e9ca-40ab-b67d-f9269743ad12.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=682&id=u3f6328f5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=853&originWidth=1153&originalType=binary&ratio=1&rotation=0&showTitle=false&size=516707&status=done&style=none&taskId=uea524789-104d-492e-b294-21b4a3d4a5f&title=&width=922.4)
改进
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650900066988-28d06541-d226-4e3c-867a-d98d65f66e7f.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=641&id=uccda7a2f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=801&originWidth=955&originalType=binary&ratio=1&rotation=0&showTitle=false&size=462949&status=done&style=none&taskId=uc3bc2469-5bdc-461b-a8ab-f7ec268f929&title=&width=764)

### 多线程

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650900395287-cc8b6f72-34f1-40fe-9371-1139a51541fa.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=330&id=u38d8ac0d&margin=%5Bobject%20Object%5D&name=image.png&originHeight=413&originWidth=789&originalType=binary&ratio=1&rotation=0&showTitle=false&size=130002&status=done&style=none&taskId=ua4246c94-dd9b-4d25-b8c1-398a557b721&title=&width=631.2)

- boss连接
- worker1，worker2负责读写



## NIO和BIO对比

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650900762952-8a3cf615-2e85-4ed8-8af3-1a3f9ee36ccb.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=153&id=u9c022b31&margin=%5Bobject%20Object%5D&name=image.png&originHeight=191&originWidth=1063&originalType=binary&ratio=1&rotation=0&showTitle=false&size=180292&status=done&style=none&taskId=ue5f22d55-10c1-4342-9ac0-9190b1a6919&title=&width=850.4)

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650900893561-63905dd0-c992-4720-9914-8c5077b4620b.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=578&id=ue60a3737&margin=%5Bobject%20Object%5D&name=image.png&originHeight=723&originWidth=1202&originalType=binary&ratio=1&rotation=0&showTitle=false&size=305309&status=done&style=none&taskId=u5a0e29c4-1295-462d-82f6-fc6e9365f0a&title=&width=961.6)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650901205602-5e5556ae-ad61-42d4-bb99-1f0d1d6106b3.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=242&id=u6ce96713&margin=%5Bobject%20Object%5D&name=image.png&originHeight=303&originWidth=889&originalType=binary&ratio=1&rotation=0&showTitle=false&size=143020&status=done&style=none&taskId=u645ecd4b-3c97-421c-9843-636547bcb69&title=&width=711.2)
同步阻塞
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650901276925-bbd76fe1-d307-45de-aeb6-402b3993ae14.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=523&id=ud15eb591&margin=%5Bobject%20Object%5D&name=image.png&originHeight=654&originWidth=623&originalType=binary&ratio=1&rotation=0&showTitle=false&size=236446&status=done&style=none&taskId=u0cb9fbf8-e21e-440e-9c7e-b31389280ad&title=&width=498.4)

同步非阻塞
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650901300225-b15f4621-3ba0-4f4c-b925-ef68ddce3f30.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=294&id=u1ff897d5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=367&originWidth=609&originalType=binary&ratio=1&rotation=0&showTitle=false&size=138122&status=done&style=none&taskId=u9fbde666-98f3-4637-bcf2-a18e492bc7d&title=&width=487.2)

同步多路复用

异步非阻塞（不存在阻塞）
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650901376836-0776a3ab-dfd8-4b58-a2bc-0c62f97ec860.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=286&id=u65642d63&margin=%5Bobject%20Object%5D&name=image.png&originHeight=357&originWidth=608&originalType=binary&ratio=1&rotation=0&showTitle=false&size=144745&status=done&style=none&taskId=u31c3bb24-f91f-4610-b96f-4f20d2e1740&title=&width=486.4)


### 零拷贝

---

传统模式
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650940299325-da0c0305-cb95-42ad-a2be-1697922c9d78.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=210&id=u8f85c76a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=263&originWidth=733&originalType=binary&ratio=1&rotation=0&showTitle=false&size=153805&status=done&style=none&taskId=u0805ad57-37aa-4951-879f-0901273c3bc&title=&width=586.4)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650940333813-5ee8d101-3968-4ee6-ae16-a24033409454.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=310&id=u26ae3bb0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=388&originWidth=698&originalType=binary&ratio=1&rotation=0&showTitle=false&size=142122&status=done&style=none&taskId=ua727841e-d221-489c-9173-8de186cfa07&title=&width=558.4)

- 用户态和内核态切换了3次
- 数据拷贝了4次

NIO优化
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650940481272-35ad0e92-f705-478d-9a6d-43348abdb17f.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=427&id=ud56a731e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=534&originWidth=1047&originalType=binary&ratio=1&rotation=0&showTitle=false&size=290912&status=done&style=none&taskId=u3e0cc5c5-872b-44b9-9631-fd13fcff44e&title=&width=837.6)

- 减少一次数据拷贝，内核态切换没减少

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650940541434-99c6821d-4572-4ada-b404-5fc28025b06d.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=403&id=uf3c27c3e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=504&originWidth=1138&originalType=binary&ratio=1&rotation=0&showTitle=false&size=365465&status=done&style=none&taskId=u98ca440e-1a69-40f4-9397-1b3498c7612&title=&width=910.4)

- 只发生了一次用户态和内核态切换

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650940643876-8c1b5626-91ba-4978-92fd-808e8cfd00a4.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=239&id=u3ba4ad05&margin=%5Bobject%20Object%5D&name=image.png&originHeight=299&originWidth=916&originalType=binary&ratio=1&rotation=0&showTitle=false&size=122247&status=done&style=none&taskId=u3d312fb5-58c8-4616-96f7-b037b13a5c0&title=&width=732.8)

- 切换一次，数据拷贝了两次

零拷贝指的是不需要拷贝到java内存中


### 异步IO（AIO）

---

![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650940930090-0f582eef-9d7c-4c1d-8188-4ffc5b5e5119.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=283&id=ub4530054&margin=%5Bobject%20Object%5D&name=image.png&originHeight=354&originWidth=1171&originalType=binary&ratio=1&rotation=0&showTitle=false&size=210497&status=done&style=none&taskId=u0e1bd4c0-498f-425e-b0d0-9faab5b865f&title=&width=936.8)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650941240718-d73107ea-3114-40bf-8d0b-e0f8b4b86aa0.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=694&id=uba9ed4dc&margin=%5Bobject%20Object%5D&name=image.png&originHeight=867&originWidth=1689&originalType=binary&ratio=1&rotation=0&showTitle=false&size=574758&status=done&style=none&taskId=u60f712eb-a674-4597-aaf4-84fe8e25621&title=&width=1351.2)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/27426792/1650941262731-d779220f-2f39-47fb-9b6c-72f4c463cc1c.png#clientId=u2b0b3e91-3802-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=234&id=udd53a0d7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=292&originWidth=900&originalType=binary&ratio=1&rotation=0&showTitle=false&size=200455&status=done&style=none&taskId=u34b68652-c943-470c-9ecb-2d28e3d22dd&title=&width=720)






## 


