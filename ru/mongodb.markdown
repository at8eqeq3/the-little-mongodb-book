\thispagestyle{empty}
\changepage{}{}{}{-1.5cm}{}{2cm}{}{}{}
![The Little MongoDB Book, By Karl Seguin](ru/title.png)\ 

\clearpage
\changepage{}{}{}{1.5cm}{}{-2cm}{}{}{}

## Об этой книге ##

### Лицензия ###
«Маленькая книга про MongoDB» распространяется под лицензией Attribution-NonCommercial 3.0 Unported license. **Вы не должны платить за эту книгу.**

Вы можете свободно копировать, распространять, изменять и публиковать эту книгу. Однако, я прошу всегда указывать автора (Karl Seguin) и не использовать ее в коммерческих целях.

Полный текст лицензии можно найти здесь:

<http://creativecommons.org/licenses/by-nc/3.0/legalcode>

### Об авторе ###
Карл Сегуин - разработчик, имеющий опыт работы в различных областях и технологиях. Он - профессиональный разработчик на .NET и Ruby. Он - участник нескольких открытых проектов, технический писатель и участник конференций. Касательно MongoDB, он принимает участие в разработке NoRM - библиотеки на C#, создал интерактивный курс [mongly](http://mongly.com), а также [Mongo Web Admin](https://github.com/karlseguin/Mongo-Web-Admin). Его бесплатный сервис для разработчиков казуальных игр [mogade.com](http://mogade.com/) также работает на MongoDB.

Карл также написал [The Little Redis Book](http://openmymind.net/2012/1/23/The-Little-Redis-Book/) ([перевод](https://github.com/kondratovich/the-little-redis-book/) этой книги на русский выполнил [Андрей Кондратович](http://twitter.com/_sparrow)).

Его блог можно найти по адресу <http://openmymind.net>, его твиттер - [@karlseguin](http://twitter.com/karlseguin)

### Благодарности ###
Я особо благодарен [Perry Neal](http://twitter.com/perryneal) за то, что он позволил мне воспользоваться его глазами, разумом и увлеченностью. Твоя помощь неоценима. Спасибо тебе.

### Актуальная версия ###
Актуальная версия исходного кода книги доступна по адресу: 

<http://github.com/karlseguin/the-little-mongodb-book>.

### О переводе ###

Перевод подготовил [Дмитрий Григорьев](http://twitter.com/at8eqeq3). Актуальную версию исходников перевода можно получить по адресу <http://github.com/at8eqeq3/the-little-mongodb-book>.

\clearpage

## Введение ##
 > Я не виноват, что главы получились такими короткими. Это все от того, что MongoDB очень легко изучать.

Часто говорят, что технология развивается немыслимыми темпами. Да, список новых технологий и техник непрерывно растет. Однако, мне всегда казалось, что фундаментальные технологии, используемые программистами, движутся значительно медленнее. Можно потратить годы на изучение того, что еще осталось актуальным. Удивляет то с какой скоростью привычные технологии заменяются новыми. Нечто, казавшееся таким привычным, внезапно оказывается под угрозой быть забытым совсем.

Самым, пожалуй, примечательным образцом таких изменений может служить рост популярности NoSQL-технологий по сравнению с реляционными базами данных. Кажется, что еще вчера весь интернет держался на нескольких СУРБД, а сегодня уже пять, или около того, NoSQL-решений показывают себя весьма полезными.

И хотя кажется, что такие вещи происходят мгновенно, в реальности могут пройти годы, пока эти технологии станут широко распространены. Начальный энтузиазм подогревается относительно небольшими группами разработчиков и компаний. Оттачиваются решения, усваиваются уроки, и вот, видя, что технологии становятся более зрелыми, все остальные постепенно начинают пробовать их самостоятельно. Частично это так применительно к NoSQL-решениям, которые не способны полностью заменить традиционные хранилища, но предназначены для решения определенного круга задач в дополнении к ним.

Кроме сказанного выше, мы должны объяснить, что мы имеем в виду, говоря «NoSQL». Это очень неконкретное название, и для разных людей оно может означать разные вещи. Лично я часто использую его, чтобы назвать некую систему, играющую роль в хранении данных. С другой стороны, NoSQL (опять же, для меня) - это вера в то, что хранение данных не обязательно происходит в одной-единственной системе. Разработчики реляционных баз данных исторически пытаются представить свои продукты универсальными, NoSQL склоняется к небольшим зонам ответственности, где для каждой задачи может быть найден лучший инструмент. Таким образом, ваш NoSQL-стек может по-прежнему использовать реляционную базу (допустим, MySQL), но также иметь Redis в качестве persistence lookup(???) определенных частей системы, и еще Hadoop для обработки больших объемов данных. Проще говоря, NoSQL - это быть открытым и знать об альтернативах, существующих и новых способах и инструментах для управления данными.

Вы, наверное, задумались, как MongoDB относится к этому всему. Являясь документ-ориентированной базой данных, Mongo - это более общее NoSQL-решение. Её можно рассматривать как альтернативу реляционным базам. И, как реляционные базы, она тоже может выиграть, будучи связанной с другими, более специализированными NoSQL-решениями. MongoDB имеет свои достоинства и недостатки, о которых мы расскажем чуть дальше в этой книге.

Как вы уже, возможно, заметили, слова «MongoDB» и «Mongo» означают одно и то же.

## Начало работы ##
Большая часть этой книги описывает основной функционал MongoDB. Поэтому мы будем работать с оболочкой MongoDB. Оболочка полезна для обучения, и, ко всему прочему, является неплохим инструментом для управления, однако при написании кода вы будете использовать MongoDB-драйверы.

Вот и первое, что мы узнаем о MongoDB - её драйверы. У MongoDB есть [множество официальных драйверов](http://www.mongodb.org/display/DOCS/Drivers) для различных языков. Эти драйверы не сильно отличаются от возможно известных вам драйверов для других БД. На основе этих драйверов сообществом разработаны более специфичные для некоторых языков и фреймворков библиотеки. Например, [NoRM](https://github.com/atheken/NoRM) - библиотека для C#, использующая LINQ, и [MongoMapper](https://github.com/jnunemaker/mongomapper) - библиотека на Ruby, совместимая с ActiveRecord. Выбрать для работы низкоуровневый драйвер или более высокоуровневую библиотеку - дело исключительно ваше. Я говорю об этом лишь из-за того, что некоторые люди при знакомстве с MongoDB не понимают, почему есть официальные драйверы и библиотеки, разработанные сообществом; первые предназначены для низкоуровневого «общения» с БД, вторые - более «заточенные» под конкретный язык или фреймворк.

Я настоятельно советую при чтении этой книги воспроизводить мои действия самостоятельно, а также исследовать возможности для решения собственных вопросов. MongoDB достаточно просто установить, так что давайте потратим пару минут на подготовку всего необходимого.

1. Обратитесь к [официальной странице загрузок](http://www.mongodb.org/downloads) и скачайте бинарный дистрибутив из первой строчки (рекомендованную стабильную версию) для своей операционной системы. Для нужд разработки пойдет и 32-битная, и 64-битная.

2. Распакуйте архив (куда вам удобно) и перейдите в каталог `bin`. Пока не нужно ничего запускать, но запомните, что  `mongod` - это серверный процесс, а `mongo` - это клиентская оболочка. С этими двумя программами мы и будем проводить большую часть нашего времени.

3. Создайте в `bin` текстовый файл с названием `mongodb.config`.

4. Добавьте в него всего одну строчку: `dbpath=PATH_TO_WHERE_YOU_WANT_TO_STORE_YOUR_DATABASE_FILES`. Например, под Windows это может быть `dbpath=c:\mongodb\data`, а под Linux - `dbpath=/etc/mongodb/data`.

5. Убедитесь, что указанный в `dbpath` путь существует.

6. Запустите mongod с параметром `--config /path/to/your/mongodb.config`

Например, для пользователя Windows, если он распаковал архив в `c:\mongodb\` и создал `c:\mongodb\data\`, то в `c:\mongodb\bin\mongodb.config` ему нужно указать `dbpath=c:\mongodb\data\`, а запускать `mongod` из командной строки, выполнив `c:\mongodb\bin\mongod --config c:\mongodb\bin\mongodb.config`.

Чтобы сэкономить буквы, можно добавить каталог `bin` в переменную окружения `PATH`. Действия для пользователей Linux и MacOS примерно такие же. Отличаться будут только пути.

Надеюсь, что все прошло успешно и MongoDB работает. Если же вы получаете ошибку, то прочтите внимательно вывод: сервер обычно очень хорошо объясняет, что с ним не так.

Теперь вы можете запустить `mongo` (без *d*), который запустит оболочку к вашему серверу. Попробуйте ввести `db.version()`, чтобы убедиться, что все работает как надо. В идеале, вы должны увидеть номер установленной вами версии.

\clearpage

## Глава 1 - Основы ##
Мы начнём наше путешествие с исследования основных действий при работе с MongoDB. Очевидно, это есть ключ к пониманию сути MongoDB, но это также поможет найти ответы на более высокоуровневые вопросы применения MongoDB.

Для начала, вот вам 6 простых концепций, которые нужно понять:

1. MongoDB вкладывает в понятие «база данных» уже привычное вам значение (оракловоды называют это «схема»). В каждом экземпляре MongoDB может быть 0 или более баз данных, каждая из которых является контейнером для всего остального.

2. База данных может содержать 0 или более «коллекций». Коллекции во многом похожи на таблицы, и представлять их именно такими не будет ошибкой.

3. Коллекции состоят из 0 или более «документов». Документ, как уже можно догадаться, очень похож на строку.

4. Документ состоит и 1 или более «полей», которые, внезапно, можно сравнить со столбцами.

5. «Индексы» в MongoDB работают примерно так же, как и их тезки в СУРБД.

6. «Курсоры» отличаются от первых пяти концепций, но они не менее важны, хотя про них и часто забывают. Я думаю, они заслуживают отдельного упоминания. Самый важный момент касательно курсоров - это то, что когда вы запрашиваете данные у MongoDB, она возвращает курсор, с которым мы и работаем - считаем количество документов, листаем вперед-назад, а не сами данные.

Еще раз, MongoDB сделана из **баз данных**, которые содержат **коллекции**. **Коллекция** состоит из **документов**. Каждый **документ** имеет **поля**. **Коллекции** могут быть **проиндексированы** для повышения производительности поиска и сортировки. И, наконец, когда мы запрашиваем данные у MongoDB, мы делаем это через **курсор**, а реальное выполнение запросов откладывается, пока данные не станут необходимы.

Вам, вероятно, интересно, зачем использовать новую терминологию (коллекции вместо таблиц, документы вместо строк, поля вместо столбцов). Чтобы всё усложнить? На самом деле, соль в том, что хотя эти понятия и похожи на своих реляционных «коллег», они не идентичны. Основное различие в том, что реляционные базы определяют **столбцы** на уровне **таблиц**, тогда как документ-ориентированная база определяет **поля** на уровне **документов**. Таким образом, каждый **документ** в **коллекции** может иметь свой собственный уникальный набор **полей**. По сути, **коллекция** - это всего лишь контейнер по сравнению с **таблицей**, а **документ** хранит намного больше информации, чем **строка**.

Хотя это и очень важно понимать, не переживайте, если пока еще не все абсолютно ясно. После пары insert-ов будет понятнее. По большому счёту, суть в том, что коллекции не принципиально, что происходит внутри неё (она бессхемна). Поля принадлежат каждому отдельному документу. Достоинства и недостатки такого подхода мы изучим в одной из следующих глав.

Предлагаю немного повозиться. Если вы еще не запустили сервер и оболочку, самое время сделать это. Оболочка выполняет JavaScript. В ней есть несколько глобальных команд, таких как `help` или `exit`. Команды, выполняемые на текущей базе данных, выполняются на объекте `db`, что-то в духе `db.help()` или `db.stats()`. Команды на определенной коллекции (которые нам нужны чаще всех), выполняются на объекте `db.COLLECTION_NAME` - `db.unicorns.help()` или `db.unicorns.count()`.

Введите в оболочке команду `db.help()`, и вы получите список команд, которые можно выполнить на объекте `db`.

Небольшое отступление. Поскольку в оболочке у нас JavaScript, если вы выполните метод и забудете про скобки `()`, вам вернется тело метода, а не результат его выполнения. Я говорю об этом, чтобы когда вы в первый раз сделаете так и увидите ответ, начинающийся с `function(...){`, вы не очень пугались. Например, если вы напишете `db.help` (без скобок), вы получите код метода `help`.

Для начала мы воспользуемся глобальным методом `use` для переключения базы данных. Введите `use learn`. Не важно, что упомянутая база данных на самом деле не существует: как только мы создадим в ней первую коллекцию, мы одновременно создадим и БД `learn`. Теперь, находясь внутри базы данных, мы можем выполнять специфичные для базы команды, такие как `db.getCollectionNames`. Сделав это, вы получите пустой массив (`[ ]`). Поскольку коллекции бессхемны, нам не нужно явно создавать их. Мы можем просто вставить документ в новую коллекцию. Для этого у нас есть команда `insert`, которой мы передаем создаваемый документ:

	db.unicorns.insert({name: 'Aurora', gender: 'f', weight: 450})

Этой строкой мы осуществляем вставку (`insert`) на коллекции `unicorns`, передавая методу единственный аргумент. Внутри MongoDB использует двоичный сериализованный JSON.  Внешне же это означает, что нам придется часто использовать JSON, как в случае с нашим параметром. Если мы теперь выполним `db.getCollectionNames()`, мы получим целых две коллекции - `unicorns` и `system.indexes`. `system.indexes` создается единожды в каждой базе данных и хранит сведения о ее индексах.

Теперь на `unicorns` можно выполнить команду `find` и получить список документов:

	db.unicorns.find()

Обратите внимание, что кроме введенных вами данных, есть еще поле `_id`. Каждый документ должен иметь уникальное поле `_id`. Вы можете генерировать его самостоятельно или позволить MongoDB создавать ObjectId за вас. Чаще всего вы будете доверять это MongoDB. По умолчанию, поле `_id` проиндексировано - это и объясняет появление коллекции `system.indexes`. Можно посмотреть и на неё:

	db.system.indexes.find()

Вы получите имя индекса, базу данных и коллекцию, для которой он создан, а также поля, входящие в индекс.

Теперь мы вернемся к обсуждению бессхемных коллекций. Давайте, вставим совсем другой документ в коллекцию `unicorns`, как-то так:

	db.unicorns.insert({name: 'Leto', gender: 'm', home: 'Arrakeen', worm: false})

Попробуйте снова выполнить `find`, чтобы перечислить документы. Когда мы узнаем чуть больше, мы обсудим это необычное поведение MongoDB, но, надеюсь, вы уже начинаете понимать, почему традиционная терминология не очень подходит нам.

### Создание селекторов ###
В дополнение к уже исследованным 6 понятиям, есть ещё один практический аспект MongoDB, который важно понять прежде, чем переходить к более сложным вещам: селекторы запросов. Селекторы запросов в MongoDB похожи на `where` в SQL. Они используются для поиска, подсчёта, обновления и удаления документов из коллекций. Селектор есть JSON-объект, в своём простейшем виде выглядящий как `{}` и совпадающий со всеми документами (`null` тоже работает). Если мы хотим найти всех единорогов женского пола, мы можем использовать `{gender: 'f'}`.

Прежде, чем окончательно зарыться в селекторы, давайте подготовим немного данных, с которыми нам предстоит возиться. Для начала удалите все, что мы уже насоздавали в коллекции `unicorns` с помощью `db.unicorns.remove()` (поскольку мы не передали никакого селектора, этот вызов уничтожит все документы). Теперь выполните следующие insert-ы, чтобы ввести данные для упражнений (копирование и вставка поможет):

	db.unicorns.insert({name: 'Horny', dob: new Date(1992,2,13,7,47), loves: ['carrot','papaya'], weight: 600, gender: 'm', vampires: 63});
	db.unicorns.insert({name: 'Aurora', dob: new Date(1991, 0, 24, 13, 0), loves: ['carrot', 'grape'], weight: 450, gender: 'f', vampires: 43});
	db.unicorns.insert({name: 'Unicrom', dob: new Date(1973, 1, 9, 22, 10), loves: ['energon', 'redbull'], weight: 984, gender: 'm', vampires: 182});
	db.unicorns.insert({name: 'Roooooodles', dob: new Date(1979, 7, 18, 18, 44), loves: ['apple'], weight: 575, gender: 'm', vampires: 99});
	db.unicorns.insert({name: 'Solnara', dob: new Date(1985, 6, 4, 2, 1), loves:['apple', 'carrot', 'chocolate'], weight:550, gender:'f', vampires:80});
	db.unicorns.insert({name:'Ayna', dob: new Date(1998, 2, 7, 8, 30), loves: ['strawberry', 'lemon'], weight: 733, gender: 'f', vampires: 40});
	db.unicorns.insert({name:'Kenny', dob: new Date(1997, 6, 1, 10, 42), loves: ['grape', 'lemon'], weight: 690,  gender: 'm', vampires: 39});
	db.unicorns.insert({name: 'Raleigh', dob: new Date(2005, 4, 3, 0, 57), loves: ['apple', 'sugar'], weight: 421, gender: 'm', vampires: 2});
	db.unicorns.insert({name: 'Leia', dob: new Date(2001, 9, 8, 14, 53), loves: ['apple', 'watermelon'], weight: 601, gender: 'f', vampires: 33});
	db.unicorns.insert({name: 'Pilot', dob: new Date(1997, 2, 1, 5, 3), loves: ['apple', 'watermelon'], weight: 650, gender: 'm', vampires: 54});
	db.unicorns.insert({name: 'Nimue', dob: new Date(1999, 11, 20, 16, 15), loves: ['grape', 'carrot'], weight: 540, gender: 'f'});
	db.unicorns.insert({name: 'Dunx', dob: new Date(1976, 6, 18, 18, 18), loves: ['grape', 'watermelon'], weight: 704, gender: 'm', vampires: 165});

Теперь у нас есть данные, и мы можем начать создавать селекторы. `{field: value}` предназначен для поиска документов, где значение поля `field` совпадает с `value`. `{field1: value1, field2: value2}` - это как бы `and`. Операторы `$lt`, `$lte`, `$gt`, `$gte` и `$ne` - это «меньше», «меньше или равно», «больше», «больше или равно», «не равно» соответственно. Например, чтобы найти всех самцов-единорогов, весящих более 700 фунтов, мы можем выполнить:

	db.unicorns.find({gender: 'm', weight: {$gt: 700}})

или (не совсем то же самое, но для демонстрации подойдёт):

	db.unicorns.find({gender: {$ne: 'f'}, weight: {$gte: 701}})

Оператор `$exists` для поиска существующего или несуществующего поля:

	db.unicorns.find({vampires: {$exists: false}})

Должно вернуть один документ. Если мы хотим объединять условия по ИЛИ, а не по И, мы используем оператор `$or`, присваивая ему массив значений, которые мы хотим объединить:

	db.unicorns.find({gender: 'f', $or: [{loves: 'apple'}, {loves: 'orange'}, {weight: {$lt: 500}}]})

Это должно вернуть всех самок единорогов, которые либо любят яблоки, либо апельсины, либо весят менее 500 фунтов.

В примере выше есть еще один примечательный момент. Возможно, вы уже заметили, что поле `loves` - это массив. MongoDB считает массивы первоклассными объектами. Это невероятно удобная штука. Однажды начав ею пользоваться, вы будете удивляться, как раньше вы могли жить без неё. Ещё интереснее то, насколько легка выборка значений на основе массивов: `{loves: 'watermelon'}` вернёт все документы, где `watermelon` есть среди значений `loves`.

На самом деле, операторов много больше, чем мы тут обсудили. Самый гибкий из них - это `$where`, который позволяет передать JavaScript-код, выполняемый на сервере. Все операторы описаны на странице [Advanced Queries](http://www.mongodb.org/display/DOCS/Advanced+Queries#AdvancedQueries) на сайте MongoDB. Мы же рассмотрели лишь основы, необходимые для старта. Но одновременно это и самые востребованные операторы.

Мы видели, как селекторы могут использоваться в команде `find`. Точно так же они могут использоваться с `remove`, которую мы уже видели, `count`, которую мы не рассматривали, но вы, возможно, уже заметили, и `update`, с которой мы вплотную познакомимся чуть позже.

`ObjectId`, который MongoDB генерирует для наших `_id`, можно выбрать с помощью:

	db.unicorns.find({_id: ObjectId("TheObjectId")})

### В этой главе ###

Мы не рассматривали ещё команду `update` и пропустили несколько интересных фишек с `find`. Однако мы установили и запустили MongoDB, коротко познакомились с командами `insert` и `remove` (на самом деле, нам про них уже почти всё известно). Мы рассмотрели команду `find` и увидели, как работают селекторы в MongoDB. Мы неплохо начали и обзавелись неплохой основой для наших будущих исследований. Хотите - верьте, хотите - нет, но вы уже знаете большую часть того, что вам нужно знать о MongoDB - её действительно легко изучить и просто использовать. Я настоятельно советую вам поиграть с вашей базой данных перед тем, как двинуться дальше. Вставьте разных документов, возможно - в другие коллекции, и познакомьтесь поближе с различными селекторами. Используйте `find`, `count` и `remove`. Через некоторое время вещи, которые казались странными и непонятными, уложатся в картинку.

\clearpage

## Глава 2 - Обновление ##
В первой главе мы познакомились с тремя из четырёх CRUD-операций (create, read, update и delete). Эта глава посвящена оставшейся - `update`. У операции `update` есть несколько неожиданных особенностей, поэтому ей и посвщена целая глава.

### Обновление: Замена против $set ###
В своей простейшей форме `update` принимает два аргумента: селектор (where) для нужных документов и какое поле нужно обновить. Если Roooooodles немного набрал вес, мы выполним:

	db.unicorns.update({name: 'Roooooodles'}, {weight: 590})

(если вы играли с коллекцией `unicorns` и она уже не содержит нужных данных, просто снесите из неё все записи и выполните заново код из первой главы).

В реальном коде вы, возможно, использовали бы `_id` для выбора полей, но поскольку я не знаю, какие `_id` сгенерировала для вас MongoDB, мы будем использовать `name`. Давайте же посмотрим на обновлённую запись:

	db.unicorns.find({name: 'Roooooodles'})

И вот вам сразу первый сюрприз от `update`. Ничего не нашлось, потому что второй параметр **заменил** исходный документ. Другими словами, `update` нашла документ по полю `name` и с чистой совестью заменила его целиком новым документом из второго параметра. Да, это не похоже на поведение `update` из SQL. В некоторых ситуациях это может быть полезным. Однако если вы хотите лишь изменить значение одного или нескольких полей, вам нужно использовать модификатор `$set`:

	db.unicorns.update({weight: 590}, {$set: {name: 'Roooooodles', dob: new Date(1979, 7, 18, 18, 44), loves: ['apple'], gender: 'm', vampires: 99}})

Это вернет потерянным полям прежние значениея. А поскольку мы не указали `weight`, оно затронуто не будет. Теперь выполним:

	db.unicorns.find({name: 'Roooooodles'})

Теперь мы получим то, что ожидали. Таким образом, правильный способ обновления веса выглядит так:

	db.unicorns.update({name: 'Roooooodles'}, {$set: {weight: 590}})

### Модификаторы update ###
В довесок к `$set`, у нас есть еще несколько модификаторов для разных интересных вещей. Эти модификаторы работают с полями, так что весь документ они не стирают. Например, модификатор `$inc` предназначен для изменения значения поля на какое-либо положительное или отрицательное число. Например, если Pilot-у ошибочно засчитали пару убитых вампиров, мы можем исправить это:

	db.unicorns.update({name: 'Pilot'}, {$inc: {vampires: -2}})

Если Aurora вдруг стала сладкоежкой, мы можем добавить значение в её список `loves` с помощью `$push`:

	db.unicorns.update({name: 'Aurora'}, {$push: {loves: 'sugar'}})

Раздел [Updating](http://www.mongodb.org/display/DOCS/Updating) сайта MongoDB содержит больше информации об этих и других модификаторах

### Upsert-ы ###
Один из самых приятных сюрпризов `update` - это поддержка т.н. `upserts`. Это обновление документа если он существует или вставка нового в противном случае. Upsert-ы удобным в некоторых ситуациях, и вы это непременно заметите. Чтобы использовать эту фишку, нужно лишь добавить третьим параметром `true`.

Житейский пример - счётчик посещений на сайте. Если мы хотим хранить количество посещений, нам нужно посмотреть, есть ли уже запись для нужной странички, и решить, одновить её или создать новую. Без третьего параметра (или если он установлен в `false`), следующий код не сделает ничего полезного:

	db.hits.update({page: 'unicorns'}, {$inc: {hits: 1}});
	db.hits.find();

Однако, с использованием upsert-ов, результат будет иным:

	db.hits.update({page: 'unicorns'}, {$inc: {hits: 1}}, true);
	db.hits.find();

Поскольку до сих пор не существовало документа, у которого `page` было бы равно `unicorns`, будет создан новый. Если мы выполним то же самое ещё раз, `hits` у существующего документа увеличится до 2.

	db.hits.update({page: 'unicorns'}, {$inc: {hits: 1}}, true);
	db.hits.find();

### Множественные обновления ###
И последний сюрприз, приготовленный нам `update`, заключается в том, что по умолчанию обновляется только один документ. Для предыдущих примеров это выглядело логичным. Однако, если вы выполните что-то в духе:

	db.unicorns.update({}, {$set: {vaccinated: true }});
	db.unicorns.find({vaccinated: true});

Вы, вероятно, ожидаете увидеть всех ваших драгоценных единорогов привитыми. На самом деле, для этого нужно установить в `true` четвертый параметр:
 
	db.unicorns.update({}, {$set: {vaccinated: true }}, false, true);
	db.unicorns.find({vaccinated: true});

### В этой главе ###
Эта глава завершает наше знакомство с CRUD-операциями, которые можно выполнять с коллекциями. Мы поближе познакомились с `update` и рассмотрели три интересных возможности. Во-первых, в отличие от обновлений в SQL, `update` в MongoDB заменяет исходный документ. Из-за этого модификатор `$set` оказывается оень полезным. Во-вторых, `update` дает нам возможность использовать upsert-ы, что особенно удобно вместе с модификатором `$inc`. И, наконец, по умолчанию `update` обновляет только первый из найденных документов.

Do remember that we are looking at MongoDB from the point of view of its shell. The driver and library you use could alter these default behaviors or expose a different API. For example, the Ruby driver merges the last two parameters into a single hash: `{:upsert => false, :multi => false}`.

Не забывайте, что сейчас мы рассматриваем MongoDB с точки зрения работы через оболочку. Используемые вами драйверы и библиотеки могут иметь другие умолчания или даже предоставлять иные API. Например, дрыйвер для Ruby объединяет последние два параметра в хэш: `{:upsert => false, :multi => false}`.

\clearpage

## Глава 3 - Поиск документов ##
В первой главе мы уже кратко взглянули на команду `find`. Однако, её возможности не ограничиваются селекторами. Мы уже упоминали, что результатом работы `find` является курсор. Давайте же посмотрим более детально, что к чему.

### Выбор полей ###
Прежде, чем вплотную заняться курсорами, вам следует знать, что `find` принимает второй аргумент. Например, мы можем найти только имена всех единорогов:

	db.unicorns.find(null, {name: 1});

По умолчанию, в ответе всегда будет поле `_id`. Но мы можем явно исключить его, указав `{name:1, _id: 0}`.

Кроме поля `_id` смешивать включение и исключение других полей нельзя. Если вы думали об этом, то это важно. Вам следует явно либо выбирать, либо исключать поля.

### Сортировка ###
Я уже неоднократно упоминал, что `find` возвращает курсор, реальное выполнение которого откладывается до победного. Однако, как вы, несомненно заметили, работая с оболочкой, `find` выполняется сразу же. Такое поведение характерно только для оболочки. Истинное поведение курсоров можно увидеть, взглянув на методы, которые можно сцепить с `find`. Первый из них - это `sort`. Он работает подобно выбору полей из предыдущего раздела. Мы указываем поля, по которым сортировать, и 1 для сортировки по возрастанию либо -1 - по убыванию. Например:

	//heaviest unicorns first
	db.unicorns.find().sort({weight: -1})
	
	//by vampire name then vampire kills:
	db.unicorns.find().sort({name: 1, vampires: -1})

Как и реляционные базы данных, MongoDB может использовать индексы при сортировке. С индексами мы познакомимся чуть позже. Однако, важно знать, что MongoDB ограничивает размер сортировки без индекса. Таким образом, при попытке отсортировать большую выборку без индекса, мы получим ошибку. Некоторые считают это ограничением. По правде говоря, я бы хотел, чтобы у всех СУБД была возможность запрещать выполнение неоптимизированных запросов (я не пытаюсь превратить каждый недостаток MongoDB в достоинство, но я достаточно насмотрелся на плохо оптимизированные БД и искренне мечтаю, чтобы в них была какая-либо строгость).

### Разбиение на страницы ###
Разбиение результата на страницы выполняется с помощью методов `limit` и `skip` курсора. Чтобы выбрать второго и третьего по весу единорога, сделаем:

	db.unicorns.find().sort({weight: -1}).limit(2).skip(1)

Использование `limit` в связке с `sort` - хороший способ избежать проблем при сортировке по неиндексированным полям

### Подсчёт ###
Оболочка позвлоляет выполнить `count` прямо на коллекции, как-то так:

	db.unicorns.count({vampires: {$gt: 50}})

В реальности же `count` - это метод курсора, в оболочку же просто встроен костыль для этого. Драйверы, не имеющие такой плюшки, требуют такого подхода (в оболочке тоже работает):

	db.unicorns.find({vampires: {$gt: 50}}).count()

### В этой главе ###
Использование `find` и курсоров - это явное преимущество. Есть еще несколько дополнительных команд, которые мы либо рассмотрим в дальнейших главах, либо которые предназначены для специфичных задач. Сейчас же вы уже должны достаточно комфортно чувствовать себя в оболочке mongo и понимать основы MongoDB/

\clearpage

## Chapter 4 - Data Modeling ##
Let's shift gears and have a more abstract conversation about MongoDB. Explaining a few new terms and some new syntax is a trivial task. Having a conversation about modeling with a new paradigm isn't as easy. The truth is that most of us are still finding out what works and what doesn't when it comes to modeling with these new technologies. It's a conversation we can start having, but ultimately you'll have to practice and learn on real code.

Compared to most NoSQL solutions, document-oriented databases are probably the least different, compared to relational databases, when it comes to modeling. The differences which exist are subtle but that doesn't mean they aren't important. 

### No Joins ###
The first and most fundamental difference that you'll need to get comfortable with is MongoDB's lack of joins. I don't know the specific reason why some type of join syntax isn't supported in MongoDB, but I do know that joins are generally seen as non-scalable. That is, once you start to horizontally split your data, you end up performing your joins on the client (the application server) anyways. Regardless of the reasons, the fact remains that data *is* relational, and MongoDB doesn't support joins.

Without knowing anything else, to live in a join-less world, we have to do joins ourselves within our application's code. Essentially we need to issue a second query to `find` the relevant data. Setting our data up isn't any different than declaring a foreign key in a relational database. Let's give a little less focus to our beautiful `unicorns` and a bit more time to our `employees`. The first thing we'll do is create an employee (I'm providing an explicit `_id` so that we can build coherent examples)

	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d730"), name: 'Leto'})

Now let's add a couple employees and set their manager as `Leto`:

	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d731"), name: 'Duncan', manager: ObjectId("4d85c7039ab0fd70a117d730")});
	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d732"), name: 'Moneo', manager: ObjectId("4d85c7039ab0fd70a117d730")});


(It's worth repeating that the `_id` can be any unique value. Since you'd likely use an `ObjectId` in real life, we'll use them here as well.)

Of course, to find all of Leto's employees, one simply executes:

	db.employees.find({manager: ObjectId("4d85c7039ab0fd70a117d730")})

There's nothing magical here. In the worst cases, most of the time, the lack of join will merely require an extra query (likely indexed).

#### Arrays and Embedded Documents ####
Just because MongoDB doesn't have joins doesn't mean it doesn't have a few tricks up its sleeve. Remember when we quickly saw that MongoDB supports arrays as first class objects of a document? It turns out that this is incredibly handy when dealing with many-to-one or many-to-many relationships. As a simple example, if an employee could have two managers, we could simply store these in an array:

	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d733"), name: 'Siona', manager: [ObjectId("4d85c7039ab0fd70a117d730"), ObjectId("4d85c7039ab0fd70a117d732")] })

Of particular interest is that, for some documents, `manager` can be a scalar value, while for others it can be an array. Our original `find` query will work for both:

	db.employees.find({manager: ObjectId("4d85c7039ab0fd70a117d730")})

You'll quickly find that arrays of values are much more convenient to deal with than many-to-many join-tables.

Besides arrays, MongoDB also supports embedded documents. Go ahead and try inserting a document with a nested document, such as:

	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d734"), name: 'Ghanima', family: {mother: 'Chani', father: 'Paul', brother: ObjectId("4d85c7039ab0fd70a117d730")}})

In case you are wondering, embedded documents can be queried using a dot-notation:

	db.employees.find({'family.mother': 'Chani'})

We'll briefly talk about where embedded documents fit and how you should use them.

#### DBRef ####
MongoDB supports something known as `DBRef` which is a convention many drivers support. When a driver encounters a `DBRef` it can automatically pull the referenced document. A `DBRef` includes the collection and id of the referenced document. It generally serves a pretty specific purpose: when documents from the same collection might reference documents from a different collection from each other. That is, the `DBRef` for document1 might point to a document in `managers` whereas the `DBRef` for document2 might point to a document in `employees`.


#### Denormalization ####
Yet another alternative to using joins is to denormalize your data. Historically, denormalization was reserved for performance-sensitive code, or when data should be snapshotted (like in an audit log). However, with the ever-growing popularity of NoSQL, many of which don't have joins, denormalization as part of normal modeling is becoming increasingly common. This doesn't mean you should duplicate every piece of information in every document. However, rather than letting fear of duplicate data drive your design decisions, consider modeling your data based on what information belongs to what document.

For example, say you are writing a forum application. The traditional way to associate a specific `user` with a `post` is via a `userid` column within `posts`. With such a model, you can't display `posts` without retrieving (joining to) `users`. A possible alternative is simply to store the `name` as well as the `userid` with each `post`. You could even do so with an embedded document, like `user: {id: ObjectId('Something'), name: 'Leto'}`. Yes, if you let users change their name, you'll have to update each document (which is 1 extra query). 

Adjusting to this kind of approach won't come easy to some. In a lot of cases it won't even make sense to do this. Don't be afraid to experiment with this approach though. It's not only suitable in some circumstances, but it can also be the right way to do it.

#### Which Should You Choose? ####
Arrays of ids are always a useful strategy when dealing with one-to-many or many-to-many scenarios. It's probably safe to say that `DBRef` aren't use very often, though you can certainly experiment and play with them. That generally leaves new developers unsure about using embedded documents versus doing manual referencing.

First, you should know that an individual document is currently limited to 4 megabytes in size. Knowing that documents have a size limit, though quite generous, gives you some idea of how they are intended to be used. At this point, it seems like most developers lean heavily on manual references for most of their relationships. Embedded documents are frequently leveraged, but mostly for small pieces of data which we want to always pull with the parent document. A real world example I've used is to store an `accounts` document with each user, something like:

	db.users.insert({name: 'leto', email: 'leto@dune.gov', account: {allowed_gholas: 5, spice_ration: 10}})

That doesn't mean you should underestimate the power of embedded documents or write them off as something of minor utility. Having your data model map directly to your objects makes things a lot simpler and often does remove the need to join. This is especially true when you consider that MongoDB lets you query and index fields of an embedded document. 

### Few or Many Collections ###
Given that collections don't enforce any schema, it's entirely possible to build a system using a single collection with a mismatch of documents.  From what I've seen, most MongoDB systems are laid out similarly to what you'd find in a relational system. In other words, if it would be a table in a relational database, it'll likely be a collection in MongoDB (many-to-many join tables being an important exception).

The conversation gets even more interesting when you consider embedded documents. The example that frequently comes up is a blog. Should you have a `posts` collection and a `comments` collection, or should each `post` have an array of `comments` embedded within it. Setting aside the 4MB limit for the time being (all of Hamlet is less than 200KB, just how popular is your blog?), most developers still prefer to separate things out. It's simply cleaner and more explicit.

There's no hard rule (well, aside from 4MB). Play with different approaches and you'll get a sense of what does and does not feel right. 

### In This Chapter ###
Our goal in this chapter was to provide some helpful guidelines for modeling your data in MongoDB. A starting point if you will. Modeling in a document-oriented system is different, but not too different than a relational world. You have a bit more flexibility and one constraint, but for a new system, things tend to fit quite nicely. The only way you can go wrong is by not trying.

\clearpage

## Chapter 5 - When To Use MongoDB ##
By now you should have a good enough understanding of MongoDB to have a feel for where and how it might fit into your existing system. There are enough new and competing storage technologies that it's easy to get overwhelmed by all of the choices. 

For me, the most important lesson, which has nothing to do with MongoDB, is that you no longer have to rely on a single solution for dealing with your data. No doubt, a single solution has obvious advantages and for a lot projects, possibly even most, a single solution is the sensible approach. The idea isn't that you must use different technologies, but rather that you can. Only you know whether the benefits of introducing a new solution outweigh the costs.

With that said, I'm hopeful that what you've seen so far has made you see MongoDB as a general solution. It's been mentioned a couple times that document-oriented databases share a lot in common with relational databases. Therefore, rather than tiptoeing around it, let's simply state that MongoDB should be seen as a direct alternative to relational databases. Where one might see Lucene as enhancing a relational database with full text indexing, or Redis as a persistent key-value store, MongoDB is a central repository for your data.

Notice that I didn't call MongoDB a *replacement* for relational databases, but rather an *alternative*. It's a tool that can do what a lot of other tools can do. Some of it MongoDB does better, some of it MongoDB does worse. Let's dissect things a little further.

### Schema-less ###
An oft-touted benefit of document-oriented database is that they are schema-less. This makes them much more flexible than traditional database tables. I agree that schema-less is a nice feature, but not for the main reason most people mention.

People talk about schema-less as though you'll suddenly start storing a crazy mismatch of data. There are domains and data sets which can really be a pain to model using relational databases, but I see those as edge cases. Schema-less is cool, but most of your data is going to be highly structured. It's true that having an occasional mismatch can be handy, especially when you introduce new features, but in reality it's nothing a nullable column probably wouldn't solve just as well.

For me, the real benefit of schema-less design is the lack of setup and the reduced friction with OOP. This is particularly true when you're working with a static language. I've worked with MongoDB in both C# and Ruby, and the difference is striking. Ruby's dynamism and its popular ActiveRecord implementations already reduce much of the object-relational impedance mismatch. That isn't to say MongoDB isn't a good match for Ruby, it really is. Rather, I think most Ruby developers would see MongoDB as an incremental improvement, whereas C# or Java developers would see a fundamental shift in how they interact with their data. 

Think about it from the perspective of a driver developer. You want to save an object? Serialize it to JSON (technically BSON, but close enough) and send it to MongoDB. There is no property mapping or type mapping. This straightforwardness definitely flows to you, the end developer.

### Writes ###
One area where MongoDB can fit a specialized role is in logging. There are two aspects of MongoDB which make writes quite fast. First, you can send a write command and have it return immediately without waiting for it to actually write. Secondly, with the introduction of journaling in 1.8, and enhancements made in 2.0, you can control the write behavior with respect to data durability. These settings, in addition to specifying how many servers should get your data before being considered successful, are configurable per-write, giving you a great level of control over write performance and data durability.

In addition to these performance factors, log data is one of those data sets which can often take advantage of schema-less collections. Finally, MongoDB has something called a [capped collection](http://www.mongodb.org/display/DOCS/Capped+Collections). So far, all of the implicitly created collections we've created are just normal collections. We can create a capped collection by using the `db.createCollection` command and flagging it as capped:

	//limit our capped collection to 1 megabyte
	db.createCollection('logs', {capped: true, size: 1048576})

When our capped collection reaches its 1MB limit, old documents are automatically purged. A limit on the number of documents, rather than the size, can be set using `max`. Capped collections have some interesting properties. For example, you can update a document but it can't grow in size. Also, the insertion order is preserved, so you don't need to add an extra index to get proper time-based sorting.

This is a good place to point out that if you want to know whether your write encountered any errors (as opposed to the default fire-and-forget), you simply issue a follow-up command: `db.getLastError()`. Most drivers encapsulate this as a *safe write*, say by specifying `{:safe => true}` as a second parameter to `insert`.

### Durability ###
Prior to version 1.8, MongoDB didn't have single-server durability. That is, a server crash would likely result in lost data. The solution had always been to run MongoDB in a multi-server setup (MongoDB supports replication). One of the major features added to 1.8 was journaling. To enable it add a new line with `journal=true` to the `mongodb.config` file we created when we first setup MongoDB (and restart your server if you want it enabled right away). You probably want journaling enabled (it'll be a default in a future release). Although, in some circumstances the extra throughput you get from disabling journaling might be a risk you are willing to take. (It's worth pointing out that some types of applications can easily afford to lose data).

Durability is only mentioned here because a lot has been made around MongoDB's lack of single-server durability. This'll likely show up in Google searches for some time to come. Information you find about this missing feature is simply out of date.

### Full Text Search ###
True full text search capability is something that'll hopefully come to MongoDB in a future release. With its support for arrays, basic full text search is pretty easy to implement. For something more powerful, you'll need to rely on a solution such as Lucene/Solr. Of course, this is also true of many relational databases.

### Transactions ###
MongoDB doesn't have transactions. It has two alternatives, one which is great but with limited use, and the other that is a cumbersome but flexible. 

The first is its many atomic operations. These are great, so long as they actually address your problem. We already saw some of the simpler ones, like `$inc` and `$set`. There are also commands like `findAndModify` which can update or delete a document and return it atomically.

The second, when atomic operations aren't enough, is to fall back to a two-phase commit. A two-phase commit is to transactions what manual dereferencing is to joins. It's a storage-agnostic solution that you do in code.  Two-phase commits are actually quite popular in the relational world as a way to implement transactions across multiple databases. The MongoDB website [has an example](http://www.mongodb.org/display/DOCS/two-phase+commit) illustrating the most common scenario (a transfer of funds). The general idea is that you store the state of the transaction within the actual document being updated and go through the init-pending-commit/rollback steps manually. 

MongoDB's support for nested documents and schema-less design makes two-phase commits slightly less painful, but it still isn't a great process, especially when you are just getting started with it. 

### Data Processing ###
MongoDB relies on MapReduce for most data processing jobs. It has some [basic aggregation](http://www.mongodb.org/display/DOCS/Aggregation) capabilities, but for anything serious, you'll want to use MapReduce. In the next chapter we'll look at MapReduce in detail. For now you can think of it as a very powerful and different way to `group by` (which is an understatement). One of MapReduce's strengths is that it can be parallelized for working with large sets of data. However, MongoDB's implementation relies on JavaScript which is single-threaded. The point? For processing of large data, you'll likely need to rely on something else, such as Hadoop. Thankfully, since the two systems really do complement each other, there's a [MongoDB adapter for Hadoop](https://github.com/mongodb/mongo-hadoop).

Of course, parallelizing data processing isn't something relational databases excel at either. There are plans for future versions of MongoDB to be better at handling very large sets of data.

### Geospatial ###
A particularly powerful feature of MongoDB is its support for geospatial indexes. This allows you to store x and y coordinates within documents and then find documents that are `$near` a set of coordinates or `$within` a box or circle. This is a feature best explained via some visual aids, so I invite you to try the [5 minute geospatial interactive tutorial](http://tutorial.mongly.com/geo/index), if you want to learn more.

### Tools and Maturity ###
You probably already know the answer to this, but MongoDB is obviously younger than most relational database systems. This is absolutely something you should consider. How much a factor it plays depends on what you are doing and how you are doing it. Nevertheless, an honest assessment simply can't ignore the fact that MongoDB is younger and the available tooling around isn't great (although the tooling around a lot of very mature relational databases is pretty horrible too!). As an example, the lack of support for base-10 floating point numbers will obviously be a concern (though not necessarily a show-stopper) for systems dealing with money.

On the positive side, drivers exist for a great many languages, the protocol is modern and simple, and development is happening at blinding speeds. MongoDB is in production at enough companies that concerns about maturity, while valid, are quickly becoming a thing of the past.

### In This Chapter ###
The message from this chapter is that MongoDB, in most cases, can replace a relational database. It's much simpler and straightforward; it's faster and generally imposes fewer restrictions on application developers. The lack of transactions can be a legitimate and serious concern. However, when people ask *where does MongoDB sit with respect to the new data storage landscape?* the answer is simple: **right in the middle**.

\clearpage

## Chapter 6 - MapReduce ##
MapReduce is an approach to data processing which has two significant benefits over more traditional solutions. The first, and main, reason it was development is performance. In theory, MapReduce can be parallelized, allowing very large sets of data to be processed across many cores/CPUs/machines. As we just mentioned, this isn't something MongoDB is currently able to take advantage of. The second benefit of MapReduce is that you get to write real code to do your processing. Compared to what you'd be able to do with SQL, MapReduce code is infinitely richer and lets you push the envelope further before you need to use a more specialized solution.

MapReduce is a pattern that has grown in popularity, and you can make use of it almost anywhere; C#, Ruby, Java, Python and so on all have implementations. I want to warn you that at first this'll seem very different and complicated. Don't get frustrated, take your time and play with it yourself. This is worth understanding whether you are using MongoDB or not.

### A Mix of Theory and Practice ###
MapReduce is a two-step process. First you map and then you reduce. The mapping step transforms the inputted documents and emits a key=>value pair (the key and/or value can be complex). The reduce gets a key and the array of values emitted for that key and produces the final result. We'll look at each step, and the output of each step.

The example that we'll be using is to generate a report of the number of hits, per day, we get on a resource (say a webpage). This is the *hello world* of MapReduce. For our purposes, we'll rely on a `hits` collection with two fields: `resource` and `date`. Our desired output is a breakdown by `resource`, `year`, `month`, `day` and `count`. 

Given the following data in `hits`:

	resource     date
	index        Jan 20 2010 4:30
	index        Jan 20 2010 5:30
	about        Jan 20 2010 6:00
	index        Jan 20 2010 7:00
	about        Jan 21 2010 8:00
	about        Jan 21 2010 8:30
	index        Jan 21 2010 8:30
	about        Jan 21 2010 9:00
	index        Jan 21 2010 9:30
	index        Jan 22 2010 5:00

We'd expect the following output:

	resource  year   month   day   count
	index     2010   1       20    3
	about     2010   1       20    1
	about     2010   1       21    3
	index     2010   1       21    2
	index     2010   1       22    1

(The nice thing about this type of approach to analytics is that by storing the output, reports are fast to generate and data growth is controlled (per resource that we track, we'll add at most 1 document per day.)

For the time being, focus on understanding the concept. At the end of this chapter, sample data and code will be given for you to try on your own.

The first thing to do is look at the map function. The goal of map is to make it emit a value which can be reduced. It's possible for map to emit 0 or more times. In our case, it'll always emit once (which is common). Imagine map as looping through each document in hits. For each document we want to emit a key with resource, year, month and day, and a simple value of 1:

	function() {
		var key = {
		    resource: this.resource, 
		    year: this.date.getFullYear(), 
		    month: this.date.getMonth(), 
		    day: this.date.getDate()
		};
		emit(key, {count: 1}); 
	}

`this` refers to the current document being inspected. Hopefully what'll help make this clear for you is to see what the output of the mapping step is. Using our above data, the complete output would be:

	{resource: 'index', year: 2010, month: 0, day: 20} => [{count: 1}, {count: 1}, {count:1}]
	{resource: 'about', year: 2010, month: 0, day: 20} => [{count: 1}]
	{resource: 'about', year: 2010, month: 0, day: 21} => [{count: 1}, {count: 1}, {count:1}]
	{resource: 'index', year: 2010, month: 0, day: 21} => [{count: 1}, {count: 1}]
	{resource: 'index', year: 2010, month: 0, day: 22} => [{count: 1}]

Understanding this intermediary step is the key to understanding MapReduce. The values from emit are grouped together, as arrays, by key. .NET and Java developers can think of it as being of type `IDictionary<object, IList<object>>` (.NET) or `HashMap<Object, ArrayList>` (Java).

Let's change our map function in some contrived way:

	function() {
		var key = {resource: this.resource, year: this.date.getFullYear(), month: this.date.getMonth(), day: this.date.getDate()};
		if (this.resource == 'index' && this.date.getHours() == 4) {
			emit(key, {count: 5});
		} else {
			emit(key, {count: 1}); 
		}
	}

The first intermediary output would change to:

	{resource: 'index', year: 2010, month: 0, day: 20} => [{count: 5}, {count: 1}, {count:1}]

Notice how each emit generates a new value which is grouped by our key.

The reduce function takes each of these intermediary results and outputs a final result. Here's what ours looks like:

	function(key, values) {
		var sum = 0;
		values.forEach(function(value) {
			sum += value['count'];
		});
		return {count: sum};
	};

Which would output:

	{resource: 'index', year: 2010, month: 0, day: 20} => {count: 3}
	{resource: 'about', year: 2010, month: 0, day: 20} => {count: 1}
	{resource: 'about', year: 2010, month: 0, day: 21} => {count: 3}
	{resource: 'index', year: 2010, month: 0, day: 21} => {count: 2}
	{resource: 'index', year: 2010, month: 0, day: 22} => {count: 1}

Technically, the output in MongoDB is:

	_id: {resource: 'home', year: 2010, month: 0, day: 20}, value: {count: 3}

Hopefully you've noticed that this is the final result we were after.

If you've really been paying attention, you might be asking yourself *why didn't we simply use `sum = values.length`?* This would seem like an efficient approach when you are essentially summing an array of 1s. The fact is that reduce isn't always called with a full and perfect set of intermediate data. For example, instead of being called with:

	{resource: 'home', year: 2010, month: 0, day: 20} => [{count: 1}, {count: 1}, {count:1}]

Reduce could be called with:

	{resource: 'home', year: 2010, month: 0, day: 20} => [{count: 1}, {count: 1}]
	{resource: 'home', year: 2010, month: 0, day: 20} => [{count: 2}, {count: 1}]

The final output is the same (3), the path taken is simply different. As such, reduce must always be idempotent. That is, calling reduce multiple times should generate the same result as calling it once. 

We aren't going to cover it here but it's common to chain reduce methods when performing more complex analysis. 

### Pure Practical ###
With MongoDB we use the `mapReduce` command on a collection. `mapReduce` takes a map function, a reduce function and an output directive. In our shell we can create and pass a JavaScript function. From most libraries you supply a string of your functions (which is a bit ugly). First though, let's create our simple data set:

	db.hits.insert({resource: 'index', date: new Date(2010, 0, 20, 4, 30)});
	db.hits.insert({resource: 'index', date: new Date(2010, 0, 20, 5, 30)});
	db.hits.insert({resource: 'about', date: new Date(2010, 0, 20, 6, 0)});
	db.hits.insert({resource: 'index', date: new Date(2010, 0, 20, 7, 0)});
	db.hits.insert({resource: 'about', date: new Date(2010, 0, 21, 8, 0)});
	db.hits.insert({resource: 'about', date: new Date(2010, 0, 21, 8, 30)});
	db.hits.insert({resource: 'index', date: new Date(2010, 0, 21, 8, 30)});
	db.hits.insert({resource: 'about', date: new Date(2010, 0, 21, 9, 0)});
	db.hits.insert({resource: 'index', date: new Date(2010, 0, 21, 9, 30)});
	db.hits.insert({resource: 'index', date: new Date(2010, 0, 22, 5, 0)});

Now we can create our map and reduce functions (the MongoDB shell accepts multi-line statements, you'll see *...* after hitting enter to indicate more text is expected):

	var map = function() {
		var key = {resource: this.resource, year: this.date.getFullYear(), month: this.date.getMonth(), day: this.date.getDate()};
		emit(key, {count: 1}); 
	};
	
	var reduce = function(key, values) {
		var sum = 0;
		values.forEach(function(value) {
			sum += value['count'];
		});
		return {count: sum};
	};

Which we can use the `mapReduce` command against our `hits` collection by doing:

	db.hits.mapReduce(map, reduce, {out: {inline:1}})

If you run the above, you should see the desired output. Setting `out` to `inline` means that the output from `mapReduce` is immediately streamed back to us. This is currently limited for results that are 16 megabytes or less. We could instead specify `{out: 'hit_stats'}` and have the results stored in the `hit_stats` collections:

	db.hits.mapReduce(map, reduce, {out: 'hit_stats'});
	db.hit_stats.find();

When you do this, any existing data in `hit_stats` is lost. If we did `{out: {merge: 'hit_stats'}}` existing keys would be replaced with the new values and new keys would be inserted as new documents. Finally, we can `out` using a `reduce` function to handle more advanced cases (such an doing an upsert). 

The third parameter takes additional options, for example we could filter, sort and limit the documents that we want analyzed. We can also supply a `finalize` method to be applied to the results after the `reduce` step.

### In This Chapter ###
This is the first chapter where we covered something truly different. If it made you uncomfortable, remember that you can always use MongoDB's other [aggregation capabilities](http://www.mongodb.org/display/DOCS/Aggregation) for simpler scenarios. Ultimately though, MapReduce is one of MongoDB's most compelling features. The key to really understanding how to write your map and reduce functions is to visualize and understand the way your intermediary data will look coming out of `map` and heading into `reduce`.

\clearpage

## Chapter 7 - Performance and Tools ##
In this last chapter, we look at a few performance topics as well as some of the tools available to MongoDB developers. We won't dive deeply into either topic, but we will examine the most import aspects of each.

### Indexes ###
At the very beginning we saw the special `system.indexes` collection which contains information on all the indexes in our database. Indexes in MongoDB work a lot like indexes in a relational database: they help improve query and sorting performance. Indexes are created via `ensureIndex`:

	db.unicorns.ensureIndex({name: 1});

And dropped via `dropIndex`:

	db.unicorns.dropIndex({name: 1});

A unique index can be created by supplying a second parameter and setting `unique` to `true`:

	db.unicorns.ensureIndex({name: 1}, {unique: true});

Indexes can be created on embedded fields (again, using the dot-notation) and on array fields. We can also create compound indexes:

	db.unicorns.ensureIndex({name: 1, vampires: -1});

The order of your index (1 for ascending, -1 for descending) doesn't matter for a single key index, but it can have an impact for compound indexes when you are sorting or using a range condition.

The [indexes page](http://www.mongodb.org/display/DOCS/Indexes) has additional information on indexes.

### Explain ###
To see whether or not your queries are using an index, you can use the `explain` method on a cursor:

	db.unicorns.find().explain()

The output tells us that a `BasicCursor` was used (which means non-indexed), 12 objects were scanned, how long it took, what index, if any was used as well as a few other pieces of useful information.

If we change our query to use an index, we'll see that a `BtreeCursor` was used, as well as the index used to fulfill the request:

	db.unicorns.find({name: 'Pilot'}).explain()

### Fire And Forget Writes ###
We previously mentioned that, by default, writes in MongoDB are fire-and-forget. This can result in some nice performance gains at the risk of losing data during a crash. An interesting side effect of this type of write is that an error is not returned when an insert/update violates a unique constraint. In order to be notified about a failed write, one must call `db.getLastError()` after an insert. Many drivers abstract this detail away and provide a way to do a *safe* write - often via an extra parameter.

Unfortunately, the shell automatically does safe inserts, so we can't easily see this behavior in action.

### Sharding ###
MongoDB supports auto-sharding. Sharding is an approach to scalability which separates your data across multiple servers. A naive implementation might put all of the data for users with a name that starts with A-M on server 1 and the rest on server 2. Thankfully, MongoDB's sharding capabilities far exceed such a simple algorithm. Sharding is a topic well beyond the scope of this book, but you should know that it exists and that you should consider it should your needs grow beyond a single server.

### Replication ###
MongoDB replication works similarly to how relational database replication works. Writes are sent to a single server, the master, which then synchronizes itself to one or more other servers, the slaves. You can control whether reads can happen on slaves or not, which can help distribute your load at the risk of reading slightly stale data. If the master goes down, a slave can be promoted to act as the new master. Again, MongoDB replication is outside the scope of this book.

 While replication can improve performance (by distributing reads), its main purpose is to increase reliability. Combining replication with sharding is a common approach. For example, each shard could be made up of a master and a slave. (Technically you'll also need an arbiter to help break a tie should two slaves try to become masters. But an arbiter requires very few resources and can be used for multiple shards.)

### Stats ###
You can obtain statistics on a database by typing `db.stats()`. Most of the information deals with the size of your database. You can also get statistics on a collection, say `unicorns`, by typing `db.unicorns.stats()`. Again, most of this information relates to the size of your collection.

### Web Interface ###
Included in the information displayed on MongoDB's startup was a link to a web-based administrative tool (you might still be able to see if if you scroll your command/terminal window up to the point where you started `mongod`). You can access this by pointing your browser to <http://localhost:28017/>. To get the most out of it, you'll want to add `rest=true` to your config and restart the `mongod` process. The web interface gives you a lot of insight into the current state of your server.

### Profiler ###
You can enable the MongoDB profiler by executing:

	db.setProfilingLevel(2);

With it enabled, we can run a command:

	db.unicorns.find({weight: {$gt: 600}});

And then examine the profiler:

	db.system.profile.find()

The output tells us what was run and when, how many documents were scanned, and how much data was returned.

You can disable the profiler by calling `setProfileLevel` again but changing the argument to `0`. Another option is to specify `1` which will only profile queries that take more than 100 milliseconds. Or, you can specify the minimum time, in milliseconds, with a second parameter:

	//profile anything that takes more than 1 second
	db.setProfilingLevel(1, 1000);

### Backups and Restore ###
Within the MongoDB `bin` folder is a `mongodump` executable. Simply executing `mongodump` will connect to localhost and backup all of your databases to a `dump` subfolder. You can type `mongodump --help` to see additional options. Common options are `--db DBNAME` to back up a specific database and `--collection COLLECTIONAME` to back up a specific collection. You can then use the `mongorestore` executable, located in the same `bin` folder, to restore a previously made backup. Again, the `--db` and `--collection` can be specified to restore a specific database and/or collection. 

For example, to back up our `learn` collection to a `backup` folder, we'd execute (this is its own executable which you run in a command/terminal window, not within the mongo shell itself):

	mongodump --db learn --out backup

To restore only the `unicorns` collection, we could then do:

	mongorestore --collection unicorns backup/learn/unicorns.bson

It's worth pointing out that `mongoexport` and `mongoimport` are two other executables which can be used to export and import data from JSON or CSV. For example, we can get a JSON output by doing:

	mongoexport --db learn -collection unicorns

And a CSV output by doing:

	mongoexport --db learn -collection unicorns --csv -fields name,weight,vampires

Note that `mongoexport` and `mongoimport` cannot always represent your data. Only `mongodump` and `mongorestore` should ever be used for actual backups.

### In This Chapter ###
In this chapter we looked a various commands, tools and performance details of using MongoDB. We haven't touched on everything, but we've looked at the most common ones. Indexing in MongoDB is similar to indexing with relational databases, as are many of the tools. However, with MongoDB, many of these are to the point and simple to use.

\clearpage

## Conclusion ##
You should have enough information to start using MongoDB in a real project. There's more to MongoDB than what we've covered, but your next priority should be putting together what we've learned, and getting familiar with the driver you'll be using. The [MongoDB website](http://www.mongodb.com/) has a lot of useful information. The official [MongoDB user group](http://groups.google.com/group/mongodb-user) is a great place to ask questions.

NoSQL was born not only out of necessity, but also out of an interest to try new approaches. It is an acknowledgement that our field is ever advancing and that if we don't try, and sometimes fail, we can never succeed. This, I think, is a good way to lead our professional lives.
