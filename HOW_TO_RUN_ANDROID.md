# كيف تشغل تطبيق NintendoAudit (نسخة أندرويد)

نفس التطبيق تماماً بالمنطق والشاشات، لكن مبني بـ **Kotlin + Jetpack Compose + Room** (مكافئ SwiftUI + SwiftData).

## 1) افتح المشروع
- افتح **Android Studio** (نسخة حديثة، Koala أو أحدث يفضل)
- **File → Open** → اختر مجلد `NintendoAuditAndroid` كامل (فيه `settings.gradle.kts`)
- Android Studio بيسوي Gradle Sync تلقائي أول ما يفتح — انتظره يخلص (أول مرة ياخذ وقت لأنه يحمّل المكتبات)
- لو طلب منك "Create Gradle Wrapper" وافق عليه

## 2) شغّل على المحاكي أو جهاز حقيقي
- من شريط الأدوات فوق اختر جهاز (Pixel أو أي محاكي API 26+)
- اضغط ▶️ Run (أو `Shift + F10`)

## 3) صلاحية الكاميرا
- مضافة مسبقاً بـ `AndroidManifest.xml` (`android.permission.CAMERA`)
- أول مرة تفتح الكاميرا بالتطبيق بيطلب أندرويد الإذن تلقائياً من المستخدم — ما تحتاج تسوي شي إضافي

## بنية المشروع
| الملف/المجلد | الوظيفة |
|---|---|
| `data/Entities.kt` | نماذج البيانات (Room @Entity) — مكافئ AuditModels.swift |
| `data/Enums.kt` | كل الـ enums (Status, Category, Severity...) |
| `data/Daos.kt` | استعلامات قاعدة البيانات (Room DAO) |
| `data/AppDatabase.kt` | إعداد قاعدة بيانات Room |
| `data/Converters.kt` | تحويل التواريخ والـ enums لتخزينها بـ SQLite |
| `data/SampleData.kt` | بيانات تجريبية أولية (متاجر + SKUs) |
| `viewmodel/AuditViewModel.kt` | كل منطق العمليات (Create/Read/Update/Delete) — مشترك لكل الشاشات |
| `ui/theme/Theme.kt` | الألوان والستايل |
| `MainActivity.kt` | نقطة الدخول + التنقل بين الشاشات (Navigation) |
| `ui/screens/DashboardScreen.kt` | لوحة التحكم والإحصائيات |
| `ui/screens/VisitListScreen.kt` | قائمة الزيارات + بدء زيارة جديدة |
| `ui/screens/VisitDetailScreen.kt` | شاشة الزيارة الرئيسية |
| `ui/screens/ScorecardScreen.kt` | تقييم النظافة/الأسعار/العرض/المعرفة |
| `ui/screens/SKUChecklistScreen.kt` | تشيك ليست المنتجات |
| `ui/screens/CompetitorListScreen.kt` | رصد المنافسين |
| `ui/screens/IssueListScreen.kt` | المشاكل والإجراءات التصحيحية |
| `ui/screens/PhotoGalleryScreen.kt` | صور الإثبات (كاميرا + مكتبة) |
| `ui/screens/MasterDataScreen.kt` | إدارة المتاجر والـ SKUs |

## ملاحظات مهمة
- **minSdk 26** (Android 8.0+) — يغطي أغلب الأجهزة بالسوق السعودي حالياً.
- كل البيانات محلية (SQLite عبر Room) — بدون أي API خارجي، تماماً زي نسخة iOS.
- أول تشغيل يزرع نفس بيانات iOS التجريبية (5 متاجر + 10 SKUs).
- ما قدرت أشغّل Gradle/Compiler هنا للتأكد 100%، فلو طلعت أخطاء بناء (build errors) بـ Android Studio، ابعت لي رسالة الخطأ وأصلحها فوراً.
- الكود بين نسخة iOS وأندرويد متطابق منطقياً 1:1 (نفس أسماء الحقول والحسابات)، فأي تعديل مستقبلي على منطق العمل لازم تسويه بالنسختين.
