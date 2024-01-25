# Система поддержки принятия решений для врачей-онкологов
## Документация проекта

### 1. Цели и предпосылки

#### 1.1 Текущий бизнес-процесс

- Не во всех регионах РФ отделения онкологии/гематологии проводят высокотехнологичное лечение.
- Пациентам приходится обращаться в центры/институты в крупных городах.
- Центры/институты в крупных городах перегружены, так как им отправляют самые разные запросы со всех уголков страны.
- Иногда пациенты напрямую обращаются к врачам-онкологам для консультации.
- Для проведения онлайн-консультации между врачами и пациентами используются такие инструменты, как `электронная почта` и `ТелеМед`.
- Однако оба эти инструмента не приспособлены для проведения онлайн-консультаций и хранения и обработки данных пациентов.
- Кроме того, из-за высокой загруженности врачи в институтах/центрах могут вовремя не проанализировать критические случаи.

#### 1.2 Выявленные проблемы

- У врачей-онкологов нет удобного инструмента для проведения онлайн-консультаций.
- Врачам необходим инструмент для ускорения принятия решений, так как в такой сфере, как онкология, очень важно вовремя отследить изменения опухоли.
- Молодым врчам требуется много времени для анализа более 200 изображений.

#### 1.3 Цель и задачи

Цель – разработать инструмент для взаимодейтсвия врачей и пациентов, в который будут интегрированы системы классификации изображений (есть/нет опухоли) и сегментации опухолей.

Задачи:
- запустить MVP,
- отдать MVP на тестирования заказчикам,
- доработать MVP с учетом ввода новых видов опухолей.

#### 1.4 Бизнес-требования и ограничения

Использование ML позволит ускорить процесс принятия врачом решения.

##### Работаем с МРТ-снимками головного мозга

Бизнес-требования:
- снимки загружаются в трекер пациентом,
- создается тикет пациента на врача,
- использование ML ни в коем случае __не призвано заменить врача__,
- результаты работы ML моделей __не будут показываться пациентам__.

##### C4 Context Level

![C4 Context Level](https://github.com/bs-muu/.github/blob/main/images/ai-screen-it-C4_Context_-_For_Presentation.drawio.png)

##### Трекер пациентов

Бизнес-требования:
- удобство UI-UX для врача,
- система уведомлений,
- модель прав доступа RBAC,
- реакции +1 / -1 на коммент для фидбека модели,
- наличие вебхуков / API,
- внешний логин на базе OAuth2 / OpenID,
- свободная коммерческая лицензия,
- открытый исходный код.

Врач и пациент будут взамодействовать через трекер. Врач будет создавать для конкрентного пациента "проект", затем будет отправлять приглашение пациенту в этот проект. Пациент сможет выложить в проект свой МРТ-снимок, который автоматически будет проанализирован ML моделями.

### 2. Методология

#### 2.1 Постановка задачи CV

Решение задачи:
- __классификации__ изображений,
- семантической __сегментации__ для попиксельной обработки изображений.

Классификация изобажений необходима для:
- фильтрации нерелевантных изображений для обучения модели сегментации,
- выделения снимка, на который стоит обратить внимание в первую очередь.

Сегментация изображений необходима для:
- проверки и визуализации пациенту снимка с подозрением,
- оценки динамики изменения опухоли,
- ранжирования спорных снимков.

#### 2.2 Постановка задачи DE

1. Multimodal Data.
2. Domain Data.
3. Interdisciplinary Teamwork.

1. Dataset.
2. Database.
3. Schema.
4. Data Service.
5. Data Benchmark.

1. Visualisation of patterns.
2. Cubes.
3. Charts.
4. Tables.
5. Graphs.

1. Relevant and clear domain-specific task.
2. Data is really a problem: complex structure, multimodal data, heterogeneous, multiple sources, dirty data or unlabeled data.
3. Simple solution (prototype of service) can be useful for end users to work with data.
4. Interdisciplinary team with truly complementary backgrounds.

1. Domain-specific task defined.
2. Analysis (summarization) of the frontier of scientific work and applied
3. Solutions on a domain-specific problem was carried out.
4. Analysis of data sources, structure and requirements for the dataset for the task was carried out.
5. Collected our own dataset from various sources.
6. A service (prototype or working solution) for storing, processing and presenting data has been developed.
7. A benchmark was made for the task, open machine learning models or data analysis algorithms were tested.

#### 2.2 Этапы решения задачи

1. Analyze the domain, problems and solutions using data in the domain.
2. Decompose tasks for working with data in the domain, determine data requirements.
3. Collect datasets, determine data quality and create data benchmarks.
4. Prototype and implement services for data storage, access and processing.
5. Work in an interdisciplinary team.

### 3. Прототип

#### 3.1 Критерий успешности решения

Успешным прототип будет считаться после получения положительной обратной связи от врачей после первого тестирования.

#### 3.2 Архитектура решения

##### Activity Diagram

![Activity Diagram](https://github.com/bs-muu/.github/blob/main/images/ai-screen-it-Activity%20diagram.drawio.png)  

##### C4 Context Level

![C4 Context Diagraml](https://github.com/bs-muu/.github/blob/main/images/ai-screen-it-C4_Context_-_For_Presentation.drawio.png)

##### C4 Container Level

![C4 Container Diagram](https://github.com/bs-muu/.github/blob/main/images/ai-screen-it-C4%20Container.drawio.png)

#### 3.3 Безопасность данных

- Так как у нас ведется работа с персональными данными пациентов, мы понимаем важность зашиты персональных данных.
- Вся работа у нас ведется на нашем собственном сервере. Данные пациентов зашифрованы.

### 4. Команда проекта

#### 4.1 Менторы

| Имя Фамилия | Должность |
| ------------- | ------------- |
| Рамиль Зайнуллин  | Инициатор-куратор проекта |
| Дмитрий Головин  | Архитектор-разработчик ПО  |
| Эндже Валиахметова | Врач нейроонколог НМИЦ им. Бурденко |
| Людмила Ясько | Старший научный сотрудник лаборатории молекулярной биологии НМИЦ ДГОИ |

#### 4.2 Студенты 1 курса AI Talent Hub

| Имя Фамилия | Должность |
| ------------- | ------------- |
| Артем Даняев | ML Engineer |
| Михаил Бекусов | ML Engineer |
| Константин Калиновский | ML Engineer |
| Александр Лакиза | Product Owner |
| Сергей Китаев | Full-stack Engineer |
| Андрей Павлов | Data Engineer |

### 5. Полезные материалы

- [Презентация 18.12.2023 на проектном семинаре](https://docs.google.com/presentation/d/1jmd8ZPJN2W_otuVlJMtpkSThPnvUJVPi6uIuxa3TRTQ/edit?usp=sharing)
- [Презентация 20.01.2024 на демо-день AI Talent Hub](https://docs.google.com/presentation/d/1SEVVAZcO-8JxKyr8NNUuodzam3GrQbnGUFPHpfWr8wo/edit?usp=sharing)
- [Пример работы](https://github.com/bs-muu/.github/assets/115554194/b15063e3-66cc-46f6-ba52-5f91288ef43b)
