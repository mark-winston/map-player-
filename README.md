# Map Player - تطبيق الخرائط والملاحة

تطبيق Android مفتوح المصدر للعثور على أقصر وأسرع الطرق بين موقعين، مع عرض خيارات بديلة متعددة وأوقات الوصول المتوقعة - مشابه لـ Google Maps لكن مع تركيز على مقارنة الطرق البديلة.

## 🎯 الميزات الرئيسية

- **البحث عن الأماكن**: بحث ذكي بالعربية عن المواقع باستخدام Google Places API
- **طرق بديلة متعددة**: يعرض 3-4 طرق مختلفة مع أوقات ومسافات متفاوتة
- **معلومات المرور الحية**: ألوان تشير لحالة المرور (أخضر = حركة خفيفة، أحمر = ازدحام شديد)
- **مقارنة بصرية**: كل طريق بلون مختلف مع عرض المدة والمسافة وحالة المرور
- **خرائط مخصصة**: نمط خريطة نظيف ومحسّن للقيادة
- **دعم RTL كامل**: واجهة عربية أصلية مع دعم RTL

## 📱 لقطات الشاشة (مخطط)

```
┌─────────────────────────────────┐
│  Map Player          [☰] [◎]    │  ← شريط البحث العلوي
│  ┌───────────────────────────┐  │
│  │ من: موقعي الحالي          │  │
│  ├───────────────────────────┤  │
│  │ إلى: الرياض، المملكة     │  │
│  └───────────────────────────┘  │
│                                 │
│        🗺️  الخريطة              │
│                                 │
│  ┌─────────────────────────┐    │  ← Bottom Sheet بالطرق البديلة
│  │ ████░░░░░░░░░░░░░░░░░░░  │    │
│  │ 🟢 أسرع طريق   40 دقيقة  │    │
│  │    عبر الطريق السريع    │    │
│  │    35 كم  ● حركة خفيفة   │    │
│  ├─────────────────────────┤    │
│  │ ░░░░████████░░░░░░░░░░░░  │    │
│  │ 🔵 أقصر طريق   45 دقيقة  │    │
│  │    عبر الشوارع الداخلية  │    │
│  │    28 كم  ● حركة متوسطة  │    │
│  ├─────────────────────────┤    │
│  │ ░░░░░░░░░░██████████████  │    │
│  │ 🟣 بديل 3      50 دقيقة  │    │
│  │    تجنب الرسوم           │    │
│  │    42 كم  ● ازدحام متوسط │    │
│  └─────────────────────────┘    │
│        [بدء التنقل ▶]           │
└─────────────────────────────────┘
```

## 🛠 المتطلبات

- **Android Studio** (Latest stable)
- **JDK 17+**
- **Android SDK** (API 34)
- **Google Maps API Key** مع تفعيل:
  - Maps SDK for Android
  - Places API
  - Directions API

## ⚙️ الإعداد والبناء

### 1. استنساخ المشروع
```bash
git clone <repo-url>
cd map-player
```

### 2. إضافة API Key
انسخ `local.properties.example` إلى `local.properties` وأضف مفتاحك:

```bash
cp local.properties.example local.properties
```

حرر `local.properties`:
```properties
MAPS_API_KEY=AIzaSyXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```

أو أضف المتغير البيئي:
```bash
export MAPS_API_KEY=AIzaSyXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```

### 3. بناء المشروع
```bash
./gradlew assembleDebug
```

أو من Android Studio: **Build → Make Project**

### 4. تشغيل التطبيق
- وصل جهاز Android (API 24+) أو شغل محاكي
- اضغط **Run** في Android Studio

## 🏗 هيكل المشروع

```
map-player/
├── app/
│   ├── src/main/
│   │   ├── java/com/mapplayer/app/
│   │   │   ├── data/
│   │   │   │   ├── api/          # Retrofit services
│   │   │   │   ├── model/        # Data models (Place, Route)
│   │   │   │   └── repository/   # MapRepository
│   │   │   ├── ui/main/
│   │   │   │   ├── MainActivity.kt
│   │   │   │   ├── MainViewModel.kt
│   │   │   │   └── RouteAdapter.kt
│   │   │   └── utils/            # Extensions, Resource
│   │   ├── res/
│   │   │   ├── layout/           # XML layouts
│   │   │   ├── drawable/         # Vector icons
│   │   │   ├── values/           # Strings, colors, themes
│   │   │   ├── anim/             # Animations
│   │   │   └── raw/              # Map style JSON
│   │   └── AndroidManifest.xml
│   ├── build.gradle.kts
│   └── proguard-rules.pro
├── build.gradle.kts
├── settings.gradle.kts
├── local.properties.example
└── README.md
```

## 🔧 التقنيات المستخدمة

| المكون | التقنية |
|-----------|----------|
| Language | Kotlin 1.9+ |
| UI | ViewBinding + Material3 |
| Architecture | MVVM + LiveData + Coroutines |
| Maps | Google Maps SDK for Android |
| Places | Google Places SDK |
| Directions | Google Directions API (Retrofit) |
| Networking | Retrofit + OkHttp + Gson |
| DI | Manual (ViewModelProvider) |

## 📋 API Endpoints المستخدمة

- **Places Autocomplete**: `https://maps.googleapis.com/maps/api/place/autocomplete/json`
- **Place Details**: `https://maps.googleapis.com/maps/api/place/details/json`
- **Directions**: `https://maps.googleapis.com/maps/api/directions/json`

## 🎨 التخصيص

### تغيير ألوان الطرق
في `colors.xml`:
```xml
<color name="route_primary">#1565C0</color>        <!-- الطريق الرئيسي -->
<color name="route_alternative_1">#00ACC1</color>  <!-- البديل الأول -->
<color name="route_alternative_2">#7B1FA2</color>  <!-- البديل الثاني -->
<color name="route_alternative_3">#FF6F00</color>  <!-- البديل الثالث -->
```

### تعديل نمط الخريطة
حرر `res/raw/map_style.json` لتخصيص مظهر الخريطة.

## 🚀 الميزات المخططة

- [ ] التوجيه الصوتي (Turn-by-turn navigation)
- [ ] حفظ الطرق المفضلة
- [ ] وضع عدم الاتصال (Offline maps)
- [ ] مشاركة الطريق عبر تطبيقات أخرى
- [ ] تنبيهات المرور الفورية
- [ ] وضع المشي/الدراجة/النقل العام
- [ ] سجل الرحلات

## 🐛 استكشاف الأخطاء

### "لم يتم العثور على طرق"
- تأكد من تفعيل **Directions API** في Google Cloud Console
- تحقق من صلاحية API Key
- تأكد من اتصال الإنترنت

### "خطأ في الحصول على الموقع"
- تأكد من منح إذن `ACCESS_FINE_LOCATION`
- تأكد من تفعيل GPS في الجهاز

### مشاكل البناء
```bash
# تنظيف وإعادة بناء
./gradlew clean assembleDebug

# تحديث التبعيات
./gradlew --refresh-dependencies
```

## 📄 الترخيص

هذا المشروع مرخص تحت رخصة MIT - راجع ملف [LICENSE](LICENSE) للتفاصيل.

## 🤝 المساهمة

المساهمات مرحب بها! يرجى:
1. عمل Fork للمشروع
2. إنشاء فرع للميزة (`git checkout -b feature/AmazingFeature`)
3. Commit التغييرات (`git commit -m 'Add AmazingFeature'`)
4. Push للفرع (`git push origin feature/AmazingFeature`)
5. فتح Pull Request

## 📞 الدعم

- **Issues**: [GitHub Issues](https://github.com/your-repo/issues)
- **Email**: support@mapplayer.app

---

**Map Player** - طريقك الأسرع، خيارك الأذكى 🗺️🚗