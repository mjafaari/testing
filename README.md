<div dir="rtl">

# Introduction   

زبان TypeScript یک سوپر‌ست نوع‌گذاری شده از JavaScript است که به زبان JavaScript کامپایل می‌شود. به بیانی دیگر، TypeScript  همان JavaScript است برای توسعه در مقیاس کاربردی. این زبان به شما امکان می دهد JavaScript را همانطور که می خواهید بنویسید و خوانایی و رفع اشکال آن را بهبود می بخشد. این زبان یک زبان شی گرای خالص است و فریمورک های معروفی مانند Angular 2.0 به این زبان نوشته شده اند.

# Requirements

همان طور که گفته شد ابتدا باید برنامه نوشته شده در زبان Typescript را به زبان JavaScript کامپایل و سپس آن را نیز تفسیر کرد. پس به `nodeJs` و `type Script Compiler(tsc)` نیاز داریم. همچنین نصب `npm` نیز توصیه می شود.

# installation

برای نصب `nodejs` از دستور زیر استفاده می کنیم:

<div dir="ltr">
	
    sudo apt install nodejs
	
</div>

برای نصب `npm` از دستور زیر استفاده می کنیم:

<div dir="ltr">
	
    sudo apt install npm
	
</div>

برای نصب `tsc` نیز از `npm` استفاده می کنیم:

<div dir="ltr">
	
    npm install -g typescript
	
</div>

حال برای کامپایل و اجرای برنامه های این زبان مراحل زیر را طی می کنیم:

1.ابتدا فایل مورد نظر را با پسوند `ts.` ذخیره می کنیم (برای مثال `test.ts`)
	
2.سپس فایل مورد نظر را با دستور `tsc [file_name].ts` به زبان js کامپایل می کنیم.(خروجی آن یک فایل مانند `test.js` است)
	
3.در نهایت برای اجرای فایل نهایی دستور `node [file_name].js` را اجرا می کنیم.
	
همچنین پکیج هایی نیز وجود دارند که مراحل 2 و 3 را ترکیب می کنند.(مانند `ts-node`)

# Differences

تایپ‌اسکریپت دربرگیرنده جاوااسکریپت است ولی تفاوت‌هایی جزیی با آن دارد که در جدول زیر به آن‌ها می‌پردازیم:

| JavaScript | TypeScript |  |
| ---------- | ---------- | --------- |
| در نسخه های قدیمی موجود نبود | استفاده از کلاس، اینترفیس، تایپ | شی‌گرایی
| وجود ندارد | با استفاده از تایپ و اینترفیس | Data binding | 
پکیج‌ها بدون نیاز به بیلد قابل استفاده هستند|پکیج‌های گوناگونی را با استفاده از npm می‌توان نصب کرد|پکیج‌های مختلف
چنین ویژگی وجود ندارد|می‌توان از Prototyping استفاده کرد|Prototyping
کدها کامپایل نمی‌شوند|کدها کامپایل می‌شوند|کامپایل
چنین ویژگی وجود ندارد|می‌توان از Annotation استفاده کرد|Annotation

- درنسخه‌های قدیمی js، شی‌گرایی وجود نداشت ولی در نسخه جدید به آن اضافه شده ولی با ts دارای تفاوت‌هایی است که در قطعه کد زیر به آن می‌پردازیم:

<div dir="ltr">
	
   	// JS🟨
	class User {
	    #name
	    constructor(name) {
	        this.#name = name;
	    }
	}
	const user = new User('Tom');
	
	// TS🟦
	class User {
	    #name: string 
	    constructor(name: string) {
	        this.#name = name;
	    }
	}
	const user = new User('Tom')

	
</div>

تنها تفاوت در تعریف متغیر name است که در ts باید نوع آن‌را مشخص کرد.

- در ts می‌توان داده‌ها را با ساختار خاصی ساخت. اینکار به وسیله‌ type و interface امکان‌پذیر است که در بخش‌های بعدی به آن‌ها اشاره می‌شود.

- در ts کد ابتدا به زبان js کامپایل و سپس اجرا می‌شود. برای همین اگر اروری داشته باشد قبل از اجرای کد باید آن‌را رفع کرد. به مثال زیر توجه کنید:

<div dir="ltr">

TS:

</div>

<div dir="ltr">

    s = "ali";
    console.log(s); // error s not defined
    s = 12;
    console.log(s); // error s not defined

</div>

<div dir="ltr">

Js:

</div>

<div dir="ltr">

    s = "ali";
    console.log(s); //ali
    s = 12;
    console.log(s); //12

</div>

- در ts ما برای annotation به شکل زیر عمل میکنیم:

<div dir="ltr">

    var variableName: TypeAnnotation = value;  

</div>

مثلا: 

<div dir="ltr">

    var age: number = 44;         // number variable  
    var name: string = "Ali";     // string variable  


</div>

اگر در ادامه به متغیر name مقداری عددی تخصیص دهیم به ارور میخوریم ولی در js این ویژگی وجود ندارد.

<div dir="ltr">

    // JS🟨
    var name = “Ali”;
    name = 44 ; // valid

    // TS🟦
    var name = “Ali”;
    name = 44 ; // error



</div>

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
