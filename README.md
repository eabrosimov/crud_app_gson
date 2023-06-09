# **CRUD APP**
Консольное CRUD приложение с возможностью сохранения в JSON файл
## **Java SE**
___
* IO
* Collection API
* Stream API
  
**Строронние библиотеки**
* Gson


## **Описание проекта**
___
Приложение работает с сущностями:
* Developer  
  * id
  * firstName
  * lastName
  * skills
  * specialty
  * status
* Skill
  * id
  * name
* Specialty
  * id
  * name
* Status  
  * ACTIVE
  * DELETED

Стандартный функционал CRUD приложения:
* Добавить
* Получить
* Получить всех
* Изменить
* Удалить

В качестве хранилища данных используется JSON файл.  
При работе с данными Java-объекты сериализуются в Json-объекты, при десериализации наоборот.

## **Структура проекта**
___
**`model`** - POJO классы  
**`repository`** - классы, реализующие доступ к файлам  
**`controller`** - обработка запросов от пользователя  
**`view`** - данные для работы с консолью

## **Список команд**
___
При запуске программы пользователь попадает в главное меню.  
Выводится список доступных команд для перемещения по редакторам хранилищ:  
**`1`** - меню редактора хранилища developers.json  
**`2`** - меню редактора хранилища skill.json  
**`3`** - меню реактора хранилища specialty.json  
**`-help`** - отображение списка доступных команд  
**`-exit`** - завершение работы программы  
  
У всех редакторов одинаковый список команд:  
**`-c`** - создать новую сущность  
**`-r`** - вывести сущность на экран получив ее по id  
**`-ra`** - вывести все сущности на экран  
**`-u`** - изменить сущность  
**`-d`** - удалить сущность  
**`-help`** - отображение списка доступных команд  
**`-exit`** - выход в главное меню

У редактора developers.json есть дополнительный список команд после команды **`-u`** позволяющий выбрать поле для изменения:  
**`first name`**  
**`last name`**  
**`skill`**  
**`specialty`**  

## **Логика**
___
### **Добавление**  
Происходит валидация введенного имени(в случае с Developer имени и фамилии).  
Имя не должно быть пустым, содержать только пробелы, а также иметь больше 16 символов.  
Допускаются только буквенные символы(латинские a-zA-Z и кириллица а-яА-Я).  
Все не буквенные символы отбрасываются.  
Допускатются пробелы между словами(кроме Developer).  

Если пользователь ввел валидное имя, объекту автоматически присваивается id равный id последнего добавленного объекта + 1 и он добавляется в файл.  
Если имя невалидное, на экран выводится соответствующее оповещение.  
  
### **Получение**  
Происходит валидация введенного id.  
Выполняется проверка на буквы, отрицательные значения, а также проверка на существование объекта с таким id.  
Если валидация прошла успешно, на экран выводится текстовое представление объекта.  
Если id невалидный, на экран выводится соответствующее оповещение.  
  
### **Изменение**  
Происходит валидация введенного id.  
Если id валидный, возвращается объект соответствующий данному id.  
Иначе выводится соответствующее оповещение.  
  
Далее пользователь вводит новое имя и происходит валидация имени.  
Если валидация прошла успешно, происходит замена в файле старого объекта на новый и на экран выводится текстовое представление обновленного объекта.  
Иначе выводится соответствующее уведомление.  
  
В случае с Developer после введенного id пользователь должен ввести нужное поле для редактирования.   
С именем и фамилией происходят вышеописанные действия.  

Если пользователь хочет добавить новый скил или специальность, он вводит id, по которому происходит поиск объекта в нужном хранилище и добавляет его Developer'y.   
Иначе, если объект не найден или id невалидный выводится соответствующее оповещение.  
  
### **Удаление**  
Происходит валидация введенного id.  
Если id валидный, из файла удаляется объект с соответствующим id.  
Иначе выводится соответствующее оповещение.  
  
В случае с Developer объект не удаляется из файла, а лишь меняет состояние поля Status с ACTIVE на DELETED. После удаления получить/изменить объект через консоль нельзя.

 
