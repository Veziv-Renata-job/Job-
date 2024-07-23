# Job-
Pentru a dezvolta un proiect care să includă un șofer și să înglobeze toate restaurantele din Brăila, putem crea o aplicație simplă folosind Java, care să gestioneze informațiile despre restaurante și să permită șoferului să preia comenzile. Voi oferi un exemplu de aplicație simplă care utilizează Java pentru backend, dar poți extinde acest exemplu pentru a include o interfață utilizator sau o bază de date.

### Structura Proiectului

1. **Model**: Clasa `Restaurant`.
2. **Serviciu**: Clasa `RestaurantService` pentru logica de business.
3. **Controler**: Clasa `RestaurantController` pentru a gestiona cererile HTTP.
4. **Main**: Clasa principală pentru a rula aplicația.

### 1. Clasa Restaurant

Această clasă va reprezenta modelul de date pentru un restaurant.
java
public class Restaurant {
    private String name;
    private String address;
    private String phoneNumber;

    public Restaurant(String name, String address, String phoneNumber) {
        this.name = name;
        this.address = address;
        this.phoneNumber = phoneNumber;
    }

    // Getters and Setters
    public String getName() {
        return name;
    }

    public String getAddress() {
        return address;
    }

    public String getPhoneNumber() {
        return phoneNumber;
    }
### 2. Clasa RestaurantService

Această clasă va conține logica de afaceri pentru gestionarea restaurantelor.
java
import java.util.ArrayList;
import java.util.List;

public class RestaurantService {
    private List<Restaurant> restaurants;

    public RestaurantService() {
        restaurants = new ArrayList<>();
        // Adăugăm câteva restaurante fictive
        restaurants.add(new Restaurant("Restaurant 1", "Str. Primăverii, Nr. 1", "0123 456 789"));
        restaurants.add(new Restaurant("Restaurant 2", "Str. Libertății, Nr. 2", "0987 654 321"));
        // Adaugă mai multe restaurante după necesitate
    }

    public List<Restaurant> getAllRestaurants() {
        return restaurants;
    }
### 3. Clasa RestaurantController

Această clasă va gestiona cererile HTTP și va returna datele despre restaurante.
java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
import java.util.List;

@RestController
public class RestaurantController {
    private RestaurantService restaurantService;

    public RestaurantController() {
        this.restaurantService = new RestaurantService();
    }

    @GetMapping("/restaurants")
    public List<Restaurant> getRestaurants() {
        return restaurantService.getAllRestaurants();
    }
}
### 4. Clasa Principală

Această clasă va inițializa aplicația Spring Boot.
java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class GlovoApplication {
    public static void main(String[] args) {
        SpringApplication.run(GlovoApplication.class, args);
    }
} 
### Configurarea Maven

Asigură-te că ai configurat Maven în `pom.xml` pentru a include Spring Boot:
xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>glovo</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <java.version>17</java.version>
        <spring.boot.version>2.5.4</spring.boot.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter</artifactId>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>
### Rularea Aplicației

După ce ai configurat proiectul, poți rula aplicația cu comanda:
bash
mvn spring-boot:run
Apoi, poți accesa lista restaurantelor la URL-ul `http://localhost:8080/restaurants'.
