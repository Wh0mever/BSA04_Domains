# Словарь данных системы доставки заказов

## Сущности и их атрибуты

### 1. Заказ (Order)
| Атрибут | Мнемоника | Тип данных | Обязательность | Описание |
|---------|-----------|------------|----------------|-----------|
| ID заказа | order_id | Integer | Да | Уникальный идентификатор заказа |
| Адрес получения | pickup_address | String(200) | Да | Адрес получения заказа |
| Адрес доставки | delivery_address | String(200) | Да | Адрес доставки заказа |
| Время комплектации | assembly_time | DateTime | Да | Время готовности заказа к отправке |
| Желаемое время доставки | desired_delivery_time | DateTime | Да | Желаемое время доставки |
| Статус | status | Enum | Да | Статус заказа (новый/в работе/доставлен/отменен) |
| Стоимость доставки | delivery_cost | Decimal(10,2) | Да | Стоимость доставки |

### 2. Курьер (Courier)
| Атрибут | Мнемоника | Тип данных | Обязательность | Описание |
|---------|-----------|------------|----------------|-----------|
| ID курьера | courier_id | Integer | Да | Уникальный идентификатор курьера |
| ФИО | full_name | String(100) | Да | Полное имя курьера |
| Контакты | contacts | String(200) | Да | Контактная информация |
| Статус | status | Boolean | Да | Статус активности (работает/не работает) |
| Геолокация | location | Point | Нет | Текущие координаты |
| Рейтинг | rating | Decimal(3,2) | Да | Рейтинг курьера |

### 3. Клиент (Customer)
| Атрибут | Мнемоника | Тип данных | Обязательность | Описание |
|---------|-----------|------------|----------------|-----------|
| ID клиента | customer_id | Integer | Да | Уникальный идентификатор клиента |
| Название | name | String(100) | Да | Название организации |
| Контактное лицо | contact_person | String(100) | Да | ФИО контактного лица |
| Телефон | phone | String(15) | Да | Контактный телефон |
| Email | email | String(50) | Нет | Электронная почта |
| Адрес | address | String(200) | Да | Адрес клиента |

### 4. Доставка (Delivery)
| Атрибут | Мнемоника | Тип данных | Обязательность | Описание |
|---------|-----------|------------|----------------|-----------|
| ID доставки | delivery_id | Integer | Да | Уникальный идентификатор доставки |
| ID заказа | order_id | Integer | Да | Ссылка на заказ |
| ID курьера | courier_id | Integer | Да | Ссылка на курьера |
| Время начала | start_time | DateTime | Да | Время начала доставки |
| Время завершения | end_time | DateTime | Нет | Время завершения доставки |
| Статус | status | Enum | Да | Статус доставки (в пути/доставлено/проблема) |
| Комментарий | comment | Text | Нет | Комментарий к доставке |

### 5. Оплата (Payment)
| Атрибут | Мнемоника | Тип данных | Обязательность | Описание |
|---------|-----------|------------|----------------|-----------|
| ID оплаты | payment_id | Integer | Да | Уникальный идентификатор оплаты |
| ID заказа | order_id | Integer | Да | Ссылка на заказ |
| Сумма | amount | Decimal(10,2) | Да | Сумма оплаты |
| Тип | type | Enum | Да | Тип оплаты (наличные/безналичные) |
| Статус | status | Enum | Да | Статус оплаты (ожидает/выполнена/отменена) |
| Дата | date | DateTime | Да | Дата и время оплаты |

### 6. Пользователь (User)
| Атрибут | Мнемоника | Тип данных | Обязательность | Описание |
|---------|-----------|------------|----------------|-----------|
| ID пользователя | user_id | Integer | Да | Уникальный идентификатор пользователя |
| Логин | login | String(50) | Да | Логин для входа |
| Пароль | password | String(100) | Да | Хеш пароля |
| Роль | role | Enum | Да | Роль в системе (админ/диспетчер/курьер) |
| Статус | status | Boolean | Да | Статус активности |
| Дата регистрации | created_at | DateTime | Да | Дата создания учетной записи |

### 7. Отчет (Report)
| Атрибут | Мнемоника | Тип данных | Обязательность | Описание |
|---------|-----------|------------|----------------|-----------|
| ID отчета | report_id | Integer | Да | Уникальный идентификатор отчета |
| Тип | type | Enum | Да | Тип отчета (доставки/оплаты/курьеры) |
| Период | period | DateRange | Да | Период отчета |
| Дата создания | created_at | DateTime | Да | Дата формирования отчета |
| Статус | status | Enum | Да | Статус отчета (формируется/готов/ошибка) |
| Данные | data | JSON | Да | Данные отчета |

### 8. Начисление (Payroll)
| Атрибут | Мнемоника | Тип данных | Обязательность | Описание |
|---------|-----------|------------|----------------|-----------|
| ID начисления | payroll_id | Integer | Да | Уникальный идентификатор начисления |
| ID курьера | courier_id | Integer | Да | Ссылка на курьера |
| Период | period | DateRange | Да | Период начисления |
| Сумма | amount | Decimal(10,2) | Да | Сумма начисления |
| Статус | status | Enum | Да | Статус начисления (расчет/выплачено/отменено) |
| Дата | date | DateTime | Да | Дата начисления | 