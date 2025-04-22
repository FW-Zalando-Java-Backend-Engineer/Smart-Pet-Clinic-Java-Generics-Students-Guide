# 🐾 SmartPetClinic – Java Generics Demo

Welcome to the **Smart Pet Clinic** – a fun, relatable Java project that brings **Java Generics** to life through a pet care management system.

Ideal for **students and junior devs**, this project focuses on mastering generics in real-world, type-safe object-oriented programming.

---

## 📦 What This Project Covers

- ✅ Generic Classes (`Cage<T>`, `Clinic<T>`)
- ✅ Generic Interfaces (`PetRecordRepository<T>`)
- ✅ Generic Methods (`<T> void treatPet(T pet)`)
- ✅ Bounded Type Parameters (`<T extends Animal>`)
- ✅ Inheritance with Generics (`Dog extends Animal`, etc.)
- ✅ Wildcards in Collections
- ✅ Type Erasure under the hood

---

## 🛠️ Technologies Used

- Java 8+ (JDK 17 friendly)
- Git Bash / Terminal
- IDE: IntelliJ / Eclipse / VS Code (your choice, no judgment... unless it’s JavaStorm 😉)

---

## 🚀 How to Run

### 🔹 1. Compile

```bash
javac -d out src/**/*.java
```

> Compiles all Java classes inside the `src` directory to the `out` folder.

### 🔹 2. Run Main

```bash
java -cp out main.PetClinicDemo
```

> `PetClinicDemo.java` is your friendly main class that kicks off the fun.

---


## 🧠 Key Concepts Explained: Deep Dive with Step-by-Step


## 📁 Project Structure

```
SmartPetClinic/
├── src/
│   ├── main/
│   │   └── PetClinicDemo.java
│   ├── clinic/
│   │   ├── Animal.java
│   │   ├── Dog.java
│   │   ├── Cat.java
│   │   ├── PetRecordRepository.java
│   ├── util/
│   │   ├── Cage.java
│   │   ├── TreatmentUtils.java
│   │   └── AnimalShelter.java
├── README.md
```

---

## ✅ `src/clinic/Animal.java`  
> Abstract base class — covers **Inheritance** and supports **Bounded Types**

```java
package clinic;

public abstract class Animal {
    private String name;

    public Animal(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public abstract void speak();
}
```

- **Purpose**: Base class for all animals (dogs, cats, etc.)
- **OOP Concept**: Abstract class with a contract: every animal **must implement** `speak()`.
- **In Generics**: This is used as a **bounded type parameter** — we constrain generics to `<T extends Animal>` for type safety.

💡 *Best Practice*: Use abstract classes to enforce behavior across subtypes while sharing common logic (like `name` here).

---

## ✅ `src/clinic/Dog.java`

```java
package clinic;

public class Dog extends Animal {
    public Dog(String name) {
        super(name);
    }

    @Override
    public void speak() {
        System.out.println("Woof! I'm " + getName());
    }
}
```

---

## ✅ `src/clinic/Cat.java`

```java
package clinic;

public class Cat extends Animal {
    public Cat(String name) {
        super(name);
    }

    @Override
    public void speak() {
        System.out.println("Meow! I'm " + getName());
    }
}
```
`Dog.java` and 🐱 `Cat.java` – Subtypes of Animal:
- **Purpose**: Subclasses of `Animal` with specific `speak()` behavior.
- These classes let us **demonstrate polymorphism** and use **generics bounded by Animal**.

🐾 *Mentor Tip*: This is where Java shines — behavior like `speak()` becomes flexible and reusable in generic methods.

---

## ✅ `src/clinic/PetRecordRepository.java`  
> Demonstrates **Generic Interfaces**

```java
package clinic;

public interface PetRecordRepository<T> {
    void save(T pet);
    T find(String name);
}
```

- **Purpose**: A generic interface for storing and retrieving pet records.
- **Why Generic?**: So we can reuse the same interface for different animal types — `Dog`, `Cat`, even `Dragon` if we ever go full fantasy. 🐉
- Used with **anonymous classes** in `PetClinicDemo`.

---

## ✅ `src/util/Cage.java`  
> Demonstrates **Generic Classes**

```java
package util;

public class Cage<T> {
    private T occupant;

    public void put(T animal) {
        this.occupant = animal;
    }

    public T get() {
        return occupant;
    }
}
```

- **Purpose**: A simple generic container for any animal.
- **Generic Magic**: You can define `Cage<Dog>` or `Cage<Cat>` without code duplication.
- **Highlights**: Java enforces **type safety** at compile-time.

📦 *Think of it like a type-safe box*. And it won't turn into spaghetti if you drop in a banana. 🍌

---

## ✅ `src/util/TreatmentUtils.java`  
> Demonstrates **Generic Methods** and **Bounded Types**

```java
package util;

import clinic.Animal;

public class TreatmentUtils {
    public static <T extends Animal> void vaccinate(T pet) {
        System.out.println("Vaccinating " + pet.getName());
        pet.speak();
    }

    public static <T extends Animal> void treatPet(T pet) {
        System.out.println("Treating " + pet.getName());
        pet.speak();
    }
}
```

- **Purpose**: Contains reusable methods that apply only to animals.
- **Bounded Generics**: `<T extends Animal>` ensures only valid types are treated.
- **Static**: So you can call them without instantiating a class.

⚠️ *Best Practice*: Use bounded types when a method works on a family of types with shared behavior — in this case, all `Animal`s can `speak()`.

---

## ✅ `src/util/AnimalShelter.java`  
> Demonstrates [**Wildcards in Collections**](https://github.com/FW-Zalando-Java-Backend-Engineer/Smart-Pet-Clinic-Java-Generics-Students-Guide/blob/main/Wildcards/README.md)

```java
package util;

import clinic.Animal;
import java.util.List;

public class AnimalShelter {
    public void printAll(List<? extends Animal> pets) {
        for (Animal pet : pets) {
            System.out.println("Sheltered: " + pet.getName());
        }
    }
}
```

- **Purpose**: Accepts any list of animals (dogs, cats, etc.).
- **Wildcard `? extends Animal`**: This means “any subtype of Animal”.
- **Why Wildcards?**: Useful when you're reading (not writing) from a generic collection.

📚 *Wildcards are tricky*, but think of `? extends T` as **read-only** and `? super T` for **write operations**.

---

## ✅ `src/main/PetClinicDemo.java`  
> Ties all concepts together

```java
package main;

import clinic.*;
import util.*;

import java.util.*;

public class PetClinicDemo {
    public static void main(String[] args) {
        // ✅ Generic Class
        Cage<Dog> dogCage = new Cage<>();
        dogCage.put(new Dog("Rex"));
        System.out.println("Dog in cage: " + dogCage.get().getName());

        // ✅ Bounded Type Parameter + Generic Method
        Dog dog = new Dog("Buddy");
        TreatmentUtils.vaccinate(dog);
        TreatmentUtils.treatPet(dog);

        // ✅ Generic Interface Usage
        PetRecordRepository<Cat> catRepo = new PetRecordRepository<Cat>() {
            private Map<String, Cat> catMap = new HashMap<>();
            public void save(Cat pet) { catMap.put(pet.getName(), pet); }
            public Cat find(String name) { return catMap.get(name); }
        };

        Cat kitty = new Cat("Whiskers");
        catRepo.save(kitty);
        System.out.println("Found cat: " + catRepo.find("Whiskers").getName());

        // ✅ Wildcards
        AnimalShelter shelter = new AnimalShelter();
        List<Animal> animals = Arrays.asList(
            new Dog("Fido"),
            new Cat("Luna")
        );
        shelter.printAll(animals);

        // ✅ Type Erasure demonstration (theory - explained in README)
        System.out.println("Type erasure prevents runtime access to generic types.");
    }
}
```

- **Purpose**: Demo app that glues all the pieces together.
- **Highlights**:
  - Uses generic class (`Cage`)
  - Calls bounded generic methods
  - Implements generic interface anonymously
  - Works with wildcards in lists

🧪 This class is the **testing ground** — like your kitchen when you’re trying to cook something new: some Dog, a bit of Cat, throw in a Shelter, and voilá — Java Gourmet.

---

### 🚀 Summary: Concepts Mastered Here

| Concept                | Where It’s Used           |
|------------------------|---------------------------|
| Generic Class          | `Cage<T>`                 |
| Generic Interface      | `PetRecordRepository<T>`  |
| Generic Method         | `treatPet`, `vaccinate`   |
| Bounded Type           | `<T extends Animal>`      |
| Wildcards              | `List<? extends Animal>`  |
| Type Erasure (Theory)  | Mentioned in Demo output  |


---

### 📘 SmartPetClinic ( Class Relationships Diagram)

<pre>
                        +------------------+
                        |     Animal       |  <--- Abstract base class
                        +------------------+
                          ▲            ▲
                   extends         extends
                          |            |
                  +-------+----+ +-----+------+
                  |    Dog     | |    Cat     |
                  +------------+ +------------+

    +---------------------+         +-----------------------------+
    |     Cage<T>         |         |  PetRecordRepository<T>     |
    | (Generic Class)     |         |  (Generic Interface)        |
    +---------------------+         +-----------------------------+
             ▲                                ▲
             |                                |
         used with                        implemented by
             |                                |
         +---+--------------------+      +----+-----------------+
         |                        |      |                      |
         |                    +--------+------------------+     |
         |                    | PetClinicDemo (main)      |     |
         |                    +---------------------------+     |
         |                          ▲         ▲           ▲     |
         |                          |         |           |     |
         |         +----------------+   +-----+-----+ +---+---+ |
         |         | TreatmentUtils |   | AnimalShelter| | Map  | |
         |         | (Generic utils)|   | (Wildcards)  | |<T>   | |
         |         +----------------+   +-------------+ +-------+ |
         |                      treats, vaccinates        stores   |
         +---------------------------------------------------------+
</pre>


---

### 🧠 Legend
- `▲` = "extends" or "implements"
- `used with`, `treated by`, etc. describe usage relationships
- `PetClinicDemo` is the orchestrator that ties all components together

---

---
## 📘 Further Reading

- [Oracle Java Generics](https://docs.oracle.com/javase/tutorial/java/generics/index.html)  
- [Baeldung Generics](https://www.baeldung.com/java-generics)

---

## ✍️ Author

Safwan • Java Mentor 
