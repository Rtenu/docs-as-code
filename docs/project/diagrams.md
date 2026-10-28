# Диаграммы

## Диаграмма последовательности

Диаграмма последовательности описывает процесс получения студентом персональных рекомендаций учебных курсов на основе его интересов и ранее пройденных дисциплин.
```mermaid
sequenceDiagram
    actor Student as Студент
    participant System as Рекомендательная система
    participant DB as База данных
    participant AI as Рекомендательный алгоритм

    Student->>System: Открыть раздел «Рекомендации»
    System->>DB: Запросить интересы и пройденные дисциплины
    DB-->>System: Вернуть данные студента

    System->>AI: Передать данные для анализа
    AI->>DB: Запросить доступные курсы
    DB-->>AI: Вернуть список курсов

    AI->>AI: Подобрать подходящие курсы
    AI-->>System: Вернуть результаты рекомендаций

    alt Подходящие курсы найдены
        System-->>Student: Показать список рекомендованных курсов
        Student->>System: Выбрать интересующий курс
        System-->>Student: Показать подробную информацию
    else Подходящие курсы не найдены
        System-->>Student: Сообщить об отсутствии рекомендаций
    end
```

## Диаграмма классов

Диаграмма классов описывает основные сущности рекомендательной системы учебных курсов, их атрибуты и связи между ними.
```mermaid
classDiagram
    class Student {
        +int id
        +string name
        +string email
    }

    class Course {
        +int id
        +string title
        +string description
    }

    class Interest {
        +int id
        +string name
    }

    class Recommendation {
        +int id
        +float score
    }

    Student "1" --> "*" Interest : выбирает
    Student "*" --> "*" Course : прошёл
    Student "1" --> "*" Recommendation : получает
    Recommendation "*" --> "1" Course : рекомендует
```