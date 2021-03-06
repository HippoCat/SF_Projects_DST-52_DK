# SF_Projects_DST-52_DK/module_02_EDA

В этом репозитории хранится решениe "Проект 2. Разведывательный анализ данных".

Проект UNICEF — международного подразделения ООН, чья миссия состоит в повышении уровня благополучия детей по всему миру. 

Суть проекта — отследить влияние условий жизни учащихся в возрасте от 15 до 22 лет на их успеваемость по математике, чтобы на ранней стадии выявлять студентов, находящихся в группе риска.

Дмитрий Кузнецов, поток DST-52 (SkillFactory), 29-31 Марта 2021



## Рекомендованная последовательность действий от организаторов

>1. Проведите первичную обработку данных. Так как данных много, стоит написать функции, которые можно применять к столбцам определённого типа.
>2. Посмотрите на распределение признака для числовых переменных, устраните выбросы.
>3. Оцените количество уникальных значений для номинативных переменных.
>4. По необходимости преобразуйте данные
>5. Проведите корреляционный анализ количественных переменных
>6. Отберите не коррелирующие переменные.
>7. Проанализируйте номинативные переменные и устраните те, которые не влияют на предсказываемую величину (в нашем случае — на переменную score).
>8. Не забудьте сформулировать выводы относительно качества данных и тех переменных, которые вы будете использовать в дальнейшем построении модели.



## Реальная последовательность анализа

 1. Загрузил датасет, первично изучил его при помощи функций display(), info(), и т.д.
 2. Разработал или позаимствовал несколько функций для анализа и преобразования данных в колонках
 3. Рассмотрел в отдельности каждую из 30 колонок
 4. Отбросил выбросы и заполнил пропуски
 5. Для каждой колонки построил гистограмму для визуализации распределения
 6. Отметил предварительные заключения о распределении для каждой колонки
 7. После очистки данных от выбросов и пропусков посчитал предварительный анализ законченым 
 8. Далее приступил к анализу зависимости уровня 'score' успеваемости от различных параметров
 9. Для анализа построил графики типа boxplot для каждой колонки для визуализации
 10. На основании анализа графиков boxplot выбрал те категориальные признаки, которые оказывают влияние на успеваемость
 11. Провел корреляционный анализ числовых столбцов, использовал для наглядности матрицу корреляций
 12. Сделал вывод о влиянии количественых признаков на успеваемость 'score'
 13. Подготовил заключение с перечнем признаков, оказывающих влияние на успеваемость 'score'
 14. Предложил использовать влияющие признаки для построения модели в дальнейшем



## Заключения


### 1. Номинативные признаки для дальнейшего включения в модель

- __school__ — аббревиатура школы, в которой учится ученик;
- __sex__ — пол ученика ('F' - женский, 'M' - мужской) - юноши в среднем получают более высокие оценки;
- __mjob/fjob__ - работа родителей. Примечательно, что лучше успевают студенты у которых либо мать работает в сфере здравоохранения, либо отец работает учителем;
- __reason__ — причина выбора школы - выбравшие школу за репутацию учаться лучше;
- __schoolsup__ — дополнительная образовательная поддержкаЧем больше дополнительная образовательная поддержка в школе, тем ниже успеваемость. Странно, поскольку выглядит как "не в коня корм";
- __higher__ — хочет получить высшее образование.

Остальные признаки не оказывают существенного влияние на уровень оценок __score__.


### 2. Числовые столбцы - обзор корреляционой матрицы

Сразу исключил из рассмотрения как малозначащие следующие числовые столбцы: __traveltime__, __famrel__ и __freetime__.

- заметная положительная корреляция между уровнем образования матери и отца __medu/fedu__. Для модели имеет смысл вывести одну величину - уровень образования в семье;
- положительная корреляция влияния уровня образования каждого из родителей позволяет предположить, что и общий уровень образования родителей будет положительно коррелировать с успеваемостью 'score';
- __age__ молодые успевают лучше, чем возрастные;
- также видна отрицателная корреляция между __studytime__ и __studytime, granular__, что позволяет предложить исключить одну из переменных при пострении модели;
- также видно положительное влияние параметра __studytime__ на успехи в учебе;
- параметры __failures__ и __goout__ снижают успеваемость. 

### 3. Общие выводы

Итак, в результате EDA для анализа влияния  условий жизни учащихся в возрасте от 15 до 22 лет на оценку по математике были получены следующие выводы:

- В данных достаточно мало пустых значений, как правило не более 10%. Пропуски были заполны случайным образом;
- Выбросы найдены в единичных количествах и были либо удалены (не более 5% данных), либо исправлены на значения согласно здравому смыслу;
- Отрицательная корреляция параметра __studytime__ и __studytime, granular__ может говорить о том, эти два параметра обратно пропорциональны друг другу; 
- Наиболее важные категориальные параметры, которые предлагается использовать в дальнейшем для построения модели:
    - __school__
    - __sex__
    - __mjob/fjob__ 
    - __reason__
    - __schoolsup__
    - __higher__
- Наиболее важные числовые столбцы, которые предлагается использовать в дальнейшем для построения модели:
    - __medu/fedu__
    - __age__
    - __studytime__
    - __failures__
    - __goout__

### 4. Комментарии на будущее

Что можно улучшать:

1. Качество написания функций - более аккуратно и универсально обрабатывать колонки разных типов;
2. Автоматизировать процесс обработки колонок используя функцию из п. 1;
3. Провести тест Стьюдента, который в данной работе практически не реализован по причине цейтнота;
4. Отводить на проект более 3-х дней, желательно не менее недели;
5. Продумать функцию, которая будет заменять пропуски не просто рандомно, а пропорционально имеющимся значениям. Таким образом будет вноситься меньше искажений в распределение.






Буду рад любой обратной связи, замечаниям и конструктивной критике об этом проекте, как от команды курса SkillFactory, так и от коллег однокурсников.

Заранее благодарен.

Д.К.
31 Марта 2021, 18:00