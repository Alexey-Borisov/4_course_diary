# Дневник по научной работе у Дьяконова А.Г. 

Дневник посвящен написанию ВКР бакалавра по теме <<Решение проблемы использования одного аккаунта несколькими пользователями в рекомендательных системах>>.


## Общая структура модели

1) Получение для каждой пользовательской сессии векторного представления (эмбеддинга). Основные варианты, которые хочется рассмотреть: ALS (есть готовая инфраструктура для проведения экспериментов), модели на основе RNN и архитектуры transformer. Интересно различие в моделях, которые учитывают последовательность и не учитывают. Также интересен учет мета-информации на уровне треков, и (возможно) на уровне сессий. В случае RNN и трансформеров должны подойти подходы из NLP.
2) Кластеризация эмбеддингов сессий для выявляения различных пользователей / паттернов потребления. Здесь стоит рассмотреть различные алгоритмы кластеризации, вообще говоря и semi-supervised, так как вероятно какая-то разметка будет присутствовать.



Ниже представлен список релевантных статей ($\pm$ все указанные статьи пойдут в список литературы к ВКР):

Использование одного аккаунта несколькими пользователями (Shared accounts / Multi-user Identification).
- [x] Jiang, J., Li, C., Chen, Y., & Wang, W. (2018). Identifying Users behind Shared Accounts in Online Streaming Services. The 41st International ACM SIGIR Conference on Research & Development in Information Retrieval.
- [x] Amy Zhang, Nadia Fawaz, Stratis Ioannidis, and Andrea Montanari. 2012. Guess who rated this movie: identifying users through subspace clustering. In Proceedings of the Twenty-Eighth Conference on Uncertainty in Artificial Intelligence (UAI'12). AUAI Press, Arlington, Virginia, USA, 944–953.
- [x] Koen Verstrepen and Bart Goethals. 2015. Top-N Recommendation for Shared Accounts. In Proceedings of the 9th ACM Conference on Recommender Systems (RecSys '15). Association for Computing Machinery, New York, NY, USA, 59–66.

Проблема multi-user в поисковых системах:
- [ ] Ryen W. White and Ahmed Hassan Awadallah. 2015. Personalizing Search on Shared Devices. In Proceedings of the 38th International ACM SIGIR Conference on Research and Development in Information Retrieval (SIGIR ’15). 523–532.
- [ ] Ryen W. White, Ahmed Hassan, Adish Singla, and Eric Horvitz. 2014. From Devices to People: Attribution of Search Activity in Multi-user Settings. In Proceedings of the 23rd International Conference on World Wide Web (WWW ’14). 431–442.

Коллаборативная фильтрация, алгоритм ALS (Alternating Least Squares):
- [ ] R. Chen, Q. Hua, Y. -S. Chang, B. Wang, L. Zhang and X. Kong, "A Survey of Collaborative Filtering-Based Recommender Systems: From Traditional Methods to Hybrid Methods Based on Social Networks," in IEEE Access, vol. 6, pp. 64301-64320, 2018.
- [ ] Y. Koren and R. Bell. Advances in collaborative filtering. In Recommender systems handbook, pages 145–186. Springer, 2011.
- [ ] Gábor Takács and Domonkos Tikk. 2012. Alternating least squares for personalized ranking. In Proceedings of the sixth ACM conference on Recommender systems (RecSys '12). Association for Computing Machinery, New York, NY, USA, 83–90.

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
  * Используется предположение <<разное устройство>> = <<разный юзер>>, что кажется вовсе не так. (хотя паттерн потребления с разных устройств может действительно отличаться). Симуляция нескольких юзеров с помощью перемешивания сессий с разных аккаунтов тоже кажется очень нереалистичной идеей (использовалось с датасетом Last.fm).
  * Сравнение с существующими методами не ясно как проводилось, в разных статьях по факту по-разному формулируют задачу. (общая проблема)

---

## 25.02.2023

Guess who rated this movie: identifying users through subspace clustering.

Более старая статья, рассматривается рекомендательная система фильмов (типо Netflix), за счет чего нет проблемы с формированием эмбеддингов сессий, работа ведется с эмбеддингами фильмов. Основное предположение заключается в том, что эмбеддинги просмотренных фильмов лежат вблизи некоторого многообразия, которое представляет собой объединение нескольких гиперплоскостей, число которых равно числу реальных юзеров. Фактически считая число юзеров известным оптимизировался определенный функционал. В результате получались эмбеддинги юзеров для всех пользователей аккаунта.

+:
 * Представлено довольно много методов определения какие объекты каким юзерам соответсвуют: кластеризация (KMeans, Spectral), EM, GPCA. В своей работе я также собираюсь рассматривать разные способы кластеризации.
 *  В итоге получаются эмбеддинги для каждого юзера аккаунта (хотя вообще их всегда можно получить просто из матричного разложения с учетом информации о том кто какие фильмы смотрел)

-:
 * Все представленные методы опираются на информацию о количестве юзеров аккаунта. А это число определяется с помощью BIC (Bayesian Information Criterion). И вообще в работе датасеты весьма скудны и работа ведется только со случаем 1-2 юзеров одного аккаунта, за счет чего реально определяется 1 или 2 человека просто применив метод для обоих вариантов и выбрав лучший по BIC.
 * Никак не используется мета-информация.
 * Основной датасет Netflix не обладал разметкой числа юзеров у аккаунта, поэтому использовали синтетический датасет. Разметкой обладал только CAMRa2011 датасет, но в нем всего 272 аккаунта были размечены как обладающие 2 юзерами, слишком уж мало.

--- 

## 25.02.2023

Top-N Recommendation for Shared Accounts.

В данной статье фактически предлагается усовершенствованный метод подсчета <<близости>> объекта аккаунту в item-based collaborative filtering. Перебираются всевозможные подмножества объектов рейтинги по которым для данного юзера известны, и берется максимальный скор по всем подмножествам. То есть на самом деле это могут быть даже не разные юзеры, а просто различные области интересов одного юзера (для рекомендаций это только +). доказывается теорема, позволяющая определить этот максимальный скор и соответсвующее подмножество за время O(nlogn), где n = <<количество объектов рейтинг для которых известен для данного аккаунта>>. Вообще говоря не очень подходит к теме multi-user identification, потому что подмножетсва оцененных объектов могут подбираться каждый раз разные при подсчете скора каждого нового объекта, то есть реально разделения оцененных объектов на группы не происходит.

+:
 * Кажется, что предложенный метод может быть полезен не только в случае shared-account, но и просто в случае нескольких ярко выраженных областей интереса у пользователя.
 * Доказывается интересная теорема, которая позволяет свести экспоненциально сложную задачу к сложности O(nlogn). 

-:
 * Снова используются только синтетические датасеты.
 * Никак не используется мета-информация.
 * Рассматривается задача коллаборативной фильтрации с 0-1 матрицей.
 * Реально юзеры не разделяются, то есть строятся рекомендации, которые суммарно лучше удовлетворяют пользователей аккаунта, но так называемого multi-user identification не происходит.

--- 
