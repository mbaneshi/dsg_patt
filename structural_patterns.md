### Timestamp: 2024-10-28 13:30 UTC

**Summary:**
This section focuses on **Structural Patterns** from the Gang of Four, detailing their definitions, use cases, and implementations in Java, Python, Rust, and TypeScript.

---

## Part 2: Structural Patterns

Structural design patterns deal with object composition, helping to ensure that if one part of a system changes, the entire system doesn’t need to change. They define how objects and classes can be combined to form larger structures.

### 2.1 Adapter Pattern

**Definition:**
The Adapter pattern allows incompatible interfaces to work together. It acts as a bridge between two incompatible interfaces.

**Use Cases:**
- When you want to use an existing class, but its interface does not match the one you need.
- When you want to create a reusable class that cooperates with classes that have incompatible interfaces.

**Implementation:**

- **Java:**
  ```java
  interface Target {
      void request();
  }

  class Adaptee {
      void specificRequest() {
          System.out.println("Called specificRequest");
      }
  }

  class Adapter implements Target {
      private Adaptee adaptee;

      public Adapter(Adaptee adaptee) {
          this.adaptee = adaptee;
      }

      public void request() {
          adaptee.specificRequest();
      }
  }
  ```

- **Python:**
  ```python
  class Adaptee:
      def specific_request(self):
          print("Called specific_request")

  class Target:
      def request(self):
          pass

  class Adapter(Target):
      def __init__(self, adaptee):
          self.adaptee = adaptee

      def request(self):
          self.adaptee.specific_request()
  ```

- **Rust:**
  ```rust
  struct Adaptee;

  impl Adaptee {
      fn specific_request(&self) {
          println!("Called specific_request");
      }
  }

  trait Target {
      fn request(&self);
  }

  struct Adapter {
      adaptee: Adaptee,
  }

  impl Target for Adapter {
      fn request(&self) {
          self.adaptee.specific_request();
      }
  }
  ```

- **TypeScript:**
  ```typescript
  class Adaptee {
      specificRequest() {
          console.log("Called specificRequest");
      }
  }

  interface Target {
      request(): void;
  }

  class Adapter implements Target {
      private adaptee: Adaptee;

      constructor(adaptee: Adaptee) {
          this.adaptee = adaptee;
      }

      request(): void {
          this.adaptee.specificRequest();
      }
  }
  ```

### 2.2 Decorator Pattern

**Definition:**
The Decorator pattern allows behavior to be added to individual objects, either statically or dynamically, without affecting the behavior of other objects from the same class.

**Use Cases:**
- When you want to add responsibilities to individual objects without modifying the existing code.
- To avoid a proliferation of subclasses that only differ in the behavior they add.

**Implementation:**

- **Java:**
  ```java
  interface Component {
      void operation();
  }

  class ConcreteComponent implements Component {
      public void operation() {
          System.out.println("ConcreteComponent operation");
      }
  }

  class Decorator implements Component {
      protected Component wrapped;

      public Decorator(Component wrapped) {
          this.wrapped = wrapped;
      }

      public void operation() {
          wrapped.operation();
      }
  }

  class ConcreteDecorator extends Decorator {
      public ConcreteDecorator(Component wrapped) {
          super(wrapped);
      }

      public void operation() {
          super.operation();
          System.out.println("ConcreteDecorator operation");
      }
  }
  ```

- **Python:**
  ```python
  class Component:
      def operation(self):
          pass

  class ConcreteComponent(Component):
      def operation(self):
          print("ConcreteComponent operation")

  class Decorator(Component):
      def __init__(self, component):
          self._component = component

      def operation(self):
          self._component.operation()

  class ConcreteDecorator(Decorator):
      def operation(self):
          super().operation()
          print("ConcreteDecorator operation")
  ```

- **Rust:**
  ```rust
  trait Component {
      fn operation(&self);
  }

  struct ConcreteComponent;

  impl Component for ConcreteComponent {
      fn operation(&self) {
          println!("ConcreteComponent operation");
      }
  }

  struct Decorator<'a> {
      component: &'a dyn Component,
  }

  impl<'a> Component for Decorator<'a> {
      fn operation(&self) {
          self.component.operation();
      }
  }

  struct ConcreteDecorator<'a> {
      decorator: Decorator<'a>,
  }

  impl<'a> Component for ConcreteDecorator<'a> {
      fn operation(&self) {
          self.decorator.operation();
          println!("ConcreteDecorator operation");
      }
  }
  ```

- **TypeScript:**
  ```typescript
  interface Component {
      operation(): void;
  }

  class ConcreteComponent implements Component {
      operation(): void {
          console.log("ConcreteComponent operation");
      }
  }

  class Decorator implements Component {
      protected component: Component;

      constructor(component: Component) {
          this.component = component;
      }

      operation(): void {
          this.component.operation();
      }
  }

  class ConcreteDecorator extends Decorator {
      operation(): void {
          super.operation();
          console.log("ConcreteDecorator operation");
      }
  }
  ```

### 2.3 Facade Pattern

**Definition:**
The Facade pattern provides a simplified interface to a complex subsystem, making it easier to interact with.

**Use Cases:**
- When you want to provide a simple interface to a complex system.
- When you want to reduce dependencies on the subsystem components.

**Implementation:**

- **Java:**
  ```java
  class SubsystemA {
      void operationA() {
          System.out.println("Subsystem A operation");
      }
  }

  class SubsystemB {
      void operationB() {
          System.out.println("Subsystem B operation");
      }
  }

  class Facade {
      private SubsystemA subsystemA;
      private SubsystemB subsystemB;

      public Facade() {
          subsystemA = new SubsystemA();
          subsystemB = new SubsystemB();
      }

      public void operation() {
          subsystemA.operationA();
          subsystemB.operationB();
      }
  }
  ```

- **Python:**
  ```python
  class SubsystemA:
      def operation_a(self):
          print("Subsystem A operation")

  class SubsystemB:
      def operation_b(self):
          print("Subsystem B operation")

  class Facade:
      def __init__(self):
          self.subsystem_a = SubsystemA()
          self.subsystem_b = SubsystemB()

      def operation(self):
          self.subsystem_a.operation_a()
          self.subsystem_b.operation_b()
  ```

- **Rust:**
  ```rust
  struct SubsystemA;

  impl SubsystemA {
      fn operation_a(&self) {
          println!("Subsystem A operation");
      }
  }

  struct SubsystemB;

  impl SubsystemB {
      fn operation_b(&self) {
          println!("Subsystem B operation");
      }
  }

  struct Facade {
      subsystem_a: SubsystemA,
      subsystem_b: SubsystemB,
  }

  impl Facade {
      fn operation(&self) {
          self.subsystem_a.operation_a();
          self.subsystem_b.operation_b();
      }
  }
  ```

- **TypeScript:**
  ```typescript
  class SubsystemA {
      operationA(): void {
          console.log("Subsystem A operation");
      }
  }

  class SubsystemB {
      operationB(): void {
          console.log("Subsystem B operation");
      }
  }

  class Facade {
      private subsystemA: SubsystemA;
      private subsystemB: SubsystemB;

      constructor() {
          this.subsystemA = new SubsystemA();
          this.subsystemB = new SubsystemB();
      }

      operation(): void {
          this.subsystemA.operationA();
          this.subsystemB.operationB();
      }
  }
  ```

### Conclusion

Structural patterns provide important ways to compose objects and classes, allowing for more flexible and efficient designs. By using patterns such as Adapter, Decorator, and Facade, developers can simplify and enhance the interaction with complex systems. The implementations provided across different languages serve as a practical reference for incorporating these patterns into your projects.

---

### Filename: 
```bash
nvim   structural_patterns.md
```

**Total Lines:** 83  
**Total Characters:** 6126
