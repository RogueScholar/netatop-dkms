KVERSION := $(shell uname -r)
KDIR := /lib/modules/$(KVERSION)/build
PWD := $(shell pwd)

obj-m   := netatop.o

netatop.o:	netatop.h	netatopversion.h

default:
		./mkversion
		netatop.ko:	netatop.c 
			$(MAKE) -C $(KDIR) M=$(PWD) modules

install:
		netatop.ko
		install -d /lib/modules/`uname -r`/extra
		install -m 0644 module/netatop.ko -t /lib/modules/`uname -r`/extra
		depmod

clean:
		rm -f *.o *.ko
		rm -f .netatop*
		rm -f netatop.ko.unsigned netatop.mod.c
		rm -f Module.symvers                
		rm -f modules.order                
		rm -fr .tmp_versions

load:
		-/sbin/rmmod netatop
		/sbin/insmod netatop.ko
