# تأسيس منصة التجارة الإلكترونية

حزمة مرحلة التأسيس والتوثيق فقط. توجيه التنفيذ الحالي: الكود والاختبارات وقاعدة البيانات محلية على الكمبيوتر/بيئة العمل، ولا يوجد نشر أو اتصال Supabase سحابي. لا تعد الوثائق إثباتًا على تنفيذ أو اختبار أي ميزة.

## نقطة البداية للوكيل
1. اقرأ [قواعد الوكلاء](AGENT_RULES.md).
2. اقرأ [الحالة](PROJECT_STATUS.md) و[الجلسة الحالية](CURRENT_SESSION.md).
3. اقرأ المهمة المحددة وملفاتها المرتبطة فقط.
4. لا تبدأ التنفيذ قبل قرار صاحب المشروع بشأن الأسئلة الموسومة `قرار مطلوب`، ولا تغيّر المرجع المعتمد بصمت.

## خريطة الوثائق
- [المرجع الرئيسي](MASTER_PROJECT.md) · [المتطلبات](REQUIREMENTS.md) · [المعمارية](PROJECT_ARCHITECTURE.md)
- [قاعدة البيانات](docs/database/DATABASE_DESIGN.md) · [واجهات API](docs/architecture/API_SPECIFICATION.md) · [الأمن](SECURITY.md)
- [التصميم](DESIGN_SYSTEM.md) · [خريطة الصفحات](docs/product/PAGE_MAP.md) · [الاختبارات](TEST_STRATEGY.md)
- [خارطة الطريق](ROADMAP.md) · [لوحة المهام](TASKS.md) · [سجل القرارات](DECISIONS.md) · [المخاطر](project-management/RISKS.md)
- [تغييرات مقترحة](PROPOSED_CHANGES.md) · [تقرير التأسيس](FINAL_REPORT.md)

## خطة التشغيل الحالية مقابل الهدف المستقبلي
التطوير حاليًا محلي مع PostgreSQL محلي؛ Supabase Cloud وVercel وGitHub Pages غير مستخدمة وقت التنفيذ. الهدف المستقبلي المقترح: Next.js + TypeScript، Supabase، وVercel. GitHub للمصدر فقط؛ GitHub Pages للوثائق/الثابت ولا تستخدم للتطبيق الديناميكي. راجع [سياسة العمل المحلي](docs/LOCAL_DEVELOPMENT_POLICY.md) و[المؤجل](DEFERRED_EXTERNAL_INTEGRATIONS.md).

الحالة الابتدائية: التوثيق مكتمل كمسودة تأسيس، جميع مهام التنفيذ `NOT_STARTED`، لا يوجد كود تطبيق ضمن هذه الحزمة.

تنفيذ محلي فقط: [السياسة](docs/LOCAL_DEVELOPMENT_POLICY.md) · [سجل التكاملات المؤجلة](DEFERRED_EXTERNAL_INTEGRATIONS.md).
