---
title: "environment variables"
date: 2022-07-18T01:18:48+04:30
draft: false
---
<div dir='rtl'>

[![img](https://user-images.githubusercontent.com/51704066/182064196-004d11d5-0228-487c-8d1b-6f1a61b75c9d.jpg)](https://user-images.githubusercontent.com/51704066/182064196-004d11d5-0228-487c-8d1b-6f1a61b75c9d.jpg)


### فهرست
> - [توضیحات](#توضیحات)
> - [تعریف موقت متغییر محیطی](#تعریف-موقت-متغیر-محیطی)
> - [تعریف دائمی متغییر محیطی](#تعریف-دائمی-متغییر-محیطی)
> - [فراخوانی متغییر های محیطی](#فراخوانی-متغییر-های-محیطی)
> - [ متغییر های محیطی پیشفرض](#متغییر-های-محیطی-پیشفرض)
> - [نویسنده یا نویسندگان](#نویسنده-یا-نویسندگان)

---
### توضیحات

متغییر های محیطی همانند متغییر هایی هستند که در برنامه نویسی استفاده می‌کنیم.
اما اگر آشنایی ندارید جعبه‌ خالی‌ای را در نظر بگیرید، شما می‌توانید هر محتوایی را داخل جعبه قرار بدین و هر موقع نیاز شد محتوای آن را بر دارید 
و یا جایگزین کنید، متغییر ها شبیه به جعبه هایی هستند با نام هایی مشخصل.

**اما متغییر های محیطی چیست؟** 

زمانی که شما با bash کار می‌کنید، متغییر هایی هستند که بر اساس فایل های کانفیگ مثل bashrc، در مفسر شما تنظیم می‌شوند.
برنامه ها و حتی خود bash از این متغییر ها در زمان اجرای برنامه استفاده می‌کنند. 
مثلا شما هر زمانی که در bash ابزاری را اجرا می‌کنید، bash باید مسیر آن ابزار را بداند تا آن را اجرا کند به همین خاطر متغییر محیطی که شامل
تمام مسیر های برنامه های اجرایی است وجود دارد و هر زمان که نام ابزار مانند ls را وارد کنید، bash از مسیر های تعریف شده در متغییر PATH
دنبال فایل اجرایی خواهد گشت و آن را اجرا خواهد کرد.

شما می‌توانید متغییر های محیطی را ویرایش کنید، و یا یک متغییر جدید بسازید.

---

###  تعریف موقت متغیر محیطی

زمانی که شما یک متغییر محیطی را در _bash_ تعریف می‌کنید، این متغییر فقط در _child process_ های bash در دسترس خواهد بود و زمانی
که از این **پروسه خارج** شوید، مقدار این **متغییر هم از بین خواهد** رفت.

برای تعریف متغییر های محیطی از کلمه `export` و سپس _نام متغییر_ استفاده کنید و با علامت `=` مقدار را برای آن متغییر تنظیم کنید.

<div dir='ltr'>

```bash
export VAR1='foo'
export VAR2=VAR1
```
</div>

> دقت کنید که در زمان تعریف متغییر های محیطی باید علامت `=` به نام _متغییر_ و _مقدار_ آن چسبیده باشد.

---

### تعریف دائمی متغییر محیطی

برای اینکه یک متغییر محیطی را دائمی کنید باید آن را در فایل های کانفیگی که زمان اجرای ترمینال خوانده می‌شوند تعریف کنید.
فایل `bashrc.` در دایرکتوری _home_ هر کاربر است، کافیست یک متغییر را داخل این فایل تعریف کنید.
<div dir='ltr'>

```bash
export VARDEFAULT='bar'
```
</div>

{{< note >}}

به این دقت داشته باشید که اگر بجای _bash_ از _shell_ های دیگری مانند _zsh_ استفاده می‌کنید، باید متغییر ها را درون فایل های _rc_ 
همان shell
ها تعریف کنید. برای مثال در _zsh_ فایل _zshrc_. فایل استارتاپ است.

{{< /note >}}


> متغییر هایی که در این فایل های
> rc
> ذخیره شوند فقط برای همان یوزر در دسترس خواهند بود.

برای اینکه این متغییر ها برای همه کاربران در دسترس باشند کافیست آنها را در مسیر
`/etc/environment`
تعریف کنید.

---

### فراخوانی متغییر های محیطی

استفاده و فراخوانی متغییر ها با استفاده از علامت `$` در سمت چپ نام‌شان است. برای مثال ما متغییر _foo_ را تعریف
و سپس چاپ می‌کنیم.
<div dir='ltr'>

```bash
export foo='bar'
echo $foo
echo 'the foo is' $foo
```
</div>

---

### متغییر های محیطی پیشفرض

همانطور که در مقدمه اشاره شد متغییر هایی وجود دارند که به صورت پیشفرض زمانی که یک _shell_ اجرا می‌شود تنظیم می‌شود. برخی از مهم
ترین های آنها:


|نام متغغیر|کاربرد|
|:----------:|:--------------------------------------------:|
|EDITOR | ویرایشگر متن پیشفرض |
|HOME | دایرکتوری کاربر فعلی |
|SHELL | مسیر shell کاربر فعلی|
|TERM | شبیه‌ساز ترمینال فعلی |
|PATH | مسیر های جست و جو برای اجرای کامند |
|MANPATH | مسر فایل man |
|LOGNAME | نام کاربر فعلی |
|TZ | منطقه زمانی که توسط ساعت سیستم استفاده می‌شود |

> برای دیدن تمامی متغییر های محیطی می‌توانید از کامند `env` استفاده کنید.

---
### نویسنده یا نویسندگان

</div>

- *[Arya](https://github.com/shabane)* | **<m.mohamadshabane@gmail.com>**

