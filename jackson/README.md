# Jackson/FasterXML: Command injection via deserialization
* Author:   Pedric Kng  
* Updated:  09 July 2018
***

## Vulnerability
CWE 502: Command injection via deserialization

Best practices for FasterXML/Jackson usage
- Avoid JsonTypeInfo annotation attributed with 'JsonTypeInfo.Id.Class'

```java
@JsonTypeInfo(use=JsonTypeInfo.Id.CLASS)
public abstract class Bicycle {
  ...
}

public class RoadBike extends Bicycle{
  ...
}
```

- Avoid usage of 'EnableDefaultTyping' vulnerable

```java
ObjectMapper om = new ObjectMapper();
om.enableDefaultTyping();
Object o = om.readValue(json, List.class);
```

- Avoid using java.lang.Object (or, java.util.Serializable) as the nominal type of polymorphic values

```Java
ObjectMapper om = new ObjectMapper();
Serializable o = om.readValue(json, List.class);
```

## Query
Extend 'Java/Cx/Java_General/Find_Unsafe_Deserializers'
See [cxql example](cx\[Java][Corp][Java_General][FindUnsafe_Deserializers].cxql)


## References
Jackson Polymorphic Deserialization [[1]]  
Blog on Jackson usage best practices [[2]]  
Jackson deserialization exploit [[3]]  

[1]:https://github.com/FasterXML/jackson-docs/wiki/JacksonPolymorphicDeserialization "Official Documentation"
[2]:https://medium.com/@cowtowncoder/on-jackson-cves-dont-panic-here-is-what-you-need-to-know-54cd0d6e8062 "Best practices"
[3]:https://blog.hackeriet.no/understanding-jackson-deserialization-exploits/ "Jackson Deserialization Exploit"
