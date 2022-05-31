# 인터페이스를 활용한 디자인 패턴(Strategy pattern)
![image](https://user-images.githubusercontent.com/59958929/171090792-78b33ddf-71d6-40c8-b8c4-4e5e487b3eac.png)
* 객체가 할 수 있는 행위들을 전략(strategy)으로 만들어두고, 
동적으로 행위의 수정이 필요한 경우 전략을 바꾸는 것만으로 수정이 가능하도록 만든 패턴이다.

## 활용사례
```ts
class VendingMachine {
    pay() {
        console.log("cash pay!");
    }
}
 
// 전략 패턴 도입
interface PaymentStrategy {
    pay(): void;
}
 
class CardPaymentStrategy implements PaymentStrategy {
    pay(): void {
        console.log("card pay!");
    }
}
 
class CashPaymentStrategy implements PaymentStrategy {
    pay(): void {
        console.log("Cash pay!");
    }
}
 
class VendingMachine {
    private paymentStrategy: PaymentStrategy;
 
    setPaymentStrategy(paymentStrategy: PaymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }
 
    pay() {
        this.paymentStrategy.pay();
    }
}
 
const vendingMachine =new VendingMachine();
 
vendingMachine.setPaymentStrategy(new CashPaymentStrategy());
vendingMachine.pay(); // cash pay
 
vendingMachine.setPaymentStrategy(new CardPaymentStrategy());
vendingMachine.pay(); // card pay
```
* 자판기 결제 방법을 현금 결제에서 카드 결제로 변경할 때, Pay 메서드 구현 변경이 필요하다.
* 메서드 수정 방식의 문제점
  * OCP(Open Closed Principle)를 위배한다.(OCP 설계 원칙)
  * OPC : 소프트웨어 개체(클래스, 모듈, 함수 등등)는 확장에 대해 열려 있어야 하고, 수정에 대해서는 닫혀 있어야 한다.
* 시스템이 커져서 확장될 경우 연동되는 시스템에도 영향을 줄 수 있다.
* 디자인 패턴으로 문제를 해결할 수 있다.
