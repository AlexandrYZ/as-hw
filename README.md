# Домашняя работа по курсу Анализ Систем

Система - Make cats free again (MCF)

## Требования

[US-010] Все коты-тестировщики (клиенты) автоматически попадают в систему. Для них доступен дашборд с заказанными услугами и кнопкой «запросить помощь».
[US-020] При запросе услуги клиенты будут видеть форму, в которой можно описать, что нужно сделать, выбрать тип услуги, увидеть примерную стоимость.
[US-021] Типы услуги задаются в админке менеджерами.
 
[US-030] Каждая выполненная или отменённая задача должна быть оплачена пользователем в полном объёме.
[US-040] Если клиент заплатил больше 10 к условных кото-единиц в сумме, ему даётся скидка в 5%, если больше 20 к — скидка 6%. За каждые 10 к скидка увеличивается на 1%, предел скидки — 12%.
[US-050] Стоимость будет задаваться после подбора воркера под услугу (матчинга). Расчёт стоимости задаётся по секретной формуле, которую пока никто не знает, поэтому для первой версии хватит задать константное значение в 100 условных кото-единиц за любую услугу.
[US-060] Люди, которые придумывали уникальную систему матчинга, используют отличные от всей компании термины: «эталонный образец» (клиент) и «обычный образец» (воркер). Никто не знает, как так вышло, но разработчики алгоритма отказываются переучиваться.
[US-070] Алгоритм матчинга — общий для любых образцов, состоит из набора шагов, по которым рассчитываются рейтинги и другие значения. Система чем-то похожа на map-reduce. Разработчики решили, что они сами будут реализовывать всю логику на любом языке, так как они не хотят делиться алгоритмом. Наша цель — использовать реализованные шаги в нужной нам последовательности, которая иногда может изменяться, при этом необходимо иметь возможность добавлять или редактировать шаги, как нам это необходимо.
[US-071] Для корректной работы матчинга необходима информация об обычных образцах (включая их сильные и слабые стороны) и результаты прошлых заказов.
[US-072] Матчинг принимает задачу и эталонный образец, а на выход выдаёт лучшего кандидата под задачу. Именно этого кандидата система автоматически назначает на задачу. И рассчитывает стоимость услуги.
Updated (12/05): матчинг всегда достает воркера, ситуаций, когда воркер не нашелся под задачу не существует
[US-080] Каждый кот, который хочет стать воркером компании MCF, должен пройти тестирование, чтобы компания была уверена, что кот входит в 3% лучших котов мира.
[US-081] Мы ожидаем 1 к заявок в день от рандомных котов, также, судя по отзывам, наши конкуренты могут попытаться нас заддосить в этом месте. Они так делали уже несколько раз с другими компаниями, после чего компании закрывались с позором.
 
[US-090] Для прохождения тестирования необходимо оставить заявку на сайте, после чего с котом связывается менеджер и назначает набор тестов, который оценит уровень потенциального кандидата.
[US-110] Менеджеры должны иметь возможность конфигурировать набор тестов под каждого отдельного кота или вакансию котов.
[US-120] По результатам тестов кот либо добавляется в общий пул рабочих с полученными характеристиками (сильными/слабыми сторонами) и прочей информацией о коте (имя, возраст, порода, цвет шерсти, фото), либо бракуется.
[US-130] Если воркер не придёт на заказ по любой причине, заказ автоматически проваливается и клиенту предлагается сделать новый заказ (по сути копию) на другую удобную дату. При этом под заказ подбирается новый воркер.

Updated (12/05): за отмененную задачу клиент платит полную стоимость как говорилось в [US-030], за созданную копию клиент опять платит по новой.

Updated (12/05): после отмены, когда создался новый заказ, пользователь должен вручную выбрать новую удобную дату, после чего под заказ автоматически подбирается воркер по инновационной системе подбора. После этого, заказ живет работает как любой другой.
[US-140] Воркер может видеть список активных для него услуг, которые он должен помочь выполнить, а также список завершённых и отменённых услуг.
[US-150] Перед выездом на заказ воркер обязан получить необходимые для заказа расходники, включая бланк приёма работы. Для этого нам необходимо сказать отделу сборки расходников, кому и подо что нужны расходники.
[US-160] Сотрудники отдела расходников сами собирают заказы на свой вкус, нам хватит только уведомить сотрудников о новом заказе и предоставить кнопку «выдано» под каждый заказ.
[US-170] Думая о том, что ещё добавить для увеличения лояльности клиентов, топ-менеджмент решил воспользоваться LLM-based catGPT-4, который подсказал добавить fur-tune-печенья в заказ каждому клиенту с предсказанием будущего. Для этого компания нашла подрядчика, который готовит печенья и привозит их по каждому запросу специально под клиента в отдел сборки расходников. Чтобы печенье попало к клиенту, необходимо отправить информацию о клиенте подрядчику, и через 10 минут печенье приедет на склад, после чего сотрудники положат его в нужный набор расходников. Хоть получение каждого печенья поштучно под клиента выглядит странно, мы всё равно решили воспользоваться этой компанией.
[US-180] Когда воркер придёт в нужное время на заказ — ему необходимо отметиться в приложении (прислать фотографию и нажать кнопку «приступил»). В конце работы необходимо прислать фотографию бумажного отчёта с подписью клиента, что всё выполнено и претензий нет. 
[US-190] Менеджеры могут случайно выбрать любой выполненный заказ и проверить качество выполненной работы. Для этого изучается вся информация по работе воркера. Иногда могут позвонить клиенту.
[US-200] Все отменённые или провальные заказы автоматически попадают в отдел по изучению качества работы. Менеджеры пытаются понять, что случилось и как исправить ситуацию. Для этого могут связаться с клиентом.
[US-210] Результат проверки качества заносится в отдельную форму, благодаря которой компания получает набор гипотез для улучшения бизнеса.
[US-220] Каждую неделю (в воскресенье) у клиента списывается сумма, равная общим затратам на запрошенные задачи. Для этого выставляется инвойс, и дальше происходит процесс списания через заданный клиентом способ.
[US-230] Каждый последний день месяца воркеру начисляется сумма, равная общим выплатам минус все штрафы за текущий месяц. Для этого выставляется инвойс, и дальше происходит процесс зачисления средств через золотую шляпу (уникальный сервис для перевода денег, никак не связанный с золотой короной).
[US-240] Воркер получает 60% от стоимости выполненной задачи, отменённые задачи не оплачиваются для воркера, за провальные задачи воркер получает штраф в 40 условных кото-единиц.
[US-250] Клиент и воркер должны видеть список всего, за что у них списались или начислились деньги.
[US-260] Необходимо показывать, сколько клиент заплатит денег в конце текущей недели, а также список всех прошлых инвойсов и статус их оплат. Для воркера нужно показывать, сколько он заработал, штрафы и также инвойсы с их статусом.
[US-270] Иногда менеджер может зачислить любое количество денег для выбранного воркера на своё усмотрение. Надо знать, кто и за что начислил деньги.
[US-280] Чтобы решить проблему низкой мотивации менеджеров MCF, была придумана система ставок. Эта система позволяет менеджерам ставить свои деньги на результат выполнения каждого заказа. Благодаря этому мы надеемся привлечь больше сотрудников в компанию. Ставки могут делать только менеджеры, которых будет не больше 15 человек. Мы не ожидаем большого количества ставок из-за общего количества заказов.
Updated (12/05): мы доверяем менеджерам, поэтому они сами между собой деньги распределяют в случае проигрыша и выигрыша. В случае, когда все проигрывают, банк уходит разработчикам
[US-290] Вся логика ставок сводится к тому, что менеджеры ставят сумму на заказ и условие. После выполнения или отмены или провала заказа система автоматически рассчитывает, кому и сколько денег надо отдать (банк делится между победителями). Это не самый критически важный проект для компании, поэтому он вряд ли будет часто меняться.
[US-300] В проекте должны быть нотификации. Все нотификации отправляются только на почту.
[US-301] Для флоу проверки и добавления новых воркеров в систему необходимо сделать систему нотификаций, где будут уведомления по каждому шагу, по approve/decline воркеров в системе и по новым заявкам от котов.
[US-302] Для флоу заказа услуг необходимо сделать систему нотификаций, где будут уведомления по изменению статуса услуги, подтверждение от клиента и воркера.
[US-303] Когда расходники готовы — необходимо отправить нотификацию воркеру, чтобы он забрал свой пакет для работы над заказом.
[US-304] При генерации инвойса как для воркера, так и для клиента необходимо отправлять нотификацию. После успешной или неуспешной оплаты также необходимо отправлять нотификацию со статусом оплаты для клиентов. Для воркеров надо отправлять только оплаченные инвойсы.
[US-305] После каждого изученного случая отделом контроля качества, необходимо отправлять результат работы на почту как клиенту, так и воркеру.
[US-306] Когда подберётся воркер под услугу, воркеру должна прийти нотификация, в которой будет сказано, где, когда и что надо будет сделать.

## Задачи
- Event Storming модель проекта
- модель данных для требуемой системы
- общую модель всех полученных коммуникаций в системе
- Выберите подходящую реализацию проекта (монолит или сервисы, как элементы системы связаны между собой).
- Описать спорные места и (или) места, которые вам кажутся критичными на данный момент.
