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

## 📂 Project Structure

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

## 🧠 Key Concepts Explained

### 💡 Generic Class – `Cage<T>`

```java
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

> This shows how a `Cage` can contain any type of animal, ensuring type safety.

---

### 💡 Bounded Types – Treat only `Animal` or subclasses

```java
public class TreatmentUtils {
    public static <T extends Animal> void vaccinate(T pet) {
        System.out.println("Vaccinating " + pet.getName());
    }
}
```

> Ensures only pets (and not humans or unrelated classes!) can be treated.

---

### 💡 Generic Interface – `PetRecordRepository<T>`

```java
public interface PetRecordRepository<T> {
    void save(T pet);
    T find(String name);
}
```

> Students can create implementations for different animals: `DogRecordRepo`, `CatRecordRepo`.

---

### 💡 Wildcards in Action

```java
public class AnimalShelter {
    public void printAll(List<? extends Animal> pets) {
        pets.forEach(p -> System.out.println(p.getName()));
    }
}
```

> Useful when handling lists of any type of `Animal` subclass in a read-only context.

---

## ✍️ Author

Safwan • Java Mentor & Pet Lover  
Twitter: [@SafwanJava](#)  
Site: [StartSteps Training](#)

---

## 📘 License

MIT License – because good knowledge should be free (and bug-free 🐛✨)
