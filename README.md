# Тестовое задание НВП Болид

Стек: Vue. 
[ТЗ](https://observant-resistance-a1d.notion.site/866da5ab78644fa7a023e024f0f038ea)
[Netlify](https://spontaneous-puffpuff-f517a6.netlify.app)

## Установка

- `npm install` - установка зависимостей
- `npm run serve` - запуск версии для разработки
- `npm run build` - сборка продакт версии

Моя версия Node: 16.13.2

# Что сделано?

- Список всех датчиков со всеми параметрами
- Форма для добавления новых датчиков
- Кнопка для удаления датчиков
- Список датчиков сохраняется в localStorage, что бы не терять информацию при перезагрузке
- Отсутствующие поля датчика не отображаются
- Валидация вводимых данных:
  - Для имени событий, нет никаких ограничений, если поле пустое подставляется "N/A",
  - Для поля температуры, проверка на число (можно и с плавающей точкой)
  - Для поля влажность, проверка на число + проверка на 0 < humidity < 100
- Валидация при обновлении данных датчика:
  - Для имени, проверка на пустое поле,
  - Для температуры на число,
  - Для влажности, на число и интервал
  
