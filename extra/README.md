### 🧬 `Animal.java` – The Abstract Backbone

```java
public abstract class Animal {
    private String name;
    public Animal(String name) { this.name = name; }
    public String getName() { return name; }
    public abstract void speak();
}
```

- **Purpose**: Base class for all animals (dogs, cats, etc.)
- **OOP Concept**: Abstract class with a contract: every animal **must implement** `speak()`.
- **In Generics**: This is used as a **bounded type parameter** — we constrain generics to `<T extends Animal>` for type safety.

💡 *Best Practice*: Use abstract classes to enforce behavior across subtypes while sharing common logic (like `name` here).

---

### 🐶 `Dog.java` and 🐱 `Cat.java` – Subtypes of Animal

```java
public class Dog extends Animal {
    public Dog(String name) { super(name); }
    public void speak() { System.out.println("Woof! I'm " + getName()); }
}
```

```java
public class Cat extends Animal {
    public Cat(String name) { super(name); }
    public void speak() { System.out.println("Meow! I'm " + getName()); }
}
```

- **Purpose**: Subclasses of `Animal` with specific `speak()` behavior.
- These classes let us **demonstrate polymorphism** and use **generics bounded by Animal**.

🐾 *Mentor Tip*: This is where Java shines — behavior like `speak()` becomes flexible and reusable in generic methods.

---

### 📇 `PetRecordRepository<T>` – Generic Interface

```java
public interface PetRecordRepository<T> {
    void save(T pet);
    T find(String name);
}
```

- **Purpose**: A generic interface for storing and retrieving pet records.
- **Why Generic?**: So we can reuse the same interface for different animal types — `Dog`, `Cat`, even `Dragon` if we ever go full fantasy. 🐉
- Used with **anonymous classes** in `PetClinicDemo`.

🧠 *Best Practice*: Keep interfaces generic so implementations stay type-safe and flexible.

---

### 🧳 `Cage<T>` – Generic Class

```java
public class Cage<T> {
    private T occupant;
    public void put(T animal) { this.occupant = animal; }
    public T get() { return occupant; }
}
```

- **Purpose**: A simple generic container for any animal.
- **Generic Magic**: You can define `Cage<Dog>` or `Cage<Cat>` without code duplication.
- **Highlights**: Java enforces **type safety** at compile-time.

📦 *Think of it like a type-safe box*. Unlike a PHP array, it won't turn into spaghetti if you drop in a banana. 🍌

---

### 💉 `TreatmentUtils.java` – Generic Methods with Bounded Types

```java
public class TreatmentUtils {
    public static <T extends Animal> void vaccinate(T pet) { ... }
    public static <T extends Animal> void treatPet(T pet) { ... }
}
```

- **Purpose**: Contains reusable methods that apply only to animals.
- **Bounded Generics**: `<T extends Animal>` ensures only valid types are treated.
- **Static**: So you can call them without instantiating a class.

⚠️ *Best Practice*: Use bounded types when a method works on a family of types with shared behavior — in this case, all `Animal`s can `speak()`.

---

### 🏠 `AnimalShelter.java` – Wildcards in Action

```java
public void printAll(List<? extends Animal> pets) { ... }
```

- **Purpose**: Accepts any list of animals (dogs, cats, etc.).
- **Wildcard `? extends Animal`**: This means “any subtype of Animal”.
- **Why Wildcards?**: Useful when you're reading (not writing) from a generic collection.

📚 *Wildcards are tricky*, but think of `? extends T` as **read-only** and `? super T` for **write operations**.

---

### 🎬 `PetClinicDemo.java` – Where It All Comes Together

```java
public class PetClinicDemo {
    public static void main(String[] args) { ... }
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

