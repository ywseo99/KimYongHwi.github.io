---
title: "내가 이해한대로 정리한 GraphQL 1편"
date: 2019-07-25 18:26:28 -0400
categories: graphql
tags: [graphql]
---

# 1. GraphQL이란
오늘날 대부분의 client는 API를 통해 필요한 데이터를 전달 받는데 이때 API는 client에서 필요로 하는 데이터에 대한 interface를 제공해야할 책임이 있다.

기존의 REST API는 데이터의 대한 interface가 추가될 때마다 새로운 endponit를 필요로 했고 API의 버전이 올라갈 수록 또는 API의 규모가 커질 수록 이런 endpoint는 무수히 늘어나 관리가 어려워진다.

이러한 문제점을 해결하기 위해 Facebook에서는 GraphQL이라는 새로운 API 표준을 제시했다. 

GraphQL은 API를 위한 Query Language이면서 query를 실행시기키 위한 runtime이다. GraphQL은 client가 필요한 데이터를 API에서 정확하게 지정할 수 있다. 고정된 데이터 구조를 반환하는 여러 endpoint 대신 GraphQL 서버는 single endpoint 만 노출하고 client가 요청한 데이터로 정확하게 응답한다.

# 2. 특징
## 2.1 Defines a data shape

### client
```
{
  query person {
    name
    age,
    hobbies {
      name
    }
  }
}
```
#### GraphQL query는 Response를 미러링 한다.

### API
```
type Query {
  person: Person
}

type Hobby {
  name: String
  category: String
}

type Person {
  id: ID
  name: String
  age: Int
  hobbies: [Hobby]
}
```

#### 따라서 client에서는 Response에 대한 예측이 가능하다. 그리고 해당 예시를 보면 client에서 query를 작성할 때 Person type에 대해서 원하는 필드를 정의할 수 있어 over fetching이나 under fetching문제를 해결할 수 있다.
