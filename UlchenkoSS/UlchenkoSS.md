Отчёт по лабораторной работе 103. Refactoring
## Выбранный проект
- Репозиторий: https://github.com/Stepan-ul/103-refactoring-exercise.git
- Исходный: https://github.com/SoftwareEngineering2026/103-refactoring-exercise.git
- Язык/папка: python (funding_raised)
- Краткое описание: учебный проект с намеренно плохим кодом — анализ
  стартап-финансирования по CSV (startup_funding.csv).
- Стек: Python 3.x, pytest
## Использованные принципы рефакторинга
- Extract Method — вынос повторяющихся блоков в функции
- Rename — осмысленные имена переменных и методов
- Replace Magic Number/String with Constant
- Guard Clauses — упрощение вложенных условий
- Разделение ответственности (SRP): загрузка данных / аналитика / вывод
## Обнаруженные проблемы
1. Дублирование загрузки CSV — одинаковый блок в функциях where и find_by. Используем Extract Method добовляем метод загрузки CSV _load_rows();
2. Дублирование маппинга row → dict — 10 полей продублированы 5 раз в функциях where и find_by. Используем Extract Method добовляем метод _row_to_dict(row) + именованные индексы колонок;
3. Дублирование фильтрации — 4 почти одинаковых блока if ... in options + цикл + append в функции where. Заменяем на цикл for по FILTER_FIELDS = {field: index};
4. Дублирование поиска первой записи — 4 блока for row ... if ... return mapped в функции find_by.Реализовать find_by через where + next();
5. Магические индексы row[1], row[4], row[9]. Используем Rename и заменяем на именованные константы COL_COMPANY_NAME = 1 и т.п.;
6. Плоская структура — нет разделения ответственности: загрузка, фильтрация, маппинг, поиск в одной функции. SRP: отдельные методы, каждый делает одно;
7. К новым строкам были написаны тесты, проходящие pytest. Тесты помещены в test_refactoring.py.
## Pull Request
PR в оригинальный репозиторий: https://github.com/SoftwareEngineering2026/103-refactoring-exercise/pull/8
