# Try out


## Contacts

Model an agenda: 

* Where we have a name, birthday, and details.


```java
public class Contact {
    private String name;
    private LocalDate birthday;
    private Map<String, String> details;
}
```



## Car/Driver registration



```java
@Entity
class Car {
    @Id
    private String plate;

    @Column
    private String city;

    @Column
    private String color;

    @UDT("owner")
    @Column
    private Owner owner;
}
```
