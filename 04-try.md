# Try out


## Contacts

Model an agenda: 

* Where we have a name, birthday, and details.

E.g.: 

```java
public class Contact {
    private String name;
    private LocalDate birthday;
    private Map<String, String> details;
}
```



## Car/Driver registration


* Where we have a Car registration.

E.g.: 


```java

class Car {

    private String plate;

    private String city;

    private String color;
    //UDT
    private Owner owner;
}

class Owner {

    private String name;
    private String number;
}
```
