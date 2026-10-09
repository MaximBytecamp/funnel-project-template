# Тема 10, часть 2 · Data Studio: GA4 и заявки

**Презентация:** https://algorthimization-course-vvodnoe.vercel.app/op03-informacionnye-tehnologii/lessons/10-data-studio/index.html

**Материалы:** https://algorthimization-course-vvodnoe.vercel.app/op03-informacionnye-tehnologii/lessons/10-data-studio/materials.html

**Файлы занятия:** [materials/tema-10-2-data-studio](../materials/tema-10-2-data-studio/) —
спецификация отчёта, формулы, таблица сверки, чек-лист.

## Содержание лекции

**Data Studio** (прежнее название — Looker Studio) — сервис Google для
отчётов и дашбордов. Он подключается к источникам данных и строит
по ним диаграммы, которые обновляются сами. В теме собирается один отчёт
из двух источников: GA4 (трафик и события) и лист `leads` (реальные
заявки).

### Три страницы отчёта

| Страница | Источник | Что на ней |
|---|---|---|
| Page 1 · Трафик | GA4 | Sessions, Active users, GA4 Lead Events; динамика по дням; таблицы source, campaign, content; устройства; фильтры периода |
| Page 2 · Заявки | Google Sheets, лист `leads` | Lead Count, заявки по статусам, источникам и датам; свои фильтры |
| Page 3 · Сопоставление | Blend из GA4 и Sheets | Sessions и заявки по паре source + campaign, Actual Leads / Sessions |

### Подготовка источника Sheets

Перед подключением проверяют: у каждой заявки непустой уникальный
`request_id`, `created_at` распознан как дата, статусы записаны одинаково.
Число заявок считают как `COUNT_DISTINCT(request_id)`. Заявки со статусом
`done` — условный `COUNT_DISTINCT` через `CASE`.

### Blend — объединение источников

**Blend** соединяет две таблицы по общим ключам, как `JOIN` в базах данных.
Здесь слева GA4 Traffic, справа Sheets Leads, ключи — Source и Campaign,
тип соединения **Left Outer**: сохраняются все строки GA4.

- Если у строки GA4 нет пары в Sheets, в столбце заявок стоит `NULL`.
  Это отсутствие совпадения; называть его нулём можно только после проверки.
- Заявки без пары в GA4 в Blend не попадают и учитываются на Page 2.
- Если добавить в Dimensions лишнее поле (статус, устройство), строки
  размножатся и Sessions посчитаются несколько раз. В лекции на модели
  180 Sessions превращались в 280, 360 или 540.
- Событие `generate_lead` подключают третьей таблицей того же источника
  GA4 с фильтром внутри неё; трафик в первой таблице не фильтруется.

### Проверка и доступ

`Actual Leads / Sessions` — отношение двух сумм. Долей сеансов,
закончившихся заявкой, его называть нельзя. Active users нельзя складывать по кампаниям:
один человек мог прийти из нескольких. Каждую цифру Blend сверяют
с исходниками.

Доступ к отчёту (Share) и доступ к данным (Data credentials) настраиваются
отдельно. Имя и email на дашборд не выводятся; скрытое поле в диаграмме
остаётся доступным в источнике. Роль Editor выдают только тем, кто
редактирует отчёт.

## Что делали на занятии

1. Записали ресурс GA4, таблицу, период и часовой пояс в `dashboard-spec.md`.
2. Собрали Page 1 из GA4 с KPI, динамикой, таблицами и фильтрами.
3. Подключили лист `leads`, проверили типы и создали Lead Count и Done Count.
4. Собрали Page 2 со своими фильтрами.
5. Собрали Blend по Source + Campaign, добавили третью таблицу для
   `generate_lead`.
6. Сверили каждую пару с исходниками и заполнили `reconciliation.csv`.
7. Проверили фильтры, периоды, права доступа.

## Что вошло в проект

- Отчёт Data Studio из трёх страниц на своих данных GA4 и своей таблице
  заявок.
- Таблица сверки GA4 и заявок — подготовка к сверке трёх источников
  в разделе 4 курса.

## Документация

- [Data Studio: обзор](https://docs.cloud.google.com/data-studio/welcome)
- [Подключение GA4](https://docs.cloud.google.com/data-studio/connect-to-google-analytics)
- [Подключение Google Sheets](https://docs.cloud.google.com/data-studio/connect-to-google-sheets)
- [Создание Blend](https://docs.cloud.google.com/data-studio/create-edit-and-manage-blends)
- [Агрегация в Blend](https://docs.cloud.google.com/data-studio/blending-tips-and-advanced-concepts)
- [COUNT_DISTINCT](https://docs.cloud.google.com/data-studio/countdistinct)
- [PARSE_DATETIME](https://docs.cloud.google.com/data-studio/parsedatetime)
- [CASE](https://docs.cloud.google.com/data-studio/case-searched)
- [Агрегация](https://docs.cloud.google.com/data-studio/aggregation-article)
- [Controls](https://docs.cloud.google.com/data-studio/about-controls)
- [Data credentials](https://docs.cloud.google.com/data-studio/data-credentials)
- [Ошибки и квоты](https://docs.cloud.google.com/data-studio/troubleshooting-guide)
