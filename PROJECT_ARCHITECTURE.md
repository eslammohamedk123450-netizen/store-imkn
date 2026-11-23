# المعمارية المقترحة — مسودة قرار

## اختيار MVP
- **Web:** Next.js App Router + TypeScript، React، واجهات server-rendered حيث يفيد SEO، مكونات client تفاعلية عند الحاجة. اعتماد إصدارات مستقرة مدعومة وقت بدء التنفيذ وتثبيتها بملف lock.
- **تشغيل المرحلة الحالية:** كل التطبيق والخدمات وPostgreSQL محلية على جهاز/بيئة الوكيل. لا Vercel deployment ولا Supabase Cloud ولا GitHub Pages runtime. GitHub يستخدم كمستودع مصدر بعد تفويض المستخدم فقط.
- **الهدف المستقبلي المقترح:** Vercel للواجهة وRoute Handlers عند اعتماد النشر؛ GitHub Pages للوثائق/الموقع الثابت فقط، وليس backend أو وظائف Next.js الديناميكية.
- **Backend & data الآن:** PostgreSQL محلي، migrations وبيانات اختبار محلية. لا اتصال Supabase. أي جزء يتطلب Supabase Cloud/Auth/RLS/Storage/Edge Functions يظل معطلًا ومؤجلًا في `DEFERRED_EXTERNAL_INTEGRATIONS.md`.
- **الهدف المستقبلي المقترح:** Supabase Postgres/Auth/Storage مع RLS، بعد تفويض منفصل واختبارات أمنية. عمليات حساسة عبر خادم موثوق. لا تكرر منطق الأعمال بين الخدمات.
- **Search:** Postgres full-text/trigram كبداية؛ قياس قبل خدمة بحث مدفوعة.
- **Email/observability:** مزودان خارجيان غير محسومين؛ طبقة adapter وتسجيل دون أسرار/معلومات دفع.

## حدود الثقة والتدفق
التشغيل الحالي: المتصفح المحلي → خادم التطبيق المحلي يتحقق من المدخلات والصلاحيات → PostgreSQL محلي بقيود ومخططات محلية. لا توجد مفاتيح أو اتصالات سحابية. لاحقًا، بعد موافقة منفصلة: Supabase Postgres/Auth/Storage وRLS؛ لا تعرض مفاتيح server/service role للمتصفح، وRLS ليست بديلًا عن تحقق الخادم.

## المجالات
Identity/RBAC، Catalog، Pricing/Promotions، Cart/Checkout، Orders/Payments، Fulfillment/Returns، Affiliate/Ledger، CMS/Theme، Notifications/Support، AI Gateway (لاحق)، Audit/Reporting.

## تشغيل وتوسع
ابدأ Modular Monolith بحدود مجال واضحة ومخطط واحد مدروس، لا microservices. تطوير محلي وPostgreSQL محلي فقط، ترحيلات SQL مراجعة وموجودة في المستودع، وبيانات اختبار مصطنعة. إعداد staging/prod والنشر مؤجل حتى موافقة مستقلة. CI يفحص lint/type/test/migrations. وظائف طويلة/مهام مجدولة لا تعتمد على request قصير؛ استعمل Queue/جدولة ملائمة عند ظهور الحاجة.

## ضوابط النشر المجاني
الخدمات المجانية لها حدود نوم/حصة/احتفاظ/نقل/وظائف تتغير وقد لا تناسب SLA أو بيانات إنتاج. التحقق من الشروط الحالية مطلوب قبل إطلاق حقيقي. لا تستخدم GitHub Pages لاستضافة لوحة إدارة أو أسرار. افصل المعاينات عن production، وامنع بيانات الإنتاج في preview.

## مخطط عالي المستوى
```text
Browser (RTL/LTR) محلي
  -> Next.js dev server محلي (validation, authorization, rate limits)
      -> PostgreSQL محلي (constraints + local migrations)
      -> local filesystem للبيانات التجريبية فقط عند الحاجة
      -> adapters محلية/mock معلّمة؛ لا دفع أو بريد أو شحن أو AI حقيقي

Supabase/Vercel integrations: DEFERRED حتى تفويض مستقل.
```

التفاصيل: [قاعدة البيانات](docs/database/DATABASE_DESIGN.md)، [API](docs/architecture/API_SPECIFICATION.md)، [القرارات](DECISIONS.md).
