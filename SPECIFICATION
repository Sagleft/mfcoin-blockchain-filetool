

# Спецификация формата BFF
Blockchain File Format - формат записи файлов в блокчейн криптовалют первого поколения.
## Преобразование произвольного файла в BFF:
1. Кодирование файла в base64;
2. Разделение на фрагменты по 18 символов;
3. Добавление фрагментов с:
	* информацией о версии формата;
	* именем файла;
	* размером файла;
	* метаданные;
	* дополнительные поля;
4. Добавление указателей на тип фрагмента:
	* основные данные;
	* данные о формате;
	* сведения о файле;
5. Преобразование фрагментов в адреса;
6. Создание транзакции;
7. Получение хеша транзакции;

Полученный хеш будет ссылкой на BFF файл.

## Преобразование BFF в файл:
1. Запрос данных о транзакции в JSON от Block Explorer API;
2. Декодирование адресов в фрагменты;
3. Разбор фрагментов по их типу;
4. Установка заголовков;
5. Сборка файла из основных данных;
6. Выдача файла;

Пример преобразования для BFF 1.2.
Пусть есть текстовой файл data.txt вида:
```
..он быстро так вперед стал наступать
И перешел чрез Рубикон так скоро,
Что мы за ним не можем поспевать.
Так с быстротой стрелы иль метеора
Он ринулся в Италию, потом
Внес смерть в Дураццо и с врагом
Так грозно он сразился при Фарсале,
Что даже там, где мутный Нил шумит,
Его удар жестоким услыхали.
```
Перевод в base64:
```
Li7QvtC9INCx0YvRgdGC0YDQviDRgtCw0Log0LLQv9C10YDQtdC0INGB0YLQsNC7INC90LDRgdGC0YPQv9Cw0YLRjArQmCDQv9C10YDQtdGI0LXQuyDRh9GA0LXQtyDQoNGD0LHQuNC60L7QvSDRgtCw0Log0YHQutC+0YDQviwK0KfRgtC+INC80Ysg0LfQsCDQvdC40Lwg0L3QtSDQvNC+0LbQtdC8INC/0L7RgdC/0LXQstCw0YLRjC4K0KLQsNC6INGBINCx0YvRgdGC0YDQvtGC0L7QuSDRgdGC0YDQtdC70Ysg0LjQu9GMINC80LXRgtC10L7RgNCwCtCe0L0g0YDQuNC90YPQu9GB0Y8g0LIg0JjRgtCw0LvQuNGOLCDQv9C+0YLQvtC8CtCS0L3QtdGBINGB0LzQtdGA0YLRjCDQsiDQlNGD0YDQsNGG0YbQviDQuCDRgSDQstGA0LDQs9C+0LwK0KLQsNC6INCz0YDQvtC30L3QviDQvtC9INGB0YDQsNC30LjQu9GB0Y8g0L/RgNC4INCk0LDRgNGB0LDQu9C1LArQp9GC0L4g0LTQsNC20LUg0YLQsNC8LCDQs9C00LUg0LzRg9GC0L3Ri9C5INCd0LjQuyDRiNGD0LzQuNGCLArQldCz0L4g0YPQtNCw0YAg0LbQtdGB0YLQvtC60LjQvCDRg9GB0LvRi9GF0LDQu9C4Lg==
```
Перевод во фрагменты:
```
|0;2               |
|1;text/plain      |
|2;546             |
|3;data.txt        |
%Li7QvtC9INCx0YvRgd%
%GC0YDQviDRgtCw0Log%
%0LLQv9C10YDQtdC0IN%
%GB0YLQsNC7INC90LDR%
%gdGC0YPQv9Cw0YLRjA%
%rQmCDQv9C10YDQtdGI%
%0LXQuyDRh9GA0LXQty%
%DQoNGD0LHQuNC60L7Q%
%vSDRgtCw0Log0YHQut%
%C+0YDQviwK0KfRgtC+%
%INC80Ysg0LfQsCDQvd%
%C40Lwg0L3QtSDQvNC+%
%0LbQtdC8INC/0L7Rgd%
%C/0LXQstCw0YLRjC4K%
%0KLQsNC6INGBINCx0Y%
%vRgdGC0YDQvtGC0L7Q%
%uSDRgdGC0YDQtdC70Y%
%sg0LjQu9GMINC80LXR%
%gtC10L7RgNCwCtCe0L%
%0g0YDQuNC90YPQu9GB%
%0Y8g0LIg0JjRgtCw0L%
%vQuNGOLCDQv9C+0YLQ%
%vtC8CtCS0L3QtdGBIN%
%GB0LzQtdGA0YLRjCDQ%
%siDQlNGD0YDQsNGG0Y%
%bQviDQuCDRgSDQstGA%
%0LDQs9C+0LwK0KLQsN%
%C6INCz0YDQvtC30L3Q%
%viDQvtC9INGB0YDQsN%
%C30LjQu9GB0Y8g0L/R%
%gNC4INCk0LDRgNGB0L%
%DQu9C1LArQp9GC0L4g%
%0LTQsNC20LUg0YLQsN%
%C8LCDQs9C00LUg0LzR%
%g9GC0L3Ri9C5INCd0L%
%jQuyDRiNGD0LzQuNGC%
%LArQldCz0L4g0YPQtN%
%Cw0YAg0LbQtdGB0YLQ%
%vtC60LjQvCDRg9GB0L%
%vRi9GF0LDQu9C4Lg==%
```
Далее преобразование в список адресов на примере MFCoin:
```
MiaU4R6xdmJ27KwcxLUGmPRkJmC79rQoXj
MfpsGDey5aRWUKY9xiKG2Fx4PxTr1z8yzQ
MadykmNfzsAFQ1vmcSqRmAqnLyUyfZKcNH
Madsb3CiVGTgwXddEkBckLq3zo47JcdkXp
MadQ5SeuMYsUmpceNTFWg1v7bTcraGryHo
MadsamTgy9HyMR2zoeXhknoJL7tWqGH5rz
MaeY5REUu26Kp1oGsV4im8HMQvGPs1yXFY
MadQ59Bv6T2TBYejbnAdMje8Uoxups9y6X
MaeaNQV1neKqevDp9ohHcMoqFgsZ8hDzRg
MaeTJHQNe5pMFHbX2DqBK5P5P2LiHoSYMm
MadQ5QwLu5UDgcoZUjrXmEBEq8g5RZa8Je
MaemAc4HBUypCemehzrLic1v2pRKXZN9Un
MadQ5RBcL2kc27HfSi2kYJoJ3QmAzFSVvy
MadnkQ8zxq5GgjCVcK1e6myLUhnVENJEzx
MadQ5RN1Lg4GowpmMJ3Pj6sME53uTNfyGH
MadsamTWNaGnHPvU3PVKcu6NUaL9wK1mHc
MadykDTZqTs9ho77rTYy6orvASoKRQodtG
Mado3VsrpLgRSRC8qQACgjd8P6wQGv88DM
MadQ5RN1LqJkKt7cnCVhLj51DPCtCf3Gnf
Madnjrf8QaQjYTdS9EawacE5MmctgEQYSb
MadQ5TPiQbj98QputDw2K7CGCUr9RKkqo3
MaemAbZkJpYwwY9bva4zYXeSDVoKb9WJo4
MadQ5VEi8oftS2t4A4kEGYyiqVVF79VzAu
MadyeKFyoCv31zNw6AX8Xs1FQu8ZYoUb1H
Maer7ymAxsKGGpd9XAWHrJ6WcnJ3UiRsse
MadniECxzdJdXeifY4dB6XRGSowcUJZu1A
MaeY9m73mfG2B8ZTh4DSMrajEJX2Ba8Lfv
Mado3E8qD6CvPfq7tbGqEUcwmGbaBwXgb8
Madv31MrQzimEmYWM1MVMnbhEXxFQPG6pr
MadQ59BvpMfzf62aCCT8R5hY8DEz1B114R
Maer7yWgc3h3UJ4kLTwMscfqP83QjkngSr
MadsamTgwgMAaAHQbnJFuLT6urUY6anW9k
MadQ8x5Dqe1Z4e8HG4WiLxV28U1kxrATD7
Madp4iyfg9CAQwXmCtUDNUN77doGYAwk3r
MadQ5CWcsNxwR1BA1tkzC1jBP3eesg4Rgu
MadniFjyYxGV7YbsJCJaoFayCBjYxUSof6
MaeoYhW1XRAjFHYMyYDs8ncdCY8Hy4X9Gg
MaeqxXdXLseamyu5uhPdagKRMsa1wSFSjw
MaeXsk5vAEJuGX8ybfiuqb6STW1ZMnUZcq
Mae4SF6KtGcR6p98qJwb6JbtNJGnAjP6YN
Maeoj1h29CRkqUt6NeDV1B4bVvKSfkUztW
Madnk9wAN56MQCaQvZTQnHRLC1huLXcmEM
MaenMDbGsUQH3rLAjkKWw24QgR8vH3Tb5P
```
Далее отправка небольшого числа монет на эти адреса в рамках одной транзакции и получение хеша:
```
10b135524e5f9d47a3f9505d70bb23dd6d6b098ba51d12f7ac99b902127e56fd
```
 
## BFF 1.2
```
%data              %
|0;version         |
|1;mime type       |
|2;size            |
|3;name.ext        |
|4;extras          |
|name.ext          |
^size              ^
```
Где точка с запятой - разделитель.
| - указатель на фрагмент с дополнительной информацией вида:
```
|id;value          |
```
version=2.

## BFF 1.1
Типы фрагментов:
```
%data              %
|name.ext          |
^size              ^
```
Где data - основные данные, name.ext - имя файла, size - размер файла в байтах.
%, |, ^ - указатели на тип фрагмента.
Каждый фрагмент имеет фиксированную длину в 20 байт.
Если фрагмент имеет длину менее 20 байт, добавляются пробелы внутри.
