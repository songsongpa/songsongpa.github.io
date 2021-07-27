---
layout: post
title: 1.1 자바 개발 간소화

categories:
- spring-in-action-4th-edition

tags:
- [spring-in-action, ejb, pojo, javabeans, bean]

toc:
- true

toc:sticky:
- true

toc_label:
- "TEST"

date: 2021-07-25
last_modified_at: 2021-07-25
---

# EJB 와 JavaBeans

### EJB(Enterprise Java Beans)
- 애플리케이션의 비즈니스 로직을 캡슐화하는 서버 측 소프트웨어 구성 요소.
- EJB는 Java API로 엔터프라이즈 수준의 애플리케이션을 개발 및 배포를 위한 아키텍처를 제공하며 개발자는 이를 사용하여 확장 가능하고 강력한 응용 프로그램을 만들 수 있다.
- EJB 응용 프로그램을 실행하려면 응용 프로그램 서버 (EJB 컨테이너)가 필요하다.
JBoss, Glassfish, Weblogic 및 Websphere 등등이 응용 프로그램 서버의 예이며 이러한 서버(WAS)는 트랜잭션을 관리하고 보안을 관리한다.

![EJB](/assets/img/EJB.png)

### EJB의 구성요소
- **Session Bean** - 단일 세션의 특정 사용자의 데이터로 사용자 세션이 종료되면 소멸된다.
- **Message Driven Bean** - 비즈니스 로직이 포함되어 있으며, 메시지 전달에 의해 호출된다.
  외부 엔티티에서  JMS(Java Messaging Service) 메시지를 사용하여 작업을 수행 할 수 있다. (원격 호출 가능)
- **Entity Bean** - 영구 데이터 스토리지를 나타내며, 사용자 데이터를 데이터베이스에 저장하는 데 사용된다.

### EJB의 장단점
- 어플리케이션 서버가 트랜잭션 , 예외 핸들링, 데이터 영속성을 관리 하여 개발자가 비즈니스 로직 구현에 집중 할 수 있게 한다.
- 하지만, EJB 어플리케이션을 이해하고 개발하기 복잡(상속, 구현과 같은 특정 규약)하며 어플리케이션 서버에 의존적(종속적)이다.

---

### JavaBeans
- 자바빈즈(JavaBeans)는 자바로 작성된 소프트웨어 컴포넌트이다.
- 자바에서 재사용 가능한 객체를 만드는 데 도움이 되는 단일 객체로 여러 객체를 캡슐화 하는 클래스.
- Java 클래스로 java.beans 패키지에서 사용 가능하다.
- 주 용도는 JSP 웹 페이지 개발에서 Model을 개발

![JavaBeans](/assets/img/JavaBeans.png)

### JavaBeans Conventions
자바빈즈 클래스로서 작동하기 위해서, 객체 클래스는 명명법, 생성법 그리고 행동에 관련된 일련의 관례를 따라야만 한다. 이러한 관례는 (빌더 형식의) 개발 도구에서 자바빈즈와의 연결을 통해 클래스의 사용과 재사용 그리고 클래스의 재배치를 가능하게 한다.

지켜야 할 관례에는 다음과 같은 것이 있다

- 클래스는 직렬화되어야 한다.(클래스의 상태를 지속적으로 저장 혹은 복원 시키기 위해)
- 클래스는 기본 생성자만을 가지고 있어야 한다.
- 클래스의 속성값을 설정하고 가져오는 `getter`, `setter` 메서드들을 사용해 접근할 수 있어야 한다.
- 클래스는 필요한 이벤트 처리 메서드들을 포함하고 있어야 한다.

### JavaBeans Features
- **Introspection** – 빈의을 기능을 결정하기 위해 분석하는 단계로, 다른 어플리케이션이 컴포넌트(객체)에 대한 정보를 얻을 수 있도록 한다.
- **Properties** – `property`는 빈의 상태의 하위요소로, `property`에 할당된 값은 컴포넌트의 동작(기능, 메소드)을 식별하는데 도움이 된다. 또한 `setter`메소드와 `getter`메소드를 통해 값을 설정하고 얻어올 수 있다.
- **Customization** – 특정 컨텍스트의 컴포넌트를 사용하는 프로세스에 대해 가이드를 제공한다.
- **Persistence** – 빈의 `property`값, 인스턴스 변수 등과같은 빈의 현재 상태를 저장하는데 도움이 된다.

### JavaBeans의 장점
- 다른 어플리케이션이 또 다른 어플리케이션의 `Bean property`와 메소드를 사용 할 수 있다.
- 다른 객체로부터 이벤트를 전달 받도록 등록할 수 있고 다른 객체에 전송되는 이벤트를 생성 할 수도 있다.

### JavaBeans의 단점
- `property`가 많을수록 `getter`, `sette`를 만들기 어렵고 인수를 받지않는 기본 생성자는 잘못된 상태(적절하지 못한 초기화)를 유발할 수 있다.
- 상투적인 코드(Boilerplate Code)가 증가 한다.(`getter`, `setter`)

### JavaBeans의 예
```java
// Serializable 구현
public class PersonBean implements java.io.Serializable {
    private String name;
    private boolean coding;

    // 기본 생성자 (인자가 없는).
    public PersonBean() {

    }

    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }

    // Different semantics for a boolean field (is vs. get)

    public boolean isCoding() {
        return this.coding;
    }

    public void setCoding(boolean coding) {
        this.coding = coding;
    }
}
```

---

### EJB와 JavaBenas의 차이
- EJB는 엔터프라이즈 소프트웨어의 모듈식 구성을 허용하는 Java API이고 JavaBeans는 다수의 객체를 단일 객체로 캡슐화하는 Java 클래스다.
- EJB는 EJB 어플리케이션을 실행하기 위한 서버 또는 EJB컨테이너가 필요하며, JavaBeans는 직렬화를 구현, 기본 생성자만 존재, `getter`, `setter` 메소드를 작성하여 `property`에 대한 접근을 허용해야 한다.


출처
<https://pediaa.com/what-is-the-difference-between-ejb-and-javabeans/>
