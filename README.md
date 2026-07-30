📋 التقرير الشامل لتثبيت واكتشاف أخطاء WSL و Ubuntu 22.04
Comprehensive WSL & Ubuntu 22.04 Installation Report
1. سجل الخطوات التفصيلي (Step-by-Step Execution Log)
• الخطوات 1 إلى 3 (الصور 1 - 3):
• العربية: قم بتشغيل موجه الأوامر Windows PowerShell بصلاحيات المسؤول (Run as Administrator) لضمان منح الأوامر الصلاحيات الكافية لتعديل ميزات النظام.
• English: Launched Windows PowerShell with elevated privileges (Run as Administrator) to grant system-level feature modification permissions.
• الخطوات 4 و 5 (الصور 4 - 5):
• العربية: قمت بتنفيذ أمر التثبيت الرئيسي wsl --install حيث بدأ النظام بتحميل المكونات الأساسية لـ Windows Subsystem for Linux (الإصدار 2.7.11).
• English: Executed wsl --install, initiating the core WSL component downloads (v2.7.11).
• الخطوات 6 و 7 (الصور 6 - 7):
• العربية: قمت بتحديد تثبيت توزيعة أوبونتو عبر الأمر wsl --install -d Ubuntu-22.04. قام النظام تلقائياً بتفعيل ميزة Platform/Virtual Machine الخيارية (VirtualMachinePlatform) باستخدام أداة DISM الخاصة بالنظام.
• English: Ran wsl --install -d Ubuntu-22.04. The system triggered optional feature activation for VirtualMachinePlatform using the DISM servicing tool.
• الخطوة 8 (الصورة 8):
• العربية: ظهرت مشكلة وتوقف التثبيت بسبب تكرار الأمر.
• English: Encountered a duplicate execution error during distro registration.
• الخطوات 9 و 10 (الصور 9 - 10):
• العربية: نافذة PowerShell مفتوحة وتنتظر إدخال أوامر التشغيل والحل.
• English: PowerShell environment ready for diagnostic and launch commands.
2. المشاكل والأخطاء التي تم مواجهتها (Problems Encountered)
• رمز الخطأ (Error Code): Wsl/InstallDistro/ERROR_ALREADY_EXISTS
• نص الرسالة (Message):
A distribution with the supplied name already exists. Use --name to chose a different name.
التحليل الفني للسبب الجذر (Technical Root Cause):
1.	بالعربية: هذا الخطأ ليس دليلاً على فشل التثبيت، بل على نجاح تسجيل التوزيعة في المحاولة الأولى. عند إعادة تنفيذ الأمر wsl --install -d Ubuntu-22.04 مرة أخرى، يرفض WSL تثبيتها لأنه يتعرف عليها كـ "توزيعة موجودة ومسجلة بالفعل".
2.	English: This error indicates that the distribution package was already registered successfully during the preceding step. Re-running the installation command fails because WSL prevents overwriting an existing distribution name.
3.	ملاحظة إضافية: تم تمكين ميزة VirtualMachinePlatform حديثاً، وبعض أجهزة Windows تتطلب إعادة تشغيل (Restart) حتى تكتمل ميزات الافتراضية (Virtualization).
3. الحلول والخطوات القادمة الموصى بها (Solutions & Next Steps)
التحقق من التوزيعات الثابتة
قم بتشغيل الأمر التالي للتأكد من وجود Ubuntu 22.04 وحالتها:

wsl --list --verbose

(أو الاختصار: wsl -l -v)

تشغيل ubunto مباشرة:
بما أن التوزيعة مضافة بالفعل، يمكنك دخول بيئة لنيكس مباشرة باستخدام:
wsl -d Ubuntu-22.04

أو افتح قائمة Start (ابدأ) وابحث عن تطبيق Ubuntu وقم بفتحه، حيث سيطلب منك إنشاء اسم مستخدم وكلمة مرور لأول مرة.
إعادة تشغيل الجهاز (System Reboot):
إذا ظهرت لك أي رسالة تطلب تفعيل الافتراضية أو الكرنل (Kernel)، يفضل إعادة تشغيل جهاز الكمبيوتر (Restart) لتطبيق تفعيل VirtualMachinePlatform.

إعادة التثبيت النظيف (Clean Reinstallation - اختياري):
في حال كانت النسخة معطوبة وترغب في مسحها وتنزيلها من الجديد:
wsl --unregister Ubuntu-22.04
wsl --install -d Ubuntu-22.04


