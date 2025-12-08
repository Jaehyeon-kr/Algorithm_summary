# Java 자료구조 & 유틸리티 치트시트

## 목차
1. [Stack](#1-stack)
2. [Queue & Deque](#2-queue--deque)
3. [List (ArrayList, LinkedList)](#3-list-arraylist-linkedlist)
4. [Set](#4-set)
5. [Map](#5-map)
6. [Heap (PriorityQueue)](#6-heap-priorityqueue)
7. [정렬 (Sorting)](#7-정렬-sorting)
8. [탐색 알고리즘 (BFS, DFS)](#8-탐색-알고리즘-bfs-dfs)
9. [유용한 유틸리티](#9-유용한-유틸리티)

---

## 1. Stack

### 사용: `java.util.Stack` 또는 `java.util.Deque`

**권장: Deque 인터페이스 사용** (Stack 클래스는 레거시)

```java
// 생성
Deque<Integer> stack = new ArrayDeque<>();

// 주요 메서드
stack.push(10);           // 스택에 추가
stack.pop();              // 맨 위 요소 제거 & 반환
stack.peek();             // 맨 위 요소 확인 (제거 X)
stack.isEmpty();          // 비어있는지 확인
stack.size();             // 크기 반환
stack.clear();            // 모든 요소 제거
```

**예제: 괄호 검사**
```java
public boolean isValid(String s) {
    Deque<Character> stack = new ArrayDeque<>();
    for (char c : s.toCharArray()) {
        if (c == '(') stack.push(c);
        else if (stack.isEmpty() || stack.pop() != '(') return false;
    }
    return stack.isEmpty();
}
```

---

## 2. Queue & Deque

### Queue: `java.util.Queue`

```java
// 생성
Queue<Integer> queue = new LinkedList<>();

// 주요 메서드
queue.offer(10);          // 큐에 추가 (add와 유사하지만 예외 대신 false 반환)
queue.poll();             // 맨 앞 요소 제거 & 반환 (없으면 null)
queue.peek();             // 맨 앞 요소 확인 (제거 X)
queue.isEmpty();          // 비어있는지 확인
queue.size();             // 크기 반환
```

### Deque (Double-Ended Queue): 양방향 큐

```java
// 생성
Deque<Integer> deque = new ArrayDeque<>();

// 앞쪽(First) 작업
deque.addFirst(10);       // 맨 앞에 추가
deque.removeFirst();      // 맨 앞 제거 & 반환
deque.peekFirst();        // 맨 앞 확인

// 뒤쪽(Last) 작업
deque.addLast(20);        // 맨 뒤에 추가
deque.removeLast();       // 맨 뒤 제거 & 반환
deque.peekLast();         // 맨 뒤 확인

// Stack처럼 사용
deque.push(30);           // = addFirst(30)
deque.pop();              // = removeFirst()
```

---

## 3. List (ArrayList, LinkedList)

### ArrayList: 동적 배열

```java
// 생성
List<Integer> list = new ArrayList<>();

// 주요 메서드
list.add(10);             // 끝에 추가
list.add(0, 5);           // 인덱스 0에 삽입
list.get(0);              // 인덱스로 접근 O(1)
list.set(0, 15);          // 값 변경
list.remove(0);           // 인덱스로 제거
list.remove(Integer.valueOf(10)); // 값으로 제거
list.size();              // 크기
list.isEmpty();           // 비어있는지
list.contains(10);        // 포함 여부
list.indexOf(10);         // 첫 번째 인덱스 찾기
list.clear();             // 모든 요소 제거

// 정렬
Collections.sort(list);                      // 오름차순
Collections.sort(list, Collections.reverseOrder()); // 내림차순
```

### LinkedList: 연결 리스트

```java
// 생성
LinkedList<Integer> list = new LinkedList<>();

// ArrayList와 동일한 메서드 + 추가 메서드
list.addFirst(10);        // 맨 앞에 추가
list.addLast(20);         // 맨 뒤에 추가
list.removeFirst();       // 맨 앞 제거
list.removeLast();        // 맨 뒤 제거
```

**선택 기준:**
- **ArrayList**: 인덱스 접근이 많은 경우 (get 자주 사용)
- **LinkedList**: 삽입/삭제가 많은 경우 (add/remove 자주 사용)

---

## 4. Set

### HashSet: 중복 제거, 순서 X

```java
// 생성
Set<Integer> set = new HashSet<>();

// 주요 메서드
set.add(10);              // 추가 (중복 시 false 반환)
set.remove(10);           // 제거
set.contains(10);         // 포함 여부 O(1)
set.size();               // 크기
set.isEmpty();            // 비어있는지
set.clear();              // 모든 요소 제거

// 순회
for (int num : set) {
    System.out.println(num);
}
```

### TreeSet: 정렬된 Set

```java
// 생성
TreeSet<Integer> set = new TreeSet<>();

// HashSet 메서드 + 추가
set.first();              // 최솟값
set.last();               // 최댓값
set.lower(10);            // 10보다 작은 최대값
set.higher(10);           // 10보다 큰 최솟값
set.floor(10);            // 10 이하의 최대값
set.ceiling(10);          // 10 이상의 최솟값
```

---

## 5. Map

### HashMap: Key-Value 저장, 순서 X

```java
// 생성
Map<String, Integer> map = new HashMap<>();

// 주요 메서드
map.put("apple", 100);    // 추가/수정
map.get("apple");         // 값 가져오기
map.getOrDefault("banana", 0); // 없으면 기본값 반환
map.containsKey("apple"); // 키 존재 여부
map.containsValue(100);   // 값 존재 여부
map.remove("apple");      // 제거
map.size();               // 크기
map.isEmpty();            // 비어있는지

// 순회
for (String key : map.keySet()) {
    System.out.println(key + " = " + map.get(key));
}

for (Map.Entry<String, Integer> entry : map.entrySet()) {
    System.out.println(entry.getKey() + " = " + entry.getValue());
}

// 빈도수 세기 패턴
map.put(key, map.getOrDefault(key, 0) + 1);
```

### TreeMap: 정렬된 Map

```java
// 생성
TreeMap<String, Integer> map = new TreeMap<>();

// HashMap 메서드 + 추가
map.firstKey();           // 최소 키
map.lastKey();            // 최대 키
map.lowerKey("apple");    // "apple"보다 작은 최대 키
map.higherKey("apple");   // "apple"보다 큰 최소 키
```

---

## 6. Heap (PriorityQueue)

### PriorityQueue: 최소 힙 (기본)

```java
// 최소 힙 (작은 값이 우선)
PriorityQueue<Integer> minHeap = new PriorityQueue<>();

// 최대 힙 (큰 값이 우선)
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());

// 주요 메서드
minHeap.offer(10);        // 추가 (add와 유사)
minHeap.poll();           // 최소값 제거 & 반환
minHeap.peek();           // 최소값 확인 (제거 X)
minHeap.isEmpty();        // 비어있는지
minHeap.size();           // 크기
minHeap.clear();          // 모든 요소 제거
```

### 커스텀 Comparator 사용

```java
// 예제 1: 절댓값 기준 최소 힙
PriorityQueue<Integer> pq = new PriorityQueue<>(
    (a, b) -> Math.abs(a) - Math.abs(b)
);

// 예제 2: 객체의 특정 필드 기준
class Student {
    String name;
    int score;
}

// 점수 오름차순
PriorityQueue<Student> pq = new PriorityQueue<>(
    Comparator.comparingInt(s -> s.score)
);

// 점수 내림차순
PriorityQueue<Student> pq = new PriorityQueue<>(
    (s1, s2) -> s2.score - s1.score
);

// 점수 내림차순 -> 이름 오름차순
PriorityQueue<Student> pq = new PriorityQueue<>(
    Comparator.comparingInt((Student s) -> s.score).reversed()
              .thenComparing(s -> s.name)
);
```

**Top-K 문제 패턴**
```java
// 상위 K개 찾기: 최소 힙 사용 (크기 K 유지)
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
for (int num : nums) {
    minHeap.offer(num);
    if (minHeap.size() > k) {
        minHeap.poll(); // 가장 작은 값 제거
    }
}
// 결과: minHeap에 상위 K개 남음
```

---

## 7. 정렬 (Sorting)

### Arrays.sort() - 배열 정렬

```java
// 기본형 배열 - 오름차순만 가능
int[] arr = {3, 1, 4, 1, 5};
Arrays.sort(arr);

// 부분 정렬 (시작 인덱스, 끝 인덱스)
Arrays.sort(arr, 0, 3); // 인덱스 0~2만 정렬

// 객체 배열 - Comparator 사용 가능
Integer[] arr2 = {3, 1, 4, 1, 5};
Arrays.sort(arr2, Collections.reverseOrder()); // 내림차순

// 람다로 커스텀 정렬
String[] words = {"apple", "pie", "banana"};
Arrays.sort(words, (a, b) -> a.length() - b.length()); // 길이 순
```

### Collections.sort() - 리스트 정렬

```java
List<Integer> list = new ArrayList<>(Arrays.asList(3, 1, 4, 1, 5));

// 오름차순
Collections.sort(list);

// 내림차순
Collections.sort(list, Collections.reverseOrder());

// 또는 리스트 메서드 사용
list.sort(Comparator.naturalOrder());      // 오름차순
list.sort(Comparator.reverseOrder());      // 내림차순
```

### Comparator 활용

```java
class Student {
    String name;
    int score;
    int age;
}

List<Student> students = new ArrayList<>();

// 1. 점수 오름차순
students.sort(Comparator.comparingInt(s -> s.score));

// 2. 점수 내림차순
students.sort(Comparator.comparingInt((Student s) -> s.score).reversed());

// 3. 다중 조건: 점수 내림차순 -> 나이 오름차순
students.sort(
    Comparator.comparingInt((Student s) -> s.score).reversed()
              .thenComparingInt(s -> s.age)
);

// 4. 이름 길이 순 -> 사전순
students.sort(
    Comparator.comparingInt((Student s) -> s.name.length())
              .thenComparing(s -> s.name)
);
```

**시간 복잡도:**
- `Arrays.sort()`: O(n log n) - Dual-Pivot Quicksort (기본형), Timsort (객체)
- `Collections.sort()`: O(n log n) - Timsort

**가장 효과적인 정렬:**
- **일반적인 경우**: `Arrays.sort()` 또는 `Collections.sort()`
- **거의 정렬된 데이터**: Timsort가 효율적 (Java 기본)
- **안정성 필요**: Collections.sort() (안정 정렬)

---

## 8. 탐색 알고리즘 (BFS, DFS)

### BFS (Breadth-First Search) - 너비 우선 탐색

**Queue 사용**

```java
public void bfs(int start) {
    Queue<Integer> queue = new LinkedList<>();
    boolean[] visited = new boolean[n];

    queue.offer(start);
    visited[start] = true;

    while (!queue.isEmpty()) {
        int current = queue.poll();
        System.out.println(current);

        // 인접 노드 탐색
        for (int next : graph[current]) {
            if (!visited[next]) {
                queue.offer(next);
                visited[next] = true;
            }
        }
    }
}
```

**최단 거리 구하기 (레벨 추적)**
```java
public int bfsShortestPath(int start, int target) {
    Queue<int[]> queue = new LinkedList<>(); // [노드, 거리]
    boolean[] visited = new boolean[n];

    queue.offer(new int[]{start, 0});
    visited[start] = true;

    while (!queue.isEmpty()) {
        int[] current = queue.poll();
        int node = current[0];
        int dist = current[1];

        if (node == target) return dist;

        for (int next : graph[node]) {
            if (!visited[next]) {
                queue.offer(new int[]{next, dist + 1});
                visited[next] = true;
            }
        }
    }
    return -1; // 도달 불가
}
```

### DFS (Depth-First Search) - 깊이 우선 탐색

**재귀 버전**
```java
boolean[] visited;

public void dfs(int node) {
    visited[node] = true;
    System.out.println(node);

    for (int next : graph[node]) {
        if (!visited[next]) {
            dfs(next);
        }
    }
}

// 호출
visited = new boolean[n];
dfs(start);
```

**Stack 버전 (반복문)**
```java
public void dfsIterative(int start) {
    Deque<Integer> stack = new ArrayDeque<>();
    boolean[] visited = new boolean[n];

    stack.push(start);

    while (!stack.isEmpty()) {
        int current = stack.pop();

        if (visited[current]) continue;
        visited[current] = true;
        System.out.println(current);

        // 역순으로 추가 (재귀와 동일한 순서)
        for (int i = graph[current].length - 1; i >= 0; i--) {
            int next = graph[current][i];
            if (!visited[next]) {
                stack.push(next);
            }
        }
    }
}
```

### 그래프 표현 방법

**인접 리스트 (추천)**
```java
// 방법 1: ArrayList 배열
List<Integer>[] graph = new ArrayList[n];
for (int i = 0; i < n; i++) {
    graph[i] = new ArrayList<>();
}
graph[0].add(1);
graph[0].add(2);

// 방법 2: HashMap (노드가 정수가 아닐 때)
Map<Integer, List<Integer>> graph = new HashMap<>();
graph.putIfAbsent(0, new ArrayList<>());
graph.get(0).add(1);
```

**인접 행렬**
```java
int[][] graph = new int[n][n];
graph[0][1] = 1; // 0 -> 1 간선
graph[1][0] = 1; // 양방향
```

**선택 기준:**
- **인접 리스트**: 간선이 적은 경우 (희소 그래프) - 메모리 효율적
- **인접 행렬**: 간선이 많은 경우 (밀집 그래프) - 간선 확인 O(1)

---

## 9. 유용한 유틸리티

### Arrays 유틸

```java
// 배열 -> 문자열
Arrays.toString(arr);         // [1, 2, 3]

// 배열 복사
int[] copy = Arrays.copyOf(arr, arr.length);
int[] range = Arrays.copyOfRange(arr, 1, 4); // 인덱스 1~3

// 배열 채우기
Arrays.fill(arr, 0);          // 모두 0으로
Arrays.fill(arr, 2, 5, -1);   // 인덱스 2~4를 -1로

// 배열 비교
Arrays.equals(arr1, arr2);    // 내용 비교

// 이진 탐색 (정렬된 배열)
int index = Arrays.binarySearch(arr, target); // O(log n)
```

### Collections 유틸

```java
// 최댓값, 최솟값
Collections.max(list);
Collections.min(list);

// 빈도수
Collections.frequency(list, 10); // 10이 몇 개?

// 뒤집기
Collections.reverse(list);

// 섞기
Collections.shuffle(list);

// 채우기
Collections.fill(list, 0);

// 복사
Collections.copy(dest, src);
```

### String 유틸

```java
String s = "hello";

// 문자 배열로 변환
char[] chars = s.toCharArray();

// 문자열 배열로 변환
String[] words = s.split(" ");

// StringBuilder (가변 문자열)
StringBuilder sb = new StringBuilder();
sb.append("hello");
sb.append(" world");
sb.reverse();
String result = sb.toString();
```

### Math 유틸

```java
Math.max(a, b);               // 최댓값
Math.min(a, b);               // 최솟값
Math.abs(x);                  // 절댓값
Math.pow(2, 3);               // 2^3 = 8
Math.sqrt(16);                // 제곱근 = 4
Math.ceil(3.2);               // 올림 = 4.0
Math.floor(3.8);              // 내림 = 3.0
Math.round(3.5);              // 반올림 = 4
```

---

## 10. 시간 복잡도 요약

| 자료구조 | 접근 | 탐색 | 삽입 | 삭제 |
|---------|------|------|------|------|
| ArrayList | O(1) | O(n) | O(n) | O(n) |
| LinkedList | O(n) | O(n) | O(1) | O(1) |
| HashSet | - | O(1) | O(1) | O(1) |
| TreeSet | - | O(log n) | O(log n) | O(log n) |
| HashMap | O(1) | O(1) | O(1) | O(1) |
| TreeMap | O(log n) | O(log n) | O(log n) | O(log n) |
| PriorityQueue | - | - | O(log n) | O(log n) |
| ArrayDeque | O(1) | - | O(1) | O(1) |

---

## 11. 자주 쓰는 패턴

### 슬라이딩 윈도우
```java
// 크기 k의 윈도우 최댓값
Deque<Integer> deque = new ArrayDeque<>();
for (int i = 0; i < nums.length; i++) {
    // 범위 벗어난 인덱스 제거
    while (!deque.isEmpty() && deque.peekFirst() < i - k + 1) {
        deque.pollFirst();
    }
    // 현재 값보다 작은 값들 제거
    while (!deque.isEmpty() && nums[deque.peekLast()] < nums[i]) {
        deque.pollLast();
    }
    deque.offerLast(i);
    if (i >= k - 1) {
        result.add(nums[deque.peekFirst()]);
    }
}
```

### Two Pointers
```java
int left = 0, right = arr.length - 1;
while (left < right) {
    if (arr[left] + arr[right] == target) {
        // 찾음
        left++;
        right--;
    } else if (arr[left] + arr[right] < target) {
        left++;
    } else {
        right--;
    }
}
```

### 빈도수 카운팅
```java
Map<Integer, Integer> freq = new HashMap<>();
for (int num : nums) {
    freq.put(num, freq.getOrDefault(num, 0) + 1);
}
```

### 역방향 순회
```java
// List 역방향
for (int i = list.size() - 1; i >= 0; i--) {
    System.out.println(list.get(i));
}

// 역방향 Iterator
Iterator<Integer> it = list.descendingIterator();
while (it.hasNext()) {
    System.out.println(it.next());
}
```

---

## 참고사항

- **ArrayList vs LinkedList**: 대부분의 경우 ArrayList가 빠름 (캐시 효율)
- **HashMap vs TreeMap**: 정렬이 필요 없으면 HashMap
- **HashSet vs TreeSet**: 정렬이 필요 없으면 HashSet
- **Stack 대신 ArrayDeque 사용**: 더 빠르고 메모리 효율적
- **Primitive vs Wrapper**: 성능이 중요하면 int[], long[] 등 사용
- **String 연결**: 반복문 안에서는 StringBuilder 사용

---

**작성일**: 2025-12-08
