---
title: "org.springframework.orm.jpa.JpaSystemException: Null value was assigned to a property"
date: "2024-03-05"
---

직역을 하자면 속성에 null 값이 할당되었다고 한다.

```
org.springframework.orm.jpa.JpaSystemException: Null value was assigned to a property [class com.rktpdyfk.TradingMatchingService.entity.Item.attack] of primitive type: 'com.rktpdyfk.TradingMatchingService.entity.Item.attack' (setter)
```

## 원인
Item Table의 attack은 MYSQL의 INT형으로 이루어져있고 이는 Null 값을 가질 수 있다. 
하지만 현재 코드상에서 Null값을 받아들이는 부분에서 에러가 발생하였다.

엔티티를 살펴보니 Item#attack이 `Int` 형으로 선언되어 있었다.
자바에서 int는 기본적으로 null 값을 가질 수 없는(primitive) 데이터 타입으로 이루어져있으며

### 해결
null값을 받기 위해선 Wrapper클래스인 Integer 혹은 Long을 사용할 수 있겠다.