# chat_tools
Набор скриптов для бесед ВКонтакте.
Внимание! Скрипты написаны на Python 2.7.
Для работы скриптов необходимо установить модули:  
`pip install vk_api pillow`
***
### antikick
Антикик - основной инструмент захвата бесед. Работая в режиме прослушивания LongPoll, он перехватывает сообщения об исключении ваших аккаунтов из любой из ваших бесед и мгновенно возвращает данный аккаунт в беседу с помощью других аккаунтов.   

Скрипт приобретает эффективность при использовании трёх и более аккаунтов. 

При первом запуске скрипт создаст файл _accounts.txt_ 
В него нужно вписать логины и пароли ваших аккаунтов в таком формате: 
_login:password 
login:password_ 

При втором запуске скрипт создаст пустой файл whitelist.txt и начнёт работу без него. 
По умолчанию, скрипт возвращает в беседы только подключённые к нему аккаунты. В whitelist можно указать id пользователей, которых вы хотите возвращать в беседы дополнительно (даже если они не подключены к скрипту). id пользователей следует указывать в числовом формате, по одному id на строчку. 

Скрипт поддерживает команды.  
***/assemble*** - приглашает в беседу все недостающие аккаунты из задействованных 
***/shutdown*** - исключает из беседы все задействованные аккаунты 

Команды принимаются только от лица задействованных аккаунтов, а так же аккаунтов, находящихся в "белом списке" (_whitelist.txt_). 
  
На данный момент ВКонтакте существует ограничение на использование метода добавления в беседу: 100 раз в 30 минут на один аккаунт.  
Скрипт, получив сообщение от сервера VK о срабатывании такого ограничения, покидает беседу с данного аккаунта, что позволяет вернуться через полчаса и не быть исключённым до этого.  

### spammer
Спамер отправляет сообщения в указанные беседы с указанной периодичностью. 
Поддерживается работа только с одним аккаунтом. 
Сообщение может состоять из текста и/или изображения(-ий) в формате jpg, png. ВКонтакте разрешает прикреплять не более 10 изображений к сообщению.  

Скрипт поддерживает параметр командной строки -t, задающий паузу между отправкой сообщений. Пауза по умолчанию (без указания параметра) составляет 0.5 секунды. В параметре можно указать количество секунд целым натуральным числом. 
Пример использования параметра:  
`python main.py -t 5`


Скрипт поддерживает ввод капчи (а она обязательно появится после отправки 10-15 одинаковых сообщений за короткий промежуток времени). Капча выводится на экран в виде окошка с картинкой и полем ввода. После ввода капчи в поле нужно нажать Enter. 

При первом запуске скрипт создаст файлы _account.txt, chats.txt_ и папку _message_. 

_account.txt_: логин и пароль через двоеточие в качестве разделителя (login:password) 

_chats.txt_: id бесед для работы скрипта (любое количество, по одному id на строку). id беседы можно посмотреть в адресной строке, например https://vk.com/im?sel=c28 соответствует 28 id беседы. Если в адресной строке многабукаф, id открытой в данный момент беседы будет соответствовать последнее значение в строке. Внимание! id указывается без буквы "c". 

_message_: папка, содержащая элементы сообщения. В ней может располагаться один .txt файл с текстом сообщения и несколько картинок в формате jpg или png. Для работы скрипта сообщение не должно быть пустым, то есть в папке должна быть как минимум одна картинка или один непустой текстовый файл.  


### title_keeper
Удерживатель названия беседы. Позволяет так же удерживать и аватарку беседы. 
Поддерживается работа только с одним аккаунтом одновременно. 

При первом запуске скрипт создаст файлы _account.txt, chats.txt_ и папку _title_ 

_account.txt_: логин и пароль через двоеточие в качестве разделителя (_login:password_) 

_chats.txt_: id бесед для работы скрипта (любое количество, по одному id на строку). id беседы можно посмотреть в адресной строке, например https://vk.com/im?sel=c28 соответствует 28 id беседы. Если в адресной строке многабукаф, id открытой в данный момент беседы будет соответствовать последнее значение в строке. Внимание! id указывается без буквы "c". 

_title_: папка, содержащая название и аватарку беседы для удержания. В ней может располагаться один .txt файл, содержащий название беседы в одну строку, и одна картинка - аватарка беседы. Для работы скрипта папка не должна быть пустой.
