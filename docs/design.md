# Проєктування бази даних

## Короткий зміст:
- [модель бізнес-об'єктів](#BusinessObjectsModel)
- [ER-модель](#ERModel)
- [реляційна схема](#RelationalSchema)

<span id="ERModel"></span>
## ER-модель
**ER-модель** - це модель даних, яка дозволяє описувати концептуальні схеми за допомогою узагальнених конструкцій блоків. ER-модель — це метамодель даних, тобто засіб опису моделей даних. Існує ряд моделей для представлення знань, але одним з найзручніших інструментів уніфікованого представлення даних, незалежного від програмного забезпечення, що його реалізує, є модель «сутність-зв'язок». Важливим є той факт, що з моделі «сутність-зв'язок» можуть бути породжені всі існуючі моделі даних (ієрархічна, мережева, реляційна, об'єктна), тому вона є найзагальнішою.

```plantuml

@startuml

entity User {
    +id : NUMBER <<PK>>
    firstname : TEXT
    lastname : TEXT
    email : TEXT
    login : TEXT
    password : TEXT
}

entity Role {
    +id : NUMBER <<PK>>
    name : TEXT
}

entity Access {
    +id : NUMBER <<PK>>
    user_id : NUMBER <<FK>>
    role_id : NUMBER <<FK>>
}

entity Data {
    +id : NUMBER <<PK>>
    name : TEXT
    description : TEXT
    ownerId : NUMBER <<FK>>
    format : TEXT
    content : TEXT
    createdAt : DATE
    updatedAt : DATE
}

entity Tag {
    +id : NUMBER <<PK>>
    name : TEXT
}

entity Category {
    +id : NUMBER <<PK>>
    name : TEXT
}

entity Link {
    +id : NUMBER <<PK>>
    data_id : NUMBER <<FK>>
    tag_id : NUMBER <<FK>>
}

User ||--o{ Access : "has"
Role ||--o{ Access : "has"
Data ||--o{ Access : "is accessed by"
Data ||--o{ Link : "has"
Tag ||--o{ Link : "is linked to"
Category ||--o{ Data : "categorizes"

@enduml
```

</center>
