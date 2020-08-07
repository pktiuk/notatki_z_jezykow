## Screen

Otwarcie nowej sesji
screeen []

Wyjście z sesji
Ctrl+a , potem 

lista aktywnych sesji
screen -ls
> There is a screen on:
>        21512.pts-4.komp-pc (07.08.2020 12:54:54)   (Attached)
>1 Socket in /run/screen/S-komp.

Dołącz do jednej z sesji
screen -r [numer_sesji]

wszystkie komendy:

```
  break       ^B b         flow        ^F f         lockscreen  ^X x         pow_break   B            screen      ^C c         width       W
  clear       C            focus       ^I           log         H            pow_detach  D            select      '            windows     ^W w
  colon       :            hardcopy    h            login       L            prev        ^H ^P p ^?   silence     _            wrap        ^R r
  copy        ^[ [         help        ?            meta        a            quit        \            split       S            writebuf    >
  detach      ^D d         history     { }          monitor     M            readbuf     <            suspend     ^Z z         xoff        ^S s
  digraph     ^V           info        i            next        ^@ ^N sp n   redisplay   ^L l         time        ^T t         xon         ^Q q
  displays    *            kill        K k          number      N            remove      X            title       A
  dumptermcap .            lastmsg     ^M m         only        Q            removebuf   =            vbell       ^G
  fit         F            license     ,            other       ^A           reset       Z            version     v

^]  paste .
"   windowlist -b
-   select -
0   select 0
1   select 1
2   select 2
3   select 3
4   select 4
5   select 5
6   select 6
7   select 7
8   select 8
9   select 9
I   login on
O   login off
]   paste .
```