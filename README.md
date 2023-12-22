# Домашнее задание 1

1. __Негативные сценарии для нарушения целей безопасности__

На вкладке "негативные сценарии" документа есть пример, по анлалогии изобразите два негативных сценария, в результате которых нарушаются цели безопасности.

В качестве отправной точки можно взять исходный код диаграммы по ссылке.

2. __Политика архитектуры__

На владке "политика архитектуры v0.00" тогоже документа есть заготовка диаграммы.

Выберите доверенные и недоверенные компоненты для целей безопасности №1-3, раскрасьте диаграмму в соответствии с нотацией политики архитектуры, обоснуйте свой выбор, сведя описание в таблицу (компонент - уровень доверия - обоснование)

__Дополнительное задание__: на вкладке "политика архитектуры v0.01" предложите свой вариант архитектуры.

Можно извенить связи, количество и функциональное назначение существующих доменов безопасности, добавить новые - цель - уменьшитть объем доверенного кода.

Сопроводите новую архитектуру описанием и анализом изменений (см. таблицы 2 и 3)

Результаты пришлите, пожалуйста в телеграмм @sobolevsp до 9:00 25 декабря.

Если возникнут вопросы, их можно задать в чате группы.

__Учащийся: Черников Дмитрий__

# Краткое описание назначения и применения продукта

Продукт - автономный дрон, предотвращающий преступления против людей путём дистанционного нелетального (и нетравмирующего) воздействия на злоумышленников.

Дрон патрулирует заданные районы и в ситуации угрозы жизни и здоровью людей воздействует с помощью электрошокера на злоумышленников.

Все решения дрон принимает самостоятельно.


# Ценности продукта и негативные события в их отношении

| Ценность | Негативное событие | Величина ущерба | Коментарий |
| :-- | :-- | :-- | :-- |
| Люди | Причинение критического вреда | Высокий | Возможно уголовное наказание |
| Люди | Причинение вреда здоровью | Высокий | Судебные иски |
| Имущество третьих лиц и/или критическая инфраструктура | Причинение ущерба | Высокий | Судебные иски, издержки на возмещение ущерба |
| Дрон | Утрата дрона | Средний | Дроны застрахованы |
| Другие дроны, воздушные суда | В результате столкновения ущерб получили другие дроны или летательные аппараты | Высокий | В худшем случае массовые жертвы (например при столкновении с пассажирским самолетом) |


# Роли пользователей

Оператор системы управления дронами:

- определяет маршрут и другие параметры задания
- вводит в систему планирования полётов
- не имеет физического доступа к дронам

Инженер службы эксплуатации:

- имеет физический доступ к дронам
- готовит дроны к работе (диагностика, зарядка, замена расходников, например, кассет электрошокера)

Оператор и дрон взаимодействуют с системами организации воздушного движения помимо системы планирования полётов.

Только инженер службы эксплуатации имеет физический доступ к дронам.

![Базовый вариант](images/страж-птица-Контекст.drawio.svg)

![Базовый сценарий](images/страж-птица-Базовый%20сценарий.drawio.svg)


# Цели безопасности

1. __Выполняются только аутентичные задания на мониторинг__
2. __Выполняются только авторизованные системой ОрВД задания__
3. __Все манёвры выполняются согласно ограничениям в полётном задании (высота, полётная зона/эшелон)__
4. В любой ситуации исключено повреждение наземной инфраструктуры
5. При любом состоянии системы возможно только нелетальное воздействие на человека
6. Любое воздействие на человека осуществляется только при условии авторизации такого режима


# Предположения безопасности

1. Аутентичная система ОрВД благонадёжна
2. Аутентичная система планирования полётов благонадёжна
3. Аутентичные сотрудники благонадёжны и обладают необходимой квалификацией
4. Только авторизованные сотрудники управляют системами

# Архитектура

| Компонент | Описание |
| :-- | :-- |
| 1. Связь |  Отвечает за взаимодействие с системой распределения полётов и системой организации воздушного движения (ОрВД) |
| 2. Сбор и анализ данных | Собирает и анализирует данные фото-видеофиксации |
| 3. Центральная система управления | Осуществляет общее управление дроном, контролирует выполнение полётного задания |
| 4. Навигация | Предоставляет спутниковые координаты дрона |
| 5. Нейтрализатор | Отвечает за физическое воздействие на правонарушителя |
| 6. Полётный контроллер | Осуществляет комплекс действий для поддержания дрона в воздухе и его перемещения в заданном направлении |
| 7. Самодиагностика | Предоставляет данные оценки состояния подсистем (например, контроля батаери) |
| 8. Приводы | Серво-приводы и драйверы для их управления - управляют скоростью вращения винтов дрона, механизацией вспомогательных крыльев (если есть) |
| 9. Контроль батареи | Предоставляет статус остаточного заряда батареи и оценку продолжительности полёта в текущем режиме энергопотребления |

## Архитектура (HLA)

![Архитектура (HLA)](images/страж-птица-Архитектура%20(HLA)%20v.0.00.drawio.svg)

## Базовый сценарий + HLA

![Базовый сценарий + HLA](images/страж-птица-Базовый%20сценарий%20+%20HLA.drawio.svg)

[Код диаграммы](http://www.plantuml.com/plantuml/uml/vLTDRnjL5DtFhtZADZ4Itn0XL7Oi-0dTJ1sJMhWpbcSIgRkueMqgLrX5I20a2aY8jMDxyDY9dRzmtp_Yl3DlvlaD7bc19GjG-kP-t7lEkVSc3v8q7AHdJtf1sarx7NKWRsGY2zd8L8zagVHGlv1CrZBH5vBZuL1z-TKN1q4GdgLnTFRaKMSGz16Xs-xsmoY5_--Im-aPd6vbyZ2IExb1n3LUBqnK-_FuG8M9Ekac_J1jF_v7aBSm_bv-eD5fVEv_VVSTXInJFPQ5VasJTXn5oZTw7qP_cihrCyIQo8r-pIx63oCzz4lKbt97cobApQho63OTnBtaQUB7_W2nVw5zBZF4V55vH66jrazW-YkXcwBxkHxHBEaCpkEaLl57nXH6D_eDQbiR-07V2Y_imNmnzUaBXZ3uzxkzEFM3l4TihcMZBvJaYcYZUUHV8DYS_qPe_Pn1-eEutKcIRdJgH_cG3MQoP6BhxpMQF8w_gRFsCNDF02ewXST4PiYs8TIvhAY6NF4pCCRZXi2iPMP1wNrzqWrhfNoAe3yx30oF2lrDu6uacKbEvqTXcdO6JuFWT12VzPNyn1IejwnQ6K4JFpW6JdYgzJdbSwpape6Fdp9bMhQGvP85nWhMHe-7XyUAoMTK4YhRdIQAquwApv45JaVC4pJwoGhPlzClaH3UUC3mmVGQ7uCMo4Gfb3FCloMUmA3Y6IYpwYc5aw4PmcF8o4mUFL8o9u3GmvvmFWupsNX8wF6HCjgl-5kKO-tCxVW6dUX46Gm2j6-XCpZRJG0fcxIe1JEu4nK8PWjELGo3h8ongmv6hZCcifIsMcG9wumELyX09fMnt2AgOjRDEmZUfmVMl3-sYwa-Qs4_001kdfM-rA_emQu09MS6tW1W59J30ATIst04EEOxN8UrmAMzCR8Zjz5ZMnCxcM-llIrll_42CPYzD8rZM8sCz1N-kwIYmMWGzEAuZr7djfnNx3FJbFwoD7Ji77MWuoTtcmoWxz0jJqXcKERRgt931vMV5wJMmFPkrsEC5p3NpmlCRrdst0_4rKp-TxbAvhcIA6FlF8yBygaTc5XPD2QiWSys5yYCDLTmZVRzU6n-XwnswwYPv_eOyZoKo_glCX5UdUghWNCSbvAe9NA7XQIwtMRnOAF8aXjC6dHYPVQRJ7ZFW8OlBycQ75rshnOEHtKRqTdMSLJRjz4Bi9SXFMggmzwYjyY9H6Q6BB0RLKbhKtvoEyJ7qfvQuaZAJBcaZLGfnbXmco_vD6MCmgjMFZSYbWSdwieKGlR-jPWYkyom2Cg1BKJJsXc0xms_6RIuk73jHdX3Z0PCgrtjBdXJ3PBVYonttflQzwwv2WhW6OsiyZwG8XHHSZNdt5RZj7LKa18LibmSUN-BhejUu8skxE0jwQk7dCQLvEwutcV6oVuDttA4PCdyNCgFoDtoKWnXmZJDqsrJPBp9at8vDq_cIITifztp442w8DKlRJ_MYs4WLyiHIYj0dzRJyUfUynvVtk--gF_rUL7_wRfG6vQyF_XU-rl1eyy__EvtD6S3XxeYwvEvtxY-7_Rwi8q7-1_-3FuR)


# Негативные сценарии для нарушения целей безопасности

Еще раз ЦБ:
1. __Выполняются только аутентичные задания на мониторинг__
2. __Выполняются только авторизованные системой ОрВД задания__
3. __Все манёвры выполняются согласно ограничениям в полётном задании (высота, полётная зона/эшелон)__
4. В любой ситуации исключено повреждение наземной инфраструктуры
5. При любом состоянии системы возможно только нелетальное воздействие на человека
6. Любое воздействие на человека осуществляется только при условии авторизации такого режима

## Анализ векторов атак и эффекта (__Для ЦБ №1-3__)

| Компонент | Атака | Эффект | Коментарий |
| :-- | :-- | :-- | :-- |
| 1. Связь | Отказ в работе | При отсутствии одновременных атак на другие компоненты ЦБ1 - ЦБ3 не нарушаются | - не получает данные для рассчета маршрута (не вылетает)<br> - не сообщает координаты, данных диагностики, события мониторинга<br> -не передает сообщение о зваершениии миссии |
| | Подмена полётного задания на неаутентичное | Нарушение __ЦБ1__, __ЦБ2__, __ЦБ3__ | |
| | Компрометация статуса авторизации вылета системой ОрВД | Нарушение __ЦБ2__ | |
| | Подмена данных: координат, данных диагностики, событий мониторинга, передаваемых в ходе работы в районе мониторинга | При отсутствии одновременных атак на другие компоненты ЦБ1 - ЦБ3 не нарушаются | - передает неверные данные, но в базовом сценарии дрон с момента получения разрешения на вылет действует автономно |
| 2. Сбор и анализ данных | ... | ЦБ1 - ЦБ3 не нарушаются | ... |
| 3. Центральная система управления | Отказ в работе | При отсутствии одновременных атак на другие компоненты ЦБ1 - ЦБ3 не нарушаются | - не осуществляет рассчет маршрута (не вылетает)<br>- не подает параментры перемещения (долетит до следующей точки и остановится)<br>- не обрабатывает результаты мониторинга<br>- не передает координаты, данные телеметрии, события мониторинга<br>- не подает команду нейтрализатору |
| | Совершение манёвров вопреки ограничениям и маршруту полётного задания| Нарушение __ЦБ3__ | |
| 4. Навигация | Отказ в работе | Нарушение __ЦБ3__ | |
| | Подмена координат, приводящих к нарушению маршрута или ограничений перемещения (например, высоты полёта) | Нарушение __ЦБ3__ | |
| 5. Нейтрализация | ... | ЦБ1 - ЦБ3 не нарушаются | ... |
| 6. Полётный контроллер | Отказ в работе | Нарушение __ЦБ3__ | |
| | Совершение манёвров вопреки ограничениям и маршруту полётного задания | Нарушение __ЦБ3__ | |
| | Снижение с превышением предельно допустимой скорости| Нарушение __ЦБ3__ | |
| 7. Самодиагностика и мониторинг | Отказ в работе | Нарушение __ЦБ3__ | -центральная система управления не может верно рассчитать данные для перемещения в район мониторинга, дрон может не долететь |
| | Подмена уровня заряда батареи | Нарушение __ЦБ3__| -центральная система управления не может верно рассчитать данные для перемещения в район мониторинга, дрон может не долететь |
| 8. Приводы | Отказ в работе | Нарушение __ЦБ3__ | |
| | Совершение манёвров вопреки ограничениям и маршруту полётного задания | Нарушение __ЦБ3__ | |
| | Снижение с превышением предельно допустимой скорости | Нарушение __ЦБ3__  | |
| 9. Контроль батареи | Отказ в работе | Нарушение __ЦБ3__ | -центральная система управления не может верно рассчитать данные для перемещения в район мониторинга, дрон может не долететь |
| | Подмена уровня заряда батареи | Нарушение __ЦБ3__| -центральная система управления не может верно рассчитать данные для перемещения в район мониторинга, дрон может не долететь |

## Атака на компонент 1. Связь

![Негативный сценарий. 1. Связь](images/Негативный%20сценарий.%201.%20Связь.svg)

[Код диаграммы (www.plantuml.com)](http://www.plantuml.com/plantuml/uml/vLVRRXjL57sVhpWAZuqhjK212bNz3yg3cvZKmfsnF9D8VOkJNb8vmYf2W91QG49z7ZiUF7PYvnVs-GM-X7NMdBcSmOELyiXJqpFxilRQQ--TF0oZzY0wVDfJE_9M4hcGM9z8AbDPwP4ib1xgbtXUuVaOpulRwivj9R_BL8zbhiztF2_gHhtEXta_yk65J_fKdz4ibKJ9Utdpr_CVx-pUtRs7yEt3AF0Fdpxk3Bm-a7Rtklss7waTH4aH_WH-Ln8ZqhLSIcnY8DLQflRdyOvgXsg_6_RRqTwJVmHv1-FlvGSQ7GH7xbS7Aqts0jzN7mqw-wxXnp1yRmhG9uWNowK-PytZHxuUkZ3rgLpJPWguIG6HeQD1q0kVXMxiJn3xBUrJqlkoyF3RDRoVm_HN4Zq50pCzebdO6Hm5eN9DxnbJ65tgDy36Pe729LvOW_bYyEbZXZ0zw7TxGUG6kKj-9hBMnqfIHSPHFFBF4Mp6_oEqVi4W_K6mrmd3hd_WHlcK1IQoO6BhxnGQFWc-hNVkC-QEGIegXKSCSbP0CgJ-bbH4glWP7EDnJM9MSc59wNsptstNe7o1eBzKET3dIYRKj15m8YcT7xUZg3Duvda7W-2mh-HdfW3U7BM2Q4Ra3uvUAJxLUa09tLToNPAFdn9bIYPb70BFM1bhQFBMhVkAoI-e923RdCOFeeuAZf05JhlCupNwoHBPlzEla13UUC2emdI2ZruBpGGKoXdcpyadE2Zw39Q9cbDki5yRUjYCnEJH8oKp4WWzR0ddyd0XQuS9FTvLHlj5_-R5Q1VcTeIzZh-l30SUohVK6PxjDe2KJLfWmGnkP0M2gT2fic6GfJ4kqS6eh8o9R4jRBNOfbZaTAkiCbfL6sSv-PPR8rmygKuysRrC5aM_FKCPKNxQm9K03zyyIQ_OrFLWR2ENam1iqZBny9E2KAnoEeCXyX-km5ZYtDqPsyDPwR36nabbr-LMzMzN2CzvWzieKZf7bHJZZLK1kqrUl5mHzxbqCFVVchD01iqqPGnQcCHk77Wov0CgT1k8tA9W79J5Cy-rrlgkzmiy9KYkYkkNr68C6tlMBZFShmfwvWRYagO5Dhf8uhcoMiIyzxsS2e7vWOgNHcB3M09OvHsOilApVAD-Dn-8tI6kpbffxNHz8Cr35slupJuJNGldbw9Kzjh9mqvG7XYqjTvnbWsKYHseOQL19LMc_ISpZ1a9SXKdIv5r2S01nHef3YU8gbr9L3wKJO6kJzAW9XprCxsJ2bc2KBBThLQWBVlNVlLn2xTqbcUoQWSlEiLkACUPSxGi-JHaZywh1vth43k5GdHaWRE07wydFTXftWPtPJ3UjZG7utl1hGelxIoRW_yJ4QE2qECdbEM_28EcDcbNU-eRotTEkl8nuHcDNUIRO8e38UpNZw1OJLRqjiMSGdX3Zn5sagwmMUACgEtiB-keX1t8fQN5fRpJcxFubtrA496H-pkL7vgvuC8OmIVzrmcs6XFSvpjTpys3kTzfxKVUe3HxB8FcO_5I7mZWbabq0ooYVrhFnz4vub4zlTc3K__g-gFzoNgWCsxi_-5pxgy7fdjgmFR2EIXiwrEHO7yljnlNbiDM7LNZUG_o3Fx__1W00)


## Атака на компонент 3. Центральная система управления


![Негативный сценарий. 3. Центральная система управления](images/Негативный%20сценарий.%203.%20Центральная%20система%20управления.svg)

[Код диаграммы (www.plantuml.com)](http://www.plantuml.com/plantuml/uml/vLVDRjj65ztFKmpyBMCQ-9h-j4OHv3tgBXXRTOGgf23I1hApd9yuK50XHT4M1PAsGD4r9OiL9LdoAyoyGf-aPmv93OSbeHfTTjEVuVsvzvnpxvKVHh4_YC-Uz4JSZNiTkLVyIxrJgRfMYRvKcPggjHwfXTH3_HBFQpnVu7bnS1JSFv3gT_EcB_6Mg9L-m-zZ6AiC3fVuUACIgP-fMrfCrOenCZq-2f06iVGpVPM_gTI4Uol_VFxz_JqX_BCu3CwUFEeCH1zbTe-xVJ-8KTslrTW8SukW2ODUg0rI97c2FUb7ygGRzVtu-F7VWho7yRVgEngTXkVkr_yVI6IPwh6QwpSqEGw3GBf6RTsZCprqIspglmmR3y9Uz3II_njqJjm47oB1EpfbPEFbrYtmQmL_2jEVoSiK4CpqY6PHPt0UHhMoFpQcC5hfjoYGt0B39LxOYFbYYjGN3658w7TxOUm6-O00JTH6NqYLIK8E191_Zc0p_Zz2wnSCqX-4nvqewWQdRfIFs62g5anS-3kDHe_3h-lKVSBS2P15f_180CuQbGmfroKbaKb-1j1ut12OjRekGEbzTTBrQwLyXg0_MGmCcHBzOGIezrHbT7xant5dy5I8qq5urfVgHwP0lMNL4geP4Jyu2gi-wJsWXWwbkhNWuxzIQLecP1m1OQoCDKHvxzwXPF9hoWcLDQS9mhWZmtDaWTC-yuXMFxL4zc_qAoI4Dnumh32TuAFmG2PAeQPX_Zp7an2IPuCogywNGcgQ0Jma8pLvz4Yg6G647dQ4St6uLXi72JtUbqRxM_xcvMnRysA6HISuaGO3WVOBw0pEnJg0b4rQr78KDADo55JXbFamgAKnjjN1o7R6H0MbdaUM4ZMdWrrcnh92r9PPE_GWU9SUMFFks3Qc_Dp3VW00N3zBhDVNz61NW98p0sy0C1BbCC2fr3OS0Oxv3jTXBN1fRuoC6CZEkAY9dSogkw_gxNrXDjoNrVPpt63yohIFaUKzkE9DG0M6Lo5wOTZdSiJKStlEja9WqcaE_i8mqpZr0Cgfuu5TQi2_GS8yAQa1d6-louqjjdvE4BSBvzRfCIODyEiNEVmtB7lc1kAMfXIQN5Ngk1hEQ6yz3wc3N4OmAHJIcj2hCm2FEJ9Zu-Mqetqt7fjlKbYJfAfsjLJrYUIbAFVs7_PtWHq0EtkMuq8NZTAoXuRCsbrNWC9kaIepmBI8nL7SBohXbGCmhj9KskPkQv1UjIAE32ycDr7rPChgnNG2x2HBZrhRa997gkZalPgG8inMWVL6bcgZV-sd6DnT9lDJJ5p9eocSN98_oIXpRli5dwP5bDolrWft9jOB1-tA50DBqdftcJcR9SZt7XT5CT2vgBp6C7nl-H7XSSUf2KYvD37QW2xNkZtsRJMex4uCsby2RI0uXr-Ad0D68yKy9MGBHHIqSNskxBXLxqyYJ8MNh77YRjbrtWkyqLKnc0lwwY6dTQaoUuSRoDcn2IY65Tyo16RX_5mgalZTyBGCOPBzaoLG94fvofDoaRUFxad7Fuwxvpv0jK64g8xH3_Mw6CsMjOygSnQczPmWZJyf3VrtEqZoFtsFvBywHvH9pg3wZU-rlpCS-cJhNi76ifPqgqkqFh2xZMjhOwSFctc8V-1Fzhy0)

## Атака на компонент 4. Навигация

![Негативный сценарий. 4. Навигация](images/Негативный%20сценарий.%204.%20Навигация.svg)


[Код диаграммы](http://www.plantuml.com/plantuml/uml/vLVDRXjb5DtFKtmAoyH8_4DKeR9ZmHjG5jF4f1RkZEMPHEekFxHDbGgh20c4H049iPuu7ZnsOkSLxlT6d7lcP_nDFLY19OjMwJVtvzvppxctkH_5_Z0-VDptubxSxvejUIM9J6KfOtiXCsDFx3D9PI69FPOC3zlcyoy-s_8y_p0EWyF73xj3Ru08lRtUm0zY-Fyk6PnEuNGZoOD0RkKQ4HTuFTQenS-ZBUD7PhyN3Vnuxz4RGLx3-7lvWKO7uP7xzPst3RACxKYczYLDzi8WCAxHUp3wKoktfuYLoBLzoIv63m9xufPep-IMDcEKcbRbCMmy3FlHayYD_JvY_qBxJAuGyrdb4VX7vgrXTz-r_nZslnA_CI2Os0lQHjtXKHWrolvGJM5qRL-Xm8NE01ZEyS96z8iMQOyPGeSmwFN3s0toBW6wbAKzDf8PGWu4a7-AO1F-6w7jKmOP3CEzRXJrWWCtoWViCfKP4nV-JhVHe_2RvkW-Oku4oA9JU2HoXMnBuft9d9J833y3Q3mk2Sn2hWfG-b_lz_n6APyWwCyr1ZfCW_uIk2ilKyde_D2Fu-xmYUST3CF3WP6Vc0BrbbKRibhnWwDNiyzqFYM7TetSrk3ZfzHeomLacQIUMgarIBczlMkO_8fqGcNhqmHXt3NX4RB0QOTvl5O_cIFxT_Qv9EgD1oWGffVuw7KmJ9H2JiFyM-893Aev0sLMFIPnKcq6y70OgUQn5qOc111ys13EnU5AbWuIThHZL03L_AQLjYlpGiDUDzWtYe67zWle5ETY7O3AcXQrG8ZhK85WL-4qkHXahiPrTJ2gEsEYOgIT3gU4dKQ7yrpW2WuiLmPLJROMFGQyYG-iUNFiEgQvzwNkXwywM1M0WKjeRi_i2_gnDm1AvI06OBZmIacOUvsIuN04HFeThYTE-4ub8JKgXBUqew8ozZDPtO2htaxxEMumUwxjgsH19dkEFsUQM-VgUVqm773ZGVNSdfEA24mtpi6VwMJMgXv0kHNKImtuhw4mJqggWFFjHRcnlShF2TBeOdNNsn6K1k3jqnpu6vOzSGDnIvCAwrmbTLmvBRMlFNTp7f16CAaOqfBmpGcaODUPRhnyu6ZVZSVcNGgGM-l9r3xifY9LKTNU_gjCXDTQ09NswXcNl73pr2U6CwstN047-qIIJ25feOd3jTyauNq392x796rphsjmAg9Cgbk9zbQEfLczbKw0ZMEo5srr5BVfDN8YaQgfG7TfAdujoq_rJd4HBKulqUJSj5pEZlCoZ37bTf_nQSmOkLUZV6v8h17AwbmBuGZ_DQE2VArn6nIgpPdJMHk0xot_K-XmXSaby3_L62sOLhkxlkXjDKXsfs7LvxwbVVUw6oy7dj4uLTuBZWX5bBEQKBoLfbQFJE9fXQUiyT9TfOky5tYZgq9zC_hQ4qfoBbbrREyaT4x_ccyPGh9aVYxfH-HkU3DEO9BziyQB52blT59kw7PbxdVzlRXtv0F8EeX7ePHw_x5P4QFL1UsWlXpvSJCdJ_4bZ_JPtIwD-LyV6lEVxWm9KgowF_ZU-0N26PzPiqMmbYeREZHfwSfpWt7BajZWmpRkuo_yWlmt)

## Атака на компонент 6. Полетный контроллер

![Негативный сценарий. 6. Полетный контроллер](images/Негативный%20сценарий.%206.%20Полетный%20контроллер.svg)

[Код диаграммы](http://www.plantuml.com/plantuml/uml/vLTDRnjL5DtFhtWAoyH8V4E4KDcnu2TqCqrCQk7EM9v9fExoGTjKgR2Aa418590GwudZ8MCdTlx2VV-8Sy_C-FbDFR82InQjqZVtuznppxstUP2auJ0zVD8FqbxQxvejUIsPNCj2nlP2fiQUsEUIormoUom57hRDLrz_kHK4uM4QHuTF7dM7mG0HUdkzGHYbyFz32ZYTmkbMieUHtCaD8ixnUgnHgvz7MoPCp7ul6OJftkEtWho1yG_o8uqEuYF_wtll6cGPsv5SsrSqsOkZoFX67y3eBqLkJn4hanlxYbMC7aRsn8Tep-IEDcD0pHqy3PiEutxoDF5ZVuZOlzA-a2l4VBxqYC86razX-Xkf6wFwYRsWMT8T7iL90_77QYeB87qDR7Eb7_JDyC8Qz8lYiySCeVmFUlquDUyCk_j-fFT9qAKixB6Hmf1oC00GruWuuRyHtpvZfC4mtkicIIywyADyn2fpcJ9xvUzLcpoElsssxXFcpi0ioeL79bV8jY3VXSmeYSBmCuZ6uuBipEMgOgR_pNulR43v345_SKHeCmtgo-2kkiobeFEZC4sxmwT1S32C3mT6VcOAuArH6wfQIOHZuDHdEbzGGxj6xbm7y5DkjEIAiaBoGAtK6gBStjurJ7v5EG7P-ZHHd7PDV8GiSDfXdg3LJsR8_hrz8Pbwum4J2DDBV0mw1X0cfQPX_Xtv10VBFeDbeXvJFJcA8JtQZ5pps0iZ4n88FMm8v_Dm9GkF2JlQCJe0o_vTrxFjpAiP3hhHlb4E0fHVKQSyL-i0UjQqm891NCiA1BD2foadGcPgxD31o5N6H5LBEnrs2JkD3kVbW2ivi5nfrBApRkZHu4rw8ERDiLrCyta7Im84SFtCx9bzIGzM1IevC_060HT1FGnmghKDHv2Zt-5wqWXSswjHDN8BEwemiPB9wkvRyVOBBnc3sGijN8SLChBd-7EckRMZGT2Fum5t3-QTUtEob03JZKlQfzgJjVCEYdm4RgU1-JNYvJ79bMg-lQntTR3qyu8qgbZTydQ46GFnzbb9_2rXJ_n0vP86bBMkadkkx9RQEyzTAg0K44mgRRGcVBi3ENHrfhkkR3ZAz-En-7NQMYkczcOtPv4tejxOVpCHnz19tqsTwt6jYqOYTrtOLBVWAZvOAB8KoacBJagjoU-IyQY13LzUahSvkkm-5av8VI1HsSg5DAi7qWkmiKFseWr7TP3U82SIwI1Ln2xCKbgB-fDR93wNrRqbZsoPmcNRs2h36DTSwLC-ZHcZz6h0vrh41k54dIiGTkzVYoagDneNGJMmfMWwQmFmlUM_1nrkBxa4_wSQeutJUc6xCzw6GOfxDSlT-9Ro_PDkWf9uHcDNUIJO8e2eUpNHkNNZj7fPiW082HUNtj-Yyx8MUAEgQl2czBKddCQP5Ex2tcV6sVqRlXK8ISZyNCkFpDtoNE1eb6dQfxjAaVCmP_LoRf_C_Mwub_QEGX3fWWGSbFgi_DH4n6WEq0xmbSoFcpbvVozvcS_kTsJC__h6cFzqOYYGQjNzoVV6RmrU-yoQBOArv6peq9HbSpmt6pUMn4OVbl40V-6tudy0)


## Атака на компонент 8. Приводы

![Негативный сценарий. 8. Приводы](images/Негативный%20сценарий.%208.%20Приводы.svg)

[Код диаграммы](http://www.plantuml.com/plantuml/uml/vLTDRnjL5Ds_N_4KbecH-8O8eR9ZmK_8PfgOrCATiJoJIDqb3MrJkS8gGW8XKK12h1t7WyTExFo5-_uHvvtnc-StUB02InQjqZVtuznppxstUP1cKJyxUTnLMIVhjlMEl9QHJ6KfOpEGcJRdvhdaif2HEPC23xlwYoy_tr4gEicI-EJnmtPVzH2XSzZfHN46_z-aWDDJEDtAw22MExb1n0LUpspKrS_37Hsb-gYJzgBiyD7VWho1yNVoFOsEazFmwpjlQsGPcw5CpIkQ72Pnh4EZzs3qXqLkdYBMI6xCArOnF8ZDUGZHNCWTRSQ0cbVm63Rh9ztqIHh6VX-nVwPz8TU8-RpoYACQrezX-Wkf6wFwYHdGB6ttJvDKlzLl7uNc7rfpMGBjQ-1Rs1Q0mZbUM8VzOZ6QCuQnFUXrkaaM1dcN_5p9qfnfAJGP1m70C4Mm2V-DqEOPW_JwoM4xJJlnSHZb0nQPoymcTlv1iUcZvEjwvpvYxX68HRNm686WXIn9To5pAgBG_0oUyRWaEGkvNX7J_Uge4zMWV8AWFtaER2yrwXl1tSeobuBE3wCiQ_UVA7NSJqvwMdva2k1rg3L5RVc3e_BYqwtFAA5zBNUUVFoKQrjoIHd2vCfQmTfgSdTtNpFvDTK4P9lJn4dMriafii1fZtbKev_CaVrRym89uOq7321Ch_1HjT1CGA6aOVuD-GG7LP_1Cb6FAPpS5WDws8pSvZ43BHCI23ri2HVm0AZBW0aptDDM_rN_fcwqAtCtmgeT7sdBWKBvA-eip-Ksi5AsQO7b8DxC2WIpHgSkXq7crjYZWv6lZ8bMBMsrs2MiD3fS8WCxgQtbMgEgplgPHuEtwO6OjyVsCVMdBUm84C3jCpSNvYKzM1MevCp06mGCb1i6E3bjmn7asEzmFQy5TlRMo8g1tHawJBQIoVhgM_CE2oyPWzaBMxYsInBYkSIV2oeQ7LMgcoGzBZ3CEzVcf980qurBscUs9nld7HI52Fmw0_CRnCjRabkg-VRIhMfL-GL1QbMiBtapn8o1UFEi9FwMi2TX8EveYc2Jg-I1g-qMxRtdVga02WWcJXjD2MiTO9bJPCQkAnkEyiDuB7w3jZQBgRdPzLdaZN0R-q-N2A-LzFtK-HuxNOHv_76nHFhzvkXWdKXIM4eQPBBIclmg8nuri17AI_8cJvy-1CC9SGSIbQrTIBr-88C0Mpja1Wqut45wWvn8P0TfHUnILz9Qkaz-aTJ8BEyjYMJBB5osZQtIZ37bIf_nQSmOfLSDFjSYDWWdwj82OVV-jPZYSgFPHU06jXHDQsC0lZVyzw35xOMJD-1T6ZPnwXQsF-DD6AIuLxFyZMygFpZfMfN4CngxoYF15W64wzM4SrkDq_fb6IaW95nS-d2BBifQPCAgoi6RqTUSSnhdKlWBUvyPP_Tl-5OW927pivCVcRlbkJY7IV7Furscu4s3dDroRfxCetPqc7LE8n3fWoWEYZihFzGHCPe7j0Ty9VFZUaxUtojUvelx7Hdzlxun-h-S60h4hRhV-LxxhI5edzwmHR2Ml0qTwhAiZ-TMu_gIsEh3CXxWB_nI_1S0)


## Атака на компонент 9. Контроль батареи

![Негативный сценарий. 9. Контроль батареи](images/Негативный%20сценарий.%209.%20Контроль%20батареи.svg)

[Код диаграммы](http://www.plantuml.com/plantuml/uml/vLTDRnjL5DtFhtZADZ4Itn0XL7Oi-0dTJ1sJMhWpbcSIgRkueMqgLrX5I20a2aY8jMDxyDY9dRzmtp_Yl3DlvlaD7bc19GjG-kP-t7lEkVSc3v8q7AHdJtf1sarx7NKWRsGY2zd8L8zagVHGlv1CrZBH5vBZuL1z-TKN1q4GdgLnTFRaKMSGz16Xs-xsmoY5_--Im-aPd6vbyZ2IExb1n3LUBqnK-_FuG8M9Ekac_J1jF_v7aBSm_bv-eD5fVEv_VVSTXInJFPQ5VasJTXn5oZTw7qP_cihrCyIQo8r-pIx63oCzz4lKbt97cobApQho63OTnBtaQUB7_W2nVw5zBZF4V55vH66jrazW-YkXcwBxkHxHBEaCpkEaLl57nXH6D_eDQbiR-07V2Y_imNmnzUaBXZ3uzxkzEFM3l4TihcMZBvJaYcYZUUHV8DYS_qPe_Pn1-eEutKcIRdJgH_cG3MQoP6BhxpMQF8w_gRFsCNDF02ewXST4PiYs8TIvhAY6NF4pCCRZXi2iPMP1wNrzqWrhfNoAe3yx30oF2lrDu6uacKbEvqTXcdO6JuFWT12VzPNyn1IejwnQ6K4JFpW6JdYgzJdbSwpape6Fdp9bMhQGvP85nWhMHe-7XyUAoMTK4YhRdIQAquwApv45JaVC4pJwoGhPlzClaH3UUC3mmVGQ7uCMo4Gfb3FCloMUmA3Y6IYpwYc5aw4PmcF8o4mUFL8o9u3GmvvmFWupsNX8wF6HCjgl-5kKO-tCxVW6dUX46Gm2j6-XCpZRJG0fcxIe1JEu4nK8PWjELGo3h8ongmv6hZCcifIsMcG9wumELyX09fMnt2AgOjRDEmZUfmVMl3-sYwa-Qs4_001kdfM-rA_emQu09MS6tW1W59J30ATIst04EEOxN8UrmAMzCR8Zjz5ZMnCxcM-llIrll_42CPYzD8rZM8sCz1N-kwIYmMWGzEAuZr7djfnNx3FJbFwoD7Ji77MWuoTtcmoWxz0jJqXcKERRgt931vMV5wJMmFPkrsEC5p3NpmlCRrdst0_4rKp-TxbAvhcIA6FlF8yBygaTc5XPD2QiWSys5yYCDLTmZVRzU6n-XwnswwYPv_eOyZoKo_glCX5UdUghWNCSbvAe9NA7XQIwtMRnOAF8aXjC6dHYPVQRJ7ZFW8OlBycQ75rshnOEHtKRqTdMSLJRjz4Bi9SXFMggmzwYjyY9H6Q6BB0RLKbhKtvoEyJ7qfvQuaZAJBcaZLGfnbXmco_vD6MCmgjMFZSYbWSdwieKGlR-jPWYkyom2Cg1BKJJsXc0xms_6RIuk73jHdX3Z0PCgrtjBdXJ3PBVYonttflQzwwv2WhW6OsiyZwG8XHHSZNdt5RZj7LKa18LibmSUN-BhejUu8skxE0jwQk7dCQLvEwutcV6oVuDttA4PCdyNCgFoDtoKWnXmZJDqsrJPBp9at8vDq_cIITifztp442w8DKlRJ_MYs4WLyiHIYj0dzRJyUfUynvVtk--gF_rUL7_wRfG6vQyF_XU-rl1eyy__EvtD6S3XxeYwvEvtxY-7_Rwi8q7-1_-3FuR)

# Политика архитектуры 

## Политика архитектуры v0.00

<style>
red { color: Red }
orange { color: Orange }
green { color: Green }
</style>

| Компонент | Уровень доверия | Обоснование |
| :-- | :-- | :-- |
| 1. Связь | <orange>Повышающий доверие</orange> (CL)| -получает низкоцелостные данные из внешних систем<br>- отвечает за аутентичность полетного задания (возможны нарушения __ЦБ1__, __ЦБ2__)<br>- сложный компонент (прием/передача/проверка аутентичности)|
| 2. Сбор и анализ данных | <red> Недоверенный </red> (MV/ML) | -не нарушает ЦБ1 - ЦБ3 |
| 3. Центральная система управления | <orange>Повышающий доверие</orange> (CXL) | -получает низкоцелостные данные от недоверенных компонентов<br> -производит рассчет маршрута, проверку достижения района (возможно нарушение __ЦБ3__) <br>- сложный компонент (рассчет маршрута/обработка результатов мониторинга/подача команды нейтрализатору/подготовка данных телеметрии, местоположения и т.п./) | 
| 4. Навигация | <orange>Повышающий доверие</orange> (SS) | -получает низкоцелостные данные из внешних систем<br> - отвечает за аутентичность данных позиционирования (единственный такой компонент)|
| 5. Нейтрализатор | <red> Недоверенный </red> (SS) | не нарушает ЦБ1 - ЦБ3 |
| 6. Полётный контроллер | <green>Доверенный</green> (ML) | - осуществляет комплекс действий для поддержания дрона в воздухе и его перемещения в заданном направлении (возможны нарушения __ЦБ3__) |
| 7. Самодиагностика | <green>Доверенный</green> (SM) | -транслирует уровень заряда батареи (возможны нарушения __ЦБ3__, дожен передать высокоцелостные данные)<br>- получает данные от различных компонентов дрона, но в текущей политике это только заряд батареи, поэтому сложность низкая |
| 8. Приводы | <green>Доверенный</green> (SS) | -управляет маневрами (возможны нарушения __ЦБ3__) |
| 9. Контроль батареи | <green>Доверенный</green> (SS) | -предоставляет статус остаточного заряда батареи и оценку продолжительности полёта в текущем режиме энергопотребления (возможны нарушения __ЦБ3__, должен предоставлять высокоцелостные данные) |

Количество компонентов:
- недоверенные компоненты 2/9
- доверенные (повышающие доверие) компоненты 7/9

![Политика архитектуры v0.00](images/страж-птица-Политика%20архитектуры%20v0.00.drawio.svg)


# Выводы

1. :white_check_mark: __Негативные сценарии для нарушения целей безопасности__

Представлены негативные сценарии для критических компонентов, т.е. таких компонентов, сценарии атак на которые могут нарушать ЦБ1 - ЦБ3

- [Атака на компонент 1. Связь](#атака-на-компонент-1-связь)
- [Атака на компонент 3. Центральная система управления](#атака-на-компонент-3-центральная-система-управления)
- [Атака на компонент 4. Навигация](#атака-на-компонент-4-навигация)
- [Атака на компонент 6. Полетный контроллер](#атака-на-компонент-6-полетный-контроллер)
- [Атака на компонент 8. Приводы](#атака-на-компонент-8-приводы)
- [Атака на компонент 9. Контроль батареи](#атака-на-компонент-9-контроль-батареи)

В таблице [Анализ векторов атак и эффекта ](#анализ-векторов-атак-и-эффекта-для-цб-№1-3) для каждого компонента представлены несколько сценариев, в том числе некоторые сценарии не нарушают цели безопасности.

:question: По-хорошему, думаю, что для каждого сценария необходимо диаграмму???

2. :white_check_mark: __Политика архитектуры__

Выбраны доверенные и недоверенные компоненты для целей безопасности №1-3, представлена диаграмма в соответствии с нотацией политики архитектуры, представлено обоснование выдора доверенных/недоверенныйх компонентов и их сложности.

:exclamation: Политика архитектуры сформулирована, на основе [базовой архитектуры](#архитектура-hla) и [базового сценария](#базовый-сценарий--hla). От себя пока ничего не добавлял.

:exclamation: В ходе работы над заданием возникли некоторые замечания по базовому сценарию:
- на этапе работы в районе мониторинга дрон не осуществляет перемещение
- уровень заряда батареи учитывается только на этапе инициализации вылета, при перемещении и при возвращении с задания уровень не учитывается
- модуль самодиагностики и мониторинга получает данные только об уровне заряда батареи, либо этот модуль лишний, либо он получает и обрабатывает данные диагностики от других систем.

Это замечания скорее к функциональной архитектуре и базовому сценарию.

:black_square_button: __Дополнительное задание__

Дополнительное задание планирую доделать к дедлайну.
