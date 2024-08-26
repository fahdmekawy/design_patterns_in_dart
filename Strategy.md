### **What is the Strategy Design Pattern?**

The **Strategy Design Pattern** is a behavioral design pattern that allows you to define a family of algorithms, encapsulate each one, and make them interchangeable. This pattern enables a class's behavior to be selected at runtime. The strategy pattern is typically used to create a set of algorithms, encapsulate each one in a separate class, and make them interchangeable within the original context object.

### Key Concepts
1. **Strategy Interface:** Defines a common interface for all strategies (algorithms).
2. **Concrete Strategies:** Implement different algorithms or behaviors by adhering to the strategy interface.
3. **Context Class:** Holds a reference to a strategy and allows the client to choose the strategy at runtime.

### Example in Dart

Let's consider a real-world example of payment methods in a shopping app. You might have different payment methods like Credit Card, PayPal, and Bitcoin. Each payment method can be treated as a different strategy.

#### Step 1: Define the Strategy Interface

```dart
abstract class PaymentStrategy {
  void pay(double amount);
}
```

#### Step 2: Create Concrete Strategies

```dart
class CreditCardPayment implements PaymentStrategy {
  @override
  void pay(double amount) {
    print('Paid \$${amount} using Credit Card.');
  }
}

class PayPalPayment implements PaymentStrategy {
  @override
  void pay(double amount) {
    print('Paid \$${amount} using PayPal.');
  }
}

class BitcoinPayment implements PaymentStrategy {
  @override
  void pay(double amount) {
    print('Paid \$${amount} using Bitcoin.');
  }
}
```

#### Step 3: Implement the Context Class

```dart
class PaymentContext {
  PaymentStrategy? _strategy;

  void setPaymentStrategy(PaymentStrategy strategy) {
    _strategy = strategy;
  }

  void makePayment(double amount) {
    if (_strategy == null) {
      print('No payment strategy selected.');
    } else {
      _strategy!.pay(amount);
    }
  }
}
```

#### Step 4: Use the Strategy Pattern

```dart
void main() {
  PaymentContext paymentContext = PaymentContext();

  // User chooses to pay using Credit Card
  paymentContext.setPaymentStrategy(CreditCardPayment());
  paymentContext.makePayment(100.0);

  // User decides to switch to PayPal
  paymentContext.setPaymentStrategy(PayPalPayment());
  paymentContext.makePayment(150.0);

  // User decides to switch to Bitcoin
  paymentContext.setPaymentStrategy(BitcoinPayment());
  paymentContext.makePayment(200.0);
}
```

### Output:
```
Paid $100.0 using Credit Card.
Paid $150.0 using PayPal.
Paid $200.0 using Bitcoin.
```

### Explanation:
- **Strategy Interface (`PaymentStrategy`)**: This is the common interface that all payment methods must implement.
- **Concrete Strategies (`CreditCardPayment`, `PayPalPayment`, `BitcoinPayment`)**: These classes implement the `PaymentStrategy` interface and provide their own implementation of the `pay` method.
- **Context (`PaymentContext`)**: This class uses the strategy interface to call the appropriate payment method. The client can change the strategy at runtime.

The **Strategy Pattern** is helpful when you need to switch between different algorithms or behaviors without modifying the context class. It adheres to the **Open/Closed Principle** because the context class is open for extension (new strategies) but closed for modification (no need to change existing code).
