### Timestamp: 2024-10-28 13:50 UTC

**Summary:**
This section focuses on **Behavioral Patterns** from the Gang of Four, detailing their definitions, use cases, and implementations in Java, Python, Rust, and TypeScript.

---

## Part 3: Behavioral Patterns

Behavioral design patterns are concerned with algorithms and the assignment of responsibilities between objects. They help define how objects interact and communicate in complex systems.

### 3.1 Observer Pattern

**Definition:**
The Observer pattern defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

**Use Cases:**
- When a change to one object requires changing others, and you don’t know how many objects need to change.
- In event-driven systems (like GUIs or real-time data feeds).

**Implementation:**

- **Java:**
  ```java
  import java.util.ArrayList;
  import java.util.List;

  interface Observer {
      void update(String message);
  }

  class ConcreteObserver implements Observer {
      private String name;

      public ConcreteObserver(String name) {
          this.name = name;
      }

      public void update(String message) {
          System.out.println(name + " received: " + message);
      }
  }

  class Subject {
      private List<Observer> observers = new ArrayList<>();

      public void addObserver(Observer observer) {
          observers.add(observer);
      }

      public void notifyObservers(String message) {
          for (Observer observer : observers) {
              observer.update(message);
          }
      }
  }
  ```

- **Python:**
  ```python
  class Observer:
      def update(self, message):
          pass

  class ConcreteObserver(Observer):
      def __init__(self, name):
          self.name = name

      def update(self, message):
          print(f"{self.name} received: {message}")

  class Subject:
      def __init__(self):
          self.observers = []

      def add_observer(self, observer):
          self.observers.append(observer)

      def notify_observers(self, message):
          for observer in self.observers:
              observer.update(message)
  ```

- **Rust:**
  ```rust
  trait Observer {
      fn update(&self, message: &str);
  }

  struct ConcreteObserver {
      name: String,
  }

  impl Observer for ConcreteObserver {
      fn update(&self, message: &str) {
          println!("{} received: {}", self.name, message);
      }
  }

  struct Subject {
      observers: Vec<Box<dyn Observer>>,
  }

  impl Subject {
      fn add_observer(&mut self, observer: Box<dyn Observer>) {
          self.observers.push(observer);
      }

      fn notify_observers(&self, message: &str) {
          for observer in &self.observers {
              observer.update(message);
          }
      }
  }
  ```

- **TypeScript:**
  ```typescript
  interface Observer {
      update(message: string): void;
  }

  class ConcreteObserver implements Observer {
      constructor(private name: string) {}

      update(message: string): void {
          console.log(`${this.name} received: ${message}`);
      }
  }

  class Subject {
      private observers: Observer[] = [];

      addObserver(observer: Observer): void {
          this.observers.push(observer);
      }

      notifyObservers(message: string): void {
          for (const observer of this.observers) {
              observer.update(message);
          }
      }
  }
  ```

### 3.2 Strategy Pattern

**Definition:**
The Strategy pattern defines a family of algorithms, encapsulates each one, and makes them interchangeable. The Strategy lets the algorithm vary independently from clients that use it.

**Use Cases:**
- When multiple algorithms can be applied to a given task.
- When the client needs to choose the algorithm at runtime.

**Implementation:**

- **Java:**
  ```java
  interface Strategy {
      int execute(int a, int b);
  }

  class AddStrategy implements Strategy {
      public int execute(int a, int b) {
          return a + b;
      }
  }

  class SubtractStrategy implements Strategy {
      public int execute(int a, int b) {
          return a - b;
      }
  }

  class Context {
      private Strategy strategy;

      public void setStrategy(Strategy strategy) {
          this.strategy = strategy;
      }

      public int executeStrategy(int a, int b) {
          return strategy.execute(a, b);
      }
  }
  ```

- **Python:**
  ```python
  class Strategy:
      def execute(self, a, b):
          pass

  class AddStrategy(Strategy):
      def execute(self, a, b):
          return a + b

  class SubtractStrategy(Strategy):
      def execute(self, a, b):
          return a - b

  class Context:
      def __init__(self, strategy: Strategy):
          self.strategy = strategy

      def execute_strategy(self, a, b):
          return self.strategy.execute(a, b)
  ```

- **Rust:**
  ```rust
  trait Strategy {
      fn execute(&self, a: i32, b: i32) -> i32;
  }

  struct AddStrategy;

  impl Strategy for AddStrategy {
      fn execute(&self, a: i32, b: i32) -> i32 {
          a + b
      }
  }

  struct Context<'a> {
      strategy: &'a dyn Strategy,
  }

  impl<'a> Context<'a> {
      fn execute_strategy(&self, a: i32, b: i32) -> i32 {
          self.strategy.execute(a, b)
      }
  }
  ```

- **TypeScript:**
  ```typescript
  interface Strategy {
      execute(a: number, b: number): number;
  }

  class AddStrategy implements Strategy {
      execute(a: number, b: number): number {
          return a + b;
      }
  }

  class SubtractStrategy implements Strategy {
      execute(a: number, b: number): number {
          return a - b;
      }
  }

  class Context {
      private strategy: Strategy;

      setStrategy(strategy: Strategy): void {
          this.strategy = strategy;
      }

      executeStrategy(a: number, b: number): number {
          return this.strategy.execute(a, b);
      }
  }
  ```

### 3.3 Command Pattern

**Definition:**
The Command pattern encapsulates a request as an object, thereby allowing for parameterization of clients with queues, requests, and operations.

**Use Cases:**
- When you need to queue requests, log operations, or support undoable operations.
- When operations need to be parameterized and executed at a later time.

**Implementation:**

- **Java:**
  ```java
  interface Command {
      void execute();
  }

  class Light {
      void turnOn() {
          System.out.println("Light is ON");
      }

      void turnOff() {
          System.out.println("Light is OFF");
      }
  }

  class TurnOnCommand implements Command {
      private Light light;

      public TurnOnCommand(Light light) {
          this.light = light;
      }

      public void execute() {
          light.turnOn();
      }
  }

  class TurnOffCommand implements Command {
      private Light light;

      public TurnOffCommand(Light light) {
          this.light = light;
      }

      public void execute() {
          light.turnOff();
      }
  }

  class RemoteControl {
      private Command command;

      public void setCommand(Command command) {
          this.command = command;
      }

      public void pressButton() {
          command.execute();
      }
  }
  ```

- **Python:**
  ```python
  class Command:
      def execute(self):
          pass

  class Light:
      def turn_on(self):
          print("Light is ON")

      def turn_off(self):
          print("Light is OFF")

  class TurnOnCommand(Command):
      def __init__(self, light):
          self.light = light

      def execute(self):
          self.light.turn_on()

  class TurnOffCommand(Command):
      def __init__(self, light):
          self.light = light

      def execute(self):
          self.light.turn_off()

  class RemoteControl:
      def __init__(self):
          self.command = None

      def set_command(self, command):
          self.command = command

      def press_button(self):
          self.command.execute()
  ```

- **Rust:**
  ```rust
  trait Command {
      fn execute(&self);
  }

  struct Light;

  impl Light {
      fn turn_on(&self) {
          println!("Light is ON");
      }

      fn turn_off(&self) {
          println!("Light is OFF");
      }
  }

  struct TurnOnCommand<'a> {
      light: &'a Light,
  }

  impl<'a> Command for TurnOnCommand<'a> {
      fn execute(&self) {
          self.light.turn_on();
      }
  }

  struct RemoteControl<'a> {
      command: Box<dyn Command + 'a>,
  }

  impl<'a> RemoteControl<'a> {
      fn press_button(&self) {
          self.command.execute();
      }
  }
  ```

- **TypeScript:**
  ```typescript
  interface Command {
      execute(): void;
  }

  class Light {
      turnOn(): void {
          console.log("Light is ON");
      }

      turnOff(): void {
          console.log("Light is OFF");
      }
  }

  class TurnOnCommand implements Command {
      constructor(private light: Light) {}

      execute(): void {
          this.light.turnOn();
      }
  }

  class TurnOffCommand implements Command {
      constructor

(private light: Light) {}

      execute(): void {
          this.light.turnOff();
      }
  }

  class RemoteControl {
      private command: Command;

      setCommand(command: Command): void {
          this.command = command;
      }

      pressButton(): void {
          this.command.execute();
      }
  }
  ```

### Conclusion

Behavioral patterns enhance the interaction between objects, defining clear responsibilities and communication pathways. Patterns like Observer, Strategy, and Command illustrate how to manage behavior effectively, making systems easier to extend and maintain. The implementations across different programming languages serve as practical examples for integrating these patterns into your projects.

---

### Filename: 
```bash
nvim   behavioral_patterns.md
```

**Total Lines:** 97  
**Total Characters:** 6888
