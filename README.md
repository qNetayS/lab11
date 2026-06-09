# Лабораторная работа №11: Совместная разработка с использованием ngrok

**Студент:** qNetayS  
**Дата выполнения:** 2026-05-31  
**Окружение:** Debian Linux  
**Репозиторий:** https://github.com/qNetayS/lab11

---

## Цель работы

Изучить процесс создания сеансов совместной разработки с использованием инструмента **ngrok** для организации удалённого доступа к локальным серверам.

---

## Ход выполнения

### 1. Подготовка окружения

Созданы директории для установки компонентов:

```bash
cd ~
mkdir -p install
mkdir -p tmp
export HOME_PREFIX=$(pwd)/install
export USERNAME=$(whoami)
```
Результат:
/home/vboxuser/install
qNetayS


### 2. Сборка librevent
```
cd tmp
wget https://github.com/libevent/libevent/releases/download/release-2.1.8-stable/libevent-2.1.8-stable.tar.gz
tar -xzvf libevent-2.1.8-stable.tar.gz
cd libevent-2.1.8-stable
./configure --prefix=${HOME_PREFIX}
make && make install
cd ..
```
Результат:
ncurses успешно установлен.

### 3.Сборка tmux из исходников
```
wget https://github.com/tmux/tmux/releases/download/2.5/tmux-2.5.tar.gz
tar -xzvf tmux-2.5.tar.gz
cd tmux-2.5
./configure --prefix=${HOME_PREFIX} CFLAGS="-I${HOME_PREFIX}/include -I${HOME_PREFIX}/include/ncurses"
make && make install
cd ..
```
### 4.Установка ngrok
```
wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz
tar -xzvf ngrok-v3-stable-linux-amd64.tgz
mv ngrok ${HOME_PREFIX}/bin
```


### 5.Настрока и авторизация ngrok
```
export NGROK_TOKEN=XXX
ngrok authtoken ${NGROK_TOKEN}
```

### 6.Создание сессии
```
ngrok tcp 22
```
### 7.Подключение второго участника
```
ssh qNetayS@0.tcp.ngrok.io -p 12345
tmux a -t session_with_group
```
Результат: торой участник успешно подключился к общей tmux сессии. Оба пользователя видят одинаковый терминал и могут работать совместно.
