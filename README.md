# Дневник по научной работе у Дьяконова А.Г. 

Дневник посвящен написанию ВКР бакалавра по теме <<Решение проблемы использования одного аккаунта несколькими пользователями в рекомендательных системах>>.



Ниже представлен список релевантных статей ($\pm$ все указанные статьи пойдут в список литературы к ВКР):

Использование одного аккаунта несколькими пользователями (Shared accounts / Multi-user Identification).
- [x] Jiang, J., Li, C., Chen, Y., & Wang, W. (2018). Identifying Users behind Shared Accounts in Online Streaming Services. The 41st International ACM SIGIR Conference on Research & Development in Information Retrieval.
- [ ] Amy Zhang, Nadia Fawaz, Stratis Ioannidis, and Andrea Montanari. 2012. Guess who rated this movie: identifying users through subspace clustering. In Proceedings of the Twenty-Eighth Conference on Uncertainty in Artificial Intelligence (UAI'12). AUAI Press, Arlington, Virginia, USA, 944–953.
- [ ] Koen Verstrepen and Bart Goethals. 2015. Top-N Recommendation for Shared Accounts. In Proceedings of the 9th ACM Conference on Recommender Systems (RecSys '15). Association for Computing Machinery, New York, NY, USA, 59–66.

Проблема multi-user в поисковых системах:
- [ ] Ryen W. White and Ahmed Hassan Awadallah. 2015. Personalizing Search on Shared Devices. In Proceedings of the 38th International ACM SIGIR Conference on Research and Development in Information Retrieval (SIGIR ’15). 523–532.
- [ ] Ryen W. White, Ahmed Hassan, Adish Singla, and Eric Horvitz. 2014. From Devices to People: Attribution of Search Activity in Multi-user Settings. In Proceedings of the 23rd International Conference on World Wide Web (WWW ’14). 431–442.

---

## 24.02.2023 

Identifying Users behind Shared Accounts in Online Streaming Services.

Довольно современная статья, поэтому по ней было удобно собрать следующие статьи для исследования. Предложен метод получения эмбеддингов треков из графа, в котором вершинами являются треки и различная мета-информация (исполнители, альбомы). Приятной особенностью является именно использование мета-информации.  С помощью случайного блуждания получаются эмбеддинги вершин. Далее однако из эмбеддингов треков эмбеддинги сессий получаются эвристическим взвешенным усреднением, что кажется не самым лучшим подходом, учитывая что вся дальнейшая работа опирается исключительно на эти эмбеддинги. Описывается использование Affinity Propagation для кластеризации сессий и последующего разделения пользователей. 

+:
  * Интересный способ борьбы с popularity bias путем подсчета вероятностей при случайном блуждании в графе с использованием информации о степенях вершин.
  * Использование мета-информации, во многих методах с этим возникают проблемы.

-: 
  * Вообще не используется информация о прослушивании треков, кажется что напротив важным является не только сам факт попадания трека в сессию, а то пропустил или полностью прослушал этот трек пользователь. Это важно потому что в реально наборы треков могут/будут совпадать (так как их выдает рекомендательная система), а вот поведение разных пользователей будет отличаться.
  * Эвристическое получение эмбеддингов сессий из эмбеддингов треков путем взвешенного усреднения.
  * Используется предположение <<разное устройство>> = <<разный юзер>>, что кажется вовсе не так. (хотя паттерн потребления с разных устройств может действительно отличаться).
  * Сравнение с существующими методами не ясно как проводилось, в разных статьях по факту по-разному формулируют задачу. (общая проблема)

---
