# Отчет по итогам проведенного тестирования.
Было проведено ручное и автоматизированное тестирование веб-приложения покупки тура.
По итогам проведенного тестирования заведены [issues](https://github.com/Andrey-Shelikhanov/Diploma.QA.Engineer/issues) с описанием найденных дефектов.

## Отчёт по итогам автоматизированного тестирования.

В соответствии с [планом](https://github.com/Andrey-Shelikhanov/Diploma.QA.Engineer/blob/main/documentation/Plan.md) было проведено автоматизированное тестирование веб-сервиса покупки тура.

#### В ходе автоматизации тестирования были реализованы:
- позитивные и негативные сценарии тестов;
- реализована поддержка двух баз данных - MySQL и PostgreSQL;
- реализованы тесты, проверяющие корректность внесения информации приложением в базу данных;

*Общее итоги автоматизированного тестирования для MySQL*


|                     | Кол-во тестов | Passed | Failed | Passed, % |
|:--------------------|:-------------:|:------:|:------:|----------:|
| Позитивные сценарии |       8       |   6    |   2    |    75,00% |
| Негативные сценарии |      38       |   30   |   8    |    78,94% |
| APITest             |       4       |   4    |   0    |   100,00% |
| Всего               |      50       |   40   |   10   |    80,00% |


*Общее итоги автоматизированного тестирования для PostgreSQL*


|                     | Кол-во тестов | Passed | Failed | Passed, % |
|:--------------------|:-------------:|:------:|:------:|----------:|
| Позитивные сценарии |       8       |   6    |   2    |    75,00% |
| Негативные сценарии |      38       |   30   |   8    |    78,94% |
| APITest             |       4       |   4    |   0    |   100,00% |
| Всего               |      50       |   40   |   10   |    80,00% |

### Отчет Allure:
![MySQL report](https://github.com/Andrey-Shelikhanov/Diploma.QA.Engineer/blob/main/documentation/pic/MySQL%20report.jpg)


![PostgreSQL report](https://github.com/Andrey-Shelikhanov/Diploma.QA.Engineer/blob/main/documentation/pic/PostgreSQL%20report.jpg)

#### Рекомендации:
1. Составить документацию для приложения.
2. Изменить заголовок web-страницы с "Заявка на карту" на соответствующее задаче сервиса(например "Покупка тура").
3. Исправить орфографические ошибки.
4. Для большей информативности рекомендуется реализовать для кнопок "Купить" и "Купить в кредит" различные режимы отображения при состоянии: когда кнопка не нажата пользователем; когда на нее наведен курсор; когда кнопка нажата и опция выбрана.
5. Если обязательные поля формы покупки тура не заполнены пользователем, рекомендуется сделать кнопку "Продолжить" неактивной.
6. Указать более точные и понятные для пользователя формулировки для индикации полей формы покупки тура, что позволит избежать неправильных действий пользователя. Например, вместо уведомления "Неверный формат" можно использовать более конкретную формулировку "Поле обязательно для заполнения".
7. Для поля "Месяц" ввести ограничение на ввод данных. Сделать возможным ввод только цифровых значений в диапазоне от 01 до 12.
8. Сделать возможность ввода в поле "Владелец" данных только на латинице с возможностью автоматического перехода букв в верхний регистр.

**Рекомендуется устранить найденные дефекты и провести повторное тестирование**

Полный список найденных дефектов находится в [issues](https://github.com/Andrey-Shelikhanov/Diploma.QA.Engineer/issues)
