# Логическая модель данных системы доставки заказов

## Описание связей между сущностями

### Основные сущности и их связи:

1. Заказ (Order) <-> Доставка (Delivery)
   - Связь: один-к-одному (1:1)
   - Описание: Один заказ имеет одну доставку

2. Курьер (Courier) <-> Доставка (Delivery)
   - Связь: один-ко-многим (1:M)
   - Описание: Один курьер может выполнять много доставок

3. Клиент (Customer) <-> Заказ (Order)
   - Связь: один-ко-многим (1:M)
   - Описание: Один клиент может иметь много заказов

4. Заказ (Order) <-> Оплата (Payment)
   - Связь: один-к-одному (1:1)
   - Описание: К одному заказу привязана одна оплата

5. Курьер (Courier) <-> Начисление (Payroll)
   - Связь: один-ко-многим (1:M)
   - Описание: Один курьер может иметь много начислений

6. Пользователь (User) <-> Курьер (Courier)
   - Связь: один-к-одному (1:1)
   - Описание: Один пользователь системы может быть связан с одним курьером

### Дополнительные связи:

1. Отчет (Report) <-> Доставка/Оплата/Курьер
   - Связь: многие-ко-многим (M:M)
   - Реализация: Через таблицу ReportData
   - Описание: Один отчет может включать данные о многих сущностях, одна сущность может входить в разные отчеты

## ER-диаграмма

```mermaid
erDiagram
    ORDER ||--|| DELIVERY : "имеет"
    COURIER ||--o{ DELIVERY : "выполняет"
    CUSTOMER ||--o{ ORDER : "создает"
    ORDER ||--|| PAYMENT : "имеет"
    COURIER ||--o{ PAYROLL : "получает"
    USER ||--o| COURIER : "связан"
    REPORT }|--|| REPORTDATA : "содержит"
    DELIVERY }|--|| REPORTDATA : "включается"
    PAYMENT }|--|| REPORTDATA : "включается"
    COURIER }|--|| REPORTDATA : "включается"

    ORDER {
        integer order_id
        string pickup_address
        string delivery_address
        datetime assembly_time
        datetime desired_delivery_time
        enum status
        decimal delivery_cost
    }

    COURIER {
        integer courier_id
        string full_name
        string contacts
        boolean status
        point location
        decimal rating
    }

    CUSTOMER {
        integer customer_id
        string name
        string contact_person
        string phone
        string email
        string address
    }

    DELIVERY {
        integer delivery_id
        integer order_id
        integer courier_id
        datetime start_time
        datetime end_time
        enum status
        text comment
    }

    PAYMENT {
        integer payment_id
        integer order_id
        decimal amount
        enum type
        enum status
        datetime date
    }

    USER {
        integer user_id
        string login
        string password
        enum role
        boolean status
        datetime created_at
    }

    REPORT {
        integer report_id
        enum type
        daterange period
        datetime created_at
        enum status
        json data
    }

    PAYROLL {
        integer payroll_id
        integer courier_id
        daterange period
        decimal amount
        enum status
        datetime date
    }

    REPORTDATA {
        integer report_id
        integer entity_id
        string entity_type
    }
``` 