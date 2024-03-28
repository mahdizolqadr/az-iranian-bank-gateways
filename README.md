<!--![GitHub All Releases](https://img.shields.io/github/downloads/ali-zahedi/az-iranian-bank-gateways/total)-->
<!--![GitHub issues](https://img.shields.io/github/issues/ali-zahedi/az-iranian-bank-gateways)-->
# AZ Iranian Bank Gateway Framework config

![GitHub](https://img.shields.io/github/license/ali-zahedi/az-iranian-bank-gateways)
![GitHub](https://img.shields.io/pypi/pyversions/az-iranian-bank-gateways.svg)
![GitHub](https://img.shields.io/pypi/v/az-iranian-bank-gateways.svg)
![GitHub](https://img.shields.io/pypi/dm/az-iranian-bank-gateways.svg?style=flat-square)
[![Join the chat at https://gitter.im/az-iranian-bank-gateways/community](https://badges.gitter.im/az-iranian-bank-gateways/community.svg)](https://gitter.im/az-iranian-bank-gateways/community?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

<p dir="rtl">
 کدهای آزاد و متن باز به زبان پایتون (python) که برای ارتباط با درگاه های بانکهای ایرانی در جنگو (Django) توسعه داده شده است.

 <p dir="rtl">
 در حال حاضر درگاه های با درگاه های زیر می توانید پرداخت کنید.
 </p>

 1. [درگاه پرداخت بانک ملی ایران (BMI)](https://mmp.sadadpsp.ir/Browse/MerchantRequestForm?@TermType_Shaparakabbr=INT)

 1. [درگاه پرداخت بانک سامان (SEP)](https://www.sep.ir/iemerchantregister)

 1. [درگاه پرداخت زرین پال](https://next.zarinpal.com/auth/register)

 1. [درگاه پرداخت آی دی پی (IDPay)](https://idpay.ir/s/664153)

 1. [درگاه پرداخت زیبال](https://zibal.ir)

 1. [درگاه پرداخت باهمتا](https://webpay.bahamta.com?rc=Sv7oH)

 1. [درگاه به پرداخت](http://www.behpardakht.com/)

 1. [درگاه پی ورژن ۱](https://www.pay.ir/)

[[_TOC_]]

<h1 dir="rtl">آموزشی</h1>

1. [یوتیوب](https://youtu.be/VnwY7DJlPKs)
1. [آپارات](https://www.aparat.com/v/DxL5J)
1. [آکادمی ژاک](https://academy.zhaak.com/course/236/python-tips)



<h1 dir="rtl">نصب</h1>

<p dir="rtl"> نصب از طریق پکیج منیجر </p>

``pip install az-iranian-bank-gateways``


<h1 dir="rtl">تنظیمات</h1>

### settings.py

<p dir="rtl"> در فایل `settings.py` تنظیمات زیر را انجام میدهیم. </p>


 ``` python
 INSTALLED_APPS = [
     # ....
     "azbankgateways",
     # ...
 ]
 AZ_IRANIAN_BANK_GATEWAYS = {
     "GATEWAYS": {
         "BMI": {
             "MERCHANT_CODE": "<YOUR MERCHANT CODE>",
             "TERMINAL_CODE": "<YOUR TERMINAL CODE>",
             "SECRET_KEY": "<YOUR SECRET CODE>",
         },
         "SEP": {
             "MERCHANT_CODE": "<YOUR MERCHANT CODE>",
             "TERMINAL_CODE": "<YOUR TERMINAL CODE>",
         },
         "ZARINPAL": {
             "MERCHANT_CODE": "<YOUR MERCHANT CODE>",
             "SANDBOX": 0,  # 0 disable, 1 active
         },
         "IDPAY": {
             "MERCHANT_CODE": "<YOUR MERCHANT CODE>",
             "METHOD": "POST",  # GET or POST
             "X_SANDBOX": 0,  # 0 disable, 1 active
         },
         "ZIBAL": {
             "MERCHANT_CODE": "<YOUR MERCHANT CODE>",
         },
         "BAHAMTA": {
             "MERCHANT_CODE": "<YOUR MERCHANT CODE>",
         },
         "MELLAT": {
             "TERMINAL_CODE": "<YOUR TERMINAL CODE>",
             "USERNAME": "<YOUR USERNAME>",
             "PASSWORD": "<YOUR PASSWORD>",
         },
         "PAYV1": {
             "MERCHANT_CODE": "<YOUR MERCHANT CODE>",
             "X_SANDBOX": 0,  # 0 disable, 1 active
         },
     },
     "IS_SAMPLE_FORM_ENABLE": True,  # اختیاری و پیش فرض غیر فعال است
     "DEFAULT": "BMI",
     "CURRENCY": "IRR",  # اختیاری
     "TRACKING_CODE_QUERY_PARAM": "tc",  # اختیاری
     "TRACKING_CODE_LENGTH": 16,  # اختیاری
     "SETTING_VALUE_READER_CLASS": "azbankgateways.readers.DefaultReader",  # اختیاری
     "BANK_PRIORITIES": [
         "BMI",
         "SEP",
         # and so on ...
     ],  # اختیاری
     "IS_SAFE_GET_GATEWAY_PAYMENT": False,  # اختیاری، بهتر است True بزارید.
     "CUSTOM_APP": None,  # اختیاری
 }
 ```

1. `GATEWAYS` :  تنظیمات مربوط به هر بانک به صورت دیکشنری های جدا در این قسمت وجود دارد. تنظیماتی مانند کلاس اجرا کننده، کلیدهای امنیتی که توسط بانک در اختیار شما قرار می گیرد.

1. `DEFAULT`: در زمانی که به سازنده فکتوری پارامتری ارسال نشود از این تنظیم به عنوان بانک پیش فرض استفاده خواهد شد و ارتباطات با این بانک برقرار می شود.

1. `CURRENCY - (IRR, IRT)`: واحد پولی که نرم افزار با آن کار می کند. این واحد پولی فارغ از واحد پولی درگاه خواهد بود.  در صورتی که واحد پولی نرم افزار با واحد پولی درگاه بانک متفاوت باشد تبدیل ریال به تومان یا بالعکس انجام خواهد شد.

1. `TRACKING_CODE_QUERY_PARAM `: پارامتری که در هنگام بازگشت از درگاه به کال بک یو آر ال تعیین شده تنظیم و ارسال می گردد. به عنوان مثال زمانی که از کاربر از درگاه بانک باز می گردد چه پرداخت موفق داشته باشد و چه نا موفق کاربر به لینکی که در هنگام استفاده از درگاه تنظیم شده است٬ ارجاع داده می شود و در انتهای آن این رشته + کد پیگیری بازگردانده می شود تا بتوان داده ها را از این طریق بازیابی کرد.

1. `TRACKING_CODE_LENGTH`: طول کد پیگیری تولید شده توسط سیستم است. دقت شود که در برخی درگاه ها مانند درگاه بانک ملی ایران، طول ۲۰ کاراکتر خطای `شماره سفارش ارسال نشده است` را می دهد.

1. `SETTING_VALUE_READER_CLASS`: با مقدار دهی به این تنظیم شما می توانید حالت یک متغیر خوان اضافه کنید که قابلیت های دیگری مثل پروایدر و پشتیبانی از یک بانک با چند اکانت و ... را به آن اضافه کنید.

1. `BANK_PRIORITIES`: این آرایه اختیاری است. زمانی که وضعیت اتصال به درگاه به صورت خودکار تعیین شده باشد، ابتدا به بانک پیش فرض متصل می شود و سپس بر این اساس شروع به اتصال خواهد کرد، تا به اولین درگاه فعال برسد. در حالت پیش فرض این آرایه خالی است که بعد از اتصال به درگاه مورد نظر در صورت خطا بقیه درگاه ها امتحان نخواهند شد.

1. `IS_SAMPLE_FORM_ENABLE`: یو آر ال های مربوط به تست درگاه بانک را فعال و یا غیر فعال می کند. در صورت فعال بودن می توانید از طریق آدرس زیر درگاه پرداخت را امتحان کنید.

   * [Sample payment](http://127.0.0.1:8000/bankgateways/sample-payment/)

1. `CALLBACK_NAMESPACE`: اگر میخواهید تابع کال بک داخلی را اوررایت کنید یا پروژه دارای اپ های مختلفی است و قسمت پرداخت در اپ جداگانه ای قرار دارد میتوانید محل قرار گیری یو آر ال های پیشفرض را تغییر دهید  برای مثال:
   ```
   'CALLBACK_NAMESPACE': 'api:payment:callback',
    ```
1. `GO_TO_BANK_GATEWAY_NAMESPACE`: اگر میخواهید تابع رفتن به دروازه بانک داخلی را اوررایت کنید یا پروژه دارای اپ های مختلفی است وقسمت پرداخت در اپ جداگانه ای قرار دارد میتوانید محل قرار گیری یو آر ال های پیشفرض را تغییر دهید برای مثال:
    ```
     'GO_TO_BANK_GATEWAY_NAMESPACE': 'api:payment:go-to-bank-gateway',
    ```
1. `SAMPLE_RESULT_NAMESPACE`: اگر میخواهید صفحه نمونه داخلی را اوررایت کنید یا پروژه دارای اپ های مختلفی است وقسمت پرداخت در اپ جداگانه ای قرار دارد میتوانید محل قرار گیری یو آر ال های پیشفرض را تغییر دهید برای مثال:
    ```
     'SAMPLE_RESULT_NAMESPACE': 'api:payment:sample-result',
    ```
1. `'IS_SAFE_GET_GATEWAY_PAYMENT'`:<br>
   ```
   'IS_SAFE_GET_GATEWAY_PAYMENT': True,
   ```
   <p dir="rtl"> توصیه میشه True باشه.</p>
   <p dir="rtl"> درصورتی که مقدار برابر با True قرار بگیرد تابع redirect_gateway از دسترس خارج میشودو باید از تابع get_gateway استفاده شود.</p>
1. `CUSTOM_APP` : <br>
   ```
   CUSTOM_APP : 'api:payment',
   ```
   <p dir="rtl">
   اگر نیاز ندارید توابع داخلی را اوررایت کنیدو فقط به این نیاز دارید که مسیر یو ار ال های داخلی را در اپ جداگانه ای قرارگیرد میتوانید از این گزینه برای ادرسی دهی محل قرار گیری اپ استفاده کنید
   </p>
### urls.py

<p dir="rtl">
 در فایل `urls.py`
</p>

```python
from django.contrib import admin
from django.urls import path

from azbankgateways.urls import az_bank_gateways_urls

admin.autodiscover()

urlpatterns = [
    path("admin/", admin.site.urls),
    path("bankgateways/", az_bank_gateways_urls()),
]
```
<p dir="rtl">
با اضافه کردن آدرس بالا به لیست یو آر ال ها، پرداخت ها پس از درگاه به این مسیر هدایت و اعتبار سنجی می شوند و سپس مجدد به سمت کال بکی که به ازای هر درخواست تنظیم می شود، مسیر یابی خواهد شد.
</p>

### Migrate
<p dir="rtl">
بعد از انجام تنظیمات دستور زیر را اجرا می کنیم.
</p>

```
python manage.py migrate
```

<h4 dir="rtl">اگر از reverse proxy و https استفاده می کنید برای رفع موارد احتمالی حتما تنظیمات این <a href="https://stackoverflow.com/questions/62047354/build-absolute-uri-with-https-behind-reverse-proxy/65934202#65934202">لینک</a> را انجام دهید.</h4>


<h1 dir="rtl">نحوه استفاده</h1>
<h2 dir="rtl">ارسال به بانک</h2>

<h3 dir="rtl">برای وقتی که تنظیمات IS_SAFE_GET_GATEWAY_PAYMENT': False'</h3>
<p dir="rtl">
 برای استفاده و اتصال به درگاه بانک کافی است یک `BankFactory` ایجاد کنیم و پارامترهای اجباری را تنظیم کنیم. سپس کاربر را می توانیم به درگاه بانک هدایت  کنیم.
</p>


```python
import logging
from django.urls import reverse
from azbankgateways import (
    bankfactories,
    models as bank_models,
    default_settings as settings,
)
from azbankgateways.exceptions import AZBankGatewaysException


def go_to_gateway_view(request):
    # خواندن مبلغ از هر جایی که مد نظر است
    amount = 1000
    # تنظیم شماره موبایل کاربر از هر جایی که مد نظر است
    user_mobile_number = "+989112221234"  # اختیاری

    factory = bankfactories.BankFactory()
    try:
        bank = (
            factory.auto_create()
        )  # or factory.create(bank_models.BankType.BMI) or set identifier
        bank.set_request(request)
        bank.set_amount(amount)
        # یو آر ال بازگشت به نرم افزار برای ادامه فرآیند
        bank.set_client_callback_url(reverse("callback-gateway"))
        bank.set_mobile_number(user_mobile_number)  # اختیاری

        # در صورت تمایل اتصال این رکورد به رکورد فاکتور یا هر چیزی که بعدا بتوانید ارتباط بین محصول یا خدمات را با این
        # پرداخت برقرار کنید.
        bank_record = bank.ready()

        # هدایت کاربر به درگاه بانک
        return bank.redirect_gateway()
    except AZBankGatewaysException as e:
        logging.critical(e)
        # TODO: redirect to failed page.
        raise e
```

<h3 dir="rtl">برای وقتی که تنظیمات IS_SAFE_GET_GATEWAY_PAYMENT': True'</h3>
<p dir="rtl">
 در این قسمت مثل مثال قبل عمل میکنیم تنها تفاوت این است که از تابع get_gateway بجای redirect_gateway استفاده میکنیم دلیل این کار افزایش امنیت و تغییر صفحهredirect میباشد.
</p>


```python
import logging
from django.urls import reverse
from django.shortcuts import render
from azbankgateways import (
    bankfactories,
    models as bank_models,
    default_settings as settings,
)
from azbankgateways.exceptions import AZBankGatewaysException


def go_to_gateway_view(request):
    # خواندن مبلغ از هر جایی که مد نظر است
    amount = 1000
    # تنظیم شماره موبایل کاربر از هر جایی که مد نظر است
    user_mobile_number = "+989112221234"  # اختیاری

    factory = bankfactories.BankFactory()
    try:
        bank = (
            factory.auto_create()
        )  # or factory.create(bank_models.BankType.BMI) or set identifier
        bank.set_request(request)
        bank.set_amount(amount)
        # یو آر ال بازگشت به نرم افزار برای ادامه فرآیند
        bank.set_client_callback_url(reverse("callback-gateway"))
        bank.set_mobile_number(user_mobile_number)  # اختیاری

        # در صورت تمایل اتصال این رکورد به رکورد فاکتور یا هر چیزی که بعدا بتوانید ارتباط بین محصول یا خدمات را با این
        # پرداخت برقرار کنید.
        bank_record = bank.ready()

        # هدایت کاربر به درگاه بانک
        context = bank.get_gateway()
        return render(request, "redirect_to_bank.html", context=context)
    except AZBankGatewaysException as e:
        logging.critical(e)
        return render(request, "redirect_to_bank.html")
```

<p dir="rtl">
در صورتیکه تمایل دارید به صورت خودکار به اولین درگاه در دسترس متصل شوید. ابتدا از قسمت تنظیمات در بخش `BANK_PRIORITIES
` اولویت های بانک های مد نظر را وارید کنید. سپس به جای استفاده از متد `factory.create` از متد ‍`factory.auto_create` در این بخش استفاده کنید.
به متد auto_create می توانید مبلغ مد نظر را نیز برای صحت سنجی از حداقل مبلغ نیز ارسال کنید.
 </p>

`set_mobile_number` متدی است که پارامتر شماره موبایل کاربری که قصد خرید دارد را به آن پاس میدهیم. این شماره موبایل جهت پرداخت و پیگیری آسان تر به درگاه ارسال می شود

<h2 dir="rtl">ساخت صفحه redirect_to_bank.html </h2>
<p dir="rtl">
این صفحه درصورتی کارمیکند که IS_SAFE_GET_GATEWAY_PAYMENT': True' و view مربوطه تنظیم شود.<br> برای این کار در پوشه templates پروژه فایل redirect_to_bank.html را ایجاد کرده و محتوای زیر را در آن قرار میدیم (میتونید با سلیقه خودتون سفاریشی کنید)
 </p>

```html
<!DOCTYPE html>
<html lang="fa">
<head>
    <meta charset="UTF-8">
    <title>انتقال به درگاه پرداخت</title>
</head>
<body>

   {% if url %}
     <h5>در حال اتصال به درگاه پرداخت ...</h5>
   {% else %}
     <h5>خطا در ارتباط با درگاه</h5>
   {% endif %}

   {% if url %}
      <form id='id_form' action="{{ url }}" method="{{ method }}">
          {% csrf_token %}
          {% for key, value in params.items %}
              <input type="hidden" name="{{ key }}" value="{{ value }}">
          {% endfor %}
      </form>

      <script type="text/javascript">
          window.onload = function () {

              function submitForm() {
                  document.forms['id_form'].submit();
              }

              submitForm();
          }
      </script>
   {% endif %}
</body>
</html>
```


<h2 dir="rtl">بازگشت از بانک</h2>

<p dir="rtl">
وضعیت رکورد بانک به شرح ذیل می باشد.
 </p>

1. `WAITING`: در انتظار برای انتقال کاربر به درگاه بانک

1. `REDIRECT_TO_BANK`: کاربر به درگاه بانک منتقل شده است ولی هنوز از درگاه باز نگشته است.

1. `RETURN_FROM_BANK`: کاربر از درگاه برگشته ولی عملیات صحت سنجی٬ یا تکمیل نشده است یا با خطا درهنگام تایید از سوی بانک مواجه شده است. در این شرایط می توان با فراخوانی مجدد در بازه زمانی کمتر از ۱۵ دقیقه که کاربر بازگشته است٬ عملیات تایید را مجدد درخواست کرد. شرح تایید مجدد در پایین تر آورده شده است.

1. `CANCEL_BY_USER`: پرداخت توسط کاربر کنسل شده است.

1. `EXPIRE_GATEWAY_TOKEN`: ارتباط با درگاه بانک برقرار شده ولی کاربر به درگاه هدایت نشده است.

1. `EXPIRE_VERIFY_PAYMENT`: در بازه زمانی ۱۵ دقیقه پس از بازگشت٬ موفق به تایید اطلاعات پرداخت نشده ایم.

1. `COMPLETE`: وضعیت پرداخت موفق است.


```python
import logging

from django.http import HttpResponse, Http404
from django.urls import reverse

from azbankgateways import (
    bankfactories,
    models as bank_models,
    default_settings as settings,
)


def callback_gateway_view(request):
    tracking_code = request.GET.get(settings.TRACKING_CODE_QUERY_PARAM, None)
    if not tracking_code:
        logging.debug("این لینک معتبر نیست.")
        raise Http404

    try:
        bank_record = bank_models.Bank.objects.get(tracking_code=tracking_code)
    except bank_models.Bank.DoesNotExist:
        logging.debug("این لینک معتبر نیست.")
        raise Http404

    # در این قسمت باید از طریق داده هایی که در بانک رکورد وجود دارد، رکورد متناظر یا هر اقدام مقتضی دیگر را انجام دهیم
    if bank_record.is_success:
        # پرداخت با موفقیت انجام پذیرفته است و بانک تایید کرده است.
        # می توانید کاربر را به صفحه نتیجه هدایت کنید یا نتیجه را نمایش دهید.
        return HttpResponse("پرداخت با موفقیت انجام شد.")

    # پرداخت موفق نبوده است. اگر پول کم شده است ظرف مدت ۴۸ ساعت پول به حساب شما بازخواهد گشت.
    return HttpResponse(
        "پرداخت با شکست مواجه شده است. اگر پول کم شده است ظرف مدت ۴۸ ساعت پول به حساب شما بازخواهد گشت."
    )
```


<h2 dir="rtl">درخواست تایید مجدد از بانک</h2>

```python
import logging
from azbankgateways import (
    bankfactories,
    models as bank_models,
    default_settings as settings,
)

factory = bankfactories.BankFactory()

# غیر فعال کردن رکورد های قدیمی
bank_models.Bank.objects.update_expire_records()

# مشخص کردن رکوردهایی که باید تعیین وضعیت شوند
for item in bank_models.Bank.objects.filter_return_from_bank():
    bank = factory.create(
        bank_type=item.bank_type, identifier=item.bank_choose_identifier
    )
    bank.verify(item.tracking_code)
    bank_record = bank_models.Bank.objects.get(tracking_code=item.tracking_code)
    if bank_record.is_success:
        logging.debug("This record is verify now.", extra={"pk": bank_record.pk})
```

## TODO

- [X] Add BMI support
- [X] Add SEP support
- [X] Add Zarinpal support
- [X] Add IDPay support
- [X] Add Zibal support
- [X] Add Bahamta support
- [X] Add BehPardakht support
- [X] Add Pay.ir V1 support
- [ ] Add Pay.ir V2 support
- [ ] Add nextpay-ir support (need MERCHANT_CODE & etc.)
- [ ] Add Paystar support (need MERCHANT_CODE & etc.)
- [ ] Add Sepah Bank support (need MERCHANT_CODE & etc.)
- [ ] Managing verification Process when Gateway Not Available
- [ ] Add celery beat for when Gateway Not Available





## توسعه

<p dir="rtl">
 اگر از این بسته استفاده می کنید و خوشتون اومده با دادن ستاره به ما دلگرمی بدید.البته که اگر زمان بگذارید و گسترش بدید خیلی استقبال می کنیم و خوشحال میشیم. البته که در هیچ کدوم از این موارد اصراری نیست.
</p>

<p dir="rtl">
برای نصب وابستگی ها از طریق زیر اقدام کنید و بعد از انجام تغییرات مرج ریکوئست ارسال کنید.
</p>

```shell
pip install -e ".[dev]"
pre-commit install
```
<p dir="rtl">
بیشتر بخوانیم:
</p>

* [flake8](https://flake8.pycqa.org/en/latest/)
* [black](https://black.readthedocs.io/en/stable/)

<p dir="rtl">
 شاد باشید و خندون
</p>


# با تشکر از
* [erfanmosaddeghi ](https://github.com/erfanmosaddeghi) برای اصلاح حداقل مبلغ زرین پال
* [sina-am](https://github.com/sina-am) اضافه کردن درگاه بانک ملت
* [joejoe-am](https://github.com/joejoe-am) برای رفع مشکل اولویت بندی در اتصال خودکار
* [mash5026](https://github.com/mash5026) برای رفع مشکل unmarshalling ERROR: For input string
* [hypy13](https://github.com/hypy13) برای آپدیت به ورژن های بالاتر از جنگو ۳.۲
* [jam4li](https://github.com/jam4li) برای اضافه کردن سندباکس زرین پال
* [ravexina](https://github.com/ravexina) رفع مشکل تسویه حساب بانک ملت
* [nimaes80](https://github.com/nimaes80) اضافه کردن درگاه pay.ir ورژن یک
* [khademmilad](https://github.com/khademmilad) پشتیبانی از پایتون ۳.۱۰ و ۳.۱۱
* [Saman-Zand-H](https://github.com/Saman-Zand-H) رفع مشکل اتصال pay.ir در برخی موارد
* [MrMRM1](https://github.com/MrMRM1)  [بابت رفع مشکل امنیتی](https://github.com/ali-zahedi/az-iranian-bank-gateways/pull/65#issuecomment-1624927632)
* [MrMRM1](https://github.com/MrMRM1) اضافه شدن قابلیت اوررایت یا تغییر ادرس یو آر ال های پیشفرض
* [shiani](https://github.com/shiani) error occurs when the main language of site is Persian and it has to use gettext_lazy translation.
* [zamoosh](https://github.com/zamoosh) اضافه کردن وضعیت های  تراکنش در بانک ملت

## License

The MIT License (MIT). Please see [License File](LICENSE) for more information.


[لینک]: https://stackoverflow.com/questions/62047354/build-absolute-uri-with-https-behind-reverse-proxy/65934202#65934202را


[لینک]: https://stackoverflow.com/questions/62047354/build-absolute-uri-with-https-behind-reverse-proxy/65934202#65934202
