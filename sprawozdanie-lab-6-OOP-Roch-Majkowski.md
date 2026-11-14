## I. Dokumentacja do lab. nr 6 - "Konstruktory i inicjalizacja obiektów"
## II. Roch Majkowski - grupa 1, semestr III
## III. Przedmiot - "Programowanie obiektowe"

## IV. Opis zadania do realizacji

Do zrealizowania były następujące zadania:

1. Napisz klasę `Student` z trzema konstruktorami: domyślnym, z samym `name` oraz z `name` i `indexNumber`.
2. Zastosuj przeciążanie konstruktorów w klasie `Rectangle` i użyj `this(...)` do delegowania między konstruktorami.
3. Utwórz klasę `Car` z walidacją danych wejściowych w konstruktorze (np. rok produkcji i pojemność silnika).
4. Utwórz klasę `Product` z polem `private final int id` oraz polami `name` i `price`. Pole `id` ma być nadawane automatycznie w konstruktorze na podstawie statycznego licznika (`1, 2, 3, ...`), a statyczna metoda `getCount()` ma zwracać liczbę utworzonych produktów (por. Przykład 8).
5. Zaimplementuj konstruktor kopiujący w klasie `AddressBookEntry` i pokaż różnicę między kopią a referencją do tego samego obiektu.
6. Napisz testowy `main`, który tworzy obiekty wszystkimi konstruktorami i wypisuje ich stan po inicjalizacji.

## V. Technologie wykorzystane w zadaniu
  - Java

## VI. Realizacja zadania
<br>

## 1. Zadanie - klasa `Student` z trzema konstruktorami

Kod wykorzystany do rozwiązania zadania (zadań):

### Klasa `Student`

```java
package Student;

public class Student {
    public String name;
    public int indexNumber;

    public Student(){ // Konstruktor bez argumentów
        this("Nieznany", 0);
    }

    public Student(String name){ // Konstruktor z argumentem dla name
        this(name,0);
    }

    public Student(String name, int indexNumber){ // Konstruktor z oby dwoma argumentami
        this.name = name;
        this.indexNumber = indexNumber;
    }

    @Override
    public String toString() {
        return "====+ Student +==== \n" +
                "Name: " + name + "\n" +
                "Index number: " + indexNumber + "\n";
    }
}
```

### Klasa `Main` (fragment)

```java
System.out.println(new Student());
System.out.println(new Student("Bob"));
System.out.println(new Student("Jan", 2));
```

#### 1a. Zrzuty ekranu pokazujące wynik działania aplikacji/skryptu:
![wynik-zadania-1](images/dzialanie_zad1.png)

#### 1b. Struktura projektu/programu:
![struktura-projektu](images/struktura_zad1.png)

<br>

## 2. Zadanie - klasa `Rectangle`

Kod wykorzystany do rozwiązania zadania (zadań):

### Klasa `Rectangle`

```java
package Rectangle;

public class Rectangle {
    private double Width;
    private double Height;

    public Rectangle() {
        this(1,1);
        System.out.println("Base constructor");
    }

    public Rectangle(double side) {
        this(side,side);
        System.out.println("Square constructor");
    }

    public Rectangle(double Width, double Height) {
        this.Width = Width;
        this.Height = Height;
        System.out.println("Full Constructor");
    }

    @Override
    public String toString() {
        return "====+ Rectangle +==== \n" +
                "Width: " + Width + "\n" +
                "Height: " + Height + "\n";
    }
}
```

### Klasa `Main` (fragment)

```java
System.out.println(new Rectangle());
System.out.println(new Rectangle(2));
System.out.println(new Rectangle(2,4));
```

#### 2a. Zrzuty ekranu pokazujące wynik działania aplikacji/skryptu:
![wynik-zadania-2](images/dzialanie_zad2.png)

#### 2b. Struktura projektu/programu:
![struktura-projektu](images/struktura_zad2.png)

<br>

## 3. Zadanie - klasa `Car` z walidacją danych

Kod wykorzystany do rozwiązania zadania (zadań):

### Klasa `Car`

```java
package Car;

public class Car {
    private final int productionYear;
    private final double engineCapacity;

    public Car(int productionYear, double engineCapacity) {
        if (productionYear < 1886 || productionYear > java.time.Year.now().getValue()) {
            throw new IllegalArgumentException("Nieprawidłowy rok produkcji: " + productionYear);
        }
        if (engineCapacity <= 0){
            throw new IllegalArgumentException("Pojemność silnika musi być dodatnia");
        }
        this.productionYear = productionYear;
        this.engineCapacity = engineCapacity;
    }

    @Override
    public String toString() {
        return "====+ Car +==== \n" +
                "Production Year: " + productionYear + "\n" +
                "Engine capacity: " + engineCapacity + "\n";
    }
}
```

### Klasa `Main` (fragment)

```java
        System.out.println(new Car(2003,30));
        try {
        new Car(1700, -1);
        } catch (IllegalArgumentException e) {
        System.out.println("Błąd: " + e.getMessage());
        }
```

#### 3a. Zrzuty ekranu pokazujące wynik działania aplikacji/skryptu:
![wynik-zadania-3](images/dzialanie_zad3.png)

#### 3b. Struktura projektu/programu:
![struktura-projektu](images/struktura_zad3.png)

#### 3c. Wnioski:
- Konstruktor klasy `Car` sprawdza rok produkcji, czyli od 1886 do tutejszego roku (sprawdzone za pomocą `java.time.Year.now()`)
- Pola `productionYear` i `engineCapacity` są `private final`, więc po utworzeniu nie można ich już zmienić.

<br>

## 4. Zadanie - klasa `Product` z polem `final` i statycznym licznikiem

Kod wykorzystany do rozwiązania zadania (zadań):

### Klasa `Product`

```java
package Product;

public class Product {
    private static int nextId = 1;
    private static int count = 0;

    private final int id;
    private String name;
    private double price;

    public Product(String name, double price) {
        this.id = nextId++;
        this.name = name;
        this.price = price;
        count++;
    }

    public static int getCount(){
        return count;
    }

    @Override
    public String toString() {
        return "====+ Product +==== \n" +
                "Id: " + id + "\n" +
                "Name: " + name + "\n" +
                "Price: " + price + "\n";
    }

}
```

### Klasa `Main` (fragment)

```java
System.out.println(new Product("PC", 4000.0));
System.out.println(new Product("Myszka", 80));
System.out.println(new Product("Pasta do zębów", 12.99));
```

#### 4a. Zrzuty ekranu pokazujące wynik działania aplikacji/skryptu:
![wynik-zadania-4](images/dzialanie_zad4.png)

#### 4b. Struktura projektu/programu:
![struktura-projektu](images/struktura_zad4.png)

<br>

## 5. Zadanie - konstruktor kopiujący w klasie `AddressBookEntry`

Kod wykorzystany do rozwiązania zadania (zadań):

### Klasa `AddressBookEntry`

```java
package AddressBookEntry;

public class AddressBookEntry {
    private String name;
    private String address;

    public AddressBookEntry(String name, String address){
        this.name = name;
        this.address = address;
    }

    public AddressBookEntry(AddressBookEntry a){
        this(a.name, a.address);
    }

    public void setAddress(String address) {
        this.address = address;
    }

    @Override
    public String toString() {
        return "====+ Address Book +==== \n" +
                "Name: " + name + "\n" +
                "Address: " + address + "\n";
    }
}
```

### Klasa `Main` (fragment)

```java
AddressBookEntry oryginalna = new AddressBookEntry("Jan Daciuk", "Gdańsk");
AddressBookEntry kopia = new AddressBookEntry(oryginalna);
AddressBookEntry referencja = oryginalna;
kopia.setAddress("Gdynia");
System.out.println(oryginalna + "\n" + kopia + "\n" + (referencja == oryginalna));
```

#### 5a. Zrzuty ekranu pokazujące wynik działania aplikacji/skryptu:
![wynik-zadania-5](images/dzialanie_zad5.png)

#### 5b. Struktura projektu/programu:
![struktura-projektu](images/struktura_zad5.png)

#### 5c. Wnioski:
- Zmienna `referencja` wskazuje na ten sam obiekt co `oryginalna`. Wynik to `referencja == oryginalna`, który jest `true`. Przypisanie referencji nie tworzy kopii.

<br>

## 6. Zadanie - testowy `main`

Kod wykorzystany do rozwiązania zadania (zadań):

### Klasa `Main`

```java
import AddressBookEntry.AddressBookEntry;
import Car.Car;
import Product.Product;
import Rectangle.Rectangle;
import Student.Student;

public class Main {
    static void main() {

        // Wywołanie zadania laboratoryjnego 1

        System.out.println(new Student());
        System.out.println(new Student("Bob"));
        System.out.println(new Student("Jan", 2));

        // Wywołanie zadanie laboratoryjnego 2

        System.out.println(new Rectangle());
        System.out.println(new Rectangle(2));
        System.out.println(new Rectangle(2,4));

        // Wywołanie zadania laboratoryjnego 3

        System.out.println(new Car(2003,30));
        try {
            new Car(1700, -1);
        } catch (IllegalArgumentException e) {
            System.out.println("Błąd: " + e.getMessage());
        }

        // Wywołanie zadania laboratoryjnego 4

        System.out.println(new Product("PC", 4000.0));
        System.out.println(new Product("Myszka", 80));
        System.out.println(new Product("Pasta do zębów", 12.99));
        System.out.println("Liczba produktów: " + Product.getCount());

        // Wywołanie zadania laboratoryjnego 5

        AddressBookEntry oryginalna = new AddressBookEntry("Jan Daciuk", "Gdańsk");
        AddressBookEntry kopia = new AddressBookEntry(oryginalna);
        AddressBookEntry referencja = oryginalna;
        kopia.setAddress("Gdynia");
        System.out.println(oryginalna + "\n" + kopia + "\n" + (referencja == oryginalna));

    }
}
```

#### 6a. Zrzuty ekranu pokazujące wynik działania aplikacji/skryptu:
![wynik-zadania-6](images/dzialanie_zad6.png)

#### 6b. Struktura projektu/programu:
![struktura-projektu](images/struktura_zad6.png)

<br>
