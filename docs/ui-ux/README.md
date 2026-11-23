# مواصفات نظام التصميم — تأسيسي

الهوية أصلية: أبيض/أخضر، هادئة وموثوقة لا تقلد علامة بعينها. الاسم والشعار النهائيان غير محددين؛ استخدم تسمية مؤقتة في التصاميم ولا تثبت علامة تجارية.

## Tokens مبدئية (تراجع باختبار تباين)
- `brand-700 #176B4D`، `brand-800 #10563D`، `brand-50 #EAF5EF`، `neutral-950 #17211C`، `neutral-600 #59665F`، `surface #FFFFFF`، `surface-muted #F5F7F5`، `danger #B42318`، `warning #9A6700`، `success #16794A`.
- Dark: خلفية `#101713`، سطح `#18221C`، نص `#EFF5F0` مع ألوان brand معدلة لضمان التباين. لا تستخدم لونًا فقط لتمييز الحالة.
- خط عربي/لاتيني مرخص ويبًا (قرار نهائي بعد مراجعة الترخيص والأداء)، fallback system. خط عربي واضح متناسق مثل Cairo/Noto Sans Arabic مرشح لا اعتماد نهائي.
- مقياس spacing 4px، radius 8/12/16px، ارتفاع لمس 44px حد أدنى، حاويات متجاوبة.

## مكونات وحالات
Button (primary/secondary/quiet/danger)، input/select/search، badge، product card، price، breadcrumb، tabs، modal/drawer، toast، pagination، skeleton، empty/error/success/loading. تعريف hover/focus-visible/disabled/invalid/busy، labels وaria، focus management.

## التجاوب والتدويل
Mobile First: شبكة 2 عمود على هاتف مناسب، تتوسع حسب المساحة؛ لا تثبت breakpoints قبل اختبار المحتوى. RTL/LTR باستخدام logical CSS properties وعدم عكس الأيقونات الدلالية عشوائيًا. أرقام وأسعار EGP محلية، تاريخ واضح، ترجمة لا تخلط الاتجاه. دعم تكبير النص وReduced Motion.

## لوحة تخصيص
tokens ومكونات الصفحة من إعداد versioned، مسودة ومعاينة وصلاحيات نشر/rollback؛ allowlist للقيم لمنع CSS/HTML injection، sanitizer للمحتوى، لا JavaScript حر من لوحة الإدارة.

معايير القبول: مراجعة تباين WCAG AA، اختبار هاتف/تابلت/سطح مكتب، تحقق RTL/LTR وdark/light، حالات الواجهة كاملة. الألوان المقترحة غير مختبرة آليًا بعد.
