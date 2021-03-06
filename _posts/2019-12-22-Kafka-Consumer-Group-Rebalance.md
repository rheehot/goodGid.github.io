---
layout: post
title:  " Kafka Consumer Groups Rebalance "
categories: Kafka
tags: Kafka
author: goodGid
---
* content
{:toc}

> 이 글의 코드 및 정보들은 [책](https://book.naver.com/bookdb/book_detail.nhn?bid=13540082)을 바탕으로 작성하였습니다.

## 리밸런스

* 하나의 컨슈머 그룹 내에서

* 토픽에 대한 소유권을

* 재조정하는 과정을

* 리밸런스라고 한다.

<br>

* 컨슈머 그룹 내에서

* 리밸런스가 일어나면

* 토픽의 각 파티션마다

* 하나의 컨슈머가 연결된다.

<br>

* 이러한 리밸런스를 통해

* 컨슈머 그룹에 컨슈머를 쉽고 안전하게 추가할 수 있고

* 제거할 수도 있어

* 높은 가용셩과 확장성을 확보할 수 있다.









### Example 

![](/assets/img/kafka/Kafka-Consumer-Group_1.png)

* 위와 같은 상황에서

* 컨슈머를 추가하면 

* 리밸런스가 일어나며

* 그 결과는 다음과 같다.

![](/assets/img/kafka/Kafka-Consumer-Group_2.png)

* 파티션 1의 소유권이 컨슈머01에서 컨슈머02로 이동했고

* 파티션 2의 소유권이 컨슈머01에서 컨슈머03으로 이동했다.

* 이렇게 소유권이 이동하는 것을

* **리밸런스(Rebalance)**라고 한다.

<br>

> 소유권이란?

* 기본적으로 컨슈머 그룹 안에서

* 컨슈머들은 메시지를 가져오고 있는 

* 토픽의 파티션에 대해 **소유권**을 공유한다.

<br>

* 즉 하나의 컨슈머마다

* 자신이 갖고 오는

* 토픽의 파티션에 대해

* 소유권을 갖는다고 생각하면 된다.




## 리밸런스의 단점

* 리밸런스를 하는 동안

* 일시적으로 컨슈머는 메시지를 가져올 수 없다.

* 그래서 리밸런스가 발생하면

* **컨슈머 그룹 전체**가 일시적으로 작업을 정지하게 된다.

<br>

* 그리고 리밸런스가 끝나면

* 컨슈머들은 각자 담당하고 있는

* 파티션으로부터 메시지를 가져온다.

---

## 참고

* [카프카, 데이터 플랫폼의 최강자 실시간 비동기 스트리밍 솔루션 카프카의 기본부터 확장 응용까지](https://book.naver.com/bookdb/book_detail.nhn?bid=13540082)