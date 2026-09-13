# Занятие 1 · Цифровая воронка

**Презентация:** https://algorthimization-course-vvodnoe.vercel.app/op03-informacionnye-tehnologii/lessons/02-cifrovaya-voronka/index.html

**Материалы:**

- вводное занятие курса: https://algorthimization-course-vvodnoe.vercel.app/op03-informacionnye-tehnologii/lessons/01-vvodnaya/index.html
- конспект лекции: https://algorthimization-course-vvodnoe.vercel.app/op03-informacionnye-tehnologii/lessons/02-cifrovaya-voronka/LESSON.md
- учебный стенд с формой заявки: https://algorthimization-course-vvodnoe.vercel.app/op03-informacionnye-tehnologii/lessons/02-cifrovaya-voronka/stend/index.html
- условия исследовательского задания: https://algorthimization-course-vvodnoe.vercel.app/op03-informacionnye-tehnologii/lessons/02-cifrovaya-voronka/RESEARCH_TASK.md

## Что разобрали

- воронка как путь человека от ссылки до заявки;
- действие, событие, заявка и статус: чем они отличаются;
- как событие уходит в аналитику: запрос `collect`, параметры `en`, `ep.*`, `dl`;
- панель Network: фильтр, Preserve log, вкладка Payload;
- точки разрыва: где на пути данные теряются или искажаются.

## Домашнее задание 1

Бланк `homework_01.md`. Срок — до начала занятия 2.

1. Три действия на сайте и события, которые при этом ушли в аналитику:
   обновить страницу (`page_view`), прокрутить до низа (`scroll`), нажать
   на товар.
2. Путь пользователя от ссылки до заявки, пять шагов.
3. Одно место на этом пути, где данные могут потеряться.
4. Скриншоты `screens/01-network.png` и `screens/02-payload.png`.

Сайт: https://shop.merch.google/ — запасные https://habr.com/ru/,
https://www.smashingmagazine.com/, https://css-tricks.com/. Открывать в Chrome
или Edge с выключенным блокировщиком рекламы, иначе запросов не будет видно.

Ветка `hw-01`, запрос на слияние в свою `main`:
[как это сделать кнопками](../docs/git/README.md#6-ветки-на-github-и-pull-request).

## Исследовательское задание

«Как собирают данные без согласия»: файл `research_01.md` в этой папке,
ветка `hw-01-research`, доклад 5–7 минут. Условия — по ссылке выше.
