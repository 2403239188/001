#Redis

##1.了解redis

redis是一款内存高速缓存数据库（磁盘IO--->内存）

	Redis 是完全开源免费的，遵守BSD协议，是一个高性能的key-value数据库。
	
	Redis 与其他 key - value 缓存产品有以下三个特点：
		Redis支持数据的持久化，可以将内存中的数据保存在磁盘中，重启的时候可以再次加载进行使用。
		Redis不仅仅支持简单的key-value类型的数据，同时还提供list，set，zset，hash等数据结构的存储。
		Redis支持数据的备份，即master-slave模式的数据备份。

##2.Redis 优势

	性能极高 – Redis能读的速度是110000次/s,写的速度是81000次/s 。
	
	丰富的数据类型 – Redis支持二进制案例的 Strings, Lists, Hashes, Sets 及 Ordered Sets 数据类型操作。
	
	原子 – Redis的所有操作都是原子性的，意思就是要么成功执行要么失败完全不执行。单个操作是原子性的。多个操作也支持事务，即原子性，通过MULTI和EXEC指令包起来。
	
	丰富的特性 – Redis还支持 publish/subscribe, 通知, key 过期等等特性。
	
##3.Redis与其他key-value存储有什么不同？

	Redis有着更为复杂的数据结构并且提供对他们的原子性操作，这是一个不同于其他数据库的进化路径。Redis的数据类型都是基于基本数据结构的同时对程序员透明，无需进行额外的抽象。
	
	Redis运行在内存中但是可以持久化到磁盘，所以在对不同数据集进行高速读写时需要权衡内存，因为数据量不能大于硬件内存。在内存数据库方面的另一个优点是，相比在磁盘上相同的复杂的数据结构，在内存中操作起来非常简单，这样Redis可以做很多内部复杂性很强的事情。同时，在磁盘格式方面他们是紧凑的以追加的方式产生的，因为他们并不需要进行随机访问。
	
	Redis单个文件的最大值时512M，memcache value最大值时1M。
	
##4.Redis适用场景

缓存分类：页面缓存（smart）、数据缓存

	页面缓存经常用到cms内存管理系统中
	数据缓存经常用到页面的具体数据中

	在开发过程中，页面的一些数据经常会被用到，并切短时间里不会发生变化，为了提高请求速度，降低网站负载，
	就把这些数据放到读取速度更高的介质上（或者通过更少的计算就可以得到数据），该行为就称为对数据的缓存。
	该介质可以是文件、数据库、内存（经常用于数据缓存）

	限时的优惠活动信息（秒杀、推荐、商品列表）	
	网站数据缓存（对于一些需要定时更新的数据，例如：积分排行榜）
		
		
##mac下redis的安装

	 1. 官网http://redis.io/ 下载最新的稳定版本,这里是3.2.0
	
	 2. sudo mv 到 /usr/local/
	
	 3. sudo tar -zxf redis-3.2.0.tar 解压文件
	
	 4. 进入解压后的目录 cd redis-3.2.0
	
	 5. sudo make test 测试编译
	
	 6. sudo make install 

	make完后 redis-2.8.17目录下会出现编译后的redis服务程序redis-server,
	还有用于测试的客户端程序redis-cli,两个程序位于安装目录 src 目录下：
	
	下面启动redis服务.
	
	$ cd src
	$ ./redis-server
	注意这种方式启动redis 使用的是默认配置。也可以通过启动参数告诉redis使用指定配置文件使用下面命令启动。
	
	$ cd src
	$ ./redis-server redis.conf
	redis.conf是一个默认的配置文件。我们可以根据需要使用自己的配置文件。
	
	查看 redis 是否启动？
	$ redis-cli
	以上命令将打开以下终端：
	
	redis 127.0.0.1:6379>
	127.0.0.1 是本机 IP ，6379 是 redis 服务端口。现在我们输入 PING 命令。
	
	redis 127.0.0.1:6379> ping
	PONG
	以上说明我们已经成功安装了redis。	

	启动redis服务进程后，就可以使用测试客户端程序redis-cli和redis服务交互了。 比如：
	
	$ cd src
	$ ./redis-cli
	redis> set foo bar
	OK
	redis> get foo
	"bar"

##Windows下安装Redis服务

Redis是有名的NoSql数据库，一般Linux都会默认支持。但在Windows环境中，可能需要手动安装设置才能有效使用。这里就简单介绍一下Windows下Redis服务的安装方法，希望能够帮到你。

	1、要安装Redis，首先要获取安装包。Windows的Redis安装包需要到以下GitHub链接找到。链接：https://github.com/MSOpenTech/redis。打开网站后，找到Release，点击前往下载页面。
	
	2、在下载网页中，找到最后发行的版本（此处是3.2.100）。找到Redis-x64-3.2.100.msi和Redis-x64-3.2.100.zip，点击下载。这里说明一下，第一个是msi微软格式的安装包，第二个是压缩包。
	
	3、双击刚下载好的msi格式的安装包（Redis-x64-3.2.100.msi）开始安装。
	
	4、选择“同意协议”，点击下一步继续。
	
	5、选择“添加Redis目录到环境变量PATH中”，这样方便系统自动识别Redis执行文件在哪里。
	6、端口号可保持默认的6379，并选择防火墙例外，从而保证外部可以正常访问Redis服务。
	7、设定最大值为100M。作为实验和学习，100M足够了。
	
	8、点击安装后，正式的安装过程开始。稍等一会即可完成。
	
	9、安装完毕后，需要先做一些设定工作，以便服务启动后能正常运行。使用文本编辑器，这里使用Notepad++，打开Redis服务配置文件。注意：不要找错了，通常为redis.windows-service.conf，而不是redis.windows.conf。后者是以非系统服务方式启动程序使用的配置文件。

	10、找到含有requirepass字样的地方，追加一行，输入requirepass 12345。这是访问Redis时所需的密码，一般测试情况下可以不用设定密码。不过，即使是作为本地访问，也建议设定一个密码。此处以简单的12345来演示。
	
	11、点击“开始”>右击“计算机”>选择“管理”。在左侧栏中依次找到并点击“计算机管理（本地）”>服务和应用程序>服务。再在右侧找到Redis名称的服务，查看启动情况。如未启动，则手动启动之。正常情况下，服务应该正常启动并运行了。

	12、最后来测试一下Redis是否正常提供服务。进入Redis的目录，cd C:\Program Files\Redis。输入redis-cli并回车。（redis-cli是客户端程序）如图正常提示进入，并显示正确端口号，则表示服务已经启动。
	 
	13、使用服务前需要先通过密码验证。输入“auth 12345”并回车（12345是之前设定的密码）。返回提示OK表示验证通过。
	
	14、实际测试一下读写。输入set mykey1 "I love you all!”并回车，用来保存一个键值。再输入get mykey1，获取刚才保存的键值。
	
	15、注意事项
	
	1.Windows使用的这个Redis是64位版本的，32位操作系统的同学就不要折腾了。
	
	2.作为服务运行的Redis配置文件，通常为redis.windows-service.conf，而不是redis.windows.conf。小心不要选错了。

##redis配置文件

	src目录下相关文件
		redis-cli        终端操作脚本
		redis-server     启动redis服务脚本文件
		redis-benchmark  压力测试文件
		redis-check-aof  检测备份文件脚本
		redis-check-dump 检测备份文件脚本
		
	编辑配置,可以通过修改 redis.conf 文件或使用 CONFIG set 命令来修改配置。
	redis.conf 配置项说明如下：

	1. Redis默认不是以守护进程的方式运行，可以通过该配置项修改，使用yes启用守护进程
	
	    daemonize no
	
	2. 当Redis以守护进程方式运行时，Redis默认会把pid写入/var/run/redis.pid文件，可以通过pidfile指定
	
	    pidfile /var/run/redis.pid
	
	3. 指定Redis监听端口，默认端口为6379，作者在自己的一篇博文中解释了为什么选用6379作为默认端口，因为6379在手机按键上MERZ对应的号码，而MERZ取自意大利歌女Alessia Merz的名字
	
	    port 6379
	
	4. 绑定的主机地址
	
	    bind 127.0.0.1
	
	5.当 客户端闲置多长时间后关闭连接，如果指定为0，表示关闭该功能
	
	    timeout 300
	
	6. 指定日志记录级别，Redis总共支持四个级别：debug、verbose、notice、warning，默认为verbose
	
	    loglevel verbose
	
	7. 日志记录方式，默认为标准输出，如果配置Redis为守护进程方式运行，而这里又配置为日志记录方式为标准输出，则日志将会发送给/dev/null
	
	    logfile stdout
	
	8. 设置数据库的数量，默认数据库为0，可以使用SELECT <dbid>命令在连接上指定数据库id
	
	    databases 16
	
	9. 指定在多长时间内，有多少次更新操作，就将数据同步到数据文件，可以多个条件配合
	
	    save <seconds> <changes>
	
	    Redis默认配置文件中提供了三个条件：
	
	    save 900 1
	
	    save 300 10
	
	    save 60 10000
	
	    分别表示900秒（15分钟）内有1个更改，300秒（5分钟）内有10个更改以及60秒内有10000个更改。
	
	 
	
	10. 指定存储至本地数据库时是否压缩数据，默认为yes，Redis采用LZF压缩，如果为了节省CPU时间，可以关闭该选项，但会导致数据库文件变的巨大
	
	    rdbcompression yes
	
	11. 指定本地数据库文件名，默认值为dump.rdb
	
	    dbfilename dump.rdb
	
	12. 指定本地数据库存放目录
	
	    dir ./
	
	13. 设置当本机为slav服务时，设置master服务的IP地址及端口，在Redis启动时，它会自动从master进行数据同步
	
	    slaveof <masterip> <masterport>
	
	14. 当master服务设置了密码保护时，slav服务连接master的密码
	
	    masterauth <master-password>
	
	15. 设置Redis连接密码，如果配置了连接密码，客户端在连接Redis时需要通过AUTH <password>命令提供密码，默认关闭
	
	    requirepass foobared
	
	16. 设置同一时间最大客户端连接数，默认无限制，Redis可以同时打开的客户端连接数为Redis进程可以打开的最大文件描述符数，如果设置 maxclients 0，表示不作限制。当客户端连接数到达限制时，Redis会关闭新的连接并向客户端返回max number of clients reached错误信息
	
	    maxclients 128
	
	17. 指定Redis最大内存限制，Redis在启动时会把数据加载到内存中，达到最大内存后，Redis会先尝试清除已到期或即将到期的Key，当此方法处理 后，仍然到达最大内存设置，将无法再进行写入操作，但仍然可以进行读取操作。Redis新的vm机制，会把Key存放内存，Value会存放在swap区
	
	    maxmemory <bytes>
	
	18. 指定是否在每次更新操作后进行日志记录，Redis在默认情况下是异步的把数据写入磁盘，如果不开启，可能会在断电时导致一段时间内的数据丢失。因为 redis本身同步数据文件是按上面save条件来同步的，所以有的数据会在一段时间内只存在于内存中。默认为no
	
	    appendonly no
	
	19. 指定更新日志文件名，默认为appendonly.aof
	
	     appendfilename appendonly.aof
	
	20. 指定更新日志条件，共有3个可选值： 
	    no：表示等操作系统进行数据缓存同步到磁盘（快） 
	    always：表示每次更新操作后手动调用fsync()将数据写到磁盘（慢，安全） 
	    everysec：表示每秒同步一次（折衷，默认值）
	
	    appendfsync everysec
	
	 
	
	21. 指定是否启用虚拟内存机制，默认值为no，简单的介绍一下，VM机制将数据分页存放，由Redis将访问量较少的页即冷数据swap到磁盘上，访问多的页面由磁盘自动换出到内存中（在后面的文章我会仔细分析Redis的VM机制）
	
	     vm-enabled no
	
	22. 虚拟内存文件路径，默认值为/tmp/redis.swap，不可多个Redis实例共享
	
	     vm-swap-file /tmp/redis.swap
	
	23. 将所有大于vm-max-memory的数据存入虚拟内存,无论vm-max-memory设置多小,所有索引数据都是内存存储的(Redis的索引数据 就是keys),也就是说,当vm-max-memory设置为0的时候,其实是所有value都存在于磁盘。默认值为0
	
	     vm-max-memory 0
	
	24. Redis swap文件分成了很多的page，一个对象可以保存在多个page上面，但一个page上不能被多个对象共享，vm-page-size是要根据存储的 数据大小来设定的，作者建议如果存储很多小对象，page大小最好设置为32或者64bytes；如果存储很大大对象，则可以使用更大的page，如果不 确定，就使用默认值
	
	     vm-page-size 32
	
	25. 设置swap文件中的page数量，由于页表（一种表示页面空闲或使用的bitmap）是在放在内存中的，，在磁盘上每8个pages将消耗1byte的内存。
	
	     vm-pages 134217728
	
	26. 设置访问swap文件的线程数,最好不要超过机器的核数,如果设置为0,那么所有对swap文件的操作都是串行的，可能会造成比较长时间的延迟。默认值为4
	
	     vm-max-threads 4
	
	27. 设置在向客户端应答时，是否把较小的包合并为一个包发送，默认为开启
	
	    glueoutputbuf yes
	
	28. 指定在超过一定的数量或者最大的元素超过某一临界值时，采用一种特殊的哈希算法
	
	    hash-max-zipmap-entries 64
	
	    hash-max-zipmap-value 512
	
	29. 指定是否激活重置哈希，默认为开启（后面在介绍Redis的哈希算法时具体介绍）
	
	    activerehashing yes
	
	30. 指定包含其它的配置文件，可以在同一主机上多个Redis实例之间使用同一份配置文件，而同时各个实例又拥有自己的特定配置文件
	
	    include /path/to/local.conf
	
##redis具体使用

	1.key的操作  除了空格、换行符 \n外，其他的字符基本都可以使用
	
	2.Redis keys 命令
	下表给出了与 Redis 键相关的基本命令：
	
	序号	命令及描述
	1	DEL key
	该命令用于在 key 存在时删除 key。
	2	DUMP key 
	序列化给定 key ，并返回被序列化的值。
	3	EXISTS key 
	检查给定 key 是否存在。
	4	EXPIRE key seconds
	为给定 key 设置过期时间。
	5	EXPIREAT key timestamp 
	EXPIREAT 的作用和 EXPIRE 类似，都用于为 key 设置过期时间。 不同在于 EXPIREAT 命令接受的时间参数是 UNIX 时间戳(unix timestamp)。
	6	PEXPIRE key milliseconds 
	设置 key 的过期时间以毫秒计。
	7	PEXPIREAT key milliseconds-timestamp 
	设置 key 过期时间的时间戳(unix timestamp) 以毫秒计
	8	KEYS pattern 
	查找所有符合给定模式( pattern)的 key 。
	9	MOVE key db 
	将当前数据库的 key 移动到给定的数据库 db 当中。
	10	PERSIST key 
	移除 key 的过期时间，key 将持久保持。
	11	PTTL key 
	以毫秒为单位返回 key 的剩余的过期时间。
	12	TTL key 
	以秒为单位，返回给定 key 的剩余生存时间(TTL, time to live)。
	13	RANDOMKEY 
	从当前数据库中随机返回一个 key 。
	14	RENAME key newkey 
	修改 key 的名称
	15	RENAMENX key newkey 
	仅当 newkey 不存在时，将 key 改名为 newkey 。
	16	TYPE key 
	返回 key 所储存的值的类型。
	
##java和redis的结合使用

 2.9.0 jar 版本下载： jedis-2.9.0.jar

连接到 redis 服务

实例

	import redis.clients.jedis.Jedis;
	 
	public class RedisJava {
	    public static void main(String[] args) {
	        //连接本地的 Redis 服务
	        //Jedis jedis = new Jedis("localhost");
 			Jedis jedis = new Jedis("localhost",6379);
       		jedis.auth("myRedis");   // 设置密码
	        System.out.println("连接成功");
	        //查看服务是否运行
	        System.out.println("服务正在运行: "+jedis.ping());
	    }
	}


Redis Java String(字符串) 实例

	实例
	import redis.clients.jedis.Jedis;
	 
	public class RedisStringJava {
	    public static void main(String[] args) {
	        //连接本地的 Redis 服务
	        Jedis jedis = new Jedis("localhost");
	        System.out.println("连接成功");
	        //设置 redis 字符串数据
	        jedis.set("runoobkey", "www.runoob.com");
	        // 获取存储的数据并输出
	        System.out.println("redis 存储的字符串为: "+ jedis.get("runoobkey"));
	    }
	}

Redis Java List(列表) 实例

	实例
	import java.util.List;
	import redis.clients.jedis.Jedis;
	 
	public class RedisListJava {
	    public static void main(String[] args) {
	        //连接本地的 Redis 服务
	        Jedis jedis = new Jedis("localhost");
	        System.out.println("连接成功");
	        //存储数据到列表中
	        jedis.lpush("site-list", "Runoob");
	        jedis.lpush("site-list", "Google");
	        jedis.lpush("site-list", "Taobao");
	        // 获取存储的数据并输出
	        List<String> list = jedis.lrange("site-list", 0 ,2);
	        for(int i=0; i<list.size(); i++) {
	            System.out.println("列表项为: "+list.get(i));
	        }
	    }
	}
		
Redis Java Keys 实例

	实例
	import java.util.Iterator;
	import java.util.Set;
	import redis.clients.jedis.Jedis;
	 
	public class RedisKeyJava {
	    public static void main(String[] args) {
	        //连接本地的 Redis 服务
	        Jedis jedis = new Jedis("localhost");
	        System.out.println("连接成功");
	 
	        // 获取数据并输出
	        Set<String> keys = jedis.keys("*"); 
	        Iterator<String> it=keys.iterator() ;   
	        while(it.hasNext()){   
	            String key = it.next();   
	            System.out.println(key);   
	        }
	    }
	}
	
	
##使用redis连接池

###redis连接池工具类

	import redis.clients.jedis.Jedis;
	import redis.clients.jedis.JedisPool;
	import redis.clients.jedis.JedisPoolConfig;
	
	public class RedisUtil {
    //Redis服务器IP
    private static String ADDR = "127.0.0.1";

    //Redis的端口号
    private static int PORT = 6379;

    //访问密码
    private static String AUTH = "qingyun";

    //可用连接实例的最大数目，默认值为8；
    //如果赋值为-1，则表示不限制；如果pool已经分配了maxActive个jedis实例，则此时pool的状态为exhausted(耗尽)。
    private static int MAX_ACTIVE = 1024;

    //控制一个pool最多有多少个状态为idle(空闲的)的jedis实例，默认值也是8。
    private static int MAX_IDLE = 200;

    //等待可用连接的最大时间，单位毫秒，默认值为-1，表示永不超时。如果超过等待时间，则直接抛出JedisConnectionException；
    private static int MAX_WAIT = 10000;

    private static int TIMEOUT = 10000;

    //在borrow一个jedis实例时，是否提前进行validate操作；如果为true，则得到的jedis实例均是可用的；
    private static boolean TEST_ON_BORROW = true;

    private static JedisPool jedisPool = null;

    /**
     * 初始化Redis连接池
     */
    static {
        try {
            JedisPoolConfig config = new JedisPoolConfig();
            config.setMaxTotal(MAX_ACTIVE);
            config.setMaxIdle(MAX_IDLE);
            config.setMaxWaitMillis(MAX_WAIT);
            config.setTestOnBorrow(TEST_ON_BORROW);
            jedisPool = new JedisPool(config, ADDR, PORT, TIMEOUT, AUTH);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    /**
     * 获取Jedis实例
     * @return
     */
    public synchronized static Jedis getJedis() {
        try {
            if (jedisPool != null) {
                Jedis resource = jedisPool.getResource();
                return resource;
            } else {
                return null;
            }
        } catch (Exception e) {
            e.printStackTrace();
            return null;
        }
    }

    /**
     * 释放jedis资源
     * @param jedis
     */
    public static void returnResource(final Jedis jedis) {
        if (jedis != null) {
            jedisPool.close();
        }
    }
	}

###使用redis

	 Jedis jedis = RedisUtil.getJedis();
    System.out.println("连接成功");
    //查看服务是否运行
    System.out.println("服务正在运行: "+jedis.ping());
    //设置 redis 字符串数据
    jedis.set("runoobkey", "www.runoob.com");
    // 获取存储的数据并输出
    System.out.println("redis 存储的字符串为: "+ jedis.get("runoobkey"));
    RedisUtil.returnResource(jedis);
	
##redis和spring的结合使用

首先进行整合配置

1.pom.xml

	<!-- config redis data and client jar--> 
	<dependency>  
		<groupId>org.springframework.data</groupId>  
		<artifactId>spring-data-redis</artifactId>  
		<version>*.*.*.RELEASE</version>  
	</dependency>      
	<dependency>  
		<groupId>redis.clients</groupId>  
		<artifactId>jedis</artifactId>  
		<version>*.*.*</version>  
	</dependency>

2.springmvc.xml

springmvc.xml内容

	<?xml version="1.0" encoding="UTF-8"?>
	<beans xmlns="http://www.springframework.org/schema/beans"
	    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:p="http://www.springframework.org/schema/p"
	    xmlns:mvc="http://www.springframework.org/schema/mvc" xmlns:context="http://www.springframework.org/schema/context"
	    xmlns:util="http://www.springframework.org/schema/util"
	    xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.0.xsd  
	        http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.0.xsd  
	        http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-3.0.xsd          
	        http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util-3.0.xsd">
	    
	    
	    <!-- 激活@Controller模式 -->
	    <mvc:annotation-driven />
	    
	    <!-- 对包中的所有类进行扫描，以完成Bean创建和自动依赖注入的功能 需要更改 -->
	    <context:component-scan base-package="com.pudp.bae.*" />
	    
	    <!-- 引入同文件夹下的redis属性配置文件 -->
	    <import resource="redis-context.xml"/>
	
	</beans>

redis-context.xml内容

	<beans xmlns="http://www.springframework.org/schema/beans" 
			xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
			xmlns:p="http://www.springframework.org/schema/p" 
			xmlns:tx="http://www.springframework.org/schema/tx"
			xmlns:context="http://www.springframework.org/schema/context"
			xsi:schemaLocation="
			http://www.springframework.org/schema/beans 
			http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
			http://www.springframework.org/schema/tx 
			http://www.springframework.org/schema/tx/spring-tx-3.0.xsd
			http://www.springframework.org/schema/context
			http://www.springframework.org/schema/context/spring-context-3.0.xsd ">
	    
	    <!-- scanner redis properties  --> 
	    <context:property-placeholder location="/WEB-INF/property/redis.properties" />
	    
	    <bean id="poolConfig" class="redis.clients.jedis.JedisPoolConfig">  
	        <property name="maxIdle" value="${redis.maxIdle}" />  
	        <property name="maxActive" value="${redis.maxActive}" />  
	        <property name="maxWait" value="${redis.maxWait}" />  
	        <property name="testOnBorrow" value="${redis.testOnBorrow}" />  
	    </bean>  
	      
	    <bean id="connectionFactory" 	class="org.springframework.data.redis.connection.jedis.JedisConnectionFactory"  
	        p:host-name="${redis.host}" 
	        p:port="${redis.port}" 
	        p:password="${redis.pass}"  
	        p:pool-config-ref="poolConfig"/>  
	      
	    <bean id="redisTemplate" class="org.springframework.data.redis.core.StringRedisTemplate">  
	        <property name="connectionFactory"   ref="connectionFactory" />  
	    </bean>      
	     
	</beans>               

Redis.properties文件内容

	#Redis settings
	#redis.host=127.0.0.1
	#redis.port=6380
	#redis.pass=qingyun
	redis.host=127.0.0.1
	redis.port=6379
	redis.pass=
	  
	redis.maxIdle=300
	redis.maxActive=600
	redis.maxWait=1000
	redis.testOnBorrow=false

Redis对象持久化操作

	package com.pudp.bae.base;
	
	import java.io.Serializable;
	
	import org.springframework.beans.factory.annotation.Autowired;
	import org.springframework.data.redis.core.RedisTemplate;
	import org.springframework.data.redis.serializer.RedisSerializer;
	
	public abstract class RedisGeneratorDao{
	    
	    @Autowired
	    protected RedisTemplate<K,V> redisTemplate ;
	
	    /** 
	     * 设置redisTemplate 
	     * @param redisTemplate the redisTemplate to set 
	     */  
	    public void setRedisTemplate(RedisTemplate<K, V> redisTemplate) {  
	        this.redisTemplate = redisTemplate;  
	    }  
	  
	    
	}
	
	
redis对象操作	
	
	@Repository(value="memberDao")
	public class MemberDaoImpl extends RedisGeneratorDao{
	    	}
	    	
	    	
	    	
redis异常解决：MISCONF Redis is configured to save RDB snapshots, but is currently not able to persist
原创 2015年09月11日 10:56:16 标签：redis /异常 /缓存服务器 8554
项目中用到redis做缓存服务器，近日出现这个异常：

redis.clients.jedis.exceptions.JedisDataException: MISCONF Redis is configured to save RDB snapshots, but is currently not able to persist on disk. Commands that may modify the data set are disabled. Please check Redis logs for details about the error.
redis.clients.jedis.Protocol.processError(Protocol.java:113)
redis.clients.jedis.Protocol.process(Protocol.java:138)
redis.clients.jedis.Protocol.read(Protocol.java:192)
redis.clients.jedis.Connection.readProtocolWithCheckingBroken(Connection.java:282)
redis.clients.jedis.Connection.getIntegerReply(Connection.java:207)
redis.clients.jedis.BinaryJedis.setnx(BinaryJedis.java:435)
com.radiadesign.catalina.session.RedisSessionManager.createSession(RedisSessionManager.java:274)
org.apache.catalina.connector.Request.doGetSession(Request.java:3014)
org.apache.catalina.connector.Request.getSession(Request.java:2378)
org.apache.catalina.connector.RequestFacade.getSession(RequestFacade.java:897)
org.apache.catalina.connector.RequestFacade.getSession(RequestFacade.java:909)
javax.servlet.http.HttpServletRequestWrapper.getSession(HttpServletRequestWrapper.java:238)
javax.servlet.http.HttpServletRequestWrapper.getSession(HttpServletRequestWrapper.java:238)
javax.servlet.http.HttpServletRequestWrapper.getSession(HttpServletRequestWrapper.java:238)
javax.servlet.http.HttpServlet.service(HttpServlet.java:620)
javax.servlet.http.HttpServlet.service(HttpServlet.java:727)
org.apache.tomcat.websocket.server.WsFilter.doFilter(WsFilter.java:52)



网上搜索，很多人都给出了解决方法，但没有详细说明问题的来龙去脉，暂且记下，待有空了研究。

解决方法：通过redis-cli连接到服务器后执行以下命令：

config set stop-writes-on-bgsave-error no

如此即可。	    	
	    	