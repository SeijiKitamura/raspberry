# Raspberry Pi セットアップ

インターネットにはセットアップの仕方がごろごろ転がっていますが
より端的に自分が必要な分だけ記載しておきます。

## インストール方法
詳細はインターネットを参照してください。
「noob」ではなくより軽快に動作する「raspbian」をおすすめします。

## 全体設定
```bash
sudo raspi-config
```

### Hostname
```bash
Advanced Options
Hostname
任意のHostnameを入力
```

### キーボード設定
```bash
Internationalisation Options
Change Keyboard Layout
Generic 105-key(Intl)PC
Japanese
The default for the keyboard layout
No compose key
```

### タイムゾーン
```bash
Internationalisation Options
Asia
Tokyo
```

### ファイル拡張
```bash
Expand Filesystem
再起動
```

### SSHサーバー有効化
```bash
Advanced Options
SSH
Enable
再起動
```

## IP Address
### 有線LAN
固定IPアドレスで運用したい場合は以下の内容を/etc/dhcpcd.confに入力
```bash
interface eth0
static ip-address=xxx.xxx.xxx.xxx/24
static routers=xxx.xxx.xxx.xxx
static domain-name-sercers=xxx.xxx.xxx.xxx
```
### ネットワーク再起動
```sudo /etc/init.d/networking restart```

### 無線LAN
固定IPアドレスで運用したい場合は以下の内容を
/etc/wpa-supplicant/wpa_supplicant.confに追加
```bash
network={
  ssid="接続したい無線LANのSSID"
  psk="パスワード"
}
```

以下の内容を/etc/dhcpcd.confに入力
```bash
interface wlan0
static ip-address=xxx.xxx.xxx.xxx/24
static routers=xxx.xxx.xxx.xxx(無線LANルーターのアドレス)
static domain-name-sercers=xxx.xxx.xxx.xxx(同上)
```

### ネットワーク再起動
```bash
sudo /etc/init.d/networking restart
sudo ifdown wlan0
sudo ifup   wlan0
```

## Update
```bash
sudo apt-get update
sudo apt-get upgrade
```

## vim
```bash
cd
sudo apt-get install -y vim
git clone https://github.com/SeijiKitamura/vimrc.git
cp vimrc/.vimrc ./
mkdir -p .vim/bunble
cd .vim/bundle
git clone git://github.com/Shougo/neobundle.vim
cd
echo "alias vi='/usr/bin/vim'" >> .bashrc
soruce .bashrc
```

## git
```bash
cd
sudo apt-get install -y git
git config --global user.name 'ユーザー名'
git config --global user.emal メールアドレス
git config --global core.editor vim
```
