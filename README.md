<p align="center"><img src="https://media.giphy.com/media/WT3ulJmR8Fv1fidZIK/giphy.gif"></p>

# Общая информация

Здесь ты сможешь найти конструкции, которые могут часто пригодится при программировании на `FASM`. По мере возможности и необходимости список будет пополняться. В данном случае рассматривается работа с MS DOS.

# Оглавление

# Конструкции для вывода




## Работа с видеопамятью

Для вывода определённой информации можно работать с видеопамятью напрямую:

```ASM
mov ax, 0xb800
mov es, ax
mov di, 0
mov word[es:di], 0xE141
```

Здесь происходит следующее. Чтобы нам обратиться к памяти, нужно использовать сегмент и смещение. Начало видеопамяти находится в ячейке 0xb800:0x0. Для работы используются пары `ds:si` и `es:di`.
В сегментный реестр данные нельзя положить напрямую, поэтому для этого мы используем `регистр АХ`.
Адрес `0xb800:0x0` содержит данные для вывода верхнего левого угла. При дальнейшем движении по памяти, вывод смещается вправо вдоль строки, как только строка заканчивается, происходит переход на следующую.

> В одной строке 80 символов. Всего на экране 25 строк.

> Чтобы сместиться на один символ, нужно выполнить смещение в памяти на ***2***. Для перехода на новую строку - ***160(0xA0)***


## Вывод одного символа

```ASM
mov ah, 0x2
mov dl, 0x41
int 0x21
```

Здесь в `AH` хранится функция прерывания. Для вывода символа это `0x2`. В `DL` хранится номер ASCII символа, который нужно вывести.

## Вывод строки

```ASM
mov ah, 0x9
mov dx, msg
int 0x21

msg: dw "Text", 0xD, 0xA, '$'
```

В `AH` хранится функция прерывания. Для вывода строки это `0x9`. В `DX` записывается адрес-смещение строки (в данном случае метка является адресом-смещения)




# Работа с прерываниями

## Собственные прерывания

```ASM

```
