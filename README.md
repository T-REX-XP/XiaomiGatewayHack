# XiaomiGatewayHack
Сборник информации по аппаратному и програмному модингу Xiaomi Gateway 


Распиновка и фото плат

## Gateway UART pinout 
![Alt text](/photo/1a8f35e3-5ff6-4d17-b97f-0bbab1bab9aa.jpg "Optional title")

## Gateway USB and UART pinout
![Alt text](/photo/ece7c702-afb3-40f1-9865-57123285bad7.jpg "Optional title")

## Get power for USB 
![Alt text](/photo/photo5208813406491095004.jpg "Optional title")

## Aqara door window sersor
![Alt text](/photo/312691b7-ba32-49bc-9d31-009b79db9db7.jpg "Optional title")



## How to create backup

```
nc -p 2222 -l | dd of=/dev/mtdblock6
```
or 

```
gzip -c -9 / dev / mtd0> /tmp/mtd0.gz  
gzip -c -9 / dev / mtd1> /tmp/mtd1.gz  
gzip -c -9 / dev / mtd2> /tmp/mtd2.gz  
gzip -c -9 / dev / mtd3> /tmp/mtd3.gz
```
or

```
tar -cvpzf backup.tar.gz --exclude = / backup.tar.gz
```

### Create backup via nand dumping 

Снятие полного образа
Чтение областей нанд
```
nand read 80800000 0 100000
nand read 80800000 300000 700000 
```
Выкачать 2 дампа  образа на компьютер, путем записи лога консоли с выводом памяти на экран, а затем преобразовать его в бинарный файл.  
```
minicom -C orig-uImage.txt
```
запускаем с записью лога
```
md.b 80800000 700000
```
выводим содержимое памяти. Чистим лишние строки от терминала. Образ готов.

запись в нанд 
```
==> loady ... 
==> nand erase 300000 700000 
==> nand write 80800000 300000 700000
```
Примерная процедура снятия образа. И восстановления.

