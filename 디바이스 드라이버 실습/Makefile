#디바이스 드라이버를 KERNEL 빌드한 헤더의 경로로 가서 build 한 뒤에, build 결과물만 현재 디렉토리로 갖고 오도록 구성된 Makefile

KERNEL_HEADERS=/lib/modules/$(shell uname -r)/build

obj-m += geonhee.o

PWD := $(CURDIR)

driver:
        make -C $(KERNEL_HEADERS) M=$(PWD) modules

clean:
        make -C $(KERNEL_HEADERS) M=$(PWD) clean
