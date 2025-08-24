+++
date = '2025-08-24T15:08:22+03:00'
draft = false
title = 'nom'
+++

![tui rss reader nom](/images/01-nom/01.png)

Консольный RSS-ридер Nom
===


1. Introduction
  • Briefly introduce yourself and express your need for a CLI-based RSS news reader.

С 2001 года командная строка присутствует в моей жизни, работе и вообще. Linux, MacOs, вот это всё.

Во времена трилобитов было такое развлечение — читать текстовые «новости» (ну как новости, всякую дребедень типа обновлений в чьих-то блогах, уведомления о каких-то новых статьях и прочее). 
Сначала это читалось через всякие отдельные программы, потом появился Google Reader, в котором у меня скопилось море всяких подписок. Все, кого я знал, много читали. Постепенноо всё ускорялось, появлялись подкасты, видео-хостинги, а google reader закрылся. Наступило время, когда подавляющее количество потребляемого контента стало даже не аудио, а видео, — чтение отошло на задний план.

Чтение для удовольствия стало проявлением ретро-субкультуры, a моём случае оно всегда было со мной. Закладки и RSS как-то сами собой заменились на Reading List в браузере Safari, но всё это время чего-то как будто не хватало, вызывая тягостное ошушение внутренней пустоты. И вот, когда давление пустоты стало нестерпимым (23 августа 2025 года), я полез в интернет искать что такого есть для меня в плане чтения RSS. И что вообще с этой технологией и пользуется ли кто-то чем-то подобным. Да, маленькое отступление — за неделю до этого я перебрал свой Reading List и собрал оттуда ссылки на что-то, что мне до сих пор интересно. Ссылки я эти засунул в NetNewsWire и несколько дней пытался с этим жить. Графический интерфейс NetNewsWire многие хвалят и я ругать его не буду, хотя он меня не устраивает. Точнее, меня не устраивает сам факт его наличия. Мне нужен был RSS-ридер с текстовым (TUI) интерфейсом. Мне нужен был современный ридер, желательно настраиваемый из текстового файла, желательно с навигацией а-ля VIM, желательно маленький и простой.
 
2. The Search for the Perfect RSS Reader
  • Discuss your search for an ideal RSS reader.
  • Mention the key features you were looking for in a news reader.

В поисковые системы ушли запросы типа Modern CLI RSS reader Macos, Reading RSS 2025, CLI import from NetNewsWire, и прочая шляпа со словами cli, shell, modern, tui.
Реультаты шли отнюдь не бурным потоком, но 5-7 ссылок на гитхаб я накопал. Первая и самая популярная штука называется [Newsboat](https://newsboat.org), которая является реинкарнацией давно увядшей читалки немецкого происхождения, написанной на C++ и называющейся Neubeireuter или как-то так (да, юмор категории «Б», настоящее название [Newsbeuter](https://newsbeuter.wordpress.com)).

Когда мне в жизни не хватает C++, я беру Arduino и угораю с ним, а в остальные моменты хочется чего-то другого.

Так что первый вариант мне не подошёл, потому не смотря на обилие настроек и текстовость, мне он показался слишком развесистым и многофункциональным. Да и как представил себе как я буду его компилировать, сразу всё упало внутренне.

Второй вариант оказался прям няшным — [Nom](https://github.com/guyfedwards/nom). Написано на go, устанавливается одной командой, конфигурируется в yaml, управляется кнопками VIM, использует Bubbletea и Glow (библиотеки, которые сделали [Charmbracelet](charm.land) — уникальные чуваки, работы которых меня удивляют и вдохновляют, про них отдельная история будет).


3. Newsboat vs. Nom: The Pros and Cons
  • Compare Newsboat and Nom, highlighting their differences.
  • Explain why you chose Nom over Newsboat, considering factors like modern design and programming language (Go).

Чем прекрасен Nom? Тем, что он не Newsboat :) Он маленький, написан на более свежем языке, красивенький, последний коммит был месяц назад.

4. The Challenge: Importing Data from NetNewsWire
  • Describe the issue of importing RSS feeds from your previous news reader (NetNewsWire).
  • Narrate the solution you discovered, using Crush to create a Python script for converting OPML to Nom-compatible
  formats.

![tui rss reader nom](/images/01-nom/03.png)

Прежде чем трогать руками Nom, нужно было понять насколько запарно будет взять мои закладки и засунуть их в Nom. NetNewsWire умеет экспортировать закладки в OPML, а Nom читает закладки из текстового yaml-файла. Частьь данных, которые есть в OPML не используются внутри Nom, но я достаточно легко смог расстаться с ними (папки и какие-то не нужные мне описания).
До кучи нашёлся повод поиграть с Crush — классная штука, от тех же Charmbracelet, которая является консольным инструментом для работы с языковыми моделями. В итоге — запускаю Crush и прошу его накатать на Питоне скрипт, который сормирует Nom-совместимый yaml-файл.  

![tui rss reader nom](/images/01-nom/04.png)

Crush поскрипел мозгами полторы минуты, выдал мне скрипт, я его немного поправил, запустил uv run opml2yaml.py и все мои закладки оказались внутри Num.

5. Setting Up and Configuring Nom
  • Guide the readers through your installation process and initial configuration of Nom.
  • Share tips and best practices for setting up filters and rules to manage your RSS subscriptions efficiently.

Установка ~~свелась к стандартной команде go install github~~... (чтобы установить, надо склонировать репозиторий, затем выполнить go build и go install), а затем, конвертации файла с закладками, который надо положить в папку приложения (написано в документации куда именно).
Скрипт можно либо написать самому либо найти где-то в инете, либо просто добавить закладки вручную или через специальный ключ при запуске программы — как удобно. Мне было прикольно потыкать Crush для этой цели.

На самом деле можно ничего не окомпилировать, поскольку для линукса, виндовса и макоса можно взять в релизах [готовую сборку](https://github.com/guyfedwards/nom/releases).

6. The First Impressions
  • Discuss your initial experiences using Nom, focusing on its modern user interface and performance.
  • Talk about any notable features or integrations you've found helpful.

Nom прекрасен — вводишь в консоли nom, нажимаешь enter и всё — вожделенный список загловков, по которым перемешаешься стрелочками или j/k. Но это если вам достаточно стандартного, обычного использования. We need to go deeper!

![tui rss reader nom](/images/01-nom/02.png)


7. Overcoming Initial Challenges
  • Describe the hurdles you faced during your learning curve with Nom (e.g., importing feeds, understanding key
  commands).
  • Detail how you overcame these challenges and are now comfortably using Nom as your primary news reader.

![tui rss reader nom](/images/01-nom/05.png)

Если вы извращенец, то можно делать как я, смотрите:
    - внутри neovim (из которого и так не часто выходим) делаем вертикальный сплит
    - в сплите (мне нравится в правом буфере) запускам терминал :terminal
    - и вот уже в терминале выполняем команду nom

![tui rss reader nom](/images/01-nom/05.png)


8. Final Thoughts and Recommendations
  • Summarize why you think Nom is a good choice for those seeking an up-to-date, efficient CLI-based RSS news reader.
  • Provide recommendations or advice for others who might be considering switching to Nom from another reader.

Что имеем в итоге: консольный RSS-ридер Nom, запихнутый внутрь Neovim, позволяющий читать новости, а в соседнем сплите можно редактировать текст или открыть там второй num, например. Ну круто же!

![tui rss reader nom](/images/01-nom/06.png)
