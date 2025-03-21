[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/7TXVPuTD)
# Object-Oriented Programming (OOP) & Java Concepts

## 1 – Why do we need to use OOP? Some major OOP languages?

Nesne Yönelimli Programlama (OOP), yazılım geliştirmede kodun daha yeniden kullanılabilir, sürdürülebilir ve yönetilebilir olmasını sağlar. OOP sayesinde yazılım modüler hale gelir ve değişiklikler yapmak kolaylaşır. Örneğin, bir uygulamanın sadece bir bileşeni değiştiğinde, tüm sistemi etkilemeden güncelleme yapabiliriz.

OOP’nin temel özellikleri şunlardır:
- **Encapsulation:** Verileri dış dünyadan korur ve sadece gerekli yerlerden erişime izin verir.
- **Inheritance:** Kod tekrarını önleyerek, bir sınıfın özelliklerini başka bir sınıfa aktarılmasını sağlar.
- **Polymorphism:** Aynı metot farklı şekillerde uygulanabilir, böylece kod esnek hale gelir.
- **Abstraction:** Gereksiz detayları gizleyerek, sadece önemli bilgileri gösterir.

**Bazı yaygın OOP dilleri:** Java, C++, Python, C#, Kotlin, Swift.

---

## 2 – Interface vs Abstract Class?

Interface ve abstract class kavramları, Java’da soyutlama sağlamak için kullanılır, ancak farklı amaçlara hizmet ederler.

- **Abstract class**, hem soyut (abstract) hem de gövdeli metotlar içerebilir. Bir sınıf yalnızca bir tane abstract class’ı miras alabilir.
- **Interface**, Java’da çoklu kalıtımı desteklemek için kullanılır ve yalnızca metot imzaları içerir. Java 8 ile birlikte interface'lerde **default ve static metotlar** da tanımlanabilir.

### **Ne zaman hangisini kullanmalıyız?**
- Eğer bir sınıfın yalnızca bir soyut sınıftan türemesi gerekiyorsa ve ortak bir temel davranış içeriyorsa, **abstract class** tercih edilir.
- Eğer bir sınıfın birden fazla farklı yetenekleri kazanması gerekiyorsa, **interface** kullanılır.

---

## 3 – Why do we need `equals()` and `hashCode()`? When to override?

Java’da `equals()` metodu, iki nesnenin içerik olarak eşit olup olmadığını kontrol ederken, `hashCode()` metodu bu nesneye özgü bir sayısal değer üretir.

Eğer bir sınıfı `HashMap`, `HashSet` veya `HashTable` gibi veri yapılarında kullanacaksak, **equals() ve hashCode() metodlarını birlikte override etmeliyiz**.

- `equals()` metodu, nesnelerin **mantıksal eşitliğini** kontrol eder.
- `hashCode()` metodu, nesneleri **hash tabanlı koleksiyonlarda** hızlı erişim için optimize eder.

**Override edilmediği durumda:**
Aynı içeriğe sahip iki nesne, `equals()` ile karşılaştırıldığında **eşit çıkabilir**, ancak `hashCode()` farklı olursa, hash tabanlı koleksiyonlarda beklenmeyen hatalar oluşabilir.

---

## 4 – Diamond Problem in Java? How to fix it?

**Diamond problem**, bir sınıfın **iki farklı üst sınıftan aynı metodu miras alması** durumunda ortaya çıkar. Bu **C++’da yaşanan bir sorundur**.

### **Java’da neden bu problem yok?**
Çünkü **Java, sınıf seviyesinde çoklu kalıtımı desteklemez**. Yani bir sınıf sadece **tek bir sınıftan türeyebilir**.

Ancak, **interface’lerde çoklu kalıtım mümkündür**. Eğer iki interface aynı metodu tanımlıyorsa, alt sınıf bu metodu **override etmek zorundadır**.

---

## 5 – Why do we need Garbage Collector? How does it run?

Java'da **bellek yönetimi Garbage Collector (GC) tarafından otomatik olarak yapılır**. GC’nin temel görevi, kullanılmayan nesneleri bellekten temizlemek ve **bellek sızıntılarını (memory leak) önlemektir**.

### **Garbage Collector çalışma prensibi:**
1. **Mark and Sweep:** Kullanılmayan nesneleri işaretler ve temizler.
2. **Generational Garbage Collection:** Nesneleri **young, old ve permanent** olarak sınıflandırarak belleği optimize eder.

GC’nin avantajı, manuel bellek yönetimini ortadan kaldırmasıdır. Ancak, **GC bazen beklenmedik anda çalışabilir ve performans kaybına neden olabilir**.

---

## 6 – Java `static` keyword usage?

Java'da **`static`** anahtar kelimesi, **bir sınıfa ait olan ancak nesneye bağlı olmayan** değişkenler ve metotlar tanımlamak için kullanılır.

### **Kullanım Alanları:**
- **Static değişkenler (class variables):** Tüm nesneler arasında paylaşılan değişkenler.
- **Static metotlar:** Nesne oluşturmadan çağrılabilen metotlar.
- **Static bloklar:** Sınıf yüklendiğinde bir kere çalışır.
- **Static iç sınıflar:** Dış sınıfın nesnesi olmadan kullanılabilir.

### **Örnek:**
```java
class StaticExample {
    static int count = 0;

    static void increment() {
        count++;
    }

    public static void main(String[] args) {
        StaticExample.increment();
        System.out.println("Static count: " + StaticExample.count);
    }
}

```

## 7 – Immutability means? Where, How, and Why to use it?

Immutable nesneler, oluşturulduktan sonra değiştirilemez. **Örneğin, `String` immutable’dır**.

### **Neden Kullanmalıyız?**
- **Thread-safe olması:** Aynı nesne birçok thread tarafından güvenli şekilde kullanılabilir.
- **Güvenlik:** Nesnenin dışarıdan değiştirilmesini önler.
- **Cache optimizasyonu:** Bellek yönetimini kolaylaştırır.

### **Nasıl Oluşturulur?**
- **Tüm alanları `final` yap.**
- **Sadece getter metotları tanımla.**
- **Constructor içinde değerleri ata ve değiştirilemez yap.**

### **Örnek:**
```java
// Immutable Class Example
final class ImmutablePerson {
    private final String name;
    private final int age;

    public ImmutablePerson(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public static void main(String[] args) {
        ImmutablePerson person = new ImmutablePerson("Alice", 30);
        System.out.println("Name: " + person.getName() + ", Age: " + person.getAge());

        // person.name = "Bob";  // Bu hata verir çünkü değişkenler final'dir.
    }
}
```

## 8 – Composition and Aggregation means and differences?

- **Composition:** Bir sınıf başka bir sınıfın bir parçasıdır ve **bağımsız çalışamaz**.
- **Aggregation:** Bir sınıf başka bir sınıfı içerir ama **bağımsız çalışabilir**.

### **Composition Örneği (Araba ve Motor)**
```java
class Engine {
    void start() {
        System.out.println("Engine is starting...");
    }
}

class Car {
    private Engine engine;

    public Car() {
        engine = new Engine();
    }

    void drive() {
        engine.start();
        System.out.println("Car is moving...");
    }
}

public class Main {
    public static void main(String[] args) {
        Car myCar = new Car();
        myCar.drive();
    }
}
```

### **Aggregation Örneği (Üniversite ve Öğrenci)**
```java
import java.util.*;

class Student {
    String name;

    Student(String name) {
        this.name = name;
    }

    void display() {
        System.out.println("Student: " + name);
    }
}

class University {
    private String universityName;
    private List<Student> students;

    public University(String universityName) {
        this.universityName = universityName;
        this.students = new ArrayList<>();
    }

    void addStudent(Student student) {
        students.add(student);
    }

    void showStudents() {
        System.out.println("Students at " + universityName + ":");
        for (Student s : students) {
            s.display();
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Student s1 = new Student("Alice");
        Student s2 = new Student("Bob");

        University uni = new University("Tech University");
        uni.addStudent(s1);
        uni.addStudent(s2);

        uni.showStudents();
    }
}
```

## 9 – Cohesion and Coupling means and differences?
- **Cohesion:** Bir sınıfın ne kadar belli bir amaca odaklandığını gösterir. **Yüksek olmalıdır.**
- **Coupling:** Bir sınıfın diğer sınıflara olan bağımlılığıdır. **Düşük olmalıdır.**

---

## 10 – Heap and Stack means and differences?
- **Heap:** Nesnelerin saklandığı alan, büyük bellek gerektiren işlemler burada tutulur.
- **Stack:** Metot çağrıları ve yerel değişkenlerin saklandığı alan.

---

## 11 – Exception means? Types of Exceptions?

Exception, programın çalışma zamanında oluşan hataları ifade eder.

### **Türleri:**
- **Checked Exceptions:** Derleme zamanında kontrol edilir. (`IOException`, `SQLException`)
- **Unchecked Exceptions:** Çalışma zamanında oluşur. (`NullPointerException`, `ArithmeticException`)

### **Örnek:**
```java
public class ExceptionExample {
    public static void main(String[] args) {
        try {
            int result = 10 / 0; // ArithmeticException
        } catch (ArithmeticException e) {
            System.out.println("Error: Cannot divide by zero.");
        }
    }
}
```

## 12 – How to summarize ‘clean code’ as short as possible?
Kod, **okunaklı, modüler ve gereksiz karmaşıklıktan uzak olmalıdır.**

---

## 13 - What is method hiding in Java?

Eğer bir **static metot** alt sınıfta **aynı isimle yeniden tanımlanırsa**, **method hiding (metot gizleme)** meydana gelir.

### **Örnek:**
```java
class Parent {
    static void display() {
        System.out.println("Parent Class");
    }
}

class Child extends Parent {
    static void display() {
        System.out.println("Child Class");
    }
}

public class Main {
    public static void main(String[] args) {
        Parent obj = new Child();
        obj.display(); // Çıktı: Parent Class
    }
}
```

## 14 - What is the difference between abstraction and polymorphism in Java?

- **Abstraction:** Detayları gizleyerek önemli bilgileri öne çıkarır (**abstract class** veya **interface** ile sağlanır).
- **Polymorphism:** Aynı metot farklı şekillerde uygulanabilir (**method overriding** ve **method overloading**).

### **Örnek:**
```java
// Abstraction
abstract class Animal {
    abstract void makeSound();
}

class Dog extends Animal {
    void makeSound() {
        System.out.println("Bark");
    }
}

// Polymorphism (Overriding)
class Cat extends Animal {
    void makeSound() {
        System.out.println("Meow");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myDog = new Dog();
        myDog.makeSound(); // Çıktı: Bark

        Animal myCat = new Cat();
        myCat.makeSound(); // Çıktı: Meow
    }
}
```
---
