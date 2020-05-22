## Домашнее задание к занятию «2.4. Циклы, параметризованные тесты и аннотации»
# Задача №2 (необязательная) - "@CsvFileSource"

### Исходный код BonusService.java
```java
package ru.netology.bonus;

public class BonusService {
  public long calculate(long amount, boolean registered) {
    int percent = registered ? 3 : 1;
    long bonus = amount * percent / 100 / 100;
    long limit = 500;
    if (bonus > limit) {
      bonus = limit;
    }
    return bonus;
  }
}
```
### Исходный код StatsServiceTest.java
```java
package ru.netology.bonus;

import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.CsvFileSource;

import static org.junit.jupiter.api.Assertions.assertEquals;

class BonusServiceTest {

  @CsvFileSource(resources = "/data.csv")
  @ParameterizedTest
  void shouldCalculate(String test, long amount, boolean registered, long expected) {
    BonusService service = new BonusService();

    // вызываем целевой метод:
    long actual = service.calculate(amount, registered);

    // производим проверку (сравниваем ожидаемый и фактический):
    assertEquals(expected, actual);
  }
}
```
### Исходный код Main.java
```java
package ru.netology.bonus;

public class Main {
  public static void main(String[] args) { }
}
```
### Исходный код data.csv
```csv
"registered user, bonus under limit",100060,true,30
"registered user, bonus over limit",100000060,true,500
"unregistered user, bonus under limit",100060,false,10
"unregistered user, bonus over limit",100000060,false,500
```
## Исходный код pom.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>ru.netology</groupId>
    <artifactId>bonus-calculator</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>11</maven.compiler.source>
        <maven.compiler.target>11</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter</artifactId>
            <version>5.4.2</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>2.22.2</version>
            </plugin>
        </plugins>
    </build>
</project>
```
## Работа написана в следующем окружении:
* Windows 10 1903 18362.778
* openjdk version "11.0.7" 2020-04-14
* OpenJDK Runtime Environment AdoptOpenJDK (build 11.0.7+10)
* OpenJDK 64-Bit Server VM AdoptOpenJDK (build 11.0.7+10, mixed mode)