# Розділ 7. Побудова моделі даних (Entity Relationship Diagram)

## 7.1. Структура бази даних
Для забезпечення ефективного зберігання великих масивів екологічної інформації спроектовано реляційну модель даних, що включає таблиці для користувачів, пристроїв та самих вимірювань.

## 7.2. ER-діаграма (Entity Relationship)

```mermaid
erDiagram
    USER ||--o{ NOTIFICATION : receives
    DEVICE ||--o{ MEASUREMENT : generates
    USER {
        int id PK
        string username
        string email
        string role
    }
    DEVICE {
        int id PK
        string sensor_type
        string location_geo
        string status
    }
    MEASUREMENT {
        int id PK
        int device_id FK
        float value
        datetime timestamp
        string unit
    }
    NOTIFICATION {
        int id PK
        int user_id FK
        string message
        datetime sent_at
    }

    7.3. Опис сутностей
USER: Містить дані про акторів системи (мешканців, екологів, адмінів).

DEVICE: Реєстр усіх підключених IoT-пристроїв з їхніми координатами.

MEASUREMENT: Найбільша таблиця, що зберігає кожен окремий показник (температура, рівень CO2 тощо) з прив'язкою до часу.

NOTIFICATION: Журнал надісланих сповіщень про критичні стани.