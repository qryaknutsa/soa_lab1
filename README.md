Разработать спецификацию в формате OpenAPI для набора веб-сервисов, реализующего следующую функциональность:

**Первый веб-сервис** должен осуществлять управление коллекцией объектов. В коллекции необходимо хранить объекты класса Ticket, описание которого приведено ниже:

```java
public class Ticket {
private Long id; //Поле не может быть null, Значение поля должно быть больше 0, Значение этого поля должно быть уникальным, Значение этого поля должно генерироваться автоматически
private String name; //Поле не может быть null, Строка не может быть пустой
private Coordinates coordinates; //Поле не может быть null
private java.time.ZonedDateTime creationDate; //Поле не может быть null, Значение этого поля должно генерироваться автоматически
private int price; //Значение поля должно быть больше 0
private double discount; //Значение поля должно быть больше 0, Максимальное значение поля: 100
private boolean refundable;
private TicketType type; //Поле может быть null
private Person person; //Поле может быть null
}
public class Coordinates {
private float x;
private Float y; //Поле не может быть null
}
public class Person {
private int height; //Значение поля должно быть больше 0
private Color eyeColor; //Поле может быть null
private Color hairColor; //Поле не может быть null
private Country nationality; //Поле может быть null
private Location location; //Поле не может быть null
}
public class Location {
private Integer x; //Поле не может быть null
private long y;
private double z;
private String name; //Поле может быть null
}
public enum TicketType {
VIP,
USUAL,
BUDGETARY,
CHEAP;
}
public enum Color {
RED,
BLACK,
BLUE,
ORANGE,
WHITE;
}
public enum Color {
GREEN,
RED,
BLUE;
}
public enum Country {
CHINA,
NORTH_KOREA,
JAPAN;
}
```


Веб-сервис должен удовлетворять следующим требованиям:

* API, реализуемый сервисом, должен соответствовать рекомендациям подхода RESTful.
* Необходимо реализовать следующий базовый набор операций с объектами коллекции: добавление нового элемента, получение элемента по ИД, обновление элемента, удаление элемента, получение массива элементов.
* Операция, выполняемая над объектом коллекции, должна определяться методом HTTP-запроса.
* Операция получения массива элементов должна поддерживать возможность сортировки и фильтрации по любой комбинации полей класса, а также возможность постраничного вывода результатов выборки с указанием размера и порядкового номера выводимой страницы.
* Все параметры, необходимые для выполнения операции, должны передаваться в URL запроса.
* Информация об объектах коллекции должна передаваться в формате **json**.
* В случае передачи сервису данных, нарушающих заданные на уровне класса ограничения целостности, сервис должен возвращать код ответа http, соответствующий произошедшей ошибке. 


Помимо базового набора, веб-сервис должен поддерживать следующие операции над объектами коллекции:

* Рассчитать сумму значений поля discount для всех объектов.
* Вернуть количество объектов, значение поля type которых меньше заданного.
* Вернуть массив уникальных значений поля type по всем объектам.

Эти операции должны размещаться на отдельных URL.

**Второй веб-сервис** должен располагаться на URL /booking, и реализовывать ряд дополнительных операций, связанных с вызовом API первого сервиса:

/sell/vip/ticket-id/person-id : скопировать указанный билет, создав такой же, но с категорией "VIP" и с удвоенной ценой
/event/{event-id}/cancel : отменить указанное событие, удалив все билеты на него

Эти операции также должны размещаться на отдельных URL.

Для разработанной спецификации необходимо сгенерировать интерактивную веб-документацию с помощью Swagger UI. Документация должна содержать описание всех REST API обоих сервисов с текстовым описанием функциональности каждой операции. Созданную веб-документацию необходимо развернуть на сервере helios.