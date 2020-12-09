<div dir="rtl">

# Introduction   

زبان TypeScript یک سوپر‌ست نوع‌گذاری شده از JavaScript است که به زبان JavaScript کامپایل می‌شود. به بیانی دیگر، TypeScript  همان JavaScript است برای توسعه در مقیاس کاربردی. این زبان به شما امکان می دهد JavaScript را همانطور که می خواهید بنویسید و خوانایی و رفع اشکال آن را بهبود می بخشد. این زبان یک زبان شی گرای خالص است و فریمورک های معروفی مانند Angular 2.0 به این زبان نوشته شده اند.

# Requirements

همان طور که گفته شد ابتدا باید برنامه نوشته شده در زبان Typescript را به زبان JavaScript کامپایل و سپس آن را نیز تفسیر کرد. پس به nodeJs و type Script Compiler(tsc) نیاز داریم. همچنین نصب npm نیز توصیه می شود.

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

	1.ابتدا فایل مورد نظر را با پسوند `.ts` ذخیره می کنیم (برای مثال `test.ts`)
	
	2.سپس فایل مورد نظر را با دستور `tsc [file_name].ts` به زبان js کامپایل می کنیم.(خروجی آن یک فایل به نام `[file_name].js` است)
	
  	3.در نهایت برای اجرای فایل نهایی دستور `node [file_name].js` را اجرا می کنیم.
	
همچنین پکیج هایی نیز وجود دارند که مراحل 2 و 3 را ترکیب می کنند.(مانند `ts-node`)

