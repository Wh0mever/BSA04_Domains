# Сущности системы онлайн-записи барбершопа

## 1. Клиент (Client)
- **Назначение**: Хранение информации о клиентах
- **Ключевые атрибуты**:
  - ID клиента (уникальный идентификатор)
  - ФИО
  - Телефон
  - Email
  - Предпочтительный канал связи
  - Статус регистрации

## 2. Услуга (Service)
- **Назначение**: Информация о предоставляемых услугах
- **Ключевые атрибуты**:
  - ID услуги
  - Название
  - Тип услуги (парикмахерская/косметологическая)
  - Длительность
  - Стоимость
  - Статус (активна/в архиве)

## 3. Мастер (Master)
- **Назначение**: Данные о мастерах
- **Ключевые атрибуты**:
  - ID мастера
  - ФИО
  - Специализация
  - Контактные данные
  - Статус

## 4. Запись (Appointment)
- **Назначение**: Информация о записях клиентов
- **Ключевые атрибуты**:
  - ID записи
  - ID клиента
  - ID услуги
  - ID мастера
  - Дата и время
  - Статус записи

## 5. Расписание (Schedule)
- **Назначение**: График работы мастеров
- **Ключевые атрибуты**:
  - ID расписания
  - ID мастера
  - Дата
  - Время начала
  - Время окончания
  - Статус

## 6. Отзыв (Review)
- **Назначение**: Отзывы клиентов об услугах
- **Ключевые атрибуты**:
  - ID отзыва
  - ID записи
  - Оценка
  - Комментарий
  - Дата создания

## 7. Оплата (Payment)
- **Назначение**: Информация об оплатах
- **Ключевые атрибуты**:
  - ID оплаты
  - ID записи
  - Сумма
  - Дата оплаты
  - Статус оплаты
  - Метод оплаты

## 8. Уведомление (Notification)
- **Назначение**: Система уведомлений клиентов
- **Ключевые атрибуты**:
  - ID уведомления
  - ID записи
  - Тип уведомления
  - Статус отправки
  - Канал связи
  - Время отправки 