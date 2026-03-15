# Розділ 6. Архітектура системи та залежності між підсистемами

## 6.1. Опис трирівневої архітектури
Інформаційна система "EcoSmart City" побудована за модульним принципом із використанням трирівневої архітектури:

1.  **Рівень збору даних (Edge Layer):** Мережа IoT-датчиків, що передають телеметрію через протокол MQTT.
2.  **Серверний рівень (Application Layer):** Центральний сервер обробки (Backend API), що здійснює валідацію, збереження та аналіз даних.
3.  **Рівень представлення (Presentation Layer):** Веб-портал та мобільний додаток для візуалізації інформації користувачам.

## 6.2. Діаграма архітектурних компонентів

```mermaid
graph TD
    subgraph "Edge Devices"
        Sensors[IoT Sensors Pool]
    end

    subgraph "Core System"
        API[Backend API Server]
        Auth[Auth Service]
        Processor[Data Processor]
    end

    subgraph "Storage"
        DB[(PostgreSQL / InfluxDB)]
    end

    subgraph "Clients"
        Web[Web Dashboard]
        App[Mobile Application]
    end

    Sensors -- "MQTT/JSON" --> Processor
    Processor --> DB
    API <--> DB
    API <--> Auth
    Web <--> API
    App <--> API

    6.3. Залежності між підсистемами
Data Processor залежить від стабільності надходження даних від Sensors.

Web/Mobile Clients повністю залежать від Backend API (REST/GraphQL).

Backend API має критичну залежність від Database для надання історичних звітів.