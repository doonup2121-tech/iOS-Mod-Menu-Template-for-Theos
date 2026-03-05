# إعدادات المعمارية والبناء
ARCHS = arm64
DEBUG = 0
FINALPACKAGE = 1
FOR_RELEASE = 1
IGNORE_WARNINGS = 1

# إبطال وضع الموبايل ليعمل على الكود سبيس
MOBILE_THEOS = 0

ifeq ($(MOBILE_THEOS),1)
  SDK_PATH = /theos/sdks/iPhoneOS11.2.sdk/
  SYSROOT = $(SDK_PATH)
else
  # إعداد الهدف ليتوافق مع المترجم المتاح
  TARGET = iphone:clang:latest:11.0
endif

## أطر العمل الأساسية ##
PROJ_COMMON_FRAMEWORKS = UIKit Foundation Security QuartzCore CoreGraphics CoreText

## ملفات المصدر ##
KITTYMEMORY_SRC = $(wildcard KittyMemory/*.cpp)
SCLALERTVIEW_SRC =  $(wildcard SCLAlertView/*.m)
MENU_SRC = Menu.mm

# تعريف مسار الثيوس الأساسي - تم التعديل ليتناسب مع Codespaces
include /theos/makefiles/common.mk

# استبدل كلمة MyCoolHack باسم مشروعك إذا أردت
TWEAK_NAME = MyCoolHack

MyCoolHack_CFLAGS = -fobjc-arc
MyCoolHack_CCFLAGS = -std=c++11 -fno-rtti -fno-exceptions -DNDEBUG

MyCoolHack_FILES = Tweak.xm $(MENU_SRC) $(KITTYMEMORY_SRC) $(SCLALERTVIEW_SRC)
MyCoolHack_LIBRARIES += substrate
MyCoolHack_FRAMEWORKS = $(PROJ_COMMON_FRAMEWORKS)

# السطر الذي تسبب في الخطأ رقم 59 و 62 تم إصلاحه هنا
include /theos/makefiles/tweak.mk

internal-package-check::
	@chmod 777 versionCheck.sh
	@./versionCheck.sh

after-install::
	install.exec "killall -9 SpringBoard || :"
