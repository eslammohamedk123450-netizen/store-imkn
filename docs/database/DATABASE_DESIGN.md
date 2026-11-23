# تصور قاعدة البيانات والعلاقات

مخطط PostgreSQL أولي منطقي؛ ليس migration جاهزًا. UUID للمفاتيح، `created_at/updated_at` عند الحاجة، FK وفهارس وقيود، أسعار integer قرش EGP مع `currency_code`، وحالات enum/check مدروسة. تطبق migrations مع مراجعة.

## الجداول الأساسية
- `profiles(user_id PK -> auth.users, display_name, phone, locale, status)`؛ لا تكرر أسرار المصادقة.
- `addresses(id,user_id, governorate_code, city, details, phone, is_default)` مع عزل مالك.
- `categories(id,parent_id,slug,sort_order,is_active)` و`category_translations(category_id,locale,name,description)`.
- `products(id,source_id,status,slug,product_type,base_price_minor,currency,...)`؛ `product_translations`؛ `product_media`؛ `product_attributes`/`attribute_values`.
- `product_variants(id,product_id,sku,price_override_minor,active)`؛ `inventory(variant_id PK,on_hand,reserved)`؛ `inventory_movements(id,variant_id,delta,reason,actor,order_id,created_at)` append-only للمستخدمين العاديين.
- `promotions`, `coupons`, `coupon_redemptions` بقيود استعمال ووقت.
- `carts(id,user_id UNIQUE,...)`, `cart_items(cart_id,variant_id,quantity)`؛ السلة ليست مرجع السعر.
- `orders(id,user_id,status,currency,subtotal_minor,shipping_minor,discount_minor,total_minor,idempotency_key,...)`؛ قيد فريد مناسب للمستخدم/المفتاح؛ `order_items` snapshot للاسم/SKU/السعر/الكمية/الخصم.
- `order_status_history(order_id,from,to,actor,reason,created_at)`.
- `payments(id,order_id,method,status,amount_minor,provider_ref,proof_object_key,reviewed_by, idempotency_ref)`؛ لا تخزن بيانات بطاقة.
- `shipments(order_id,zone_id,carrier,tracking_number,status)`؛ `shipping_zones`, `shipping_rules`.
- `return_requests`, `return_items`, `refund_records`، صلاحيات انتقال حالات.
- `affiliate_profiles(user_id,status,approved_by,...)`, `referral_links`, `affiliate_clicks` (احتفاظ محدود/تقليل IP)، `attributions(order_id UNIQUE,affiliate_id,...)`, `commission_entries(order_id,affiliate_id,amount_minor,status)` بقيد فريد يمنع التكرار، `payout_requests`, `ledger_entries` append-only.
- `favorites(user_id,product_id UNIQUE)`.
- `content_pages`, `home_sections`, `content_revisions(status,version,...)`، معاينة مقيّدة.
- `staff_roles`, `role_permissions`, `user_role_assignments`؛ لا تعتمد على role يرسله العميل.
- `audit_events(actor_id,action,entity_type,entity_id,request_id,metadata_redacted,created_at)` append-only لغير أصحاب الامتياز التشغيلي.
- `notifications`, `support_tickets/messages` مع سياسات عزل.
- AI لاحقًا: `ai_providers` بلا مفاتيح خام للقراءة العادية؛ الأسرار في secret store، `ai_usage` دون prompt حساس زائد.

## العلاقات والمعاملات
Order لديه عدة order_items وpayment attempts وstatus history؛ attribution/commission فريدان حسب سياسة الإسناد. إنشاء الطلب مع إعادة التحقق من أسعار ومخزون ثم حجز/خصم ذريًا، معالجة تعارض المخزون بمعاملة أو RPC مقيدة. اعتماد الدفع/المرتجع/العمولة عمليات منفصلة بصلاحيات وتدقيق. لا تثق بسطور السلة أو سعر العميل.

## RLS مبدئي
- كتالوج منشور للقراءة العامة فقط؛ مسودات الإدارة فقط.
- profile/address/cart/favorite/order/return/notification: `auth.uid() = user_id`، والموظف وصول عبر permission server-side/RLS مدروس.
- المسوق يرى ملفه وروابطه وتقاريره/عمولاته فقط؛ لا يعدل المبالغ أو حالة الاعتماد.
- عمليات الكتابة المالية/الحالات من وظائف موثوقة ذات تحقق وتدقيق، وليس سياسة عامة تسمح تحديث الجدول.
- Storage: bucket إثباتات الدفع خاص، مفاتيح مرتبطة بالطلب/المالك، MIME وحجم وفحص، signed URLs قصيرة العمر.
- service role لا يستخدم إلا server-side وبأقل مساحة، وكل مسار يتجاوز RLS يفرض تحققًا صريحًا ويختبر.

قبل التنفيذ: مصفوفة كل جدول (select/insert/update/delete لكل دور)، فهارس للـFK/filters، retention، حماية soft-delete، واختبارات RLS بمستخدمين مختلفين.
