# ختمة رتّل — حملة الـ 600 ألف

جمعية رتّل لتحفيظ القرآن الكريم بنجران · نوفمبر وديسمبر 2026.

## الملفات
| الملف | الوظيفة |
| --- | --- |
| `index.html` | **الصفحة العامة**: الختمة (30 جزءًا × 20 ألف ريال)، أبواب الخير، آخر المساهمات، طرق التبرع |
| `admin/index.html` | **لوحة التحكم** (بتسجيل دخول): تسجيل الدخل والإنجازات، السجل، الرسائل |
| `site-config.js` | طرق التبرع وبيانات التواصل في الصفحة العامة |
| `firebase-config.js` | إعدادات Firebase |
| `firestore.rules` | قواعد الحماية |
| `assets/` | الشعار وتنسيق لوحة التحكم |

## كيف تعمل الحماية
- الصفحة العامة تقرأ مستندًا واحدًا فقط `public/summary` فيه أرقام مجمّعة (بدون أسماء متبرعين ولا أعضاء ولا تعهدات).
- لوحة التحكم تتطلب تسجيل دخول Firebase. البيانات التفصيلية (`income` و`activities`) لا يقرؤها ولا يكتبها إلا الإيميلات الأربعة المكتوبة في `firestore.rules`.
- كل ما يسجله أحد الأعضاء يحدّث الملخص العام تلقائيًا.

## التفعيل (مرة واحدة)
1. أنشئ مشروعًا في https://console.firebase.google.com
2. **Build ← Firestore Database ← Create database** (موقع قريب مثل `me-central2`).
3. **Build ← Authentication ← Get started ← Email/Password ← Enable**.
4. من تبويب **Users** اضغط **Add user** وأضف الأربعة: إيميل وكلمة مرور لكل شخص.
5. في `firestore.rules` استبدل الإيميلات الأربعة بإيميلاتهم نفسها، ثم الصق الملف في Firestore ← **Rules** واضغط **Publish**.
6. **Project settings ← Your apps ← `</>`** سجّل تطبيق ويب وانسخ قيم `firebaseConfig` إلى `firebase-config.js`.
7. من **Authentication ← Settings ← User actions** عطّل إنشاء الحسابات الذاتي (Enable create) إن ظهر، ثم ارفع الملفات.
8. افتح `/admin/` وسجّل الدخول، وأضف أول دخل: ستظهر الأرقام في الصفحة العامة فورًا.

بدون الخطوات أعلاه يعمل الموقع في **وضع تجريبي** على جهازك فقط، ولا يوجد تسجيل دخول.

## النشر برابط بدون اسم الحساب
GitHub Pages يضع اسم الحساب في الرابط دائمًا. للحصول على رابط مثل `ratl.netlify.app`:
**Netlify**: Add new site ← Import from GitHub ← اختر المستودع (Build command فارغ، Publish directory = `.`) ← ثم Site settings ← Change site name.
بديل: **Cloudflare Pages** يعطي `اسم.pages.dev` بالطريقة نفسها.

## طرق التبرع
عدّل `site-config.js` (آيبان أو رابط منصة) وسيظهر في الصفحة العامة.

## تعديل الأعضاء أو المبادرات
في `admin/index.html` ابحث عن `const MEMBERS` و`const INITS`.
المستهدف والمدة: `const START='2026-11-01', END='2026-12-31', TARGET=600000, DAILY=10000` (وفي `index.html` السطر نفسه).
