# 📘 JVM (Java Virtual Machine)

## 🧠 JVM이란?
- **Java Virtual Machine**의 약자로, 자바 프로그램을 실행시키는 **가상 머신**
- OS 위에서 동작하며 **플랫폼 독립성**을 제공
- **메모리 관리** 및 **Garbage Collection(GC)** 수행
- 자바 프로그램을 **스택 기반**으로 실행 (하드웨어는 보통 레지스터 기반)

---

## ❓ 왜 JVM을 알아야 하나?
- **한정된 메모리를 효율적으로 사용**해 성능을 최적화하기 위해
- **메모리 구조 이해**는 자바 프로그램의 속도 저하, 튕김 등을 예방하는 데 필수

---

## ⚙️ 자바 프로그램 실행 과정
1. JVM이 OS에서 메모리를 할당받음
2. `javac`가 `.java` → `.class`로 컴파일
3. **Class Loader**가 클래스 파일 로딩
4. **Execution Engine**이 바이트코드 실행
5. **Runtime Data Area**에 바이트코드 배치 및 실행
6. GC, Thread 동기화 등 관리 작업 수행

---

## 🧩 JVM 구성 요소

### 1. Class Loader
- `.class` 파일을 JVM으로 로딩하는 모듈
- 런타임 중 필요한 클래스만 동적으로 로딩

### 2. Execution Engine
- 바이트코드를 **네이티브 코드로 변환**해 실행
  - **Interpreter**: 한 줄씩 실행 (느림)
  - **JIT 컴파일러**: 반복되는 코드를 네이티브 코드로 변환 후 캐싱

### 3. Garbage Collector
- 사용되지 않는 객체를 자동으로 메모리에서 제거

### 4. Runtime Data Area (메모리 영역)

#### - PC Register
- 각 쓰레드마다 존재, 현재 실행 중인 명령의 주소 저장

#### - JVM Stack
- 메소드 호출 시 스택 프레임 생성
- 지역변수, 파라미터, 연산 결과 등 저장

#### - Native Method Stack
- JVM 외부 언어(C 등)의 네이티브 코드 실행 영역

#### - Method Area (Class Area)
- 클래스 구조, 메서드 정보, 상수 풀 등 저장
- GC의 대상

#### - Heap
- `new` 연산자로 생성된 **객체와 배열** 저장
- GC가 관리
  - **Young 영역 (Eden, Survivor 0/1)**: 새 객체 저장
  - **Old 영역**: 오래 살아남은 객체 저장
  - **Permanent Generation**: 클래스 메타정보 저장 (현재는 Metaspace로 대체됨)

---

## 📝 참고 요약

| 구성 요소           | 설명                                           |
|--------------------|------------------------------------------------|
| Class Loader       | 클래스 로딩 및 링크                            |
| Execution Engine   | 바이트코드 실행 (인터프리터 + JIT)            |
| GC                 | 불필요한 객체 메모리 자동 회수                 |
| Stack              | 메소드 단위 스택 프레임 구성                   |
| Heap               | 객체 저장 및 GC 대상                           |
| Method Area        | 클래스 구조와 메소드 바이트코드 저장           |
| Native Method Stack| JNI를 통한 네이티브 코드 실행 영역            |
| PC Register        | 현재 실행 명령 위치 저장                       |

---
