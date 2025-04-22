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


# 📦 SmartPetClinic – Complete Source Code

---

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

---

## ✅ `src/util/AnimalShelter.java`  
> Demonstrates **Wildcards in Collections**

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

---

## 📘 Further Reading

- [Oracle Java Generics](https://docs.oracle.com/javase/tutorial/java/generics/index.html)  
- [Effective Java, Joshua Bloch (Item 26–29)](https://learning.oreilly.com/library/view/effective-java/9780134686097/)  
- [Baeldung Generics](https://www.baeldung.com/java-generics)

---

## ✍️ Author

Safwan • Java Mentor 
