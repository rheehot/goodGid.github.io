---
layout: post
title:  " 파일 저장 장치 "
date:   2018-04-14
excerpt: " 파일 저장 장치 "
cate : "posts"
tag:
- File Processing
---

# 파일 저장 장치의 특성


---


# 저장 장치의 계층

---

# 디스크 데이터 접근

* 데이타 접근 시간의 구분
    1. 탐구 시간 (Seek Time)
    2. 회전 지연 시간 (Rotational Latency Time)
    3. 전송 시간 (Transfer Time)


---


## 1. 탐구 시간 (Seek Time) : s

* 원하는 데이터가 있는 실린더(or 트랙)에 <br> R/W헤드를 위치시키는데 걸리는 시간

* 평균 탐구 시간 (Average Seek Time : s )
    * 한 파일이 몇 개 `인접 실린더`에 기록되면 `헤드 평균 이동`은 감소

---


## 2. 회전 지연 시간 (Rotational Latency) : r

* `탐구완료`에서 `자료전송` 시작까지의 지연 <br> r = 1/2 * (1회전시간)

Q. 회전속도가 3600 rpm인 디스크에서 r은 몇 ms인가?
{: .notice}


```    
1회전시간을 X라 하면
60 sec : 3600 r = X : 1
X = 60 / 3600 = 0.01667 sec = 16.67ms
r = 1/2 * 16.67 = 8.33ms
```    


---

## 3. 전송 시간 (Transfer Time)

* 전송 시간 : 블록의 섹터들과 이들 사이의 갭들이 헤드 밑을 회전하며 통과하는데 걸리는 시간

* 전송률 : 초당 데이터가 전송되는 속도 (bps : bits per second)


---


## 4. 블록의 판독

* 여러 개의 블록을 효율적으로 전송하려면 ? <br> --> 여러 개의 연속적인 블록을 `같은 실린더`에 저장

---


## 5. 블록의 기록과 갱신

* 블록의 기록 

헤드가 판독하는 대신 기록하는 것을 제외하고 블록의 판독 과정과 동일

* 블록의 갱신
    * 디스크에서 직접 갱신은 불가능
        1. 메인 메모리로 블록 이동
        2. 메인 메모리 내의 블록 사본을 갱신
        3. 갱신된 블록 사본을 디스크에 기록

<br> 

* 블록 갱신 지연 시간 : 블록 판독 시간 + 사본 갱신 시간 + 기록 시간 <br> 메인 메모리 내에서의 블록 갱신 시간은 보통 무시 <br> Cause : 메인 메모리는 Fast

---


## 6. 블로킹

* `블록`
    * 데이터 전송의 단위 : `물리적` 레코드 

* 블록의 크기
    * 너무 크면 단점은? 
        1. 불필요한 데이터 전송 --> 불필요한 Data도 같이 전송
        2. 메인 메모리 내에 `과도한 버퍼공간` 요구 ==> 메모리 효율성 저하



---

## 6-(1) 블로킹 인수 (Blocking Factor) : Bf

### `블로킹`

기억공간과 I/O 효율을 위해 `몇 개`의 `논리적 레코드`를

`하나`의 `물리적 레코드(블록)`에 저장시키는 것

* 블로킹 인수 = B / R       ## R : 레코드 크기 , B : 블록 크기

* 장점

1. 갭으로 인한 기억 공간의 낭비 감소

2. I/O 시간의 감소

* 단점

1. 버퍼 크기 만큼 주기억장치 내의 사용 공간

2. 블록의 일부 처리를 위해 블록 전체를 전송


---

## 블로킹 방법

1.고정 길이 블로킹 : 가장 큰 레코드를 기준 <br> 관리하기 쉽다.

- fixed length records

- fixed length block

<br>

2.신장된 가변 길이 블로킹 // 신장 : 한 레코드가 인접한 몇 개 블록에 걸쳐 저장

- varable length records

- fixed length block with spanning

- 구현, 판독, 갱신이 어려움 

<br>

3.비 신장된 가변 길이 블로킹 

- varable length records

- fixed length block with no spanning

- 저장공간 낭비가 심함


{% capture images %}
    /assets/img/posts/fp_sd_1.png
{% endcapture %}
{% include gallery images=images caption="Screenshots of Problem Explain" cols=1 %}


---