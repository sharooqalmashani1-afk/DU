# DU Smart Assistant — دليل التشغيل والنشر

موقع تجريبي مستقل للرد على استفسارات جامعة ظفار. **ليس منتجًا أو خدمة معتمدة أو رسمية من الجامعة.** صورة الخلفية مقدمة من مالك المشروع. لا يتطلب النموذج الجاهز أي مفاتيح أو خادم ليعمل بنمط الأسئلة الشائعة.

## الملفات
- `index.html`: واجهة الموقع والبطاقات والمحادثة
- `style.css`: التصميم المتجاوب باللغتين
- `script.js`: الترجمة، البحث في الأسئلة الشائعة والتواصل الاختياري مع AI
- `assets/du-campus.png`: صورة الجامعة المرفقة
- `worker.js`: خادم Cloudflare منفصل لتفعيل Gemini (اختياري)

## تشغيل فوري
1. فك الضغط واحتفظ بالملفات والمجلد `assets` بنفس الأسماء.
2. افتح `index.html` في Chrome. تعمل الأزرار والأسئلة الشائعة واللغة العربية/الإنجليزية مباشرة.
3. هذا الوضع **ليس ذكاءً اصطناعيًا توليديًا**؛ الاستفسارات خارج الموضوعات المعروفة تحصل على توجيه رسمي بدل جواب مخترع.

## نشر GitHub Pages
1. أنشئ مستودعًا **جديدًا** اسمه `du-smart-assistant` بدل الكتابة فوق DhofarCare.
2. ارفع `index.html`, `style.css`, `script.js` ومجلد `assets` إلى جذر المستودع. لا ترفع `worker.js` على أنه موقع.
3. افتح Settings → Pages → Build and deployment → Deploy from a branch → main / (root) → Save.
4. سيكون عنوان الموقع المتوقع `https://YOUR-USERNAME.github.io/du-smart-assistant/` بعد اكتمال النشر.

## تفعيل Gemini عبر Cloudflare (اختياري)
1. أنشئ مفتاح Gemini من https://aistudio.google.com/apikey واحتفظ به سرّيًا.
2. في Cloudflare اختر Workers & Pages → Create → Start with Hello World، وسمِّ Worker جديدًا `du-assistant-api` (لا تستبدل خادم `dhofarcare-api` الذي يستخدم للحجوزات المنزلية).
3. اضغط Edit code، واستبدل كل الكود بمحتوى `worker.js` ثم Deploy.
4. في Settings → Variables and Secrets أضف `GEMINI_API_KEY` من نوع **Secret** بقيمة المفتاح، وأضف `ALLOWED_ORIGINS` من نوع Text بقيمة `https://YOUR-USERNAME.github.io` (من دون مسار المستودع). اضغط Deploy.
5. داخل `script.js` عدّل أول سطر إعداد من `API_URL: ''` إلى `API_URL: 'https://du-assistant-api.YOUR-SUBDOMAIN.workers.dev'`. ارفع الملف المعدّل إلى GitHub.
6. افتح الموقع وجرّب سؤالًا مفتوحًا بالعربية والإنجليزية. إذا تعطلت الخدمة تظهر إجابة الأسئلة الشائعة الاحتياطية.

**أمان مهم:** إن واجهة Gemini العامة تحتاج قيود استخدام ومكافحة إساءة الاستخدام (rate limiting / Cloudflare Turnstile) قبل نشر الخدمة للعامة؛ CORS وحده لا يحمي API من استدعاءات غير المتصفح. لا تخزن أو ترسل بيانات طلاب شخصية، كلمات مرور أو ملفات سرية إلى Gemini. راجع سياسة الجامعة وحماية البيانات قبل أي تشغيل رسمي.

## ما هي البيانات المؤكدة؟
- المصدر الرسمي للتخصصات: https://www.du.edu.om/programs-and-degrees-offered/
- تقويم 2026–2027: https://www.du.edu.om/ar/academic-calendar-2026-2027/
- دائرة القبول والتسجيل: https://www.du.edu.om/department-of-admission-registration-2/
- التواصل: https://www.du.edu.om/contact-us/
- إعلان استقبال طلبات 2026–2027: https://www.du.edu.om/ar/dhofar-university-opens-admissions-for-2026-2027/

**تحديث البيانات:** موعد تسجيل المقررات 7–10 سبتمبر 2026 وفق التقويم ليس بالضرورة آخر موعد لقبول الطلبة الجدد. لا توجد في المشروع رسوم محددة مفترضة. راجع الروابط الرسمية لتحديث الإجابات دوريًا.
