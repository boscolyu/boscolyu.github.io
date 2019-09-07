---
layout: post
Title: "MyBatis, JPA, Hibernate"
Author: bosco lyu
Date: 
Meta: "IT"
---

# JPA나 MyBatis를 사용하는 이유
* 이제는 JDBC API로 개발하는 개발자는 없다.
* JDBC가 아닌 Hibernate나 MyBatis를 사용한다.

## JPA 모토
### 개발자는 SQL 매퍼가 아니다.

```
객체를 데이터베이스에 CRUD하려면 너무 많은 SQL과 JDBC API를 코드로 작성해야 한다는 점이다. 

                                    - java ORM 표준 JPA 프로그래밍 -
```

#### JDBC Programming
* 쿼리를 작성함.
* 쿼리를 실행함.
* 쿼리 결과를 객체에 담아서 반환함.
* CRUD에 대해서 모두 작업을 해주어야 함.

```java
// 불편한 JDBC Programming
public class MemberDAO {
    public Member findByID(Strng memberId) throws SQLException {
        try {
            String sql = "SELECT member_id, name FROM MEMBER M WHERE member_id = ?"

            ...

            ResultSet rs - stmt.executeQuery(sql);

            String memberId = rs.getString("member_id");
            String name = rs.getString("name");

            Member member = new Member();
            member.setMemberID(memberId);
            member.setName(name);
            return member;
        }
        finally {
            rs.close();
            stmt.close();
        }
    }
}

```

#### JPA Programming

* 기존 데이터 클래스에 DB와 매핑할 annotation을 추가함.
* EntityManager를 이용해서 조회함.

```java
// annotation을 이용한 JPA programming 
import javax.persistence.*;

@Entity
@Table(name-"MEMBER")
public class Member { 
    @Id
    @Column(name = "ID")
    private String id;

    @Column(name ="name")
    private String name;

}

public class MemberDAO {
    public Member findById (EntityManager em, String id) {
        Member findMember = em.find(Member.class, id);
        return findMember;
    }
}

```

### 개발자는 DB relation기반의 개발이 아닌 객체 지향의 개발을 하고 싶다. (패러다임 불일치)

```
객체는 참조를 사용해서 다른 객체와 연관관계를 가지고 참조에 접근해서 연관된 객체를 조회한다. 
반면에 테이블은 외래 키를 사용해서 다른 테이블과 연관관계를 가지고 조인을 사용해서 연관된 테이블을 조회한다.

                                    - java ORM 표준 JPA 프로그래밍 -
```
#### JDBC Programming

```java
memberDAO.getMember();
memberDAO.getMemberWithTeam();
memberDAO.getMemberWithOrderWithDelivery();
```

#### JPA Programming
* 지연로딩을 통해서 객체 참조를 자유롭게 할 수 있다.

```java
Member member = jpa.find(Member.class. memberId);

Team team = member.getTeam();
Order order = member.getOrder();
order.getOrderDate();
```

### definition 

* 오라클에 정의된 Java Persistence API definition
```
The Java Persistence API provides a POJO persistence model for object-relational mapping. 
The Java Persistence API was developed by the EJB 3.0 software expert group as part of JSR 220, 
but its use is not limited to EJB software components. 
It can also be used directly by web applications and application clients,
and even outside the Java EE platform, for example, in Java SE applications. 
```

### history
JPA는 기존 EJB에서 제공하던 엔터티 빈을 대체하는 기술이다. JSR 220에 정의된 EJB 3.0 스펙의 일부로 정의되어 있지만 컨테이너에 의존하지 않는 방식이어서 웹 모듈, Java SE 클라이언트에서도 사용이 가능하다.
JDBC처럼 Java에서는 표준 API만 정의한 것이며, 사용자는 원하는 JPA의 구현체인 Persistence Provider를 선택해서 사용할 수 있다.

### 장점
* JDBC API를 사용하는 개발자
    * 비지니스 로직을 작성하는 것보다 JDBC API 개발에 더 시간을 많이 들인다.
### 구성 요소
* javax.persistance 패키지에 정의된 API
* JPQL
* 객체/관계 메타데이터 

## Hibernate
### 위키피디아의 정의
```
Hibernate ORM(Hibernate ORM)은 자바 언어를 위한 객체 관계 매핑 프레임워크이다. 
객체 지향 도메인 모델을 관계형 데이터베이스로 매핑하기 위한 프레임워크를 제공한다.
```
### Hibernate 사이트 정의
* Object/Relational Mapping
```
Hibernate ORM enables developers to more easily write applications whose data outlives the application process. As an Object/Relational Mapping (ORM) framework, Hibernate is concerned with data persistence as it applies to relational databases (via JDBC). Unfamiliar with the notion of ORM?
```

* JPA Provider
    * 자체 API와 함께 JPA의 Provider로 구현체를 가지고 있음.
```
In addition to its own "native" API, Hibernate is also an implementation of the Java Persistence API (JPA) specification. 
As such, it can be easily used in any environment supporting JPA including Java SE applications, 
Java EE application servers, Enterprise OSGi containers, etc.
```
* GNU LGPL 2.1로 배포되는 자유 소프트웨어.
### term
* HQL
* JPQL

### java, jpa, hibernate mapping
* Java SDK와 JPA, Hibernate같의 버전 매핑 정보는 다음과 같다. 

| Hibernate ORM | 5.2 | 5.1 | 5.0 |
| --- | --- | --- | --- |
| Java | 8+ | 6+ | 6+ |
| JPA  | 2.1 | 2.1 | 2.1 |

### Supported JPA Versions
* JPA 1.0: ORM 3.2+
* JPA 2.0: ORM 3.5+
* JPA 2.1: ORM 4.3+

## iBatis

## MyBatis
* definition in site
```
MyBatis is a first class persistence framework with support for custom SQL, 
stored procedures and advanced mappings. 
MyBatis eliminates almost all of the JDBC code and manual setting of parameters and retrieval of results. 
MyBatis can use simple XML or Annotations for configuration and map primitives, 
Map interfaces and Java POJOs (Plain Old Java Objects) to database records.
```
* JDBC로 개발해야하는 상당히 반복적인 코드들을 XML에 기술된 쿼리문과 매핑해서 생산성을 향상시켜주는 framework이다.

## MyBatis vs JPA vs Hibernate
* google trend에서 찾아보면 한국에서만 MyBatis를 선호하고 있음을 알 수 있음.

<img src="/images/fulls/2017-10-13-01.png" width="100%">


## reference
### MyBatis
* http://www.mybatis.org/mybatis-3/ko/index.html
* http://www.mybatis.org/mybatis-3/configuration.html
* http://uwostudy.tistory.com/19

### JPA
* https://www.jcp.org/en/jsr/detail?id=220
* https://jcp.org/en/jsr/detail?id=338
* https://ko.wikipedia.org/wiki/%EC%9E%90%EB%B0%94_%ED%8D%BC%EC%8B%9C%EC%8A%A4%ED%84%B4%EC%8A%A4_API
* http://www.oracle.com/technetwork/java/javaee/tech/persistence-jsp-140049.html

### Hibernate
* http://hibernate.org/
* https://ko.wikipedia.org/wiki/%ED%95%98%EC%9D%B4%EB%B2%84%EB%84%A4%EC%9D%B4%ED%8A%B8
* http://hibernate.org/orm/releases/
* http://hibernate.org/orm/releases/5.2/
* https://docs.jboss.org/hibernate/stable/orm/userguide/html_single/Hibernate_User_Guide.html

### etc
* http://cocomo.tistory.com/194
* https://zeroturnaround.com/rebellabs/the-curious-coders-java-web-frameworks-comparison-spring-mvc-grails-vaadin-gwt-wicket-play-struts-and-jsf/
* https://zeroturnaround.com/rebellabs/developer-productivity-report-2012-java-tools-tech-devs-and-data/
* http://javacan.tistory.com/entry/94

