# استراتيجية الاختبار

لا اختبارات منفذة في مرحلة التأسيس. كل مهمة تضيف اختباراتها ولا تعتمد على نجاح build وحده.

## المستويات
- Unit: قواعد السعر والتقريب، انتقالات الحالات، أهلية العمولة/الإرجاع، validators.
- Integration: Postgres constraints/RPC، RLS بمستخدمين وأدوار متعددة، Storage policies، auth والطلبات.
- E2E: رحلة تصفح→سلة→طلب، إثبات يدوي→مراجعة، شحن→تسليم→عمولة/إرجاع، locale/theme/admin.
- Security: IDOR، privilege escalation، السعر/المخزون، replay، brute-force/rate limit، رفع ملفات، headers/CORS، dependency/secrets.
- Performance: baseline للصفحات العامة وCheckout وquery plans تحت حمل متفق عليه؛ لا SLA قبل تحديد ميزانية وحركة.
- Recovery: استعادة نسخة إلى بيئة معزولة وقياس RPO/RTO بعد اعتماد الأهداف.

## بوابات القبول
lint/typecheck، unit/integration، migrations نظيفة، RLS tests، E2E للمسار المتأثر، مراجعة أمنية، accessibility smoke، لا ثغرات حرجة/عالية بلا معالجة أو قبول موثق، تقرير نتائج حقيقي. بيانات الاختبار لا تحتوي PII حقيقية.

تفاصيل السيناريوهات: `tests/` وملفات المهام ذات الصلة.
