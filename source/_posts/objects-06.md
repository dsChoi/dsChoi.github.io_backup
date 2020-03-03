---
title: chapter 06. 메시지와 인터페이스
tags:
  - object
categories: 도서
date: 2020-02-18 22:26:34
---


# chapter 06. 메시지와 인터페이스

객체지향 프로그래밍에 대한 가장 흔한 오해 

*  애플리케이션은 클래스의 집합으로 구성된다. 

> ` 애플리케이션`은 클래스로 구성되지만` 메시지를 통해 정의`된다.

## 01. 협력과 메시지

### 클라이언트-서버 모델

* 협력안에서 메시지를 전송하는 객체를 **클라이언트**
* 메세지를 수신하는 객체를 **서버**



**클라이언트와 서버 역할을 동시에 수행하는 Movie**

<img src="./objects-06/image-20200223211641253.png" alt="image-20200223211641253" style="zoom:50%;" />







객체가 독립적으로 수향할 수 있는 것보다 더 큰 책임을 수행하기 위해서는 다른 객체와 협력해야 한다는 것.

두 객체 사이의 협력을 가능하게 해주는 매개채가 바로 메시지.

### 메시지와 메시지 전송

**메세지**

객체들이 협력하기 위해 사용할 수 있는 유일한 교통 수단.

* 오퍼레이션 명 + 인자로 구성

**메시지 전송 or 메시지 패싱**

한 객체가 다른 객체에게 도움을 요청하는 것

**메시지 전송자** - 클라이언트

메시지를 전송하는 객체

**메시지 수신자** - 서버

메시지를 수신하는 객체



condition : 수신자

isSatisfiedBy : 오퍼레이션 명

screening : 인자

Ex) condition.isSatisfiedBy(screening);



### 메시지와 메서드

**메서드**

메시지를 수신했을 때 실제로 실행되는 함수 또는 프로시저

ex) 동일한 이름의 변수에게 동일한 메시지를 전송하더라도 객체의 타입에 따라 실행되는 메서드가 달라질 수 있다.



메시지 전송자와 메시지 수신자는 서로에 대한 상세한 정보를 알지 못한 채 단지 메시지라는 얇고 가는 끈을 통해 연결된다. 실행 시점에 메시지와 메서드를 바인딩 하는 메커니즘은 두 객체 사이의 결합도를 낮춤으로써 유연하고 확장 가능한 코드를 작성할 수 있게 만든다.

### 퍼블릭 인터페이스와 오퍼레이션

**퍼블릭 인터페이스**

객체가 의사소통을 위해 외부에 공개하는 메시지의 집합

**오퍼레이션**

퍼블릭 인터페이스에 포함된 메시지

**메서드**

메시지를 수신했을 때 실제로 실행되는 코드

> 인터페이스의 각 요소는 오퍼레이션이다. 오퍼레이션은 구현이 아닌 추상화다. 반면 UML 의 메서드는 오퍼레이션을 구현한 것이다. 

<img src="./objects-06/image-20200223212722901.png" alt="image-20200223212722901" style="zoom:50%;" />

### 시그니처

**시그니처**

오퍼레이션(또는 메서드)의 이름과 파라미터 목록을 합친 것

**오퍼레이션**

실행 코드 없이 시그니처만 정의한 것

**메서드**

시그니처에 구현을 더한 것

---

> 오퍼레이션 관점에서 다형성이란 동일한 오퍼레이션 호출에 대해 서로 다른 메서드들이 실행 되는 것 

---

**용어 정리**

* 메시지 : 객체가 다른 객체와 협력하기 위해 사용하는 의사소통 메커니즘
* 오퍼레이션 : 객체가 다른 객체에게 제공하는 추상적인 서비스.
* 메서드 : 메시지에 응답하기 위해 실행되는 코드 블록. 오퍼레이션의 구현. 동일한 오퍼레이션이라고 해도 메서드는 다를 수 있다. 
* 퍼블릭 인터페이스: 객체가 협력에 참여하기 위해 외부에서 수신할 수 있는 메시지의 묶음.
* 시그니처: 오퍼레이션이나 메서드의 명세를 나타낸 것. 이름과 인자의 목록을 포함.

## 02. 인터페이스와 설계 품질

**좋은 인터페이스의 조건**

* 최소한의 인터페이스
* 추상적인 인터페이스

### 디미터 법칙

> 객체의 내부 구조에 강하게 결합되지 않도록 협력 경로를 제한하라.
>
> "낯선 자에게 말하지 말라" 또는 "오직 인접한 이웃하고만 말하라."

**디미터 법칙을 따르기 위한 조건** 

* this 객체
* 메서드의 매개변수
* this 의 속성
* this의 속성인 컬렉션의 요소
* 메서드 내에서 생성된 지역 객체

**디미터 법칙과 캡슐화**

```java
screening.getMovie().getDiscountConditions(); //디미터 법칙을 위반하는 전형적인 코드
// 기차 충돌(train wreck)

...

  screening.calculateFee(audienceCount); // 디미터 법칙을 따르도록 코드를 개선하여 메시지 수신자의 내부 구조에 관해 묻지 않게 된다.
```



### 묻지말고 시켜라

훌륭한 메시지는 객체의 상태에 관해 묻지 말고 원하는 것을 시켜야 한다는 것을 강조한다.



>  절차적인 코드는 정보를 얻은 후에 결정한다. 객체지향 코드는 객체에게 그것을 하도록 시킨다.



* 내부의 상태를 묻는 오퍼레이션을 인터페이스에 포함시키고 있다면 더 나은 방법은 없는지 고민해 보라. 
* 내부의 상태를 이용해 어떤 결정을 내리는 로직이 객체 외부에 존재한다면 해당 객체가 책임져야하는 행동이 외부로 누수된 것이다.
* 상태를 묻는 오퍼레이션을 행동을 요청하는 오퍼레이션으로 대체함으로써 인터페이스를 향상시켜라. 
* 



### 의도를 드러내는 인터페이스

**켄트벡의 메서드를 명명하는 두가지 방법** 

1. 메서드가 작업을 어떻게  수행하는지를 나타내도록 이름 짓는 것

```java
public class PeriodCondition {
  public boolean isSatisfideByPeriod(Screening screening) {... }
  
}

public class SequenceCondition {
  public boolean isSatisfiedBySequence(Screening screening) { ... }
  
}
```

위 스타일이 좋지 않은 이유 두가지 

	1. 메서드에 대해 제대로 커뮤니케이션 하지 못한다. 
	2. 메서드 수준에서 캡슐화를 위반한다

2. '어떻게' 가 아니라 '무엇'을 하는지를 드러내는 것

```java
public class PeriodCondition {
  public boolean isSatisfiedBy(Screening screening) {... }
  
}

public class SequenceCondition {
  public boolean isSatisfiedBy(Screening screening) { ... }
  
}
```

어떻게 하느냐가 아니라 무엇을 하느냐에 따라 메서드의 이름을 짓는 패턴을 `의도를 드러내는 선택자` 라고 한다. 

**메서드에 의도를 드러낼수 있는 이름을 붙이기 위한 방법 - 켄트벡**

> 매우 다른 두번째 구현을 상항하라. 그러고 해당 메서드에 동일한 이름을 붙인다고 상상해라. 그렇게 하면 아마도 그 순간에 여러분이 할 수 잇는 가장 추상적인 이름을 메서드에 붙일 것이다.



의도를 드러내는 선택자를 인터페이스 레벨로 확장한 의도를 드러내는 인터페이스를 제시함. - 에릭에반스



`객체에게 묻지 말고 시키되 구현 방법이 아닌 클라이언트의 의도를 드러내야 한다.`



### 함께 모으기

**디미터 법칙을 위반하는 티켓 판매 도메인**

```java
public class Theater {
	private TicketSeller ticketSeller;

	public Theater(TicketSeller ticketSeller) {
		this.ticketSeller = ticketSeller;
	}

	public void enter(Audience audience) {
		if (audience.getBag().hasInvitation()) {
			Ticket ticket = ticketSeller.getTicketOffice().getTicket();
			audience.getBag().setTicket(ticket);
		} else {
			Ticket ticket =ticketSeller.getTicketOffice().getTicket();
			audience.getBag().minusAmount(ticket.getFee());
			ticketSeller.getTicketOffice().plusAmount(ticket.getFee());
			audience.getBag().setTicket(ticket);
		}
	}
}
```



## 03. 원칙의 함정

### 디미터 법칙은 하나의 도트(.) 를 강제하는 규칙이 아닌다.

```java
IntStream.of(1,15,20,3,9).filter(x -> x > 10).distinct().count();
```

디미터의 법칙  "오직 하나의 도트만을 사용해라" 라는 관점에서 위의 코드는 위반되었다고 볼수 있다. 

하지만. of, filter, distinct 메서드는 intStream instance를 반환하기에 디미터 법칙을 위반하지 않는다.



디미터 법칙은 `결합도` 와 관련된 것이며 이 결합도가 문제가 되는 것은 객체의 내부 구조가 외부로 노출되는 경우로 한정한다. 

여러 개의 도트를 사용한 코드가 객체의 내부 구조를 노출하고 있는가? 라는 질문을 하기를 바란다.



### 결합도와 응집도의 충돌

묻지 말고 시켜라와 디미터 법칙을 준수하는 것이 항상 긍정적인 결과로만 나타나지 안흔ㄴ다. 

모든 상황에서 위임 메서드를 추가하면 같은 퍼블릭 인터페이스 안에 어울리지 않는 오퍼레이션이 공존하게 된다. 



**클래스는 하나의 변경 원인만을 가져야한다.** 서로 상관 없는 책임들이 함께 뭉쳐있는 클래스는 응집도가 낮으며 낮은 변경으로도 쉽게 무너질수 있다. 



---

디미터 법칙의 위반 여부는 묻는 대상이 객체인지, 자료 구조인지에 달려있다고 설명한다. 객체는 내부 구조를 숨겨야 하므로 디미터 법칙을 따르는 것이 좋지만 자료 구조라면 당연히 내부를 노출해야 하므로 디미터 법칙을 적용할 필요가 없다. 



원칙을 맹신하지 마라. 원칙이 적절한 상황과 부적절한 상황을 판단할 수 있는 안목을 길러라. 

설계는 트레이드오프의 산물이다. 소프트웨어 설계에 존재하는 몇 안되는 법칙중 하나는` "경우에 따라 다르다"` 라는 사실을 명심하라



## 04. 명령-쿼리 분리 원칙

**루틴(routine)**

어떤 절차를 묶어 호출 가능하도록 이름을 부여한 기능 모듈

* 프로시저 : 부수효과를 발생시킬 수 있지만 값을 반환할 수 없다.
* 함수 : 값을 반환할 수 있지만 부수효과를 발생시킬수 없다.

**명령(command) 와 쿼리(query)**

* 객체의 인터페이스 측면에서 프로시저와 함수를 부루는 또다른 이름
* 명령 : 객체의 상태를 수정하는 오퍼레이션
* 쿼리 : 객체와 관련된 정보를 반환하는 오퍼레이션

**명령-쿼리 분리 원칙**

* 오퍼레이션은 부수효과를 발생시키는 명령이거나 부수효과를 발생시키지 않는 쿼리여야 한다.
* 어떤 오퍼레이션도 명령인 동시에 쿼리여서는 안된다.

**명령과 쿼리를 분리하기 위한 규칙**

> * 객체의 상태를 변경하는 명령은 반환값을 가질 수 없다.
>
> * 객체의 정보를 반환하는 쿼리는 상태를 변경할 수 없다.



**명령-쿼리 인터페이스(Command-Query Interface) - 마틴 파울러**

* 명령-쿼리 분리 원칙에 따라 작성된 객체의 인터페이스



****



### 반복 일정의 명령과 쿼리 분리하기

```java

public class Event {
    private String subject;
    private LocalDateTime from;
    private Duration duration;

    public Event(String subject, LocalDateTime from, Duration duration) {
        this.subject = subject;
        this.from = from;
        this.duration = duration;
    }

    public boolean isSatisfied(RecurringSchedule schedule){
        if (from.getDayOfWeek() != schedule.getDayOfWeek() ||
                !from.toLocalTime().equals(schedule.getFrom()) ||
                !duration.equals(schedule.getDuration())
        ) {
            reschedule(schedule);
            return  false;
        }
        return true;
    }

    private void reschedule(RecurringSchedule schedule) {
        from = LocalDateTime.of
                (from.toLocalDate().plusDays(daysDistance(schedule)), schedule.getFrom());
        duration = schedule.getDuration();
    }

    private long daysDistance(RecurringSchedule schedule) {
        return schedule.getDayOfWeek().getValue() - from.getDayOfWeek().getValue();
    }
}
```





```java
public class Event {
  public boolean isSatisfied(RecurringSchedule schedule) {...}
  public void reschedule(RecurringSchedule schedule) {  ... }
}



..... 
  
  /** client 호출 **/
  if(!event.isSatisfied(schedule)){
    event.reschedule(schedule);
  }
```



* 명령과 쿼리를 분리함으로써 예측가능하고 이해하기 쉬우며 디버깅이 용이한 동시에 유지보수가 수월해졌다.



### 명령-쿼리 분리와 참조 투명성

### 책임에 초점을 맞춰라

* 디미터 법칙
  * 협력이라는 컨텍스트 안에서 객체보다 메시지를 먼저 결정하면 두 객체 사이의 구조적인 결합도를 나줄 수 있다.
* 묻지 말고시켜라
  * 메시지를 먼저 선택하면 묻지 말고 시켜라 스타일에 따라 협력을 구조화하게 된다. 클라이언트 관점에서 메시지를 선택하기 때문에 필요한 정보를 물을 필요 없이 원하는 것을 표현한 메시지를 전송하면 된다.
* 의도를 드러내는 인터페이스
  * 메시지를 먼저 선택한다는 것은 메시지를 전송하는 클라이언트의 관점에서 메시지의 이름을 정한다는 것. 
* 명령-쿼리 분리 원칙
  * 예측가능한 협력을 만들기 위해 명령과 쿼리를 분리



**훌륭한 메시지를 얻기 위한 출발점**은 책임 주도  설계 원칙을 따르는 것. 

책임 주도 설계에서는 객체가 메시지를 선택하는 것이 아닌 메시지가 객체를 선택하기 때문에 협력에 적합한 메시지를 결정할 수 있는 확률이 높아진다. 


