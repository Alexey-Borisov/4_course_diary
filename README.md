# Дневник по научной работе у Дьяконова А.Г. (активный раздел)

В данный момент я работаю ML-инженером в группе музыкальных рекомендаций VK. Хотел бы провести ресерч по Session-based Recommender Systems (SBRS).

Появилась мысль насчет более конкретной темы: по сессиям пользователя выявлять его паттерны поведения. То есть в зависимости от настроения, времени и тд. пользователь может по-разному потреблять контент, возможно даже, что в реальности несколько пользователей пользуются одним аккаунтом. Можно строить некоторые представления сессий и кластеризовать их выявляя тем самым паттерны поведения пользователя.

Начну со следующей обзорной статьи: [A Survey on Session-based Recommender Systems](https://arxiv.org/pdf/1902.04864.pdf).

Список ниже будет дополняться статьями, которые я буду изучать:
-[] How Jing and Alexander J Smola. 2017. Neural survival recommender. In WSDM. ACM, 515–524. SBRS на основе LSTM для рекомендаций музыки/фильмов.
-[] Massimo Quadrana and et al. 2017. Personalizing session-based recommendations with hierarchical recurrent neural networks. In RecSys. ACM, 130–137. 3 статьи ниже также используют RNN для SBRS.
-[] Balázs Hidasi and Alexandros Karatzoglou. 2018. Recurrent neural networks with top-k gains for session-based recommendations. In CIKM. 843–852.
-[] Balázs Hidasi, Alexandros Karatzoglou, Linas Baltrunas, and Domonkos Tikk. 2016. Session-based recommendations with recurrent neural networks. In ICLR. 1–10.

___

## A Survey on Session-based Recommender Systems

Основательная статья, в которой подробно описывается классификация SBRS, отличия SBRS от Sequential RS. Ссылки здесь отличный отправной пункт по статьям на тему SBRS. Однако здесь еще не упоминается использование трансформеров для SBRS (первая версия статьи вышла в 2019 году).

___



