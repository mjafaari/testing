<div dir="rtl">

# Introduction   

Redis یک محل ذخیره سازی منبع باز و پیشرفته key-value و یک راه حل مناسب برای ایجاد برنامه های وب با عملکرد بالا و مقیاس پذیر است.

Redis دارای سه ویژگی اصلی است که آن را متمایز می کند.

- پایگاه داده خود را کاملاً در حافظه نگهداری می کند ، فقط برای ماندگاری از دیسک استفاده می کند.
- در مقایسه با بسیاری از ذخیره سازی های داده key-value ، یک مجموعه نسبتاً غنی از انواع داده دارد.
- می تواند داده ها را برای هر تعدادی از slave ها تکرار کند.


# Advantages

موارد زیر مزایای خاصی از Redis است:

- بسیار سریع است و می تواند حدود 110000، SET در ثانیه و حدود 81000، GET در ثانیه انجام دهد.

- از انواع داده های غنی پشتیبانی می کند : بطور محلی از بسیاری از انواع داده ها مانند list ،set ،sorted set و hash ها پشتیبانی می کند. این مسئله حل انواع مشکلات را آسان می کند.

- عملیات اتمیک هستند : تمام عملیات در Redis اتمیک هستند، که اطمینان می دهد در صورت دسترسی همزمان دو کلاینت، سرور مقدار به روز شده را دریافت می کند.

- ابزار چند منظوره: Redis یک ابزار چند منظوره است و می تواند در موارد مختلفی استفاده می شود مانند ذخیره سازی، صف های پیام رسانی (Redis بطور طبیعی از انتشار / اشتراک پشتیبانی می کند )، هرگونه داده کوتاه مدت در برنامه مانند تعداد بازدید صفحه وب و غیره.


# Installation

برای نصب Redis در اوبونتو به ترمینال بروید و دستورات زیر را تایپ کنید:

<div dir="ltr">
	
    $ sudo apt-get update 
    $ sudo apt-get install redis-server
	
</div>

با این کار Redis روی دستگاه شما نصب می شود.

شروع کار:

<div dir="ltr">
	
    $ redis-server
	
</div>

چک میکنیم که آیا Redis کار میکند یا نه:

<div dir="ltr">
	
    $ redis-cli 
    
</div>

با این کار یک Redis Prompt باز می شود.

<div dir="ltr">
	
    redis 127.0.0.1:6379>
    
</div>

در دستورالعمل فوق ، 127.0.0.1 آدرس IP دستگاه شما و 6379 پورتی است که سرور Redis بر روی آن اجرا می شود. اکنون دستور PING زیر را تایپ کنید.

<div dir="ltr">
	
    redis 127.0.0.1:6379> ping 
    PONG

</div>

این نشان می دهد که Redis با موفقیت بر روی دستگاه شما نصب شده است.

### نصب  Redis Desktop Managerبر روی اوبونتو

برای نصب Redis desktop manager در اوبونتو ، فقط پکیج آن را از https://redisdesktop.com/download دانلود کنید. پکیج را باز کنید و آن را نصب کنید. Redis desktop manager به شما رابط کاربری مدیریت کلیدها و داده های Redis را می دهد.

# Configuration

درRedis ، یک فایل (redis.conf)  در دایرکتوری root موجود است. اگرچه می توانید تمام تنظیمات Redis را با دستور Redis CONFIG دریافت و تنظیم کنید.

سینتکس دستور Redis CONFIG:

<div dir="ltr">
	
    redis 127.0.0.1:6379> CONFIG GET CONFIG_SETTING_NAME
    
</div>

مثال:

<div dir="ltr">
	
    redis 127.0.0.1:6379> CONFIG GET loglevel  
    1) "loglevel" 
    2) "notice"
    
</div>

برای گرفتن همه تنظیمات configuration از * در جای CONFIG_SETTING_NAME استفاده میکنیم:

<div dir="ltr">
	
    redis 127.0.0.1:6379> CONFIG GET *  
      1) "dbfilename" 
      2) "dump.rdb" 
      3) "requirepass" 
      4) "" 
      5) "masterauth" 
      6) "" 
      7) "unixsocket" 
      8) "" 
      9) "logfile" 
     10) "" 
     11) "pidfile" 
     12) "/var/run/redis.pid" 
     13) "maxmemory" 
     14) "0"
     15) "maxmemory-samples" 
     16) "3" 
     17) "timeout" 
     18) "0" 
     19) "tcp-keepalive" 
     20) "0" 
     21) "auto-aof-rewrite-percentage" 
     22) "100" 
     23) "auto-aof-rewrite-min-size" 
     24) "67108864" 
     25) "hash-max-ziplist-entries" 
     26) "512" 
     27) "hash-max-ziplist-value" 
     28) "64" 
     29) "list-max-ziplist-entries" 
     30) "512" 
     31) "list-max-ziplist-value" 
     32) "64" 
     33) "set-max-intset-entries" 
     34) "512" 
     35) "zset-max-ziplist-entries" 
     36) "128" 
     37) "zset-max-ziplist-value" 
     38) "64" 
     39) "hll-sparse-max-bytes" 
     40) "3000" 
     41) "lua-time-limit" 
     42) "5000" 
     43) "slowlog-log-slower-than" 
     44) "10000" 
     45) "latency-monitor-threshold" 
     46) "0" 
     47) "slowlog-max-len" 
     48) "128" 
     49) "port" 
     50) "6379" 
     51) "tcp-backlog" 
     52) "511" 
     53) "databases" 
     54) "16" 
     55) "repl-ping-slave-period" 
     56) "10" 
     57) "repl-timeout" 
     58) "60" 
     59) "repl-backlog-size" 
     60) "1048576" 
     61) "repl-backlog-ttl" 
     62) "3600" 
     63) "maxclients" 
     64) "4064" 
     65) "watchdog-period" 
     66) "0" 
     67) "slave-priority" 
     68) "100" 
     69) "min-slaves-to-write" 
     70) "0" 
     71) "min-slaves-max-lag" 
     72) "10" 
     73) "hz" 
     74) "10" 
     75) "no-appendfsync-on-rewrite" 
     76) "no" 
     77) "slave-serve-stale-data" 
     78) "yes" 
     79) "slave-read-only" 
     80) "yes" 
     81) "stop-writes-on-bgsave-error" 
     82) "yes" 
     83) "daemonize" 
     84) "no" 
     85) "rdbcompression" 
     86) "yes"
     87) "rdbchecksum" 
     88) "yes" 
     89) "activerehashing" 
     90) "yes" 
     91) "repl-disable-tcp-nodelay" 
     92) "no" 
     93) "aof-rewrite-incremental-fsync" 
     94) "yes" 
     95) "appendonly" 
     96) "no" 
     97) "dir" 
     98) "/home/deepak/Downloads/redis-2.8.13/src" 
     99) "maxmemory-policy" 
    100) "volatile-lru" 
    101) "appendfsync" 
    102) "everysec" 
    103) "save" 
    104) "3600 1 300 100 60 10000" 
    105) "loglevel" 
    106) "notice" 
    107) "client-output-buffer-limit" 
    108) "normal 0 0 0 slave 268435456 67108864 60 pubsub 33554432 8388608 60" 
    109) "unixsocketperm" 
    110) "0" 
    111) "slaveof" 
    112) "" 
    113) "notify-keyspace-events" 
    114) "" 
    115) "bind" 
    116) ""

</div>

### ویرایش configuration:

برای به روزرسانی configuration، می توانید مستقیماً فایل redis.conf را ویرایش کنید یا می توانید config ها را از طریق دستور CONFIG set به روز کنید.

سینتکس دستور CONFIG SET:

<div dir="ltr">
	
    redis 127.0.0.1:6379> CONFIG SET CONFIG_SETTING_NAME NEW_CONFIG_VALUE
    
</div>

مثال:

<div dir="ltr">
	
    redis 127.0.0.1:6379> CONFIG SET loglevel "notice" 
    OK 
    redis 127.0.0.1:6379> CONFIG GET loglevel  
    1) "loglevel" 
    2) "notice" 
    
</div>

# Instructions

از دستورات Redis برای انجام برخی عملیات در سرور Redis استفاده می شود.

برای اجرای دستورات در سرور Redis ، به یک سرویس گیرنده Redis نیاز دارید. سرویس گیرنده Redis در پکیج Redis موجود است که قبلاً آن را نصب کرده ایم.

در زیر سینتکس بخش کاربری Redis آورده شده است:

<div dir="ltr">
	
    $ redis-cli 
    
</div>

مثال زیر توضیح می دهد که چگونه می توانیم کلاینت Redis را راه اندازی کنیم.

برای شروع ، ترمینال را باز کرده و دستور redis-cli را تایپ میکنیم. این به سرور محلی متصل می شود و اکنون می توانید هر دستوری را اجرا کنید.

<div dir="ltr">
	
    $ redis-cli 
    redis 127.0.0.1:6379> 
    redis 127.0.0.1:6379> PING  
    PONG

</div>

در مثال بالا ، ما به سرور Redis که در دستگاه محلی در حال اجرا است متصل می شویم و یک دستور PING را اجرا می کنیم که بررسی می کند آیا سرور در حال اجرا است یا خیر.

دستورات را در سرور راه دور اجرا میکنیم.

برای اجرای دستورات در سرور از راه دور Redis ، باید توسط همان مشتری redis-cli به سرور متصل شوید.

<div dir="ltr">
	
    $ redis-cli -h host -p port -a password
    
</div>

مثال زیر نحوه اتصال به سرور راه دور Redis را نشان می دهد ، که بر روی میزبان 127.0.0.1 ، پورت 6379 اجرا می شود و mypass رمز عبور آن است. 

<div dir="ltr">
	
    $redis-cli -h 127.0.0.1 -p 6379 -a "mypass" 
    redis 127.0.0.1:6379> 
    redis 127.0.0.1:6379> PING  
    PONG

</div>

# Radis Data Types

Redis ۵ نوع داده را ساپورت میکند:

- String
- Hash
- List
- Set
- Sorted Set

### String: 

کامند های String در Redis برای مدیریت مقادیر رشته استفاده میشوند. برای استفاده از کامند های رشته از سینتکس زیر استفاده میشود:

<div dir="ltr">
	
    redis 127.0.0.1:6379> COMMAND KEY_NAME
    
</div>

رشته در Redis دنباله ای از بایت ها است. در Redis رشته ها binary safe هستند به این معنی که طول مشخصی دارند و انتهای آن توسط هیچ علامت خاتمه دهنده خاصی تعیین نمی شود. بنابراین می توان هر چیزی که تا 512 مگابایت است را در یک رشته ذخیره کرد.

مثال:

<div dir="ltr">
	
    redis 127.0.0.1:6379> SET name "value" 
    OK 
    redis 127.0.0.1:6379> GET name 
    "value"
    
</div>

در مثال بالا SET  و GET دستورات Redis هستند ، “name” کلید استفاده شده در Redis و”value”    مقدار رشته ای است که در Redis ذخیره می شود.

#### بعضی دستورات پایه ای رشته عبارت اند از:

- SET key value

    این دستور مقدار را در کلید مشخص شده تنظیم می کند.

- GET key

    مقدار یک کلید را برمیگرداند.

- GETRANGE key start end

    یک زیررشته از رشته ذخیره شده در یک کلید را برمیگرداند.

- GETSET key value

    مقدار رشته یک کلید را تنظیم می کند و مقدار قدیمی آن را برمی گرداند.

- SETNX key value

    مقدار کلید را تنظیم می کند (فقط در صورت وجود کلید).
    
- STRLEN key

    طول مقدار ذخیره شده در یک کلید را برمیگرداند.
- INCRBY key increment

    مقدار عدد یک کلید را به مقدار داده شده افزایش می دهد.

- DECR key

    مقدار عدد یک کلید را یک واحد کاهش می دهد.

- APPEND key value

    مقداری را به یک کلید اضافه می کند.

### Hash:

Hash ها در Redis، مپ هایی هستند بین فیلد های رشته و مقادیر رشته. از این رو، آنها بهترین نوع داده برای نمایش object ها هستند. در Redis هر هش می تواند بیش از 4 میلیارد جفت فیلد-مقدار را ذخیره کند.

یک مثال:

<div dir="ltr">
	
    redis 127.0.0.1:6379> HMSET hash name "redis tutorial" 
    description "redis basic commands for caching" likes 20 visitors 23000 
    OK 
    redis 127.0.0.1:6379> HGETALL hash  
    1) "name" 
    2) "redis tutorial" 
    3) "description" 
    4) "redis basic commands for caching" 
    5) "likes" 
    6) "20" 
    7) "visitors" 
    8) "23000"
    
</div>

در مثال بالا ، جزئیات (نام ، توضیحات ، پسندیدن ها ، بازدیدکنندگان) را در یک هش به نام "hash" ست کرده ایم.

#### بعضی دستورات پایه ای هش عبارت اند از:

- HDEL key field2 [field2]

    یک یا چند فیلد هش را حذف می کند.
    
- HEXISTS key field

    تعیین می کند که فیلد هش وجود دارد یا نه.

- HGET key field

    مقدار فیلد هش ذخیره شده در کلید مشخص شده را میگیرد.

- HLEN key

    تعداد قسمتهای هش را بدست می آورد.

- HMSET key field1 value1 [field2 value2 ]

    چندین فیلد هش را روی چندین مقدار ست می کند.

- HSET key field value

    مقدار رشته فیلد هش را تنظیم می کند.

- HKEYS key

    همه فیلد های یک هش را میگیرد.
    
- HVALS key

    تمام مقادیر یک هش را میگیرد.

### List 

Listها در Redis لیستی از رشته ها هستند که براساس ترتیب درج مرتب شده اند. می توان عناصر را در لیست Redis به قسمت اول یا اخر لیست اضافه کرد.

حداکثر طول یک لیست 232 - 1 عنصر است (4294967295 ، بیش از 4 میلیارد عنصر در هر لیست).

مثال:

<div dir="ltr">
	
    redis 127.0.0.1:6379> LPUSH tutorials redis 
    (integer) 1 
    redis 127.0.0.1:6379> LPUSH tutorials mongodb 
    (integer) 2 
    redis 127.0.0.1:6379> LPUSH tutorials mysql 
    (integer) 3 
    redis 127.0.0.1:6379> LRANGE tutorials 0 10  
    1) "mysql" 
    2) "mongodb" 
    3) "redis"

</div>

در مثال بالا ، سه مقدار با دستور LPUSH در لیست Redis با نام "tutorials" وارد شده است.

#### بعضی دستورات پایه ای لیست عبارت اند از:

- BLPOP key1 [key2 ] timeout

    اولین عنصر موجود در لیست را حذف کرده و برمیگرداند یا تا زمان قابل دسترسی شدن یکی از آنها مسدود می شود.

- BRPOP key1 [key2 ] timeout

    آخرین عنصر موجود در لیست را حذف کرده و برمیگرداند یا تا زمان قابل دسترسی شدن یکی از آنها مسدود می شود.

- BRPOPLPUSH source destination timeout

    مقداری را از یک لیست pop می کند ، آن را به لیست دیگری push می کند و آن را برمی گرداند. یا تا زمانی که یکی در دسترس باشد بلاک می شود.

- LINDEX key index

    یک عنصر از لیست را با index میگیرد.

- LINSERT key BEFORE|AFTER pivot value

    یک عنصر را قبل یا بعد از عنصر دیگری در لیست قرار می دهد.

- LLEN key

    طول یک لیست را بدست می آورد.

- LPOP key

    اولین عنصر لیست را حذف و دریافت می کند.

- LRANGE key start stop

    بازه ای از عناصر را از لیست دریافت می کند.

- LREM key count value

    عناصر را از لیست حذف می کند.

- LSET key index value

    مقدار یک عنصر لیست را با استفاده از شاخص آن ست می کند.

- LTRIM key start stop

    لیست را تا محدوده مشخص شده کوتاه می کند.

- RPOP key

    آخرین عنصر لیست را حذف و برمی گرداند.

- RPOPLPUSH source destination

    آخرین عنصر را از لیست حذف کرده و به لیست دیگری اضافه می کند و برمی گرداند.

- RPUSH key value1 [value2]

    یک یا چند مقدار را به یک لیست اضافه می کند.

- RPUSHX key value

    مقداری را به لیست اضافه می کند (فقط در صورت وجود لیست) 

### Set

Set ها در Redis  مجموعه ای مرتب نشده از رشته های منحصر به فرد است. منحصر به فرد به این معنا است که اجازه تکرار داده ها در یک کلید را نمی دهد. Set در Redis اضافه کردن، حذف کردن و تست کردن وجود عضو در O(1) انجام می شود (زمان ثابت بدون توجه به تعداد عناصر موجود در مجموعه). حداکثر طول یک لیست  232 - 1 عنصر است (4294967295 ، بیش از 4 میلیارد عنصر در هر مجموعه).

مثال:

<div dir="ltr">
	
    redis 127.0.0.1:6379> SADD tutorials redis 
    (integer) 1 
    redis 127.0.0.1:6379> SADD tutorials mongodb 
    (integer) 1 
    redis 127.0.0.1:6379> SADD tutorials mysql 
    (integer) 1 
    redis 127.0.0.1:6379> SADD tutorials mysql 
    (integer) 0 
    redis 127.0.0.1:6379> SMEMBERS tutorials  
    1) "mysql" 
    2) "mongodb" 
    3) "redis"

</div>

در مثال بالا، سه مقدار در مجموعه Redis با نام "tutorials" توسط دستور SADD وارد شده است.

#### بعضی دستورات پایه ای set عبارت اند از:

- SADD key member1 [member2]

    یک یا چند عضو را به مجموعه اضافه می کند.

- SCARD key

    تعداد اعضای یک مجموعه را بدست می آورد.

- SDIFF key1 [key2]

    چندین مجموعه را از هم کم می کند.

- SDIFFSTORE destination key1 [key2]

    چندین مجموعه را کم می کند و مجموعه حاصل را در یک کلید ذخیره می کند

- SINTER key1 [key2]

    چندین مجموعه را با هم تلاقی می دهد

- SINTERSTORE destination key1 [key2]

    چندین مجموعه را تلاقی می دهد و مجموعه حاصل را در یک کلید ذخیره می کند

- SISMEMBER key member

    تعیین می کند که آیا یک مقدار داده شده عضوی از مجموعه است یا نه.

- SMEMBERS key

    همه اعضا را در یک مجموعه قرار می دهد

- SMOVE source destination member

    یک عضو را از یک مجموعه به مجموعه دیگر منتقل می کند

- SPOP key

    یک عضو تصادفی را از یک مجموعه حذف و برمی گرداند. 

- SRANDMEMBER key [count]

    یک یا چند عضو تصادفی را از یک مجموعه دریافت می کند

- SUNION key1 [key2]

    مجموعه های متعددی را به هم اضافه می کند

### Sorted Set:

Sorted Set ها در Redis با ویژگی منحصر به فرد مقادیر ذخیره شده در یک مجموعه ، مشابه Redis Sets است. تفاوت در این است که ، هر عضوی از یک مجموعه مرتب شده با نمره ای همراه است که برای گرفتن مجموعه مرتب شده از کوچکترین به بیشترین امتیاز استفاده می شود.

در مجموعه مرتب شده Redis ، اضافه کردن، حذف کردن و تست کردن وجود عضو در O(1) انجام می شود (زمان ثابت بدون توجه به تعداد عناصر موجود در مجموعه). حداکثر طول یک لیست  232 - 1 عنصر است (4294967295 ، بیش از 4 میلیارد عنصر در هر مجموعه).

مثال:

<div dir="ltr">
	
    redis 127.0.0.1:6379> ZADD tutorials 1 redis 
    (integer) 1 
    redis 127.0.0.1:6379> ZADD tutorials 2 mongodb 
    (integer) 1 
    redis 127.0.0.1:6379> ZADD tutorials 3 mysql 
    (integer) 1 
    redis 127.0.0.1:6379> ZADD tutorials 3 mysql 
    (integer) 0 
    redis 127.0.0.1:6379> ZADD tutorials 4 mysql 
    (integer) 0 
    redis 127.0.0.1:6379> ZRANGE tutorials 0 10 WITHSCORES  
    1) "redis" 
    2) "1" 
    3) "mongodb" 
    4) "2" 

</div>

در مثال فوق ، سه مقدار با score آن ها در مجموعه مرتب شده Redis با نام "tutorials" توسط دستور ZADD وارد شده است.

#### بعضی دستورات پایه ای set sorted عبارت اند از:

- ZADD key score1 member1 [score2 member2]

    یک یا چند عضو را به مجموعه مرتب شده اضافه می کند یا score آن را در صورت وجود به روز می کند.

- ZCARD key

    تعداد اعضای یک مجموعه مرتب شده را برمیگرداند.

- ZCOUNT key min max

    تعداد اعضای مجموعه مرتب شده با score ای در محدوده مقادیر داده شده را می شمارد.

- ZINCRBY key increment member

    score یک عضو مجموعه مرتب شده را افزایش می دهد

- ZINTERSTORE destination numkeys key [key ...]

    چندین مجموعه مرتب شده را تلاقی می دهد و مجموعه مرتب شده حاصل را در یک کلید جدید ذخیره می کند

- ZLEXCOUNT key min max

    تعداد اعضای مجموعه مرتب شده بین یک دامنه لغت نامه را مشخص می کند.

- ZRANGE key start stop [WITHSCORES]

    طیفی از اعضای مجموعه مرتب شده را بر اساس شاخص شان برمی گرداند

- ZRANGEBYLEX key min max [LIMIT offset count]

    طیفی از اعضای مجموعه مرتب شده را بر اساس محدوده لغت نامه، برمی گرداند

- ZRANK key member

    شاخص یک عضو را در یک مجموعه مرتب شده تعیین می کند

- ZREM key member [member ...]

    یک یا چند عضو را از یک مجموعه مرتب شده حذف می کند

- ZREMRANGEBYRANK key start stop

    همه اعضای مجموعه مرتب شده در شاخص های داده شده را حذف می کند

- ZREMRANGEBYSCORE key min max

    همه اعضای مجموعه مرتب شده با امتیاز های داده شده را حذف می کند

- ZREVRANGE key start stop [WITHSCORES]

    طیفی از اعضا را در یک مجموعه مرتب شده بر اساس شاخص ، با امتیازات مرتب شده از بالا به پایین برمی گرداند

- ZREVRANK key member

    شاخص یک عضو را در یک مجموعه مرتب سازی شده ، با امتیازات از بالا به پایین تعیین می کند

- ZSCORE key member

    امتیاز مرتبط با عضو داده شده را در یک مجموعه مرتب می شود

- ZUNIONSTORE destination numkeys key [key ...]

چندین مجموعه مرتب شده را اضافه می کند و مجموعه مرتب شده حاصل را در یک کلید جدید ذخیره می کند.

</div>
