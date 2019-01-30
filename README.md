Скрипт для настройки слоёв Yocto

**Перед использованием**

***Настройка ОС***

Для Ubuntu необходимо поставить следующие пакеты:
```
sudo apt-get install git build-essential python diffstat texinfo gawk chrpath dos2unix wget unzip socat doxygen libc6:i386 libncurses5:i386 libstdc++6:i386 libz1:i386
```

Переконфигурировать shell на bash

```
sudo dpkg-reconfigure dash
```
В диалоговом окне выбрать 'No'

***Установка Cross-компилятора***

```
wget https://releases.linaro.org/components/toolchain/binaries/7.2-2017.11/arm-linux-gnueabihf/gcc-linaro-7.2.1-2017.11-x86_64_arm-linux-gnueabihf.tar.xz
tar -Jxvf gcc-linaro-7.2.1-2017.11-x86_64_arm-linux-gnueabihf.tar.xz -C $HOME
wget https://releases.linaro.org/components/toolchain/binaries/7.2-2017.11/aarch64-linux-gnu/gcc-linaro-7.2.1-2017.11-x86_64_aarch64-linux-gnu.tar.xz
tar -Jxvf gcc-linaro-7.2.1-2017.11-x86_64_aarch64-linux-gnu.tar.xz -C $HOME
```

**Установка и настройка Yocto**

```
git clone git://github.com/Technokom/oe-layersetup.git tksdk
cd tksdk
./oe-layertool-setup.sh -f configs/tk-sdk-<version>-config.txt
cd build
. conf/setenv
export TOOLCHAIN_PATH_ARMV7=$HOME/gcc-linaro-7.2.1-2017.11-x86_64_arm-linux-gnueabihf
export TOOLCHAIN_PATH_ARMV8=$HOME/gcc-linaro-7.2.1-2017.11-x86_64_aarch64-linux-gnu
```

**Сборка системы**
```
MACHINE=skit-am437x bitbake tk-base-image
```