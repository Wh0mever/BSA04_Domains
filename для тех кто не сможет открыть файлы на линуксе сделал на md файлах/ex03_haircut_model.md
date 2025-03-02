# Логическая модель данных системы онлайн-записи барбершопа

## Описание связей между сущностями

### Основные сущности и их связи:

1. Клиент (Client) <-> Запись (Appointment)
   - Связь: один-ко-многим (1:M)
   - Описание: Один клиент может иметь много записей

2. Мастер (Master) <-> Запись (Appointment)
   - Связь: один-ко-многим (1:M)
   - Описание: Один мастер может иметь много записей

3. Услуга (Service) <-> Запись (Appointment)
   - Связь: один-ко-многим (1:M)
   - Описание: На одну услугу может быть много записей

4. Мастер (Master) <-> Расписание (Schedule)
   - Связь: один-ко-многим (1:M)
   - Описание: У одного мастера может быть много записей в расписании

5. Запись (Appointment) <-> Отзыв (Review)
   - Связь: один-к-одному (1:1)
   - Описание: К одной записи может быть привязан один отзыв

6. Запись (Appointment) <-> Оплата (Payment)
   - Связь: один-к-одному (1:1)
   - Описание: К одной записи привязана одна оплата

7. Запись (Appointment) <-> Уведомление (Notification)
   - Связь: один-ко-многим (1:M)
   - Описание: К одной записи может быть привязано несколько уведомлений

### Дополнительные связи:

1. Мастер (Master) <-> Услуга (Service)
   - Связь: многие-ко-многим (M:M)
   - Реализация: Через таблицу MasterServices
   - Описание: Один мастер может выполнять много услуг, одну услугу могут выполнять много мастеров

## ER-диаграмма

```mermaid
erDiagram
    CLIENT ||--o{ APPOINTMENT : "делает"
    MASTER ||--o{ APPOINTMENT : "принимает"
    SERVICE ||--o{ APPOINTMENT : "включает"
    MASTER ||--o{ SCHEDULE : "имеет"
    APPOINTMENT ||--o| REVIEW : "имеет"
    APPOINTMENT ||--o| PAYMENT : "имеет"
    APPOINTMENT ||--o{ NOTIFICATION : "генерирует"
    MASTER }|--|| MASTERSERVICES : "предоставляет"
    SERVICE }|--|| MASTERSERVICES : "выполняется"

    CLIENT {
        integer client_id
        string full_name
        string phone
        string email
        enum contact_channel
        boolean status
    }

    MASTER {
        integer master_id
        string full_name
        string specialization
        string contacts
        boolean status
    }

    SERVICE {
        integer service_id
        string name
        enum type
        integer duration
        decimal price
        enum status
    }

    APPOINTMENT {
        integer appointment_id
        integer client_id
        integer service_id
        integer master_id
        datetime datetime
        enum status
    }

    SCHEDULE {
        integer schedule_id
        integer master_id
        date date
        time start_time
        time end_time
        enum status
    }

    REVIEW {
        integer review_id
        integer appointment_id
        integer rating
        text comment
        datetime created_at
    }

    PAYMENT {
        integer payment_id
        integer appointment_id
        decimal amount
        datetime date
        enum status
        enum method
    }

    NOTIFICATION {
        integer notification_id
        integer appointment_id
        enum type
        enum status
        enum channel
        datetime sent_at
    }

    MASTERSERVICES {
        integer master_id
        integer service_id
    }
``` 