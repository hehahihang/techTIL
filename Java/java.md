# JAVA

## JVM 동작 순서
1. Heap 영역에 존재하는 객체들에 대해 접근이 가능한지 확인
2. GC Root에서부터 시작하여, 참조값을 따라가며 접근 가능한 객체들에 Mark한다.
  * GC Root가 될 수 있는 대상
  - JVM 메모리의 Stack 영역 존재하는 참조변수
  - Method Area의 Static 데이터
3. Mark 되지 않은 객체 즉, 접근할 수 없는 객체는 제거한다.

## GC(Garbage Collector)
### GC구조
#### Young Generation(Minor GC)
- Eden 영역 1개, Survivor 영역
  * Eden 영역
    - 새롭게 생성된 객체가 위치
    - 해당 영역이 꽉차면, GC가 발생하면서 Mark, Sweap 과정이 발생 -> Minor GC
    - 아직 사용중인 객체는 Survivor 영역으로 이동하며, Eden 영역에서는 사라짐
  * Survivor 영역
    - 또 다시 Eden 영역이 꽉차면, GC가 발생하면서 Eden, Survivor 영역에 접근할 수 없는 객체를 제거
    - 나머지 살아남은 객체는 다른 Survivor 영역으로 이동한다.
    - 다른 Survivor 영역으로 이동한 객체는 age가 증가한다.
    - 특정 age를 넘어가는 경우 Old Generation으로 이동한다(promotion)
- Minor GC라고 함

#### Old Generation
- Young 영역보다 크기가 크다.
- GC가 적게 발생하고, 시간은 오래걸린다.

### GC종류
1. Parallel GC
2. G1 GC
