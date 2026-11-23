# مواصفة API وحدود الخدمة (مبدئية)

أسلوب أولي: Next.js Route Handlers لخدمات الويب الحساسة أو Supabase Edge Functions باختيار موثق؛ لا تنشئ واجهة عامة غير لازمة. JSON، تحقق schema على الخادم، رد أخطاء موحد `{code,message,requestId}` دون تفاصيل داخلية. مصادقة جلسة Supabase، authorization في كل طلب، rate limits للأفعال المكلفة، idempotency للطلب/الدفع/السحب.

| مجال | عمليات متوقعة | ضوابط |
|---|---|---|
| Catalog | GET products/categories/search | المنشور فقط، pagination، allowlist filters |
| Cart | GET/PUT items | جلسة؛ الكمية موجبة وحدود؛ سعر يعاد حسابه |
| Checkout | POST /checkout | login، idempotency، تحقق سعر/مخزون/منطقة، إنشاء ذري |
| Orders | GET mine, POST cancel | ملكية؛ انتقالات حالة مسموحة فقط |
| Payment proof | POST upload intent/submit | bucket خاص، حد وحجم ونوع، مراجعة بشرية |
| Admin catalog | CRUD/publish | RBAC خادمي، تدقيق، تحقق صلاحية ومدخلات |
| Returns | POST request, admin decision | ملكية ثم صلاحية قرار، قواعد سياسة، حركة مخزون موثقة |
| Affiliate | apply, links, stats, payout request | الموافقة، نطاق بيانات المسوق، حدود سحب، مراجعة |
| Webhooks | endpoint حسب المزود عند إضافته | توقيع/تاريخ/nonce/تكرار آمن، secret server-side |

لا تعتبر هذه عقود نهائية؛ لكل endpoint لاحقًا OpenAPI/schema، أكواد حالات، حدود pagination، idempotency semantics، سياسة صلاحيات واختبارات.
