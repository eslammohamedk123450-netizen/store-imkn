# خريطة الصفحات والتنقل

## متجر عام
- `/[locale]` الصفحة الرئيسية: وحدات قابلة للترتيب، بحث، أقسام، عروض منشورة.
- `/[locale]/c/[slug]` القسم؛ فلاتر/فرز/صفحات.
- `/[locale]/p/[slug]` المنتج؛ معرض، variants، توفر، وصف، منتجات مرتبطة.
- `/[locale]/search?q=` نتائج بحث.
- `/[locale]/cart` السلة.
- `/[locale]/checkout` دخول ثم عنوان/شحن/طريقة دفع/مراجعة.
- `/[locale]/policies/[slug]`, `/help`, `/track` وفق سياسة إظهار لا تكشف طلب غير مالكه.
- `/[locale]/auth/*` دخول/إنشاء/استعادة.

## مساحة العميل (تتطلب جلسة)
`/account`, `/account/profile`, `/account/addresses`, `/account/orders`, `/account/orders/[id]`, `/account/returns`, `/account/favorites`, `/account/notifications`, `/account/support`.

## المسوق
`/affiliate/apply`, `/affiliate` لوحة، `/affiliate/links`, `/affiliate/campaigns`, `/affiliate/orders`, `/affiliate/earnings`, `/affiliate/payouts`; وصول مسوق معتمد فقط، البيانات ذاتية النطاق.

## الإدارة (كل صفحة محمية في الخادم)
`/admin` dashboard؛ `/products`, `/categories`, `/inventory`, `/orders`, `/payments`, `/shipping`, `/returns`, `/customers`, `/affiliates`, `/commissions`, `/support`, `/content/pages`, `/content/home`, `/design`, `/locales`, `/notifications`, `/reports`, `/staff`, `/roles`, `/settings`, `/audit`. أقسام AI/providers لاحقًا.

كل صفحة: metadata، حالات تحميل/فارغ/خطأ، رفض وصول مناسب، اتجاه ولغة، سجلات غير حساسة. صفحات الإدارة لا تُفهرس. خريطة أولية وتحتاج اختبار تدفقات استخدام مع أصحاب المصلحة.
