# Глава 2

## Введение

Параллельное программирование заслужило репутацию как одна из самых сложных областей, с которыми программист может столкнуться. Научные работы и книги предупреждают об опасностях дедлока, лайвлока, гонки условий, неопределенностей, ограничений закона Амдала по масштабируемости и чрезмерных задержек в реальном времени. И эти опасности вполне реальны. Мы, авторы, собрали неисчислимые годы опыта работы с ними: все эмоциональные шрамы, седые волосы и их потери, которые появляется после встречи с такими опасностями.

Однако, новые технологии, которые сложны для использования при появлении, неизбежно становятся проще со временем. Например, в свое время редкое умение водить машину сейчас является обычной вещью во многих странах. Такое большое изменение произошло по двум простым причинам: 

1. Машины стали дешевле и легче доступны. Таким образом, большее количество людей получило возможность научится водить.
2. Машины стали более просты в эксплуатации благодаря автоматическим трансмиссиям, дросселям, стартерам, значительно увеличенной надежности и набору других технологических улучшений.

Это является правдой и для других технологий, включая компьютеры. Теперь не нужно работать с перфокартами для того, чтобы программировать.
Электронные таблицы (spreadsheets) позволяют обывателям получать такие результаты от их компьютеров, получение которых требовало бы работы команды специалистов несколько десятков лет назад. Возможно, наиболее яркий пример - это веб-серфинг и создание контента. С начала 2000 годов с помощью разных социально-сетевых инструментов это могут делать люди без специального обучения и тренировки. Не так давно как в 1968 году такой процесс был далеким исследовательским проектом [Eng68], описываемым в свое время как "приземление летающей тарелки на лужайку перед Белым домом".

Следовательно, если вы желаете спорить, что параллельное программирование останется таким же сложным, как оно воспринимается многими сейчас, то это вы, кто должен приводить доказательства этого тезиса. При этом не стоит забывать о многих исторических контрпримерах в различных областях человеческих достижений. 

### Исторические сложности параллельного программирования

Как следует из названия, это книга исповедует другой подход. Вместо того чтобы жаловаться на сложности параллельного программирования, она изучает их причины и помогает читателю их преодолеть. Как мы увидим дальше, эти сложности разделяются на несколько категорий, включая:

1. Исторически высокую цену и относительную редкость параллельных систем.
2. Отсутствие опыта работы с параллельными системами у обычных исследователей и практиков.
3. Малое количество публично доступного параллельного кода.
4. Отсутствие широко понимаемой инженерной дисциплины параллельного программирования.
5. Высокие накладные расходы на коммуникацию по сравнению с обработкой данных, даже в сильно связанных вычислительных системах с разделяемой памятью.

Многие из этих сложностей уже на пути к преодолению.
 
1. За последние несколько десятков лет благодаря закону Мура стоимость параллельных систем упала с порядка цены на дом до порядка цены на велосипед. Научные работы, говорящие о преимуществах мультиядерных процессоров, были опубликованы в начале 1996 года [OHN+96]. IBM внедрила одновременно многопоточность в передовую линейку процессоров POWER в 2000 году и мультиядерность в 2001. Intel внедрила гиперпоточность в их двухъядерные процессоры в 2005 году. Sun последовала за ними с мультиядерным/мультипоточным процессором Niagara также в конце 2005. Более того, в 2008 году уже было сложно найти однопроцессорную настольную систему, а одноядерные процессоры остались только в нетбуках и встроенных устройствах. К 2012 году даже смартфоны начали выпускаться с несколькими процессорами.

2. Приход дешевых и широкодоступных мультиядерных систем значит, что в свое время редкий опыт параллельного программирования теперь доступен практически каждому исследователю и практику. На самом деле, параллельные системы сейчас по карману даже школьнику и любителю. Мы, следовательно, можем ожидать увеличение открытий и инноваций в областях, окружающих параллельные системы. Эта увеличивающаяся осведомленность через некоторое время сделает однажды ужасно дорогую область параллельного программирования более обычной и дружественной. 

3. В 20 веке большинство крупных систем, которые использовали высоко параллезированное программное обеспечение, были закрытыми тщательно охраняемыми внутренними секретами. На контрасте с этим, 21 век увидел многочисленные проекты параллельного ПО с открытым кодом (следовательно  публично доступных), включая ядро Linux [Tor03c], системы управления базами данных [Pos08, MS08] и системы передач сообщений [The08, UoC08]. Эта книга в основном будет сфокусирована на ядре Linux, но предоставит много материала, подходящего и для прикладных приложений.

4. Даже, несмотря на то что большинство проектов параллельного программирования в 1980-х и в 1990-х были проприетарными, эти проекты дали жизнь сообществу разработчиков: тех кто понимает инженерную дисциплину, необходимую для разработки параллельного кода производственного качества. Одна из главных целей книги - показать эту дисциплину.

5. К сожалению, с пятой проблемой (высокой ценой коммуникации по отношению к обработке данных) все еще борются. К этой проблеме было приковано много внимания с начала нового тысячелетия. К сожалению, согласно Стивену Хокингу конечная скорость света и атомная природа материи, скорее всего, ограничат прогресс в этой области [Gar 07, Moo03]. К счастью, с этой проблемой борются еще с конца 1980 годов, так что вышеупомянутая инженерная дисциплина разработала практичные и эффективные стратегии для ее обхождения. Кроме всего прочего, проектировщики аппаратного обеспечения становятся все более знакомы с этими проблемами, так что, возможно, будущее "железо" будет более дружественным к параллельному программному обеспечению. Смотрите обсуждается в разделе 3.3.

[**Быстрый вопрос 2.1:**](../master/quick-quiz.md#Быстрый-вопрос-21) Ну хватит!! Параллельное программирование было невообразимо сложным многие десятилетия. Вы же, судя по всему, указываете на то, что оно не так сложно. На что вы намекаете?

[**Быстрый вопрос 2.2:**](../master/quick-quiz.md#Быстрый-вопрос-22) Как параллельное программирование вообще может быть таким же легким, как последовательное программирование?

Несмотря на то что параллельное программирование может и не так сложно, как оно преподносится, оно все еще пока сложнее, чем его последовательный аналог. Следовательно, имеет смысл рассмотреть его альтернативы. Однако, невозможно аргументировано рассматривать альтернативы без понимания целей. Эта тема рассматривается в следующем разделе.

## Цели параллельного программирования

Три главные цели параллельного программирования (в дополнение к целям последовательного программирования):

1. Производительность
2. Эффективность
3. Общность

[**Быстрый вопрос 2.3:**](../master/quick-quiz.md#Быстрый-вопрос-23) Серьезно? А что насчет корректности, поддерживаемости, надежности и так далее?

[**Быстрый вопрос 2.4:**](../master/quick-quiz.md#Быстрый-вопрос-24) И если корректность, поддерживаемость и надежность не попали в список, почему попали эффективность и общность?

[**Быстрый вопрос 2.5:**](../master/quick-quiz.md#Быстрый-вопрос-25) Учитывая, что намного сложнее доказать корректность параллельных программ, чем последовательных, опять, не должна ли все-таки корректность быть в списке?

[**Быстрый вопрос 2.6:**](../master/quick-quiz.md#Быстрый-вопрос-26) Как насчет того, чтобы просто весело проводить время?

Каждая из этих целей тщательно разобрана в следующих разделах:

### 2.2.1 Производительность

Производительность - это главная цель большинства усилий, связанных с параллельным программированием. В конце концов, если 
производительность - не забота, почему бы не сделать себе услугу: просто писать последовательный код и быть счастливым? Это будет намного проще и, скорее всего, вы сделаете намного больше вещей быстрее.

[**Быстрый вопрос 2.7:**](../master/quick-quiz.md#Быстрый-вопрос-27) Разве не существует ситуаций, когда параллельное программирование - это не о производительности?

Имейте в виду, что "производительность" толкуется здесь довольно широко, включая как масштабируемость (производительность каждого процессора), так и коэффициент полезного действия (например, производительность на ватт энергии).

Тем не менее фокус производительности сдвинулся с аппаратного обеспечения к параллельному программному обеспечению. Этот сдвиг происходит из-за того, что хотя закон Мура продолжает приносить увеличение плотности транзисторов, он перестал увеличивать производительность для традиционных однопоточных программ. Это можно увидеть на графике 2.1, который показывает, что написание однопоточного кода и простое ожидание догона процессора до нужной производительности через год или два, может уже не быть подходящим вариантом. Учитывая последние тенденции всех главных производителей по отношению к мультиядерным/мультипоточным системам, параллелизм - это выход для тех, кто хочет достичь максимальной производительности от системы.

![График 2.1](../master/clockfreq.png?raw=true)

График 2.1: Тенденция показателя MIPS/тактовая частота для процессоров Intel

Даже так, производительность является более важной, чем масштабируемость, особенно учитывая, что наиболее простой способ достичь линейной масштабируемости - это понизить производительность каждого процессора [Tor01]. Если вам дана 4-процессорная система, что вы предпочтете: программу, которая выполняет 100 транзакций в секунду на одном процессоре, но не масштабируется или программу, которая выполняет 10 транзакций в секунду, но отлично масштабируется? Первый вариант смотрится лучше, однако ответ может изменится, если у вас появится 32-процессорная система. 

Однако, только потому, что у вас есть несколько процессоров, вы не обязаны всех их использовать. Даже учитывая недавние уменьшение цен на мультипроцессорные системы. Ключевая идея в том, что параллельное программирование по своей сути - это оптимизация производительности и, следовательно, все лишь возможная оптимизация из многих доступных. Если ваша программа достаточна быстра в таком виде, в котором она сейчас написана, нет причины оптимизировать ее как путем распараллеливания, так и путем применения потенциальных "классических" последовательных оптимизаций. Кстати, если вы собираетесь применить параллелизм как оптимизацию к последовательной программе, вам надо будет сравнивать параллельные алгоритмы с лучшими последовательными. Это может потребовать некоторого внимания, так как слишком много работ при анализе производительности параллельных алгоритмов игнорируют их последовательные аналоги.

### 2.2.2 Эффективность

[**Быстрый вопрос 2.8:**](../master/quick-quiz.md#Быстрый-вопрос-28) Зачем нужна вся эта болтовня о нетехнических вопросах? И не только о нетехнических вопросах, а и об эффективности всех этих вещей? Кого это волнует?

Эффективность становилась все более важной в последние десятилетия. Для того чтобы увидеть эту тенденцию, вспомните, что цена ранних компьютеров равнялась десяткам миллионов долларов, в то время как средняя зарплата инженера была порядка нескольких десятков тысяч долларов в год. Если выделенная команда из десяти инженеров увеличивала производительность такой машины даже на 10%, то их зарплаты окупались во много раз.

Одной из таких машин был CSIRAC, старейший все еще целый компьютер с хранимой программой в памяти. Он был введен в работу в 1949 году[Mus04, Mel06]. Так как эта машина была построена в дотранизестерную эру, то она состояла из 2000 электронных ламп, работала с тактовой частотой 1 КГц, потребляла 30 кВт энергии и весила более, чем три тонны. Эта машина имела всего 768 слов оперативной памяти и можно без опасения сказать, что она не страдала от тех проблем производительности, с которыми сталкиваются современные масштабные программные проекты.

Сегодня достаточно трудно купить машину с такой маленькой вычислительной мощностью. Возможно, ближайший эквивалент - это 8-битный встраиваемый микропроцессор на базе древнего Z80 [Wik08], но даже старый Z80 имел тактовую частоту процессора, более чем в 1000 раз превышающую CSIRAC. Процессор Z80 имел 8500 тысяч транзисторов и мог быть куплен в 2008 году менее, чем за 2$ US за штуку партиями по тысяче. На контрасте с CSIRAC, цена разработки программного обеспечения может являться всем, чем угодно, но не важным фактором для Z80.

CSIRAC и Z80 - две точки в долговременной тенденции, как мы можем видеть на графике 2.2.

![График 2.2](../master/mipsperbuck.png?raw=true)

График 2.2: MIPS на кристалл для процессоров Intel

Этот график отображает аппроксимацию вычислительной мощности на кристалл за последние три десятилетия и показывает постоянное увеличение этой величины на 4 порядка. Надо учитывать, что приход мультиядерных процессоров сделал возможным продолжение этого увеличения, несмотря на потолок тактовой частоты, с которым столкнулись инженеры в 2003 году.

Одно из неизбежных последствий быстрого уменьшения цен на аппаратное обеспечение, это то, что эффективность программного обеспечения становится все более важной. Теперь недостаточно просто эффективно использовать "железо": вместе с ним необходимо крайне эффективно использовать разработчиков ПО. Это давно уже не новость для последовательного аппаратного обеспечения, но параллельное аппаратное обеспечение стало недорогим только недавно. Именно поэтому высокая эффективность стала критично важной при создании параллельного программного обеспечения.

[**Быстрый вопрос 2.9:**](../master/quick-quiz.md#Быстрый-вопрос-29) Учитывая насколько дешевыми стали параллельные системы, как люди могут позволить платить программистам, работающими с этими системами?

Возможно в свое время единственной целью параллельного программного обеспечения была производительность. Теперь же, однако, эффективность выходит из тени.

### 2.2.3 Общность

Один из способов оправдать высокую цену разработки параллельного программного обеспечения, это достижение максимальной общности.
При всех прочих равных, более общий программный артефакт может быть распространен между большим количеством пользователей, чем менее общий. 

К сожалению, за счет общности часто приходится жертвовать производительностью, эффективностью или тем и другим. Для того чтобы увидеть это, рассмотрим следующие популярные программные среды:

**С/C++ "блокировки плюс потоки"** : Эта категория, которая включает потоки POSIX (pthreads) [Ope97], потоки Windows и другие среды уровня ядра операционной системы, предлагает отличную производительность (по крайней мере в границах одной симметричной мультипроцессорной системы (SMP-системы)) и хорошую общность. Жаль, что только эффективность относительно низка. 

**Java** : Это язык общего назначения и по своей природе мультипоточная программная среда. Он, по широко распространенному мнению, предлагает большую эффективность, чем C или C++ за счет автоматической сборки мусора и большой стандартной библиотеки. Однако его производительность, несмотря на то что она была сильна улучшена в начале 2000-х годов, уступает С и С++.

**MPI** : Этот интерфейс передачи сообщений [MPI08], на котором  работают крупнейшие научные и технические вычислительные кластерами в мире. Он предлагает не имеющие равных производительность и масштабируемость. В теории, MPI является интерфейсом общего назначения, но в большинстве своем он используется для научных и технических вычислений. Его эффективность, по мнению многих, даже ниже, чем у подхода С/C++ "блокировки плюс потоки". 

**OpenMP** : Это набор директив для компилятора, который может быть использован для распараллеливания циклов. Следовательно, он крайне специфичен для этой задачи и она (специфичность) часто ограничивает производительность. Однако, OpenMP намного легче в использовании, чем MPI или С/C++ "блокировки плюс потоки".

**SQL** : Язык структурных запросов [Int92] специфичен для реляционных баз данных. Однако его производительность достаточно хороша, что показано тестами совета по производительности обработки транзакций (TPC benchmark) [Tra01]. Эффективность отлична. Факт, что SQL позволяет людям эффективно использовать большие параллельные системы, несмотря на малые знания - или их отсутствие - о принципах параллельного программирования. 

Нирвана сред параллельного программирования - та, которая предложит производительность мирового уровня, эффективность и общность - просто пока не существует. До тех пор, пока такая нирвана не появится, необходимо будет искать инженерные компромиссы между производительностью, эффективностью и общностью. Один из таких компромиссов показан на графике 2.3, который показывает, как эффективность становится все более важной на верхних уровнях системного стека, в то время как производительность и общность на более низких. 

![График 2.3](../master/ppgrelation.png?raw=true)

График 2.3: Уровни программного обеспечения и производительность, эффективность и общность.

Затраты на высокую цену разработки, понесенные на низких уровнях, обязаны быть распределены на равно большие группы пользователей (здесь важную роль играет общность) и потеря производительности на низких уровнях не может быть легко восстановлена выше по стеку. На верхних уровнях стека может быть всего несколько пользователей специфичного приложения и в этом случае забота об эффективности имеет первостепенное значение. Это объясняет тенденцию к "раздуванию программного обеспечения" выше по стеку: дополнительное аппаратное обеспечение обычно дешевле, чем дополнительные разработчики. Эта книга предназначена для разработчиков, работающих на самых низких уровнях стека, где производительность и общность величины большой важности.

Важно заметить, что компромисс между производительностью и общностью существовал веками во многих областях. Для примера, гвоздомет более эффективен для забивания гвоздей, чем молоток. Но молоток, в отличие от гвоздомета, может быть использован для множества других вещей, кроме как забивания гвоздей. Следовательно, не должны удивлять похожие компромиссы, появляющиеся в сфере параллельных вычислений. Этот компромисс схематично показан на графике 2.4.

![График 2.4](../master/generality.png?raw=true)

График 2.4: Компромисс между эффективностью и общностью.

Здесь пользователи 1, 2, 3 и 4 имеют специфичные задачи, для реализации которых им нужен компьютер. Наиболее эффективный из возможных для пользователя язык или среда  - это тот(та), который(ая) просто делает его работу, не требуя дополнительного программирования, конфигурации или другой настройки.

[**Быстрый вопрос 2.10:**](../master/quick-quiz.md#Быстрый-вопрос-210) Это до смешного недостижимая цель! Почему бы не сфокусироваться на чем-нибудь более достижимом на практике?

К сожалению, система, которая просто делает задачу, нужную пользователю 1, скорее всего, не подойдет для задачи пользователя 2. Другими словами, наиболее эффективные языки и среды предметно-ориентированные и, следовательно, по определению теряют общность.

Другая возможность, это привязать конкретный язык программирования или среду к аппаратному обеспечению (пример: ассемблер, С, С++ или Java) или к некоторой абстракции (пример: Haskell, Prolog или Snobol), как показано на круговой области рядом с центром на графике 2.4. Эти языки могут рассматриваться общими в том смысле, что они одинаково плохо подходят для задач, требуемых пользователям 1, 2, 3 и 4. Другими словами, их общность достигается за счет уменьшенной эффективности по сравнению с предметно-ориентированными языками и средами. Что еще хуже, язык, который привязан к абстракции, скорее всего, страдает от проблем с производительностью и масштрабируемостью до тех пор, пока кто-нибудь не придумает как эффективно отобразить эту абстракцию на реальное аппаратное обеспечение.

После того как мы знаем о трех часто конфликтующих целях параллельного программирования - производительности, эффективности и общности, время попробовать избежать этих конфликтов путем рассмотрения его альтернатив.

## 2.3 Альтернативы параллельному программированию

Для того чтобы тщательно рассмотреть альтернативы параллельному программированию, вы для начала должны решить, какие именно улучшения вы ожидаете от параллелизма. Как мы видели в разделе 2.2, главные цели параллельного программирования - это производительность, эффективность и общность. Так как эта книга предназначена для разработчиков, работающих с производительно-значимым кодом на низких уровнях стека программного обеспечения, остаток этой главы будет сфокусирован в основном на улучшении производительности.

Важно помнить что параллелизм - это всего лишь один из способов улучшить производительность. Другие известные подходы перечислены ниже в порядке возрастания сложности:

1. Запустить несколько экземпляров последовательной программы.
2. Изменить приложение, чтобы оно использовало существующее параллельное программное обеспечение.
3. Применить оптимизации производительности к последовательной программе.

Эти подходы описаны в следующих разделах.

### 2.3.1 Несколько экземпляров последовательного приложения

Запуск нескольких экземпляров последовательного приложение может позволить вам использовать параллельное программирование, на самом деле его не используя. Существует большое количество способов достигнуть этого в зависимости от структуры приложения.

Если ваше приложение анализирует большое количество разных сценариев или независимых наборов данных, один из самых простых и эффективных подходов - создать одну последовательную программу, которая делает одну часть анализа, затем используя любую из доступных сред для выполнения скриптов (например, оболочку bash), запустить несколько экземпляров приложения параллельно. В некоторых случаях этот подход может быть легко расширен на кластер машин.

Этот подход может смотреться как "нечестный", и некоторые называют такие приложения "позорно параллельными". И в самом деле, такой подход имеет несколько потенциальных недостатков, включая увеличивающее потребление памяти, трату циклов процессора на перевычисление общих промежуточных результатов и увеличивающееся количество копируемых данных. Однако, он часто крайне эффективен и позволяет достигнуть увеличения производительности с малыми затратами или вообще без них.

### 2.3.2 Использование существующего параллельного программного обеспечения

В текущее время уже нет недостатка в средах для параллельного программирования, которые предоставляют однопоточную программную среду. Например, реляционные базы данных[Dat82], сервера веб-приложений и среды для выполнения задач типа разделяй-и-властвую (map-reduce). Типичная архитектура системы управления базы данных предоставляет независимую среду для каждого пользователя, который генерирует SQL-запросы. Эти пользовательские запросы запускаются одновременно на общей реляционной базе данных. Клиент отвечает только за взаимодействие с пользователем, а база данных берет на себя полную ответственность за сложные проблемы, окружающие параллелизм и сохраняемость данных.

Выбор этого подхода часто сопряжен с некоторыми потерями производительности по сравнению с аккуратно вручную запрограммированным полностью параллельным приложением. Однако эти потери часто оправданы, учитывая большое уменьшение прикладываемых усилий при разработке приложения.

### 2.3.3 Оптимизация производительности

Вплоть до начала 2000 годов, производительность процессоров увеличивалась каждые 18 месяцев. В таких условиях, часто было более важно создавать новую функциональность, чем выполнять аккуратные оптимизации производительности. Сейчас же, учитывая, что по закону Мура увеличивается "только" плотность транзисторов вместо увеличения как плотности транзисторов, так и производительности отдельных элементов, стоит задуматься о важности оптимизации производительности. В конце концов, новые поколения аппаратного обеспечения больше не приносят значительных улучшений производительности в однопоточной среде. Более того, многие оптимизации могут также требовать дополнительный расход энергии. 

С этой точки зрения, параллельное программирование всего лишь одна из оптимизаций производительности, хотя и становящаяся все более привлекательной с удешевлением и расширением доступности параллельных систем. Однако, не нужно забывать, что ускорение, полученное от распараллеливания, строго ограничено количеством процессоров. В противоположность этому, ускорение от применения классических однопоточных оптимизации программного обеспечения может быть намного больше. Например, замена длинного связанного списка либо на хеш-таблицу или двоичное дерево поиска может улучшить производительность на несколько порядков. Такая сильно оптимизированная однопоточная программа может работать намного быстрее, чем ее неоптимизированный параллельный аналог, делая параллелизацию ненужной. Конечно, сильно оптимизированная параллельная программа будет работать еще лучше, но не нужно забывать про дополнительные силы на разработку такого решения.

Более того, различные программы могут иметь разные "бутылочные горлышки" в производительности. Например, если ваша программа проводит большое количество времени, ожидая данных от диска, использование нескольких процессоров может только увеличить время ожидания. В самом деле, если программа читает один большой файл, лежащий последовательно на вращающемся диске, параллелизация вашей программы может сделать ее медленней из-за дополнительной работы по позиционированию головок. Более мудро оптимизировать доступ к данным, например:
 
* сделать файл был меньше (и следовательно быстрее для чтения);
* разделить файл на части, которые могут быть доступны параллельно с различных дисков;
* закэшировать в основной памяти данные, к которым наиболее часто обращаются;
* уменьшить, если возможно, количество данных, которые нужно прочитать.

[**Быстрый вопрос 2.11:**](../master/quick-quiz.md#Быстрый-вопрос-211)  Какие другие "бутылочные горлышки" могут предотвратить увеличение производительности от добавления процессоров? 

Параллелизм может быть мощной техникой оптимизации, но он не только ни является единственной техникой, но и не подходит во всех ситуациях. Конечно, чем проще распараллелить вашу программу, тем более привлекательной становится параллелизация как возможная оптимизация. В это же время она имеет репутацию сложной дисциплины, что подводит нас к вопросу "Что же делает параллельное программирование таким тяжелым?".

### 2.4 Что делает параллельное программирование тяжелым?

Важно учесть, что сложность параллельного программирования происходит как и из человеческих факторов, так и из технических свойств этой области. Необходимо быть людьми, чтобы иметь возможность указывать параллельным системам что им делать (это и называется программированием). Но параллельное программирование является двусторонней коммуникацией, в которой производительность и масштабируемость программы являются каналом от машины к человеку. Если говорить кратко, человек пишет программу, которая говорит компьютеру, что ему делать и компьютер критикует программу путем ее производительности и масштабируемости. Следовательно, обращение к абстракциям или к математическому анализу часто бывает сильно ограниченными инструментом.

Во времена производственной революции, производительность взаимодействия между человеком и машиной рассчитывалась с помощью работ по изучению человеческого фактора, позже названных "изучение трудовых движений и затрат времени". Хотя в истории было несколько работ по изучению параллельного программирования с учетом человеческого фактора [ENS05, ES05, HCS+05, SS94], эти работы были очень узко специализированы и, следовательно, не могли показать никаких глобальных результатов. Более того, учитывая, что крайние точки обычного диапазона эффективности программистов отличаются более, чем на порядок, нереалистично ожидать достойной работы, способной определить, скажем, 10% разницу в эффективности. Несмотря на то что разницы в несколько порядков, которые такие работы *могут* надежно определить, крайне ценны, большинство впечатляющих улучшений склонны быть длинными сериями улучшений по 10%.

Мы, следовательно, должны выбрать другой подход.

Один из таких подходов - тщательно рассмотреть задачи, с которыми сталкивается параллельное программирование, но которые не являются обязательными для последовательного аналога. Позже мы можем рассчитать как хорошо язык программирования или среда помогает разработчику с этими задачами. Задачи распадаются на 4 категории, как показано на графике 2.5, каждая из которых описана в следующих секциях. 

![График 2.5](../master/four_task_categories.png?raw=true)

График 2.5: Категории задач, требуемых для параллельного программирования

### 2.4.1 Разделение работы

Разделение работы абсолютно необходимо для параллельного выполнения: если существует один большой "кусок" работы, то он может быть выполнен в лучшем случае на одном процессоре в одну единицу времени, что по определению является последовательным процессом. Однако, разделение кода требует большой осторожности. Например, нечетное разделение может выльется в последовательное выполнение, как только маленькие части закончат выполнение [Amd67]. В менее крайних случаях, разделение нагрузки может быть использовано для полной утилизации доступного аппаратного обеспечения и достижении требуемой производительности и масштабируемости.

Хотя разделение и может сильно увеличить производительность и масштабируемость, оно также может увеличить и сложность. Например, разделение может усложнить обработку глобальных ошибок и событий: параллельной программе потребуется поддерживать непростую синхронизацию, для того чтобы безопасно обрабатывать глобальные события. Говоря более обще, каждое разделение требует некоторой коммуникации. В конце концов, если поток не взаимодействует вообще ни с кем, он не имеет никакого эффекта, и, следовательно, нет никакой необходимости в его выполнении. Однако, так как коммуникация вызывает дополнительные накладные расходы, бездумное разделение может вызывать сильные падения производительности.

Даже более того, количество одновременно выполняющихся потоков часто обязано быть контролируемым, так как каждый поток отъедает глобальные ресурсы системы, например, пространство в кэшах процессора. Если слишком большое количество потоков будет выполняться одновременно, то кэши процессоров переполнятся, что выльется в промахи в кэшах, и это, в свою очередь, понизит производительность. С другой стороны, большое количество потоков часто необходимо для нахлеста потоков вычислений и ввода/вывода, что позволяет более полно утилизировать устройства ввода/вывода.

[**Быстрый вопрос 2.12:**](../master/quick-quiz.md#Быстрый-вопрос-212) Кроме размера кэшей процессоров, что еще может ограничивать количество одновременно выполняющихся потоков?

В конце концов, разрешение потокам выполняться одновременно сильно увеличивает количество состояний программы, что может сделать ее сложной для понимания и отладки, ухудшая ее эффективность. При прочих равных, меньшее количество состояний ведет к более привычной структуре и более легкому пониманию программы - хотя это скорее человеческий фактор, чем технически или математически обоснованное заявление. Программы с хорошим параллельным дизайном могут иметь огромное количество состояний, но тем не менее быть простыми для понимания из-за их правильной структуры, в то время как программы с плохим дизайном могут быть абсолютно непонятными, несмотря на относительно небольшое количество состояний. Лучшие дизайны используют "позорный параллелизм", или преобразуют программу таким образом, чтобы она имела "позорно параллельное" решение. В любом случае "позорно параллельный" - это позор богатых. В любом случае хорошие дизайны параллельных программ можно пересчитать на пальцах, поэтому требуется больше исследований для того, чтобы делать общие заявления о количестве состояний и структуре программы.

### 2.4.2 Контроль параллельного доступа

В обычной однопоточной последовательной программе, один поток имеет полный доступ ко всем программным ресурсам. Наиболее часто этими ресурсами являются структуры данных в памяти, но также могут быть процессоры, память (включая кэши), устройства ввода-вывода, ускорители вычислений, файлы и многое другое.

Первая проблема контроля параллельного доступа появляется в случае, когда доступ к ресурсу зависит от его местоположения. Например, во многих средах передачи сообщений доступ к локальным переменным происходит через выражения и присваивания, а вот доступ к удаленным переменным осуществляется уже с помощью совершенно другого синтаксиса (обычно как раз передачей сообщений). POSIX потоки [Ope97], SQL [Int92] и среды с разделенным глобальным адресным пространством (PGAS), такие как Unified Parallel C (UPC) [EGCD03] предлагают неявный доступ к таким переменным, в то время MPI [MPI08] требует явный доступ из-за передачи сообщений.

Другая проблема контроля параллельного доступа заключается в определении того, как потокам координировать доступ к ресурсам. Эта координация может быть произведена с помощью большого количества механизмов синхронизации, которые предлагают параллельные языки и среды: передачу сообщений, блокировки, транзакции, подсчет ссылок, явное разделение времени, разделенные атомарные переменные и разграничение владения данными. Многие традиционные заботы параллельного программирования такие как дедлок, лайвлок и откат транзакции растут из этой координации. Можно было включить сравнение этих механизмов синхронизации, например, блокировок и транзакционной памяти [MMW07], но такая сравнение выходит за рамки этого раздела (смотрите разделы 16.2 и 16.3 для более подробной информации о транзакционной памяти).

### 2.4.3 Разделение ресурсов и репликация

Самые эффективные параллельные алгоритмы и системы используют параллелизм ресурсов таким образом, что обычно мудро начинать параллелизацию путем разделения наиболее частых на запись и репликацией частых на чтение ресурсов. Если исследуемый ресурс - такого типа, он может быть разделены среди компьютерных систем, устройств хранения, NUMA узлов, ядер процессора (или матриц или аппаратных потоков), страниц памяти, кэш-линий, экземпляров примитивов синхронизации или критических секций кода. Например, разделение данных по примитивам блокировок называется "блокировка данных" [BK85].

Разделение ресурсов часто зависит от приложения. Например, приложения, работающие с цифрами, разделяют матрицы по строкам, колонкам или подматрицам, в то время как коммерческие приложения склонны разделять часто записываемые и реплицировать часто читаемые структуры данных. Таким образом, коммерческое приложение может привязать данные для конкретного заказчика всего к нескольким компьютерам в большом кластере. Приложение может как статически разделять данные, так и динамически менять разделение с течением времени.

Разделение ресурсов очень эффективно, но оно может быть крайне непростым для сложных сильно связных структур данных.
 
### 2.4.4 Взаимодействие с аппаратным обеспечением

Взаимодействие с аппаратным обеспечением обычно является областью действия операционной системы, компилятора, библиотек или другой инфраструктуры. Однако, разработчики, работающие c новым функционалом аппаратного обеспечения и новыми компонентами, будут часто вынуждены работать напрямую с таким "железом". Более того, прямой доступ к аппаратному обеспечению может быть нужен при выжимании последних соков производительности из системы. В этом случае разработчику может потребоваться привязать или сконфигурировать приложение к геометрии кэшей, системной топологии или внутреннему протоколу общения целевой системы.

В некоторых случаях аппаратное обеспечение может быть рассмотрено как ресурс, который может быть разделен или контролирован для доступа, как описано в предыдущих разделах.

### 2.4.5 Возможности композиции

Хотя эти четыре возможности являются фундаментальными, хорошие инженерные практики используют их композицию. Например, подход с распараллеливанием данных сначала разделяет их таким образом, чтобы минимизировать необходимость коммуникаций между частями, затем соответственно разделяет код и, наконец, сопоставляет разделенные данные и потоки, максимизируя пропускную способность и в то же время минимизируя коммуникацию между потоками, как показано на графике 2.6. 

![График 2.6](../master/four_task_order.png?raw=true)

График 2.6: Порядок задач параллельного программирования

Разработчик может рассмотреть каждое разделение в отдельности, что сильно уменьшает количество состояний и, в свою очередь, увеличивает эффективность. Несмотря на то что некоторые проблемы не могут быть разделены, ловкие преобразование в формы, разрешающие разделение, иногда могут сильно увеличить как производительность, так и масштабируемость [Met99].

### 2.4.6 Как языки и среды помогают с этими задачами

Хотя многие среды требуют от разработчика вручную работать с этими задачами, существуют проверенные среды, которые приносят значительную автоматизацию. Пример для подражания - реляционные базы данных, многие реализации которых автоматически параллезируют большие одиночные запросы, одновременное выполнение независимых запросов и обновлений.

Эти четыре категории задач обязаны быть решены во всех параллельных программах, но, конечно, это не значит, что разработчик обязан решать их вручную. Мы можем увидеть все большую автоматизацию этих четырех задач с удешевлением и увеличением доступности параллельных систем.

[**Быстрый вопрос 2.13**](../master/quick-quiz.md#Быстрый-вопрос-213) Существуют ли другие препятствия в параллельном программировании?

## 2.5 Обсуждение

Этот раздел дал обзор сложностям, целям и альтернативам параллельному программированию. За этим обзором следовало обсуждение того, что делает параллельное программирование тяжелым. После него было дано описание высокоуровневых подходов для решения сложностей параллельного программирования. Теперь мы готовы перейти к следующей главе, которая погружает нас в актуальные свойства параллельного аппаратного обеспечения, на котором работает наше параллельное программное обеспечение. 
