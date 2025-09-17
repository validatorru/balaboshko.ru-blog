+++
date = '2025-09-17T04:28:22+03:00'
draft = false
title = 'челендж — удаляю свой блог и разворачиваю его заново на Ubuntu 24.04 и Nginx за 10 минут!'
+++

_Ten Minutes nginx installation challenge_


![Ten Minutes nginx installation challenge](/images/06-nginx/00.jpeg)



*В общем, план таков и больше никаков:*

▌║█║▌│║▌║▌█║▌║ ▌║█║▌│║▌║▌█║▌║ ▌║█
1. *Write an outline*\
    Составление тактического плана перед цифровым десантом — признак высокого интеллекта (а вовсе не паранойи)
2. *Backup the hell out of everything*\
    Ритуал уважения к своему будущему «я», которое в параллеьной вселенной проклинает нас сидя на холодном кафеле душевой и обнимая себя за коленки. Именно поэтому мы и бэкапим всё, что не приколочено, а то, что приколочено, отковыриваем и тоже бэкапим
    - VPS snapshot,
    - files (/etc + /home)
3. *Delete existing Ubuntu VPS*\
    Отправить в цифровое небытие всё, что только что было упорядоченными словами и мыслями, сначала убедиться, что убиваем именно _ТОТ_ сайт, который хотим удалить
    - make sure the site is UP
    - delete the VPS
    - make sure the site is DOWN
4. *Upload SSH-key via hosting UI*\
    Чтобы не вводить пароли на глазах у изумлённой публики.\
    Ну и вообще, ключи — это очень хорошо и полезно!
5. *Install fresh Ubuntu Server LTS on the VPS instance*\
    Пиу-пиу, убунту 24.04 появляется на нашем VPS
    - tell it to use SSH-key
6. *Start video, start the timer*\
    Этот шаг я продолбал, потому что запустил таймер и видео где-то на третьем шаге
7. *Configure Users*\
    Ходить на сервер от имени пользователя root — к проблемам с нервной системой, ergo, делаем своего пользователя из трёх букв
    - access VPS as a root
    - add _bzz_ user with sudo access
    - exit
    - check _bzz_ login
7. *Upload SSH-key via ssh-copy-id*\
    Снова ключ, закидываем на сервер уже для _bzz_ и уже не через UI, а через консоль
    - access the VPS via ssh
8. *Install nginx*
    - update Ubuntu
    - see default Nginx page in Safari
    - add bzz to www-data group (gpasswd -a www-data bzz) — вот на этом моменте я затупил и решил подсмотреть
    - chmod /home/bzz/www to 775
    - create a new webroot folder
    - create a test index.html
    - add a new nginx config file
    - restart nginx
    - see the new page
9. *Install SSL certificates*\
    Ну какой же сайт без SSL, вы что, смеётесь? Тут, кстати, столкнулся впервые с ситуацией, когда apt что-то делал в фоновом режиме и отказался с первого раза устанавливать что бы то ни было. Интересно
10. *Restart nginx*
    - test everything
11. *Stop the timer, stop the video*
12. *Publish a blog post*\
    _Done_

▓▃▂▁▂▃▅▆▇█████▇▆▅▃▂▁<iframe width="720" height="405" src="https://rutube.ru/play/embed/fbea225d02c65add5389b7e0011ff549/" style="border: none;" allow="clipboard-write; autoplay" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>


Видео длится 18 минут, из которых я полторы минуты выбираю саундрек (не для вас, а для себя, вы всё равно ничего не услышите), потом щзабываю как добавить пользователя в нужную мне группу, чтобы Nginx увидел мою папку, а затем решаю установить SSL-сертификаты и гуглю яндексом всплывшую ошибку.

А, ну и ещё я смешно мечусь между окнами в tmux потому что забыл, что в чистой убунте в командной строке не включены vim-клавиши :) 

