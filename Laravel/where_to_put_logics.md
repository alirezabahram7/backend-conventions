
#منطق برنامه هایمان را در کجا قرار دهیم.

ی از اصلی‌ترین چالش‌های برنامه‌نویسان خصوصا در رعایت اصول سالید (SOLID) این است که منطق برنامه را دقیقا در کجا قرار دهیم. در فریمورک لاروال عموما کنترلر را محل قرارگیری منطق برنامه می‌دانند اما این امر با ماهیت کنترلر و اصول سالید در تناقض است. من در ادامه سعی می‌کنم پیشنهاداتی برای توزیع منطق سیستم در کلاس‌ها و توابع مختلف در ساختار لاراول ارایه دهم ( این قرارداد پیشنهادی می‌تواند با کمی تغییر در فریمورک‌ها و زبان‌های دیگر هم مورد استفاده قرار بگیرد). تاکید می‌کنم که این صرفا یک قرارداد پیشنهادی‌ست.

###- Controller Classes

    - اتصال روت ها به خروجی ریسورس
    - لاجیک در این جا نباید باشد
    - فقط دریافت و فراهم کردن خروجی برای کلاینت

###- Model Classes

    - روابط با دیگر مدل ها
    - اسکوپ‌ها ( کویری‌های پرکاربرد روی یک ریسورس خاص)
- attributes

###- Service Classes

    - عملیاتی که بر روی یک یا دو ریسورس مشخص انجام می‌گیرد
    - ترجیحا به صورت سینگلتون ایجاد شود
    - ترجیحا هیچ درگیری مستقیمی با پایگاه داده ندارد.
    - اطلاعاتی را در درون آبجکت‌هایش نگه ندارد
    - حتما از یک اینترفیس مرجع پیاده سازی شود

###- Action Classes

    - مشابه سرویس اما فقط یک کار انجام می‌دهد
    - از لحاظ ساختار و عملکرد مثل جاب‌هاست : یک تابع  handle  دارد.

###- Job Classes

    - استفاده در صف ها
    - یک کار مشخص در یک صف مشخص
    - منطق مربوط به ان کار خاص در صورتیکه قابل استفاده مجدد است بهتر است در جایی دیگر قرار داده شود

###-Traits

    - راه حل پی اچ پی برای مسئله ارث بری چندگانه
    - توابع مورد استفاده در کلاس های مختلف که به ریسورس خاصی مربوط یاوابسته نیستند
    - در ضمن جامعیت هلپرها را هم ندارند

###- Observer Classes

    - کارهایی که قبل یا بعد از یک رخداد CRUD لازم است انجام شود
    - بخش زیادی از منطق کنترلر که مربوط به انجام عملیاتی قبل یا بعد از عملیات اصلی ست در اینجا قرار می گیرد
    - باید توجه داشت که در بروزرسانی و درج چندگانه اطلاعات این کلاس ها فراخوانده نمی شوند
    - در موارد مرتبط با رخدادهای کراد بهتر است از آبزرور به جای ایونت/لیسنر استفاده شود.

###- Event/Listener Classes

    - در مواردی که نیاز است پس از انجام یک عمل خاص فرایند یا فرایندهای خاص دیگری فراخوانده و اجرا شوند

###- Helper Functions

    - توابع پراستفاده
    - عمدتا محاسباتی
    - بدون وابستگی به ریسورس

###- Repository Classes

    - برای استفاده در مواردی که با داده ی پایگاه داده سر و کار داریم
    - شامل کوئری های مختلف 
    - کوئری هایی که می توانند در اسکوپ ها قرار گیرند بهتر است در ریپازیتوری نباشند
    - در صورتی که از ORM استفاده می شود( مگر در کوئری های پیچیده‌تر ) بهتر است از ریپازیتوری استفاده نشود.
    - حتما از یک اینترفیس مرجع پیاده سازی شده باشد.

###- Pipe Classes

    - در مواردی که چند تابع یا چند کلاس لازم است روی یک دیتا یا ریسورس پردازش خاصی انجام دهند و نتیجه را به کلاس یا تابع دیگر پاس دهند

###- Facades
`در مواردی که چند تابع یا چند کلاس قرار است روی یک موجودیت کار کنند. پیچیدگی همه کلاس‌ها و توابع تحت عنوان یک کلاس facade پنهان می‌شود. (ر ک الگوی طراحی Facade)
`

