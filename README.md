
# Comprehensive WSL & Ubuntu 22.04 Installation Report

## 1. سجل الخطوات التفصيلي (Step-by-Step Execution Log)

  • الخطوات 1 إلى 3 :
•  قم بتشغيل موجه الأوامر Windows PowerShell بصلاحيات المسؤول (Run as Administrator) لضمان منح الأوامر الصلاحيات الكافية لتعديل ميزات النظام.

• Launched Windows PowerShell with elevated privileges (Run as Administrator) to grant system-level feature modification permissions.

![img alt](https://github.com/taleensami001-lgtm/Installation-and-Configuration-of-ROS-2-Humble-on-Ubuntu-WSL/blob/e52729cbc0f8e644848befcf07dffbf268254e95/IMG_1854.jpeg)


• الخطوات 4 و 5 ::
• قمت بتنفيذ أمر التثبيت الرئيسي wsl --install حيث بدأ النظام بتحميل المكونات الأساسية لـ Windows Subsystem for Linux (الإصدار 2.7.11).

•  Executed wsl --install, initiating the core WSL component downloads (v2.7.11).

![img alt](https://github.com/taleensami001-lgtm/Installation-and-Configuration-of-ROS-2-Humble-on-Ubuntu-WSL/blob/e52729cbc0f8e644848befcf07dffbf268254e95/IMG_1855.jpeg)

• الخطوات 6 و 7 :
• قمت بتحديد تثبيت توزيعة أوبونتو عبر الأمر wsl --install -d Ubuntu-22.04. قام النظام تلقائياً بتفعيل ميزة Platform/Virtual Machine الخيارية (VirtualMachinePlatform) باستخدام أداة DISM الخاصة بالنظام.

•  Ran wsl --install -d Ubuntu-22.04. The system triggered optional feature activation for VirtualMachinePlatform using the DISM servicing tool.

• الخطوة 8 :
• ظهرت مشكلة وتوقف التثبيت بسبب تكرار الأمر.

• Encountered a duplicate execution error during distro registration.

• الخطوات 9 و 10 :
• نافذة PowerShell مفتوحة وتنتظر إدخال أوامر التشغيل والحل.

• PowerShell environment ready for diagnostic and launch commands.


## 2. المشاكل والأخطاء التي تم مواجهتها (Problems Encountered)

• رمز الخط
أ (Error Code): Wsl/InstallDistro/ERROR_ALREADY_EXISTS

• نص الرسالة (Message):
A distribution with the supplied name already exists. Use --name to chose a different name.

![img alt](https://github.com/taleensami001-lgtm/Installation-and-Configuration-of-ROS-2-Humble-on-Ubuntu-WSL/blob/cf58db1ac9a900321944f88366243429f0eb97e5/IMG_1856.jpeg)

التحليل الفني للسبب الجذر (Technical Root Cause):
1. هذا الخطأ ليس دليلاً على فشل التثبيت، بل على نجاح تسجيل التوزيعة في المحاولة الأولى. عند إعادة تنفيذ الأمر wsl --install -d Ubuntu-22.04 مرة أخرى، يرفض WSL تثبيتها لأنه يتعرف عليها كـ "توزيعة موجودة ومسجلة بالفعل".
2.
 This error indicates that the distribution package was already registered successfully during the preceding step. Re-running the installation command fails because WSL prevents overwriting an existing distribution name.

4.	ملاحظة إضافية: تم تمكين ميزة VirtualMachinePlatform حديثاً، وبعض أجهزة Windows تتطلب إعادة تشغيل (Restart) حتى تكتمل ميزات الافتراضية (Virtualization).
 
3. الحلول والخطوات القادمة الموصى بها (Solutions & Next Steps)

 التحقق من التوزيعات الثابتة
قم بتشغيل الأمر التالي للتأكد من وجود Ubuntu 22.04 وحالتها:

wsl --list --verbose
(أو الاختصار: wsl -l -v)

![img alt](https://github.com/taleensami001-lgtm/Installation-and-Configuration-of-ROS-2-Humble-on-Ubuntu-WSL/blob/6c58a39f0c9fd7ca4fb47ccc360560c9c4e0cf8b/IMG_1858.jpeg) 

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

![img alt](https://github.com/taleensami001-lgtm/Installation-and-Configuration-of-ROS-2-Humble-on-Ubuntu-WSL/blob/f5ba0703afc5b5725c4fdfd687dc23a2b9df60ba/IMG_1859.jpeg)

WSL Environment / بيئة WSL:

• Successfully switched into Ubuntu 22.04 (wsl -d Ubuntu-22.04).

• تم التبديل بنجاح إلى نظام Ubuntu 22.04.

![img alt](https://github.com/taleensami001-lgtm/Installation-and-Configuration-of-ROS-2-Humble-on-Ubuntu-WSL/blob/fc810d1191de4ec6573cb61545c9ab8f8504a44d/IMG_1860.jpeg)

• System Upgrade / ترقية النظام:

• Completed sudo apt update && sudo apt upgrade -y.

![img alt](https://github.com/taleensami001-lgtm/Installation-and-Configuration-of-ROS-2-Humble-on-Ubuntu-WSL/blob/34363589a9f62ecc2227f3676d79db49c58a6555/IMG_1861.jpeg)
![img alt](https://github.com/taleensami001-lgtm/Installation-and-Configuration-of-ROS-2-Humble-on-Ubuntu-WSL/blob/fe4c560c84d71ea0e8fc5b83d700a3245e24bb97/IMG_1862.jpeg)
• اكتمل تنفيذ أمر التحديث.

• Current Command / الأمر الحالي:
• Ready to execute/finishing sudo apt install software-properties-common curl -y.

• جاهز للتنفيذ أو في طور إنهاء الأمر.

![img alt](https://github.com/taleensami001-lgtm/Installation-and-Configuration-of-ROS-2-Humble-on-Ubuntu-WSL/blob/464c655ce032c24b3bfe499c28e7398e9db5a566/IMG_1863.jpeg)
![img alt](https://github.com/taleensami001-lgtm/Installation-and-Configuration-of-ROS-2-Humble-on-Ubuntu-WSL/blob/e1c36d547b01568ee32377ebdbc8305f59dfad2d/IMG_1864.jpeg)

Remaining Setup Steps / خطوات الإعداد المتبقية

Once the current command finishes running, press Enter (if you haven't yet) and copy/paste these remaining commands sequentially from your guide:
بمجرد الانتهاء من تشغيل الأمر الحالي، اضغط على زر Enter (إذا لم تفعل ذلك بعد) وانسخ/ألصق هذه الأوامر المتبقية بالتسلسل من دليلك:

Step 1: Add the ROS GPG Key / الخطوة الأولى: إضافة مفتاح ROS GPG

sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg

![img alt](https://github.com/taleensami001-lgtm/Installation-and-Configuration-of-ROS-2-Humble-on-Ubuntu-WSL/blob/210cb67a8a622dcea235429dcebffccd6a0b6cd9/IMG_1865.jpeg)


Step 2: Add the ROS Repository / الخطوة الثانية: إضافة مستودع ROS

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

![img alt](https://github.com/taleensami001-lgtm/Installation-and-Configuration-of-ROS-2-Humble-on-Ubuntu-WSL/blob/f7762d104669ee2fb924169fa6776931e0770c8c/IMG_1866.jpeg)

## Step 3: Update Package List & Install ROS 2 / الخطوة الثالثة: تحديث قائمة الحزم وتثبيت ROS 2

sudo apt update

![img alt](https://github.com/taleensami001-lgtm/Installation-and-Configuration-of-ROS-2-Humble-on-Ubuntu-WSL/blob/70eafb936bd045f97579f5d11f7b88f55dc5ea0d/IMG_1868.jpeg)
![img alt](https://github.com/taleensami001-lgtm/Installation-and-Configuration-of-ROS-2-Humble-on-Ubuntu-WSL/blob/6171974dfc12c5e3cf5da3eea26bbf524e26f601/IMG_1869.jpeg)

sudo apt install ros-humble-desktop -y

![img alt](https://github.com/taleensami001-lgtm/Installation-and-Configuration-of-ROS-2-Humble-on-Ubuntu-WSL/blob/6c86a2a820696f87f8baccd5b85a0949c95076d4/IMG_1871.jpeg)
![img alt](https://github.com/taleensami001-lgtm/Installation-and-Configuration-of-ROS-2-Humble-on-Ubuntu-WSL/blob/8f3e077b91365d871e1559feb26ef8fa7bf55df1/IMG_1872.jpeg)

## Step 4: Automatically Source ROS 2 Environment / الخطوة الرابعة: تهيئة بيئة ROS 2 تلقائياً

To ensure ROS 2 commands work every time you open a terminal:
لضمان عمل أوامر ROS 2 في كل مرة تفتح فيها نافذة الأوامر (Terminal):

echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
source ~/.bashrc

![img alt](https://github.com/taleensami001-lgtm/Installation-and-Configuration-of-ROS-2-Humble-on-Ubuntu-WSL/blob/1abbff264ff8b88ebcae6079f4a8feb8eb6c875a/IMG_1873.jpeg) 

Great news—ROS 2 Humble is fully installed and working!

أخبار رائعة—تم تثبيت ROS 2 Humble بنجاح وهو يعمل بالكامل!

The error message ros2: 
error: unrecognized arguments: --version is actually proof of success. 
It means your shell recognized the ros2 command and loaded the CLI properly—the ros2 command-line tool simply doesn't support a --version flag!

رسالة الخطأ ros2: error: unrecognized arguments: --version هي في الواقع دليل على النجاح. هذا يعني أن النظام تعرف على الأمر ros2 وقام بتحميل واجهة سطر الأوامر بشكل صحيح—أداة سطر الأوامر ros2 ببساطة لا تدعم الخيار --version!
 
How to Verify Your ROS 2 Setup

كيفية التحقق من إعداد ROS 2 الخاص بك

1. Check the Active ROS Distribution

1. التحقق من إصدار ROS النشط

Run this command to confirm your environment variable is loaded:

قم بتشغيل هذا الأمر للتأكد من تحميل متغير البيئة الخاص بك:

echo $ROS_DISTRO

Expected Output: humble
المخرجات المتوقعة: humble

Perfect! $ROS_DISTRO = humble
Your ROS 2 Humble environment is officially configured and loaded properly in your terminal.

ممتاز! $ROS_DISTRO = humble
تم إعداد بيئة ROS 2 Humble الخاصة بك رسمياً وتحميلها بشكل صحيح في واجهة الأوامر.


