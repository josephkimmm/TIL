# 🌱 가비지 컬렉션 (Garbage Collection, GC)

최근 스프링을 공부하면서 자바의 기본 개념을 다시 돌아보고 있고, 그 과정에서 JVM의 메모리 관리 방식인 **가비지 컬렉션(GC)** 에 대해 자연스럽게 관심이 생겼다.

자바는 개발자가 직접 메모리를 해제하지 않아도, **JVM이 더 이상 사용하지 않는 객체를 감지하여 자동으로 제거**해주는 GC 기능을 제공한다.

---

## 📌 GC는 언제 발생할까?

GC는 **객체가 더 이상 참조되지 않을 때** 발생한다.  
자바는 객체의 **도달 가능성(Reachability)** 을 기준으로 가비지 여부를 판단한다.

> 도달할 수 없다 = GC 대상

도달 가능한 객체는 다음 기준 중 하나 이상에 해당한다:

- 스택(Local 변수 등)에 있는 객체  
- static 변수로 참조되고 있는 객체  
- 다른 객체가 참조 중인 객체  

이러한 기준점들을 **GC Root** 라고 하며, GC는 GC Root에서 출발하여 참조 그래프를 따라 도달 가능한 객체만 남긴다.

---

## 🧼 GC의 종류

### 🔹 Minor GC

- **Young 영역**(Eden + Survivor 영역)에서 발생
- 객체가 생성되면 우선 **Eden 영역**에 저장된다
- Minor GC 발생 시, 살아남은 객체는 **Survivor 영역**으로 이동
- 여러 번 살아남은 객체는 **Old 영역으로 승격(Promotion)**

### 🔹 Major GC (또는 Full GC)

- **Old 영역**에서 발생
- 오래된 객체들 중 더 이상 사용되지 않는 것들을 제거
- 이 과정에서는 **stop-the-world** 가 발생해 애플리케이션 실행이 잠깐 멈출 수 있음

---

## ⚙️ 다양한 GC 알고리즘

JVM은 애플리케이션 특성에 맞게 다양한 GC 알고리즘을 제공한다:

| GC 이름        | 특징                                       | 적합한 환경                    |
|----------------|--------------------------------------------|---------------------------------|
| Serial GC      | 단일 스레드로 동작. 구조가 단순             | 메모리 자원이 적은 단일 앱 환경 |
| Parallel GC    | 멀티 스레드로 GC 처리. Throughput 중시     | 서버 환경 등 처리량 우선인 경우 |
| CMS GC         | 대부분 GC 작업을 애플리케이션과 동시에 수행 | 지연시간이 중요한 웹 서비스     |
| G1 GC          | 힙을 Region으로 나눠서 효율적 관리          | 대규모 힙, Java 9 이후 기본 GC  |
| ZGC / Shenandoah | 매우 짧은 중단 시간 (low latency 지향)     | 최신 시스템, 지연 민감한 서비스 |

> 📌 최근에는 CMS보다 G1, ZGC가 더 자주 사용됨

---

## ✅ 내가 이해한 핵심 요약

- GC는 자바의 **스마트한 청소부**이다
- 객체의 **Reachability(도달 가능성)** 으로 생존 여부를 결정
- **Minor GC**는 Young 영역, **Major GC**는 Old 영역에서 발생
- **stop-the-world**는 GC 시 JVM이 잠시 멈추는 현상이며 성능에 영향 줄 수 있음
- GC 알고리즘은 서비스의 성격에 따라 적절히 선택해야 한다

---

## 📷 시각 자료 (Eden, Survivor, Old 영역)

![Java Memory Model](https://i.stack.imgur.com/Wz6vY.png)  
<sub>출처: [Stack Overflow - Java GC Heap Structure](https://stackoverflow.com/questions/3245117/how-does-java-garbage-collection-work)</sub>

---

## 🔗 참고 자료
- [Java Garbage Collection](https://asfirstalways.tistory.com/159)
- [네이버 D2 블로그 - GC 이야기](https://d2.naver.com/helloworld/1329)
- [Inpa Dev](https://inpa.tistory.com/entry/JAVA-%E2%98%95-%EA%B0%80%EB%B9%84%EC%A7%80-%EC%BB%AC%EB%A0%89%EC%85%98GC-%EB%8F%99%EC%9E%91-%EC%9B%90%EB%A6%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%F0%9F%92%AF-%EC%B4%9D%EC%A0%95%EB%A6%AC)

