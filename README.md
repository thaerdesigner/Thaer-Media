# Thaer Media — Website

Static marketing website for **Thaer Media** (design / branding / social-media agency). Plain
HTML/CSS/JS — no build tool, no package manager, no framework, no server-side code. Open the main
[`index.html`](index.html) to browse the homepage, contact page, course page, and six work galleries
offline. Shared content remains centralized in [`assets/js/data.js`](assets/js/data.js).
See **"التحكم بمحتوى الموقع"** below for the full guide to that file.

## Running locally

No build step. Keep the `assets/` folder beside `index.html`, then open `index.html` directly.
Use the site's links to move between all pages and galleries without a server. For a local HTTP
preview, run:

```bash
npx serve .
# or
python -m http.server 8000
```

Then visit `http://localhost:8000` (or whatever port the tool prints).

## Pages

| File | Description |
|---|---|
| `index.html` | Main offline entry point: homepage, contact, course, and six work-gallery views. Bilingual (AR/EN toggle in the header). |
| `work-social.html`, `work-identity.html`, `work-ads.html`, `work-print.html`, `work-content.html`, `work-marketing.html` | Standalone web versions of the work galleries. |
| `contact/index.html` | Published contact page at `/contact`. |
| `socialmedia.courses1/index.html` | Published course page at `/socialmedia.courses1`; its metadata uses the supplied course share design. |
| `contact.html` and `work-*.html` | Standalone compatibility copies; the main `index.html` also contains offline versions. |

## صور معاينة الروابط

كل صور المعاينة بصيغة PNG موجودة في [`assets/previews/`](assets/previews/). استبدل الصورة مع إبقاء
اسم الملف نفسه لتحديث المعاينة:

| الصفحة | ملف الصورة |
|---|---|
| الرئيسية والتواصل | `home-contact.png` |
| الدورة | `course.png` |
| أعمال السوشيال ميديا | `work-social.png` |
| الهوية البصرية | `work-identity.png` |
| الحملات الإعلانية | `work-ads.png` |
| المطبوعات | `work-print.png` |
| صناعة المحتوى | `work-content.png` |
| التسويق | `work-marketing.png` |

بيانات معاينة الرابط في كل صفحة تشير مباشرةً إلى الصورة المقابلة بهذا المجلد.

The public pages use clean URLs such as `/contact`, `/socialmedia.courses1`, and `/work-social`.
Keep the root `.htaccess` file when uploading to an Apache host; it redirects old `.html` and
`index.html` addresses and serves the clean routes.

From `index.html`, use the header, service cards, course slider, or CTA to switch between the
embedded views without opening a separate local HTML file. The offline views use local images,
styles, scripts, and page content from `assets/`. Custom web fonts are hosted remotely; without an
internet connection, the browser uses the declared system-font fallbacks.

## Project structure

```
assets/
  previews/  PNG images used for link previews on every public page
  css/       base.css (shared header/footer/tokens), home.css, work.css, contact.css
  js/        data.js (all content), render.js (builds pages from data.js), main.js (homepage), work.js (other 7 pages)
  images/    logo, hero photo, About section photos
  ad-slides/ homepage carousel images, all 1440 × 480 pixels
  service-icons/   the 6 homepage service icons
  work-covers/     homepage work-teaser cover photos (ar/ and en/ variants)
```

---

## التحكم بمحتوى الموقع من خلال data.js

معظم نصوص وصور صفحات الموقع الرئيسية موجودة بملف واحد:
**[`assets/js/data.js`](assets/js/data.js)**. الهدف إنك تقدر تعدّل أي نص أو تبدّل أي صورة بنفسك من
غير ما تحتاج تلمس ملفات الـHTML أو تطلب من مبرمج كل تعديل بسيط.

### قبل ما تبدأ

- افتح `assets/js/data.js` بأي محرر نصوص (Notepad، أو أفضل: VS Code لأنه بيلوّن الكود ويسهّل رؤية
  الأخطاء).
- **اعمل نسخة احتياطية من الملف قبل أي تعديل كبير** (انسخ `data.js` والصقه باسم مختلف، مثلاً
  `data-backup.js`) حتى تقدر ترجع للنسخة الأصلية لو صار خطأ.
- بعد أي تعديل، **افتح الموقع بالمتصفح وتأكد إنه شغال طبيعي** قبل ما تعتبر التعديل خلص. لو صار خطأ
  إملائي بالملف (نسيت فاصلة أو قوس)، الموقع كله بيتوقف عن الظهور — هاي الطريقة الوحيدة تكتشف فيها.

### القاعدة الذهبية: لا تلمس إلا اللي بين علامتي التنصيص

كل سطر بالملف شكله تقريباً هيك:

```js
whatsappDisplay: "+970 59 935 1383",
```

- `whatsappDisplay:` هو اسم الحقل — **لا تغيّره أبداً**.
- `"+970 59 935 1383"` هو القيمة — **هاي بس اللي تعدّلها**، وخليها دائماً بين علامتي تنصيص `" "`.
- الفاصلة `,` بآخر السطر **لازم تبقى موجودة** (إلا آخر عنصر بقائمة، احياناً بدون فاصلة — إذا مش
  متأكد، خلي الفاصلة، ما بتأثر).
- لا تحذف أي قوس `{ }` أو `[ ]` إلا وأنت متأكد شو بتسوي (شوف قسم "إضافة/حذف عنصر من قائمة" تحت).

### النصوص ثنائية اللغة {ar, en}

النصوص الثنائية اللغة المعرّفة في الملف مبنية بهالشكل:

```js
heading: { ar: "الرئيسية", en: "Home" }
```

`ar` هو النص اللي بيظهر بالوضع العربي، و`en` هو نفس النص بالإنجليزي. **لازم تعدّل الاثنين مع بعض**
حتى يبقى المحتوى متطابق باللغتين — لو عدّلت `ar` بس وتركت `en` قديم، زوار النسخة الإنجليزية رح
يشوفوا نص قديم ما بيطابق التعديل.

بعض العناوين (مثل عنوان الهيرو بالصفحة الرئيسية أو عناوين الأقسام) فيها وسوم HTML بسيطة داخل النص،
مثلاً:

```js
heading: { ar: "<span class='section-kicker'>خدماتنا:</span> ما نستطيع تقديمه...", en: "..." }
```

`<span class='section-kicker'>...</span>` هو اللي بيلوّن أول جزء من العنوان بالذهبي — لو عدّلت النص
جوا الوسم خليه بنفس الشكل (افتح `<span class='...'>` وسكره `</span>` بنفس المكان)، بس غيّر الكلام
اللي بالنص نفسه.

### تبديل صورة

كل حقل صورة قيمته مسار ملف، مثلاً:

```js
photo: "assets/images/hero-person.jpg"
```

1. احفظ الصورة الجديدة داخل نفس المجلد المذكور (`assets/images/` هون)، بنفس الاسم أو باسم جديد.
2. لو استخدمت اسم جديد، بدّل المسار بالكامل بالقيمة الجديدة، مثلاً:
   `photo: "assets/images/hero-person-2026.jpg"`.
3. **خلي صيغة الملف قريبة من الأصل** (jpg يبدّل بـjpg، png بـpng) **وحجم/نسبة أبعاد الصورة مقاربة
   للأصلية** — الموقع مبني على أبعاد معينة لكل صورة (خصوصاً صورة الهيرو وصور قسم "من نحن")، وصورة
   بنسبة أبعاد مختلفة جداً ممكن تظهر مقصوصة أو مشوهة.
4. الصورة لازم تكون فعلاً موجودة بنفس المسار المكتوب بالضبط (بما فيها حالة الأحرف بالإنجليزي) وإلا
   رح تظهر مكسورة.

**مجلدات الصور المستخدمة حالياً:**

| المجلد | يحتوي على |
|---|---|
| `assets/images/` | شعار الموقع، صورة الهيرو، صور قسم "من نحن" |
| `assets/ad-slides/` | صور سلايدر الصفحة الرئيسية. ملفات `ad-slide-01.jpg` إلى `ad-slide-05.jpg` للعربية، وملفات `ad-slide-01-en.jpg` إلى `ad-slide-05-en.jpg` للإنجليزية. استبدل كل صورة بالنسخة الجديدة بالاسم نفسه والأبعاد **1440 × 480**؛ تتبدل الصور تلقائيًا حسب لغة الموقع. |
| `assets/service-icons/` | أيقونات الخدمات الست بالصفحة الرئيسية |
| `assets/work-covers/ar/` و `assets/work-covers/en/` | صور غلاف شريط "مختارات من أعمالنا" — **نسختين منفصلتين**، وحدة تظهر بالوضع العربي ووحدة بالإنجليزي (`coverAr`/`coverEn`) |

### إضافة أو حذف عنصر من قائمة (array)

أشياء زي "آراء العملاء" أو معرض صور كل صفحة خدمة هي **قائمة (array)** — محصورة بين قوسين مربعين
`[ ]`، وجوّاها عدة عناصر `{ ... }` مفصولين بفواصل. مثال من آراء العملاء:

```js
testimonials: [
  { avatar: "01", quote: { ar: "...", en: "..." }, author: { ar: "...", en: "..." } },
  { avatar: "02", quote: { ar: "...", en: "..." }, author: { ar: "...", en: "..." } },
  { avatar: "03", quote: { ar: "...", en: "..." }, author: { ar: "...", en: "..." } }
]
```

**لإضافة عنصر رابع:** انسخ آخر `{ ... }` بالكامل (من `{` لـ `}`)، الصقه بعده، وضيف فاصلة `,` بعد
العنصر اللي قبله. بعدين عدّل القيم الجديدة جوا النسخة الملصوقة:

```js
testimonials: [
  { avatar: "01", quote: { ar: "...", en: "..." }, author: { ar: "...", en: "..." } },
  { avatar: "02", quote: { ar: "...", en: "..." }, author: { ar: "...", en: "..." } },
  { avatar: "03", quote: { ar: "...", en: "..." }, author: { ar: "...", en: "..." } },
  { avatar: "04", quote: { ar: "رأي العميل الجديد هون", en: "New client quote here" }, author: { ar: "اسم العميل", en: "Client name" } }
]
```

القائمة بتستوعب أي عدد عناصر من غير ما يخرب شكل الموقع — الشرائح والبطاقات بترتب نفسها تلقائياً.

**لحذف عنصر:** احذف `{ ... }` تبعه بالكامل، وتأكد إن آخر عنصر متبقي بالقائمة **بدون فاصلة بعده**
(الفاصلة بتيجي بين العناصر بس، مش بعد آخر وحدة).

نفس الأسلوب بالضبط ينطبق على: منصات التواصل (`socials`)، روابط القائمة العلوية (`nav`)، خدمات
الصفحة الرئيسية (`services`)، شريط الأعمال (`workTeaser`)، خطوات "كيف نعمل" (`process`)، ومعرض كل
صفحة خدمة (`work.social.gallery` وهيك).

### أهم الأقسام بالملف — وين تلاقي كل شي

| القسم | يتحكم بـ |
|---|---|
| `meta` | عنوان تبويب المتصفح ووصف محركات البحث |
| `contact` | رقم الواتساب والإيميل — **مصدر واحد**، يظهر تلقائياً بالفوتر وصفحة التواصل وزر الهيدر |
| `headerCta` | نص زر "ابدأ مشروعك" بأعلى كل صفحة |
| `socials` | أيقونات وروابط منصات التواصل بالفوتر |
| `nav` | روابط القائمة العلوية بالصفحة الرئيسية |
| `home.hero` | عنوان ووصف وأزرار وصورة الهيرو بأعلى الصفحة الرئيسية |
| `home.services` | بطاقات الخدمات الست |
| `home.workTeaser` | شريط "مختارات من أعمالنا" |
| `home.about` | قسم "من نحن": الصور الثلاث، العنوان، النص، النقاط الأربع |
| `home.process` | خطوات "كيف نعمل" الخمس |
| `home.testimonials` | آراء العملاء (السلايدر) |
| `home.cta` | قسم "لنبدأ" قبل الفوتر مباشرة |
| `footer` | نصوص الفوتر (يظهر بكل الصفحات الثمانية) |
| `work.social` / `work.identity` / `work.ads` / `work.print` / `work.content` / `work.marketing` | عنوان ووصف ومعرض كل صفحة خدمة (كل وحدة فيها `gallery` منفصلة) |
| `contactPage` | كل محتوى صفحة `contact.html`: العنوان، بطاقات التواصل، خطوات "كيف نبدأ" |

### ملاحظة عن معرض الأعمال (gallery)

كل عنصر بمعرض صفحات الخدمات الست شكله هيك:

```js
{ number: "01", title: { ar: "مساحة عمل", en: "Project Space" }, description: { ar: "سيتم إضافة المشروع هنا.", en: "The project will be added here." }, image: "" }
```

حالياً `image: ""` فاضية بكل العناصر، فبيظهر مكانها خلفية زخرفية بدل صورة حقيقية. **أول ما يصير
عندك صورة فعلية للمشروع**: احفظها بمجلد `assets/images/` (أو أي مجلد تفضله جوا `assets/`)، وحط
مسارها بدل الفراغين، مثلاً `image: "assets/images/project-01.jpg"` — وقتها بتظهر صورة المشروع
الحقيقية بدل الخلفية الحالية تلقائياً. عدّل كمان `title` و`description` ليوصفوا المشروع الفعلي
بدل النص المؤقت "سيتم إضافة المشروع هنا".

### أشياء ما بتتغير من data.js

بعض الأشياء مش "محتوى نصي/صورة" بسيط، فمتعمّدين تركها بره data.js — تغييرها يحتاج تعديل كود
(تواصل مع المبرمج):

- شعار الموقع بالوضع الفاتح/الداكن (`logo.png` / `logo-light.png`) وشكل التبديل بينهم.
- أيقونات منصات التواصل نفسها (الشكل/الرسمة) — تقدر تغيّر **الرابط** من `socials` بحرية، بس شكل
  الأيقونة (Instagram، WhatsApp...) مرسوم بالكود.
- الروابط الداخلية (إلى أي قسم/صفحة يوصل كل رابط) — هاي بنية تنقل الموقع، مو محتوى.

### أخطاء شائعة (وكيف تتجنبها)

- **نسيان فاصلة أو قوس** — أشيَع سبب يوقف الموقع بالكامل. لو الموقع بعد تعديل صار صفحة بيضاء أو
  توقف عن العمل، أول شي راجع آخر تعديل عملته وتأكد كل `{ }` و`[ ]` و`,` زي ما كانت.
- **تعديل `ar` بدون `en` (أو العكس)** — بيخلي لغة وحدة قديمة عن الثانية.
- **حذف علامات التنصيص `" "`** — لازم كل نص يكون محاط فيها بالكامل.
- **تغيير اسم حقل** (اللي قبل `:`) — لا تلمسه أبداً، حتى لو غلط إملائي بسيط برأيك؛ الكود بيدور على
  الاسم بالضبط.
