# MultiAssetSniperMT5

![الأسواق والمنصة والاستراتيجية](assets/project-badges.svg)

## الميزات الرئيسية

- Expert Advisor لأسواق `XAUUSD` و`EURUSD` على شارتات M5 مستقلة، مع Magic Number منفصل لكل سوق. يقبل لاحقات الوسيط لهذين الرمزين، ويرفض الرموز غير المدعومة.
- يدعم حسابات MT5 التجريبية والحقيقية لدى الوسطاء الذين يوفرون أحد الرمزين المدعومين وحساب Hedging. حسابات Netting غير مدعومة لأن Multi-TP يحتاج إلى مراكز منفصلة.
- يدعم Multi-TP وATR Grid وMartingale وإدارة السلة وSmart Trailing.
- تتوفر ملفات إعدادات مستقلة: [`Gold.set`](Gold.set) و[`EURUSD.set`](EURUSD.set).

## استراتيجية التداول

تُقيَّم إشارات BUY وSELL على شمعة M5 المغلقة باستخدام EMA 13 وEMA 34 وRSI وADX. يُحسب EMA 200 على H1 ويصبح مرشحًا للدخول فقط عند تفعيل `Input_UseMacroFilter`؛ قيمته الافتراضية `false`. يُستخدم ATR على H1 لتحديد تباعد Grid. عند تحقق الإشارة، يفتح Multi-TP ثلاث صفقات منفصلة في حساب Hedging.

## معلمات الإدخال

| السوق وملف الإعداد | اللوت الابتدائي | Magic Number | حد السبريد بالنقاط |
|---|---:|---:|---:|
| XAUUSD — `Gold.set` | 0.01 | 55555 | 450 |
| EURUSD — `EURUSD.set` | 0.01 | 55557 | 15 |

في الملفين: `Input_UseAutoLot=false`، و`Input_LotMultiplier=1.6`، و`Input_MaxGridLevels=8`، وMulti-TP وBasket SL مفعّلان. يمكن تعديل جميع القيم من **Inputs** في MT5. افحص مواصفات الرمز لدى وسيطك قبل الاستخدام؛ الحد الأدنى للوت والسبريد قد يتغيران.

## التثبيت

1. نزّل المشروع من **Code → Download ZIP** أو نفّذ `git clone https://github.com/man9orq8/MultiAssetSniperMT5.git`.
2. ثبّت [MT5 على macOS](https://www.metatrader5.com/en/terminal/help/start_advanced/install_mac) أو [MT5 على Windows](https://www.metatrader5.com/en/download)، ثم سجّل الدخول إلى حساب Demo أو Real لدى وسيطك. يلزم أن يدعم الوسيط MT5 والرمز المطلوب وحساب Hedging.
3. داخل MT5 اختر **File → Open Data Folder**. انسخ [`MultiAssetSniperMT5.ex5`](MultiAssetSniperMT5.ex5) إلى `MQL5/Experts/MultiAssetSniperMT5/`، وملفي `.set` إلى `MQL5/Presets/`. الملفان `.mq5` و`.ex5` صالحان للمنصتين؛ لا تعتمد على مجلد تثبيت البرنامج بدل Data Folder.
4. حدّث **Navigator**. افتح شارتات XAUUSD وEURUSD على M5، وأرفق EA بكل شارت، ثم حمّل ملف SET المطابق من **Inputs → Load**.
5. فعّل **Allow Algo Trading** في خصائص كل EA وزر **Algo Trading** العام، وراقب **Experts** و**Journal**. أبقِ MT5 متصلًا والماك مستيقظًا، لأن إدارة الصفقات تتم داخل EA أثناء تشغيل المنصة.

إذا احتجت التجميع من المصدر، افتح [`MultiAssetSniperMT5.mq5`](MultiAssetSniperMT5.mq5) في MetaEditor واضغط **F7**؛ راجع الأخطاء قبل استخدام ملف EX5 الناتج.

## العلوي

يعمل هذا الإصدار على الأسواق المدعومة بصورة مستقلة، مع قيم ATR قابلة للضبط بحسب مواصفات الرمز وفحص توافق حساب Hedging.

## ⚠️ إخلاء مسؤولية المخاطر

Grid وMartingale قد يسببان خسائر كبيرة. لا يضع EA وقف الخسارة أو جني الربح على خادم الوسيط عند الدخول، لذلك تتوقف إدارة المخارج البرمجية عند إغلاق MT5 أو نوم الجهاز. يمكن استخدامه على حساب Demo أو Real لدى وسيط MT5 متوافق؛ التشغيل على حساب حقيقي قد يؤدي إلى خسارة رأس المال.

## مؤلف MANSOUR ALAJMI

