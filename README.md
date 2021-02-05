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

رشته در Redis دنباله ای از بایت ها است. رشته ها در Redis، binary safe هستند به این معنی که طول مشخصی دارند و انتهای آن توسط هیچ علامت خاتمه دهنده خاصی تعیین نمی شود. بنابراین می توان هر چیزی که تا 512 مگابایت است را در یک رشته ذخیره کرد.

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

Hash ها در Redis، map هایی هستند بین فیلد های رشته و مقادیر رشته. از این رو، آنها بهترین نوع داده برای نمایش object ها هستند. در Redis هر هش می تواند بیش از 4 میلیارد جفت فیلد-مقدار را ذخیره کند.

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



# TypeScript basic syntax

برخی نکات اولیه در سینتکس TypeScript:

- semicolon در TypeScript اختیاری است. هر دستور در TypeScript یک عبارت نام دارد. یک خط می‌تواند شامل چندین دستور باشد به شرطی که دستورات توسط semicolon از یکدیگر جدا شده باشند.

- TypeScript، حساس به بزرگی حروف است.

- TypeScript یک زبان Object Oriented است. اشیا در این زبان سه feature اصلی دارند:

	1. State
	2. Behavior
	3. Identity

- کامنت در TypeScript بصورت زیر گذاشته میشوند:

<div dir="ltr">

    //this is single line comment 
	 
    /* This is a  
    Multi-line comment 
    */

</div>

- برای پرینت یک پیام از سینتکس زیر استفاده میشود:

<div dir="ltr">
	
    console.log("hello world")
    
</div>

# type

- Any: دیتا تایپ “Any” سوپر همه ی تایپ هاست و بصورت داینامیک یک تایپ را مشخص میکند. 
- Built-in types: 

	-تفاوت Null و Undefined: متغیری که در ابتدا undefined مشخص شده یعنی مقدار یا شی ای به آن اختصاص داده نشده است ولی متغیر null به معنی آن است که به این متغیر شی ای که مقداری ندارد اختصاص داده شده است.

- User-defined types

![enter image description here](https://www.tutorialspoint.com/typescript/images/data_types.jpg)

# variable

متغیر ها در TypeScript بصورت زیر تعریف میشوند:

![enter image description here](https://www.tutorialspoint.com/typescript/images/declare_type.jpg)

در این تعریف بخش type-annotation و value اختیاری است و میتوانند در تعریف مشخص نشوند.
مثال:

<div dir="ltr">
	
    var score: number = 50;
    
</div>

# Condition و Loop

-نمونه کد برای تصمیم گیری در یک Condition:

<div dir="ltr">
	
    if (num % 2==0) { 
        console.log("Even"); 
    } else {
        console.log("Odd"); 
    }
    
</div>

۳ روش برای ایجاد حلقه در جهت اجرای چند باره یک بخش از کد وجود دارد:

- for loop:

<div dir="ltr">
	
    for (initial_count_value; termination-condition; step) {
        //statements 
    }
    
</div>
    
- while loop:

<div dir="ltr">
	
    while(condition) { 
        // statements if the condition is true 
    }

</div>

- do… while:

<div dir="ltr">
	
    do {
        //statements 
    } while(condition)
    
</div>	

# Function

فانکشن شامل یک سری عبارت است تا یک تسک خاص را انجام دهند. فانکشن درواقع یک بلوک منطقی برای مرتب سازی کد است. برای دسترسی به کد این بلوک فانکشن را صدا میزنیم که به این ترتیب کد reusable میشود.

سینتکس فانکشن به صورت زیر است:

<div dir="ltr">

    function func_name( param1 [:datatype], param2 [:datatype]…) { 
        // function body   
    }

</div>

که وجود پارامتر ها اختیاری است.

همچنین سینتکس برای صدا زدن یک فانکشن بصورت زیر است:

<div dir="ltr">

    function_name(param1 , param2…)

</div>

-یک نمونه کد برای ایجاد یک فانکشن و صدا زدن آن:

<div dir="ltr">

    function disp_details(id, name, mail_id) {
        console.log("ID:", id);
        console.log("Name", name);
	
    if (mail_id != undefined)
        console.log("Email Id", mail_id);
    }
    disp_details(123, "John");

</div>

### توابع بازگشتی:

تابع بازگشتی روشی برای تکرار یک عمل به طریقی است که یک فانکشن بتواند خودش را صدا بزند.

-یک نمونه کد برای ایجاد یک تابع recursive و صدا زدن آن:

<div dir="ltr">

    function factorial(number) {
        if (number <= 0) {         // termination case
            return 1; 
        } else {     
            return (number * factorial(number - 1));     // function invokes itself
        } 
    }; 
    console.log(factorial(6));      // outputs 720 

</div>

# Numbers

TypeScript مانند JavaScript مقادیر عددی را بصورت اشیا از حنس عدد ساپورت میکند. شی Number یک مقدار عددی را به یک نمونه از کلاس Number تبدیل میکند و این کلاس برای آن مثل یک wrapper عمل میکند.

-سینتکس مناسب برای ساختن یک Number Object:

<div dir="ltr">

    var var_name = new Number(value)

</div>

-بعضی از property های شی Number در زیر لیست شده اند:

- MAX_VALUE: بزرگ ترین عددی که در این زبان امکان وجودش هست. 
- MIN_VALUE: کوچک ترین عددی که در این زبان امکان وجودش هست. 
- NaN: نشان دهنده مقداری است که از جنس عدد نیست. (Not a Number) 

-در صورتی که یک مقدار غیر عددی به constructor شی Number پاس داده شود constructor، NaN برمیگرداند.

-برخی method های شی Number در زیر لیست شده اند:

- ()toExponential: این متد یک رشته برمیگرداند که نمایش عدد به فرم نمایی است.
- ()toPrecision: این متد عدد را با دقت مشخص شده (تعداد ارقام با اهمیت) نشان میدهد.
- ()toString: با ورودی گرفتن یک پایه، عدد را در مبنای مشخص شده بصورت رشته برمیگرداند.
- ()valueOf: مقدار primitive عدد را برمیگرداند.

# Strings

شی String مقدار primitive رشته را همراه با تعدادی method کمکی، در برمیگیرد.

-سینتکس برای ایجاد یک شی String:

<div dir="ltr">

    var var_name = new String(string);

</div>

-یک مثال کد از کاربرد این شی همراه با متد دسترسی به طول رشته:


<div dir="ltr">
    var uname = new String("Hello World") 
    console.log(uname) 
    console.log("Length "+uname.length) 
</div>

-برخی method های شی String در زیر لیست شده اند:

- ()charAt: کاراکتر موجود در شاخص مشخص شده را برمیگرداند.
- ()concat:متن دو رشته را با هم پیوند میزند و یک رشته جدید برمیگرداند.
- ()search: یک عبارت را در یک رشته جست و جو میکند.
- ()split: یک شی String را تقسیم کرده و بصورت یک آرایه از رشته ها برمیگرداند.
- ()replace: یک زیر رشته از رشته را با یک زیر رشته دیگر جایگزین میکند.
- ()substr: یک زیر رشته کاراکتر را که از شاخص مشخص شده شروع شده اند و تا تعداد مشخص شده پیش رفته است را برمیگرداند.
- ()toLowerCase: کاراکتر های رشته را به حروف کوچک تبدیل میکند و برمیگرداند.
- ()toUpperCase: کاراکتر های رشته را به حروف بزرگ تبدیل میکند و برمیگرداند.
- ()toString: یک رشته برمیگرداند که شی را نمایش بدهد.
- ()valueOf: مقدار رشته را برمیگرداند.

# Array

آرایه یک مجموعه از value ها را ذخیره میکند.

<div dir="ltr">

    var array_name[:datatype];        //declaration 
    array_name = [val1,val2,valn..]   //initialization

</div>

برخی از method هایی که در TypeScript برای آرایه وجود دارند در زیر لیست شده اند:

- ()concat

	یک آرایه جدید شامل جوین شده آرایه با یک آرایه دیگر را برمیگرداند.

- ()filter

	یک آرایه جدید برمیگرداند که با شرایط ذکر شده فیلتر شده اند.

- ()forEach

	یک فانکشن را برای همه المنت های آرایه صدا میزند.

- ()indexOf

	شاخص اولین المنت آرایه برابر با مقدار مشخص شده را برمیگرداند یا اگر چنین المنتی در آرایه موجود نباشد ۱- را برمیگرداند.

- ()pop

	آخرین المنت آرایه را حذف میکند و آن را برمیگرداند.

- ()push

	یک یا چند المنت جدید را به آخر آرایه اضافه میکند و طول جدید آرایه را برمیگرداند.

- ()sort

	المنت های آرایه را مرتب و سورت میکند.
	
# Tuples

Tuple ها برای زمانی که احتیاج داریم یک مجموعه از مقادیری با انواع مختلف ذخیره کنیم به کار میآیند زیرا آرایه ها این کار را نمیتوانند انجام بدهند.

-سینتکس برای تعریف یک tuple:

<div dir="ltr">

    var tuple_name = [value1,value2,value3,…value n]

</div>

-مثال:

<div dir="ltr">
	
    var mytuple = [10,"Hello"];
    
</div>

دسترسی به اعضای tuple هم به شکل زیر صورت میگیرد:

<div dir="ltr">
	
    var tup = [] 
    tup[0] = 12 
    tup[1] = 23 
    
</div>

-دو تا از عملگر هایی که روی یک tuple قابل انجام است در زیر توضیح داده شده اند:

- ()Push: یک عضو به tuple اضافه میکند.
- ()Pop: عضو آخر tuple را حذف میکند و آن را برمیگرداند.

-تخریب ساختار tuple: به این معنا که ساختار بندی آن را از بین میبریم. 

-مثالی از تخریب ساختار یک tuple:

<div dir="ltr">
	
    var a =[10,"hello"] 
    var [b,c] = a 
    console.log( b )   //10 
    console.log( c )   //hello
    
</div>

# Union

TypeScript این قابلیت را به برنامه میدهد که یک یا چند تایپ را با هم ترکیب کند. تایپ Union یک روش برای نشان دادن این است که یک مقدار میتواند یکی از چند تایپ ذکر شده را داشته باشد.

-سینتکس برای نشان دادن تایپ Union:

<div dir="ltr">

    Type1|Type2|Type3 

</div>

-یک مثال از تعریف متغیر با استفاده از Union:

<div dir="ltr">

    var val:string|number 
    val = 12 
    console.log("numeric value of val "+val) 
    val = "This is a string" 
    console.log("string value of val "+val)

</div>

-یک مورد استفاده دیگر union type ها به عنوان پارامتر فانکشن هاست:

<div dir="ltr">

    function disp(name:string|string[]) { 
        if(typeof name == "string") { 
            console.log(name) 
        } else { 
            var i; 
      
            for(i = 0;i<name.length;i++) { 
                console.log(name[i])
            } 
        } 
    } 

</div>

Union تایپ ها همچنین میتوانند در آرایه ها یا اینترفیس ها مورد استفاده واقع شوند:

<div dir="ltr">

    var arr:number[]|string[]; 
    var i:number; 
    arr = [1,2,4] 
    console.log("**numeric array**")  

    for(i = 0;i<arr.length;i++) { 
        console.log(arr[i]) 
    }  

    arr = ["Mumbai","Pune","Delhi"] 
    console.log("**string array**")  

    for(i = 0;i<arr.length;i++) { 
        console.log(arr[i]) 
    } 

</div>

در این قطعه کد اعضای آرایه میتوانند از نوع رشته یا عددی باشند.

# Interface

اینترفیس ها شامل ۳ بخش زیر هستند:

1. properties
2. methods
3. events

اینترفیس ها فقط این اعضا را declare میکنند و define کردن این اعضا بر عهده کلاسی است که آن را پیاده سازی میکند.

-روش تعریف اینترفیس:

<div dir="ltr">

    interface interface_name { 
        ...
    }

</div>

-یک مثال از تعریف و پیاده سازی یک اینترفیس توسط یک کلاس:

<div dir="ltr">

    interface IPerson { 
        firstName:string, 
        lastName:string, 
        sayHi: ()=>string 
    } 

    var customer:IPerson = { 
        firstName:"Tom",
        lastName:"Hanks", 
        sayHi: ():string =>{return "Hi there"} 
    } 

</div>

# Class

TypeScript درواقع همان JavaScript است که شی گرایی را ساپورت میکند. یک کلاس در TypeScript، داده های یک شی را محصور میکند. برای تعریف یک کلاس از سینتکس زیر استفاده میکنیم:

<div dir="ltr">
	
    class class_name {
        //class scope 
    }

</div>

یک کلاس میتواند ۳ بخش زیر را شامل شود:

1. Fields
2. Constructors
3. Functions

-یک مثال از یک کلاس که شامل هر ۳ این اعضا است در زیر آمده است:

<div dir="ltr">

    class Car { 
        //field 
        engine:string; 
 
        //constructor 
        constructor(engine:string) { 
            this.engine = engine 
        }  

        //function 
        disp():void { 
            console.log("Engine is  :   "+this.engine) 
        } 
    }

</div>

# Object

یک object یک نمونه است که شامل مجموعه ای از کلید ها و مقدار هاست. این مقدار ها میتوانند عددی، فانکشن یا حتی آرایه از شی های دیگر باشند.

- سینتکس object بصورت زیر است:

<div dir="ltr">

    var object_name = { 
        key1: “value1”, //scalar value 
        key2: “value”,  
        key3: function() {
             //functions 
        }, 
        key4:[“content1”, “content2”] //collection  
    };

</div>

-یک نمونه کد برای تعریف یک object و دسترسی به اعضای آن:

<div dir="ltr">

    var person = { 
        firstname:"Tom", 
        lastname:"Hanks" 
    }; 
    //access the object values 
    console.log(person.firstname) 
    console.log(person.lastname)

</div>

همچنین در صورتی که بخواهیم مقادیری را به object اضافه کنیم. TypeScript با استفاده از تعریف یک method template این اجازه را به ما میدهد. مثلا در قطعه کد زیر ما یک فانکشن را به شی person اضافه میکنیم:

<div dir="ltr">

    var person = {
        firstName:"Tom", 
        lastName:"Hanks", 
        sayHello:function() {  }  //Type template 
    } 
    person.sayHello = function() {  
        console.log("hello "+person.firstName)
    } 

</div>

</div>
