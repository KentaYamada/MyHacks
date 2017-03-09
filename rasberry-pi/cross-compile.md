# Rasberry Piのクロスコンパイル環境構築
## 1. 実行環境
- Mac OS X EI Captian(10.11.6)
- Ubuntu14.04LTS(on VirtualBox)

## 2. ツールチェーンの準備
```
  # gitがインストールされていない場合
  sudo apt-get install git

  # ツールチェーンのダウンロード
  mkdir ~/raspi
  cd ~/raspi/
  git clone https://github.com/raspberrypi/tools.git

  # 環境変数にパスを設定
  vim ~/.bashrc
  export PATH=$HOME/rpi/tools/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian-x64/bin:$PATH

  # 設定反映
  source ~/.bashrc
```

## 3. クロスコンパイル実験
```
  vim /path/to/hello.c

  #include <stdio.h>

  int main(void)
  {
      printf("Hello, Rasberry Pi\n");
      return 0;
  }
```

```
  vim /path/to/Makefile

  CXX=arm-linux-gnueabihf-gcc
  CFLAGS=-Wall -O2
  all:
      $(CXX) $(CFLAGS) -o hello hello.c
  clean:
      rm -f hello
```

```
  # ビルド
  $ make

  # scp等でrasberry piにバイナリファイルを転送
  scp hello pi@192.168.xxx.xxx:/home/pi

  # ssh等でログインして実行
  ssh pi@192.168.xxx.xxx
  $ ./hello
  Hello, Rasberry Pi
  と表示されれば成功
```
