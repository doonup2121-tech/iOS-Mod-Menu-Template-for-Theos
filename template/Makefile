# إعدادات المعمارية والبناء
ARCHS = arm64
DEBUG = 0
FINALPACKAGE = 1
FOR_RELEASE = 1
IGNORE_WARNINGS = 1

# الهدف ليتوافق مع أحدث SDK موجودة في السيرفر
TARGET = iphone:clang:latest:11.0

## أطر العمل الأساسية ##
PROJ_COMMON_FRAMEWORKS = UIKit Foundation Security QuartzCore CoreGraphics CoreText

## ملفات المصدر ##
KITTYMEMORY_SRC = $(wildcard KittyMemory/*.cpp)
SCLALERTVIEW_SRC = $(wildcard SCLAlertView/*.m)
MENU_SRC = Menu.mm

# السطر ده هو السر: بيخلي الثيوس يقرأ مكانه من السيرفر أوتوماتيك
include $(THEOS)/makefiles/common.mk

TWEAK_NAME = MyCoolHack

MyCoolHack_CFLAGS = -fobjc-arc
MyCoolHack_CCFLAGS = -std=c++11 -fno-rtti -fno-exceptions -DNDEBUG

# تجميع كل الملفات في عملية البناء
MyCoolHack_FILES = Tweak.xm $(MENU_SRC) $(KITTYMEMORY_SRC) $(SCLALERTVIEW_SRC)
MyCoolHack_LIBRARIES += substrate
MyCoolHack_FRAMEWORKS = $(PROJ_COMMON_FRAMEWORKS)

include $(THEOS)/makefiles/tweak.mk

# تنظيف وتجهيز قبل البناء
internal-package-check::
	@chmod +x versionCheck.sh
	@./versionCheck.sh || true

after-install::
	install.exec "killall -9 SpringBoard || :"
