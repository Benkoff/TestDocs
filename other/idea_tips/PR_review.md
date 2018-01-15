# Как сделать Pull Request ревью при помощи IDEA

1. Подготовка.
Для начала надо прописать путь к установленному git, если он не установлен, то установить и прописать. Для Windows: 
Control Panel -- System -- Advanced system settings -- Advanced -- Environment Variables -- System variables -- Path (Edit) -- New. 
В моем случае гит установлен в C:\Program Files\Git\cmd.

2. Запускаем IDEA, открываем проект, выбираем Terminal, где набираем:
```
git fetch upstream pull/73/head:pr-73
```
* upstream - должен быть прописан (прописывается автоматически при импорте проекта) в файле конфигурации .git\config примерно так: 
```
[remote "upstream"]
	url = https://github.com/JujaLabs/juja-platform.git
	fetch = +refs/heads/*:refs/remotes/upstream/*
```
* pull/73/head - путь к Pull Request номер 73, соответственно, для PR#100500 это будет pull/100500/head
* pr-73 - название локальной ветки, куда будут загружены предложенные в PR изменения.

3. Справа внизу в IDEA написано что то вроде CTRL   UTF-8  Git:develop, жмем туда, где Git:имя_ветки и 
выбираем в разделе Local Branches созданную нами локальную ветку и дальше **checkout** для переключения в нее или **compare**, 
чтобы сравнить предложенные изменения с оригинальным кодом.

4. Удобно читаем код, запускаем, если нужно, параллельно пишем свои комментарии и замечания, как обычно в окошке соответствующего Pull Request на гитхабе.

Идея, как загрузить код из Pull Request, взята тут: https://blog.scottlowe.org/2015/09/04/checking-out-github-pull-requests-locally/
