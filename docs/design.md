# Проєктування бази даних

## Короткий зміст:
- [модель бізнес-об'єктів](#BusinessObjectsModel)
- [ER-модель](#ERModel)
- [реляційна схема](#RelationalSchema)


<span id="BusinessObjectsModel"></span>
## Модель бізнес-об'єктів
**Модель бізнес-об'єктів** - це опис сутностей, класів або об'єктів даних, які стосуються певної предметної області. Вона включає характеристики (атрибути), що описують ці сутності, та зв'язки між ними, демонструючи, як вони пов'язані між собою в межах системи.

<center style="
    border-radius:4px;
    border: 1px solid #cfd7e6;
    box-shadow: 0 1px 3px 0 rgba(89,105,129,.05), 0 1px 1px 0 rgba(0,0,0,.025);
    padding: 1em;"
>

```plantuml
@startuml

  entity User <<ENTITY>> #93C1F5
  entity User.id <<NUMBER>> 
  entity User.firstname <<TEXT>> 
  entity User.lastname <<TEXT>> 
  entity User.email <<TEXT>> 
  entity User.login <<TEXT>> 
  entity User.password <<TEXT>> 

  entity Role <<ENTITY>> #93C1F5
  entity Role.id <<NUMBER>> 
  entity Role.name <<TEXT>> 

  entity Access <<ENTITY>> #93C1F5

  entity Data <<ENTITY>> #93C1F5
  entity Data.id <<NUMBER>> 
  entity Data.name <<TEXT>>
  entity Data.description <<TEXT>>
  entity Data.ownerId <<NUMBER>> 
  entity Data.format <<TEXT>> 
  entity Data.content <<TEXT>> 
  entity Data.createdAt <<DATE>> 
  entity Data.updatedAt <<DATE>> 

  entity Tag <<ENTITY>> #93C1F5
  entity Tag.id <<NUMBER>> 
  entity Tag.name <<TEXT>> 

  entity Category <<ENTITY>> #93C1F5
  entity Category.id <<NUMBER>> 
  entity Category.name <<TEXT>> 

  entity Link <<ENTITY>> #93C1F5


  User *-u- User.password
  User *-u- User.login
  User *-u- User.email
  User *-u- User.lastname
  User *-u- User.firstname
  User *-u- User.id

  Role *-d- Role.name
  Role *-d- Role.id

  Data *-d-- Data.updatedAt
  Data *-d-- Data.createdAt
  Data *-d-- Data.content
  Data *-d-- Data.format
  Data *-d-- Data.ownerId
  Data *-d-- Data.description
  Data *-d-- Data.name
  Data *-d-- Data.id

  Tag *-u- Tag.name
  Tag *-u- Tag.id

  Category *-u- Category.name
  Category *-u- Category.id
  Category "0,1" --o "0,*" Category

  User "1,1"-d-"0,*" Access
  Role "1,1"-u-"0,*" Access

  Access "0,*"-r-"1,1" Data

  Data "1,1"-r-"0,*" Link
  Link "0,*"-r-"1,1" Tag

  Data "1,1"-u-"1,1" Category

@enduml
```

</center>