# Carla

## 环境配置
```bash
apt-get install -y gnupg2
apt-get install software-properties-common
apt-get install libomp5
```

## 安装Carla
1. Set up the Debian repository in the system
```bash
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1AF1527DE64CB8D9
add-apt-repository "deb [arch=amd64] http://dist.carla.org/carla $(lsb_release -sc) main"
```