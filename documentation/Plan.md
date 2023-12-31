# План автоматизации тестирования сервиса покупки туров

---

## Предусловие выполнения сценария:
1. Скачать проект с Github (https://github.com/Andrey-Shelikhanov/Diploma.QA.Engineer) командой git clone
2. Открыть проект в IntelliJ IDEA
3. Запустить SUT (System Under Test) 
4. Открыть страницу покупки тура по ссылке http://localhost:8080 (ссылка на страницу доступна только при запущенном SUT).

## Валидными данными при заполнении полей формы приняты:

1. Номер карты: 16 цифр
2. Месяц: число от 01 до 12. Но не ранее текущего месяца, в случае если в поле “Год” указан текущий год
3. Год: две последние цифры текущего или последующих годов
4. Владелец: Фамилия и Имя на латинице через пробел
5. СVC/CVV: три цифры

## Номера карт, используемых для тестирования:

- Номер валидной карты: "4444 4444 4444 4441" статус карты "APPROVED"
- Номер не валидной карты: "4444 4444 4444 4442" статус карты "DECLINED"

## Перечень автоматизируемых сценариев:

---
**Позитивные сценарии**

---
### Сценарий 1
*Заявка "Оплата по карте", заполненная валидными данными карты со статусом *Approved* успешно одобрена банком*

**Шаги:**

1. В браузере перейти по адресу http://localhost:8080
2. Нажать кнопку "Купить"
3. Проверить название формы "Оплата по карте"
4. В поле "Номер карты" ввести: 4444 4444 4444 4441
5. В поле "Месяц" ввести: 08
6. В поле "Год" ввести: 23
7. В поле "Владелец" ввести: Ivanov Ivan
8. В поле "CVC/CVV" ввести: 111
9. Нажать кнопку "Продолжить"

**Ожидаемый результат:**
Оплата проходит. Выведено сообщение "Успешно. Операция одобрена банком." Запись в БД информации о совершенной покупке со статусом “APPROVED” в соответствующие таблице

### Сценарий 2
*Заявка "Оплата по карте", заполненная данными карты со статусом *Declined* отклонена банком*

**Шаги:**

1. В браузере перейти по адресу http://localhost:8080
2. Нажать кнопку "Купить"
3. Проверить, что название формы - "Оплата по карте"
4. В поле "Номер карты" ввести: 4444 4444 4444 4442
5. В поле "Месяц" ввести: 08
6. В поле "Год" ввести: 23
7. В поле "Владелец" ввести: Ivanov Ivan
8. В поле "CVC/CVV" ввести: 111
9. Нажать кнопку "Продолжить"

**Ожидаемый результат:**
Покупка отклонена, вывод системного сообщения “Ошибка! Банк отказал в проведении операции”. Запись в БД информации об отклонении операции покупки со статусом “DECLINED” в соответствующие таблице

### Сценарий 3
*Отправка формы заявки, в которой поле "Владелец" содержит значение введенное в верхнем регистре. Остальные поля заполнены валидными данными.*

**Шаги:**

1. В браузере перейти по адресу http://localhost:8080
2. Нажать кнопку "Купить"
3. Проверить, что название формы - "Оплата по карте"
4. В поле "Номер карты" ввести: 4444 4444 4444 4441 
5. В поле "Месяц" ввести: 08
6. В поле "Год" ввести: 23
7. Поле "Владелец" ввести: IVANOV IVAN
8. В поле "CVC/CVV" ввести: 111
9. Нажать кнопку "Продолжить"

*Ожидаемый результат:*
Выведено сообщение "Успешно. Операция одобрена банком!". Происходит запись в БД информации о совершенной покупке

### Сценарий 4
*Отправка формы заявки, в которой поле "Владелец" содержит значение через дефис. Остальные поля формы содержат валидные данные.*

**Шаги:**

1. В браузере перейти по адресу http://localhost:8080
2. Нажать кнопку "Купить"
3. Проверить, что название формы - "Оплата по карте"
4. В поле "Номер карты" ввести: 4444 4444 4444 4441 
5. В поле "Месяц" ввести: 08
6. В поле "Год" ввести: 23
7. Поле "Владелец" ввести: Rimsky-Korsakov Ivan
8. В поле "CVC/CVV" ввести: 111
9. Нажать кнопку "Продолжить"

*Ожидаемый результат:*
Выведено сообщение "Успешно. Операция одобрена банком!". Происходит запись в БД информации о совершенной покупке

---
**Негативные сценарии**

---
### Сценарий 1

*Заявка "Оплата по карте", заполненная данными карты, отсутствующими в БД банка, отклонена банком*

**Шаги:**

1. В браузере перейти по адресу http://localhost:8080
2. Нажать кнопку "Купить"
3. Проверить, что название формы - "Оплата по карте"
4. В поле "Номер карты" ввести: 7777 7777 7777 7777
5. В поле "Месяц" ввести: 08
6. В поле "Год" ввести: 23
7. В поле "Владелец" ввести: Ivanov Ivan
8. В поле "CVC/CVV" ввести: 111
9. Нажать кнопку "Продолжить"

**Ожидаемый результат:**
Появляется сообщение "Ошибка! Банк отказал в проведении операции". Запись в БД информации о совершенных операциях не происходит.

### Сценарий 2
*Отправка формы заявки с пустым полем "Номер карты". Остальные поля формы заполнены валидными значениями*

**Шаги:**

1. В браузере перейти по адресу http://localhost:8080
2. Нажать кнопку "Купить"
3. Проверить, что название формы - "Оплата по карте"
4. В поле "Номер карты" ввести: 
5. В поле "Месяц" ввести: 08
6. В поле "Год" ввести: 23
7. В поле "Владелец" ввести: Ivanov Ivan
8. В поле "CVC/CVV" ввести: 111
9. Нажать кнопку "Продолжить"

**Ожидаемый результат:**
Форма заявки не отправляется. Появляется индикация "Неверный формат" под полем "Номер карты". Запись в БД информации о совершенных операциях не происходит.

### Сценарий 3
*Отправка формы заявки, в которой поле "Номер карты" содержит одну цифру. Остальные поля формы заполнены валидными данными*

**Шаги:**

1. В браузере перейти по адресу http://localhost:8080
2. Нажать кнопку "Купить"
3. Проверить, что название формы - "Оплата по карте"
4. В поле "Номер карты" ввести: 1
5. В поле "Месяц" ввести: 08
6. В поле "Год" ввести: 23
7. В поле "Владелец" ввести: Ivanov Ivan
8. В поле "CVC/CVV" ввести: 111
9. Нажать кнопку "Продолжить"

**Ожидаемый результат:**
Форма заявки не отправляется. Появляется индикация "Неверный формат" под полем "Номер карты". Запись в БД информации о совершенных операциях не происходит.

### Сценарий 4
*Отправка формы заявки, в которой поле "Номер карты" содержит 15 цифр. Остальные поля формы заполнены валидными данными*

**Шаги:**

1. В браузере перейти по адресу http://localhost:8080
2. Нажать кнопку "Купить"
3. Проверить, что название формы - "Оплата по карте"
4. В поле "Номер карты" ввести: 4444 4444 4444 444
5. В поле "Месяц" ввести: 08
6. В поле "Год" ввести: 23
7. В поле "Владелец" ввести: Ivanov Ivan
8. В поле "CVC/CVV" ввести: 111
9. Нажать кнопку "Продолжить"

**Ожидаемый результат:**
Форма заявки не отправляется. Появляется индикация "Неверный формат" под полем "Номер карты". Запись в БД информации о совершенных операциях не происходит.

### Сценарий 5
*Отправка формы заявки, в которой поле "Месяц" пустое. Остальные поля формы заполнены валидными данными.*

**Шаги:**

1. В браузере перейти по адресу http://localhost:8080
2. Нажать кнопку "Купить"
3. Проверить, что название формы - "Оплата по карте"
4. В поле "Номер карты" ввести: 4444 4444 4444 4441
5. В поле "Месяц" ввести:
6. В поле "Год" ввести: 23
7. Поле "Владелец" ввести: Ivanov Ivan
8. В поле "CVC/CVV" ввести: 111
9. Нажать кнопку "Продолжить"

**Ожидаемый результат:**
Форма заявки не отправляется. Появляется индикация "Неверный формат" под полем "Месяц". Запись в БД информации о совершенных операциях не происходит.

### Сценарий 6

*Отправка формы заявки, в которой поле "Месяц" содержит значение больше 12. Остальные поля формы заполнены валидными данными.*

**Шаги:**

1. В браузере перейти по адресу http://localhost:8080
2. Нажать кнопку "Купить"
3. Проверить, что название формы - "Оплата по карте"
4. В поле "Номер карты" ввести: 4444 4444 4444 4441
5. В поле "Месяц" ввести: 13
6. В поле "Год" ввести: 23
7. Поле "Владелец" ввести: Ivanov Ivan
8. В поле "CVC/CVV" ввести: 111
9. Нажать кнопку "Продолжить"

**Ожидаемый результат:**
Форма заявки не отправляется. Появляется индикация "Неверно указан срок действия карты" под полем "Месяц". Запись в БД информации о совершенных операциях не происходит.

### Сценарий 7
*Отправка формы заявки, в которой поле "Месяц" меньше значения "01". Остальные поля формы заполнены валидными данными.*

**Шаги:**

1. В браузере перейти по адресу http://localhost:8080
2. Нажать кнопку "Купить"
3. Проверить, что название формы - "Оплата по карте"
4. В поле "Номер карты" ввести: 4444 4444 4444 4441
5. В поле "Месяц" ввести: 00
6. В поле "Год" ввести: 23
7. Поле "Владелец" ввести: Ivanov Ivan
8. В поле "CVC/CVV" ввести: 111
9. Нажать кнопку "Продолжить"

**Ожидаемый результат:**
Форма заявки не отправляется. Появляется индикация "Неверно указан срок действия карты" под полем "Месяц". Запись в БД информации о совершенных операциях не происходит.


### Сценарий 8
*Отправка формы заявки, в которой поле "Месяц" содержит значение предыдущее от текущего. Остальные поля формы заполнены валидными данными.*

**Шаги:**

1. В браузере перейти по адресу http://localhost:8080
2. Нажать кнопку "Купить"
3. Проверить, что название формы - "Оплата по карте"
4. В поле "Номер карты" ввести: 4444 4444 4444 4441
5. В поле "Месяц" ввести: 07
6. В поле "Год" ввести: 23
7. Поле "Владелец" ввести: Ivanov Ivan
8. В поле "CVC/CVV" ввести: 111
9. Нажать кнопку "Продолжить"

**Ожидаемый результат:**
Форма заявки не отправляется. Появляется индикация "Неверно указан срок действия карты" под полем "Месяц".


### Сценарий 9
*Отправка формы заявки, в которой поле "Год" пустое. Остальные поля формы заполнены валидными данными.*

**Шаги:**

1. В браузере перейти по адресу http://localhost:8080
2. Нажать кнопку "Купить"
3. Проверить, что название формы - "Оплата по карте"
4. В поле "Номер карты" ввести: 4444 4444 4444 4441
5. В поле "Месяц" ввести: 08
6. В поле "Год" ввести: 
7. Поле "Владелец" ввести: Ivanov Ivan
8. В поле "CVC/CVV" ввести: 111
9. Нажать кнопку "Продолжить"

**Ожидаемый результат:**
Форма заявки не отправляется. Появляется индикация "Неверный формат". Запись в БД информации о совершенных операциях не происходит.


### Сценарий 10
*Отправка формы заявки, в которой поле "Год" содержит значение соответствующее любому предыдущему году. Остальные поля формы заполнены валидными данными.*

**Шаги:**

1. В браузере перейти по адресу http://localhost:8080
2. Нажать кнопку "Купить"
3. Проверить, что название формы - "Оплата по карте"
4. В поле "Номер карты" ввести: 4444 4444 4444 4441
5. В поле "Месяц" ввести: 08
6. В поле "Год" ввести: 22
7. Поле "Владелец" ввести: Ivanov Ivan
8. В поле "CVC/CVV" ввести: 111
9. Нажать кнопку "Продолжить"

**Ожидаемый результат:**
Форма заявки не отправляется. Появляется индикация "Истек срок действия карты". Запись в БД информации о совершенных операциях не происходит.


### Сценарий 11
*Отправка формы заявки, в которой поле "Год" содержит значение +10 лет к текущему значению года. Остальные поля формы заполнены валидными значениями.*

**Шаги:**

1. В браузере перейти по адресу http://localhost:8080
2. Нажать кнопку "Купить"
3. Проверить, что название формы - "Оплата по карте"
4. В поле "Номер карты" ввести: 4444 4444 4444 4441
5. В поле "Месяц" ввести: 08
6. В поле "Год" ввести: 33
7. Поле "Владелец" ввести: Ivanov Ivan
8. В поле "CVC/CVV" ввести: 111
9. Нажать кнопку "Продолжить"

**Ожидаемый результат:**
Форма заявки не отправляется. Появляется индикация «Неверно указан срок действия карты» под полем "Год".

### Сценарий 12
*Отправка формы заявки, в которой поле "CVC/CVV" пусто. Остальные поля формы заполнены валидными значениями.*

**Шаги:**

1. В браузере перейти по адресу http://localhost:8080
2. Нажать кнопку "Купить"
3. Проверить, что название формы - "Оплата по карте"
4. В поле "Номер карты" ввести: 4444 4444 4444 4441
5. В поле "Месяц" ввести: 08
6. В поле "Год" ввести: 23
7. Поле "Владелец" ввести: Ivanov Ivan
8. В поле "CVC/CVV" ввести:
9. Нажать кнопку "Продолжить"

*Ожидаемый результат:*
Форма заявки не отправляется. Появляется индикация "Неверный формат" под полем "CVC/CVV". Запись в БД информации о совершенных операциях не происходит.


### Сценарий 13
*Отправка формы заявки, в которой поле "CVC/CVV" содержит 1 цифру. Остальные поля формы заполнены валидными значениями.*

*Шаги:*

1. В браузере перейти по адресу http://localhost:8080
2. Нажать кнопку "Купить"
3. Проверить, что название формы - "Оплата по карте"
4. В поле "Номер карты" ввести: 4444 4444 4444 4441
5. В поле "Месяц" ввести: 08
6. В поле "Год" ввести: 23
7. Поле "Владелец" ввести: Ivanov Ivan
8. В поле "CVC/CVV" ввести: 1
9. Нажать кнопку "Продолжить"

*Ожидаемый результат:*
Форма заявки не отправляется. Появляется индикация "Неверный формат" под полем "CVC/CVV". Запись в БД информации о совершенных операциях не происходит.


### Сценарий 14
*Отправка формы заявки, в которой поле "CVC/CVV" содержит 2-е цифры. Остальные поля формы заполнены валидными значениями.*

**Шаги:**

1. В браузере перейти по адресу http://localhost:8080
2. Нажать кнопку "Купить"
3. Проверить, что название формы - "Оплата по карте"
4. В поле "Номер карты" ввести: 4444 4444 4444 4441
5. В поле "Месяц" ввести: 08
6. В поле "Год" ввести: 23
7. Поле "Владелец" ввести: Ivanov Ivan
8. В поле "CVC/CVV" ввести: 22
9. Нажать кнопку "Продолжить"

*Ожидаемый результат:*
Форма заявки не отправляется. Появляется индикация "Неверный формат" под полем "CVC/CVV". Запись в БД информации о совершенных операциях не происходит.

### Сценарий 15
*Отправка формы заявки, в которой поле "Владелец" пустое. Остальные поля формы содержат валидные данные.*

**Шаги:**

1. В браузере перейти по адресу http://localhost:8080
2. Нажать кнопку "Купить"
3. Проверить, что название формы - "Оплата по карте"
4. В поле "Номер карты" ввести: 4444 4444 4444 4441 
5. В поле "Месяц" ввести: 08
6. В поле "Год" ввести: 23
7. Поле "Владелец" ввести:
8. В поле "CVC/CVV" ввести: 111
9. Нажать кнопку "Продолжить"

*Ожидаемый результат:*
Форма заявки не отправляется. Появляется индикация "Поле обязательно для заполнения" под полем "Владелец". Запись в БД информации о совершенных операциях не происходит.

### Сценарий 16
*Отправка формы заявки, в которой поле "Владелец" содержит фамилию на латинице, а имя отсутствует. Остальные поля формы заполнены валидными данными.*

**Шаги:**

1. В браузере перейти по адресу http://localhost:8080
2. Нажать кнопку "Купить"
3. Проверить, что название формы - "Оплата по карте"
4. В поле "Номер карты" ввести: 4444 4444 4444 4441 
5. В поле "Месяц" ввести: 08
6. В поле "Год" ввести: 23
7. Поле "Владелец" ввести: Ivanov
8. В поле "CVC/CVV" ввести: 111
9. Нажать кнопку "Продолжить"

*Ожидаемый результат:*
Форма заявки не отправляется. Появляется индикация "Неверный формат" под полем "Владелец". Запись в БД информации о совершенных операциях не происходит.

### Сценарий 17
*Отправка формы заявки, в которой поле "Владелец" содержит фамилию и имя на кириллице. Остальные поля формы заполнены валидными данными.*

**Шаги:**

1. В браузере перейти по адресу http://localhost:8080
2. Нажать кнопку "Купить"
3. Проверить, что название формы - "Оплата по карте"
4. В поле "Номер карты" ввести: 4444 4444 4444 4441 
5. В поле "Месяц" ввести: 08
6. В поле "Год" ввести: 23
7. Поле "Владелец" ввести: Иванов Иван
8. В поле "CVC/CVV" ввести: 111
9. Нажать кнопку "Продолжить"

*Ожидаемый результат:*
Форма заявки не отправляется. Появляется индикация "Неверный формат" под полем "Владелец". Запись в БД информации о совершенных операциях не происходит.

### Сценарий 18
*Отправка формы заявки, в которой поле "Владелец" заполнено цифрами. Остальные поля формы заполнены валидными данными*

**Шаги:**

1. В браузере перейти по адресу http://localhost:8080
2. Нажать кнопку "Купить"
3. Проверить, что название формы - "Оплата по карте"
4. В поле "Номер карты" ввести: 4444 4444 4444 4441 
5. В поле "Месяц" ввести: 08
6. В поле "Год" ввести: 23
7. Поле "Владелец" ввести: 12345 12345
8. В поле "CVC/CVV" ввести: 111
9. Нажать кнопку "Продолжить"

*Ожидаемый результат:*
Форма заявки не отправляется. Появляется индикация "Неверный формат" под полем "Владелец". Запись в БД информации о совершенных операциях не происходит.

### Сценарий 19
*Оправка формы заявки, в которой поле "Владелец" заполнено спец. символами. Остальные поля формы заполнены валидными данными.*

**Шаги:**

1. В браузере перейти по адресу http://localhost:8080
2. Нажать кнопку "Купить"
3. Проверить, что название формы - "Оплата по карте"
4. В поле "Номер карты" ввести: 4444 4444 4444 4441 
5. В поле "Месяц" ввести: 08
6. В поле "Год" ввести: 23
7. Поле "Владелец" ввести: 

       ~-+/*?><|@#$%^&()
8. В поле "CVC/CVV" ввести: 111
9. Нажать кнопку "Продолжить"

*Ожидаемый результат:*
Форма заявки не отправляется. Появляется индикация "Неверный формат" под полем "Владелец". Запись в БД информации о совершенных операциях не происходит.

***По аналогии с кнопкой "Купить" протестировать все позитивные (1-4) и негативные сценарии (1-19) для кнопки "Купить в кредит".***

# API тесты

---

## Запросы (через Postman):

    - Отправка POST запроса "купить" с валидным body и карты со статусом APPROVED
    Ожидаемый результат: ответ сервера - код 200, запись в БД со статус карты APPROVED.

    - Отправка POST запроса "купить" с валидным body и карты со статусом DECLINED	
    Ожидаемый результат: ответ сервера - код 200, запись в БД со статусом карты DECLINED.

    - Отправка POST запроса "купить в кредит" с валидным body и карты со статусом APPROVED
    Ожидаемый результат: ответ сервера - код 200, запись в БД со статус карты APPROVED

    - Оправка POST запроса "купить в кредит" с валидным body и карты со статусом DECLINED	
    Ожидаемый результат: ответ сервера - код 200, запись в БД со статусом карты DECLINED.

## Перечень используемых инструментов:
| **Инструмент**|                                                          **Обоснование выбора**                                                           |
|:---: |:-----------------------------------------------------------------------------------------------------------------------------------------:|
|JDK 11 |              Программный пакет, который нужен для создания Java-приложений, т.к. потребуются инструменты работающие с Java.               |
|IntelliJ IDEA|                                                   Удобная среда подготовки авто-тестов.                                                   |
|Gradle|                                                       Система управление проектами.                                                       |
|JUnit 5 |                                             Платформы для написания автотестов и их запуска.                                              |
|DBeaver|                                              Удобный инструмент для работы с базами данных.                                               |
|Selenide| Фреймворк для процесса автоматизированного тестирования ПО; позволяет комфортно создавать програмный код при тестировании веб-интерфейса. |
|MySQL|                                          Свободная реляционная система управления базами данных.                                          |
|PostgreSQL|                        Свободная объектно-реляционная система управления базами данных с открытым исходным кодом.                         |
|Faker|                       Генерация данных искусственного наполнителя для приложения и его потребностей в тестировании.                       |
|Github|                                                       Хранилище SUT и авто-тестов.                                                        
|Allure|                                     Наглядная визуализация создания отчетов о выполнении авто-тестов.                                     

## Перечень и описание возможных рисков при автоматизации:

-  Трудности при настройке инструментов, необходимых для автоматизированного тестирования (одновременная поддержка 2-х СУБД, запуск контейнеров и SUT);
-  Отсутствие документации на тестируемое приложение;
-  Зависимость авто-тестов от текущей реализации веб-элементов (при возможном изменении структуры сайта, в ходе реализации проекта, есть риск что авто-тесты упадут;
-  Отсутствие проверки графической составляющей авто-тестами;
-  Состояние верстки при тех или иных действиях посетителя, комфортность выбранной цветовой схемы оформления и тд.

## Интервальная оценка с учётом рисков (в часах):
- С учётом вышеназванных рисков на автоматизацию требуется ориентировочно, 90 рабочих часов

## План сдачи работ:

- Подготовка к проведению тестирования (запуск SUT, подготовка плана автоматизации) - 9 рабочих часов; ориентировочная дата сдачи 10.08.2023
-  Написание и прогон авто-тестов - 54 рабочих часов; ориентировочная дата сдачи 18.08.2023
-  Составление *Issue* - 9 рабочих часов; ориентировочная дата сдачи 28.06.2023
-  Оформление отчёта по итогам тестирования - 9 рабочих часов; 21.08.2023
-  Оформление отчёта по итогам автоматизации - 9 рабочих часов. 22.08.2023