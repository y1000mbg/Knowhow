# 外付けHDDやUSBメモリにLinuxをインストールする

## 概要

外部メディアにLinuxをインストールして使いたかったので方法を調べました。  
外付けHDDにインストールしておけばいつでも同じ環境を使えるので便利かなぁと思います。

2.5インチSSDにインストールしておけば読み書きも高速で快適な予感がします。

## 必要資材

- 外付けメディア（HDD or USBメモリ）
- VirtualBox環境
  - ※ホストOSはWindowsでもLinuxでも可能

___VirtualBox環境はLinuxインストール用に使います。  
実PC環境で実施したい場合はブート用のLinuxメディアを用意すればVirtualBox環境は不要です。___

## 実施環境

- ホストOS：Ubuntu 18.04 LTS
- 仮想環境：VirtualBox 5.2.12

## 作業の流れ

1. インストール先メディアを接続
2. VirtualBoxから **実HDD（インストール先メディア）** を扱う為のVDIを作成
3. VirtualBoxで仮想環境を作成
4. Linuxのインストール

## 作業詳細

### 1. インストール先メディアを接続

Ubuntuは外部メディアが接続されると自動でマウントされます。
fidiskコマンドなどを使用しデバイス名を特定します。

```
$ sudo fdisk -l
```

### 2. VirtualBoxから実HDD（インストール先メディア）を扱う為のVDIを作成

VirtualBoxでは実ディスクをそのまま取り扱えません。  
実ディスクと紐付けるvdiファイルを作成し、vdiファイル経由で実ディスクにアクセスします。

```
## 凡例
## VBoxManage internalcommands createrawvmdk -filename ${作成するvdiファイル名} -rawdisk ${外付けデバイス名}

## rootで作業
# VBoxManage internalcommands createrawvmdk -filename /root/hdd1.vdi -rawdisk /dev/sdb
```

### 3. VirtualBoxで仮想環境を作成

通常通りGUIから仮想マシンを作成し起動

### 4. Linuxのインストール

VirtualBox上から見ると```/dev/sda```が実ディスクになっているので通常手順でLinuxをインストールします。

## 備考

外付けメディアからLinuxを起動した際に内蔵ディスクがsdbなどで見えることがあります。ブートに成功した **外付けメディアがsda扱いになるので、内蔵メディアが外付け扱い** のような状態です （ややこしいですか……）  
lsblkコマンド、fdiskコマンドなどで見えるのでデバイスとして認識されているのでrootユーザーでマウントすれば中身が見えるかもしれません **（未検証）**
