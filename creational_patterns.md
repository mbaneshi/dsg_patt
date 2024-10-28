### Timestamp: 2024-10-28 13:10 UTC

**Summary:**
This elaboration on the first part focuses on **Creational Patterns** from the Gang of Four, detailing their definitions, use cases, and implementations in Java, Python, Rust, and TypeScript.

---

## Part 1: Creational Patterns

Creational design patterns are concerned with the way of creating objects in a manner suitable to the situation. These patterns can be divided into class-creation patterns and object-creational patterns. They provide various mechanisms for object creation, which increase flexibility and reuse of existing code.

### 1.1 Singleton Pattern

**Definition:**
The Singleton pattern ensures a class has only one instance and provides a global point of access to that instance.

**Use Cases:**
- When exactly one instance of a class is needed to control actions (e.g., logging, configuration settings).
- Managing shared resources like database connections.

**Implementation:**

- **Java:**
  ```java
  public class Singleton {
      private static Singleton instance;

      private Singleton() {}

      public static Singleton getInstance() {
          if (instance == null) {
              instance = new Singleton();
          }
          return instance;
      }
  }
  ```

- **Python:**
  ```python
  class Singleton:
      _instance = None

      def __new__(cls):
          if cls._instance is None:
              cls._instance = super(Singleton, cls).__new__(cls)
          return cls._instance
  ```

- **Rust:**
  ```rust
  use std::sync::{Mutex, Arc};

  struct Singleton {
      // fields here
  }

  impl Singleton {
      fn instance() -> Arc<Mutex<Self>> {
          static mut INSTANCE: Option<Arc<Mutex<Singleton>>> = None;
          unsafe {
              INSTANCE.get_or_insert_with(|| Arc::new(Mutex::new(Singleton {}))).clone()
          }
      }
  }
  ```

- **TypeScript:**
  ```typescript
  class Singleton {
      private static instance: Singleton;

      private constructor() {}

      public static getInstance(): Singleton {
          if (!Singleton.instance) {
              Singleton.instance = new Singleton();
          }
          return Singleton.instance;
      }
  }
  ```

### 1.2 Factory Method Pattern

**Definition:**
The Factory Method pattern defines an interface for creating an object but lets subclasses alter the type of objects that will be created.

**Use Cases:**
- When a class can't anticipate the class of objects it must create.
- Delegating the instantiation process to subclasses.

**Implementation:**

- **Java:**
  ```java
  abstract class Product {
      public abstract void use();
  }

  class ConcreteProductA extends Product {
      public void use() {
          System.out.println("Using Product A");
      }
  }

  class ConcreteProductB extends Product {
      public void use() {
          System.out.println("Using Product B");
      }
  }

  abstract class Creator {
      public abstract Product factoryMethod();
  }

  class ConcreteCreatorA extends Creator {
      public Product factoryMethod() {
          return new ConcreteProductA();
      }
  }

  class ConcreteCreatorB extends Creator {
      public Product factoryMethod() {
          return new ConcreteProductB();
      }
  }
  ```

- **Python:**
  ```python
  from abc import ABC, abstractmethod

  class Product(ABC):
      @abstractmethod
      def use(self):
          pass

  class ConcreteProductA(Product):
      def use(self):
          print("Using Product A")

  class Creator(ABC):
      @abstractmethod
      def factory_method(self) -> Product:
          pass

  class ConcreteCreatorA(Creator):
      def factory_method(self) -> Product:
          return ConcreteProductA()
  ```

- **Rust:**
  ```rust
  trait Product {
      fn use_product(&self);
  }

  struct ConcreteProductA;

  impl Product for ConcreteProductA {
      fn use_product(&self) {
          println!("Using Product A");
      }
  }

  trait Creator {
      fn factory_method(&self) -> Box<dyn Product>;
  }

  struct ConcreteCreatorA;

  impl Creator for ConcreteCreatorA {
      fn factory_method(&self) -> Box<dyn Product> {
          Box::new(ConcreteProductA)
      }
  }
  ```

- **TypeScript:**
  ```typescript
  interface Product {
      use(): void;
  }

  class ConcreteProductA implements Product {
      public use() {
          console.log("Using Product A");
      }
  }

  abstract class Creator {
      abstract factoryMethod(): Product;
  }

  class ConcreteCreatorA extends Creator {
      factoryMethod(): Product {
          return new ConcreteProductA();
      }
  }
  ```

### 1.3 Abstract Factory Pattern

**Definition:**
The Abstract Factory pattern provides an interface for creating families of related or dependent objects without specifying their concrete classes.

**Use Cases:**
- When a system should be independent of how its products are created, composed, and represented.
- When you want to provide a library of products that can be easily swapped out.

**Implementation:**

- **Java:**
  ```java
  interface AbstractFactory {
      ProductA createProductA();
      ProductB createProductB();
  }

  class ConcreteFactory1 implements AbstractFactory {
      public ProductA createProductA() {
          return new ConcreteProductA1();
      }
      public ProductB createProductB() {
          return new ConcreteProductB1();
      }
  }

  class ConcreteFactory2 implements AbstractFactory {
      public ProductA createProductA() {
          return new ConcreteProductA2();
      }
      public ProductB createProductB() {
          return new ConcreteProductB2();
      }
  }
  ```

- **Python:**
  ```python
  class AbstractFactory(ABC):
      @abstractmethod
      def create_product_a(self):
          pass

      @abstractmethod
      def create_product_b(self):
          pass

  class ConcreteFactory1(AbstractFactory):
      def create_product_a(self):
          return ConcreteProductA1()

      def create_product_b(self):
          return ConcreteProductB1()
  ```

- **Rust:**
  ```rust
  trait AbstractFactory {
      fn create_product_a(&self) -> Box<dyn Product>;
      fn create_product_b(&self) -> Box<dyn Product>;
  }

  struct ConcreteFactory1;

  impl AbstractFactory for ConcreteFactory1 {
      fn create_product_a(&self) -> Box<dyn Product> {
          Box::new(ConcreteProductA1)
      }
      fn create_product_b(&self) -> Box<dyn Product> {
          Box::new(ConcreteProductB1)
      }
  }
  ```

- **TypeScript:**
  ```typescript
  interface AbstractFactory {
      createProductA(): ProductA;
      createProductB(): ProductB;
  }

  class ConcreteFactory1 implements AbstractFactory {
      createProductA(): ProductA {
          return new ConcreteProductA1();
      }
      createProductB(): ProductB {
          return new ConcreteProductB1();
      }
  }
  ```

### Conclusion

Creational patterns play a vital role in object creation and management within software systems. Understanding these patterns allows developers to produce code that is more flexible and easier to maintain. The above examples provide a solid foundation for implementation across different programming languages, allowing developers to choose the most appropriate one for their project needs.

---

### Filename: 
```bash
nvim   creational_patterns.md
```

**Total Lines:** 78  
**Total Characters:** 5570
