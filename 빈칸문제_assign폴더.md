# 빈칸 채우기 문제 - Assign 폴더 (20문제)

## 문제 1: 괄호 검사기 - 빈 배열 처리
```java
public static boolean isPair(char[] brackets) {
    var stack = new Stack<Character>();
    if (brackets.length == 0) {
        ____________________;  // 빈 배열일 때 반환값
    }
    // ... 나머지 코드
}
```
**힌트**: 빈 배열은 괄호가 없으므로 유효한 괄호 쌍입니다.

<details>
<summary>정답 보기</summary>

```java
return true;
```

빈 배열은 검사할 괄호가 없으므로 자동으로 올바른 괄호 쌍으로 간주됩니다.
</details>

---

## 문제 2: 괄호 검사기 - 여는 괄호 처리
```java
public static boolean isPair(char[] brackets) {
    var stack = new Stack<Character>();
    for (int i = 0; i < brackets.length; i++) {
        char ch = brackets[i];
        if (isOpenBracket(ch)) {
            ____________________;  // 여는 괄호를 만났을 때 처리
        }
        // ... 나머지 코드
    }
    return stack.isEmpty();
}
```
**힌트**: 여는 괄호는 나중에 매칭할 닫는 괄호를 찾기 위해 저장해야 합니다.

<details>
<summary>정답 보기</summary>

```java
stack.push(ch);
```

여는 괄호 `(`, `[`, `{`를 만나면 스택에 push하여 나중에 대응하는 닫는 괄호와 매칭할 수 있도록 합니다.
</details>

---

## 문제 3: 괄호 검사기 - 스택이 비었을 때 처리
```java
public static boolean isPair(char[] brackets) {
    var stack = new Stack<Character>();
    for (int i = 0; i < brackets.length; i++) {
        char ch = brackets[i];
        if (isOpenBracket(ch)) {
            stack.push(ch);
        }
        else if (isCloseBracket(ch)) {
            if (stack.isEmpty()) {
                ____________________;  // 스택이 비었는데 닫는 괄호가 나온 경우
            }
            // ... 나머지 코드
        }
    }
    return stack.isEmpty();
}
```
**힌트**: 닫는 괄호에 대응하는 여는 괄호가 없다는 의미입니다.

<details>
<summary>정답 보기</summary>

```java
return false;
```

스택이 비어있는데 닫는 괄호가 나온다는 것은 매칭되는 여는 괄호가 없다는 의미이므로 올바르지 않은 괄호 쌍입니다.
</details>

---

## 문제 4: 괄호 검사기 - 괄호 쌍 불일치 처리
```java
public static boolean isPair(char[] brackets) {
    var stack = new Stack<Character>();
    for (int i = 0; i < brackets.length; i++) {
        char ch = brackets[i];
        if (isOpenBracket(ch)) {
            stack.push(ch);
        }
        else if (isCloseBracket(ch)) {
            if (stack.isEmpty()) {
                return false;
            }
            char openBracket = stack.pop();
            if (!isMatchingPair(openBracket, ch)) {
                ____________________;  // 괄호 쌍이 일치하지 않을 때
            }
        }
    }
    return stack.isEmpty();
}
```
**힌트**: `(`와 `]` 처럼 서로 다른 종류의 괄호가 매칭된 경우입니다.

<details>
<summary>정답 보기</summary>

```java
return false;
```

여는 괄호와 닫는 괄호의 타입이 일치하지 않으면 (예: `(]`) 올바르지 않은 괄호 쌍입니다.
</details>

---

## 문제 5: 괄호 검사기 - 최종 검사
```java
public static boolean isPair(char[] brackets) {
    var stack = new Stack<Character>();
    if (brackets.length == 0) {
        return true;
    }
    for (int i = 0; i < brackets.length; i++) {
        char ch = brackets[i];
        if (isOpenBracket(ch)) {
            stack.push(ch);
        }
        else if (isCloseBracket(ch)) {
            if (stack.isEmpty()) {
                return false;
            }
            char openBracket = stack.pop();
            if (!isMatchingPair(openBracket, ch)) {
                return false;
            }
        }
    }
    ____________________;  // 모든 괄호 검사가 끝난 후 반환값
}
```
**힌트**: 모든 괄호가 올바르게 매칭되었다면 스택이 비어있어야 합니다.

<details>
<summary>정답 보기</summary>

```java
return stack.isEmpty();
```

모든 처리가 끝난 후 스택이 비어있으면 모든 여는 괄호가 닫는 괄호와 매칭되었다는 의미입니다. 스택에 남아있으면 매칭되지 않은 여는 괄호가 있다는 의미입니다.
</details>

---

## 문제 6: 이진 트리 삽입 - 루트 노드 설정
```java
void insert(T data) {
    var newNode = new Node<>(data);

    if (root == null) {
        ____________________;  // 트리가 비어있을 때 새 노드 처리
        return;
    }

    Queue<Node<T>> queue = new LinkedList<>();
    queue.offer(root);
    // ... 나머지 코드
}
```
**힌트**: 트리가 비어있으면 새 노드가 트리의 첫 번째 노드가 됩니다.

<details>
<summary>정답 보기</summary>

```java
root = newNode;
```

트리가 비어있을 때는 새로운 노드를 루트 노드로 설정합니다.
</details>

---

## 문제 7: 이진 트리 삽입 - 왼쪽 자식 삽입
```java
void insert(T data) {
    var newNode = new Node<>(data);

    if (root == null) {
        root = newNode;
        return;
    }

    Queue<Node<T>> queue = new LinkedList<>();
    queue.offer(root);

    while (!queue.isEmpty()) {
        var current = queue.poll();

        if (current.left == null) {
            ____________________;  // 왼쪽 자식이 비어있을 때
            return;
        } else {
            queue.offer(current.left);
        }
        // ... 나머지 코드
    }
}
```
**힌트**: 레벨 순서 삽입에서 왼쪽 자식이 비어있으면 그 위치에 삽입합니다.

<details>
<summary>정답 보기</summary>

```java
current.left = newNode;
```

현재 노드의 왼쪽 자식이 비어있으면 새 노드를 왼쪽 자식으로 설정하고 삽입을 완료합니다.
</details>

---

## 문제 8: 이진 트리 삽입 - 오른쪽 자식 삽입
```java
void insert(T data) {
    var newNode = new Node<>(data);
    Queue<Node<T>> queue = new LinkedList<>();
    queue.offer(root);

    while (!queue.isEmpty()) {
        var current = queue.poll();

        if (current.left == null) {
            current.left = newNode;
            return;
        } else {
            queue.offer(current.left);
        }

        if (current.right == null) {
            ____________________;  // 오른쪽 자식이 비어있을 때
            return;
        } else {
            queue.offer(current.right);
        }
    }
}
```
**힌트**: 왼쪽 자식이 차 있고 오른쪽 자식이 비어있으면 오른쪽에 삽입합니다.

<details>
<summary>정답 보기</summary>

```java
current.right = newNode;
```

현재 노드의 오른쪽 자식이 비어있으면 새 노드를 오른쪽 자식으로 설정하고 삽입을 완료합니다.
</details>

---

## 문제 9: 전위 순회 (Preorder) - 루트 방문
```java
private void preorderHelper(Node<T> node, List<T> result) {
    if (node == null) return;

    ____________________;               // 1. 루트 방문
    preorderHelper(node.left, result);  // 2. 왼쪽 서브트리 순회
    preorderHelper(node.right, result); // 3. 오른쪽 서브트리 순회
}
```
**힌트**: 전위 순회는 루트 → 왼쪽 → 오른쪽 순서입니다.

<details>
<summary>정답 보기</summary>

```java
result.add(node.data);
```

전위 순회(Preorder)는 루트를 먼저 방문한 후 왼쪽, 오른쪽 서브트리를 순회합니다.
</details>

---

## 문제 10: 중위 순회 (Inorder) - 방문 순서
```java
private void inorderHelper(Node<T> node, List<T> result) {
    if (node == null) return;

    inorderHelper(node.left, result);   // 1. 왼쪽 서브트리 순회
    ____________________;                // 2. 루트 방문
    inorderHelper(node.right, result);  // 3. 오른쪽 서브트리 순회
}
```
**힌트**: 중위 순회는 왼쪽 → 루트 → 오른쪽 순서입니다.

<details>
<summary>정답 보기</summary>

```java
result.add(node.data);
```

중위 순회(Inorder)는 왼쪽 서브트리를 먼저 방문하고, 루트를 방문한 후, 오른쪽 서브트리를 순회합니다. BST에서는 정렬된 순서로 값을 얻을 수 있습니다.
</details>

---

## 문제 11: 후위 순회 (Postorder) - 루트 방문 위치
```java
private void postorderHelper(Node<T> node, List<T> result) {
    if (node == null) return;

    postorderHelper(node.left, result);  // 1. 왼쪽 서브트리 순회
    postorderHelper(node.right, result); // 2. 오른쪽 서브트리 순회
    ____________________;                 // 3. 루트 방문
}
```
**힌트**: 후위 순회는 왼쪽 → 오른쪽 → 루트 순서입니다.

<details>
<summary>정답 보기</summary>

```java
result.add(node.data);
```

후위 순회(Postorder)는 왼쪽과 오른쪽 서브트리를 모두 방문한 후 마지막으로 루트를 방문합니다. 트리 삭제나 수식 트리 계산에 유용합니다.
</details>

---

## 문제 12: BFS - 큐 초기화
```java
List<T> bfs() {
    List<T> result = new ArrayList<>();

    if (root == null) return result;

    Queue<Node<T>> queue = new LinkedList<>();
    ____________________;  // BFS 시작을 위한 초기 설정

    while (!queue.isEmpty()) {
        var current = queue.poll();
        result.add(current.data);
        // ... 나머지 코드
    }

    return result;
}
```
**힌트**: BFS는 루트 노드부터 시작합니다.

<details>
<summary>정답 보기</summary>

```java
queue.offer(root);
```

BFS(너비 우선 탐색)는 루트 노드를 큐에 넣는 것으로 시작합니다.
</details>

---

## 문제 13: BFS - 왼쪽 자식 큐에 추가
```java
List<T> bfs() {
    List<T> result = new ArrayList<>();
    Queue<Node<T>> queue = new LinkedList<>();
    queue.offer(root);

    while (!queue.isEmpty()) {
        var current = queue.poll();
        result.add(current.data);

        if (current.left != null) {
            ____________________;  // 왼쪽 자식 처리
        }
        // ... 나머지 코드
    }

    return result;
}
```
**힌트**: 현재 노드의 왼쪽 자식을 다음 레벨 탐색을 위해 준비합니다.

<details>
<summary>정답 보기</summary>

```java
queue.offer(current.left);
```

현재 노드의 왼쪽 자식이 존재하면 큐에 추가하여 다음 레벨에서 방문할 수 있도록 합니다.
</details>

---

## 문제 14: BFS - 오른쪽 자식 큐에 추가
```java
List<T> bfs() {
    List<T> result = new ArrayList<>();
    Queue<Node<T>> queue = new LinkedList<>();
    queue.offer(root);

    while (!queue.isEmpty()) {
        var current = queue.poll();
        result.add(current.data);

        if (current.left != null) {
            queue.offer(current.left);
        }
        if (current.right != null) {
            ____________________;  // 오른쪽 자식 처리
        }
    }

    return result;
}
```
**힌트**: 현재 노드의 오른쪽 자식도 다음 레벨 탐색에 포함해야 합니다.

<details>
<summary>정답 보기</summary>

```java
queue.offer(current.right);
```

현재 노드의 오른쪽 자식이 존재하면 큐에 추가하여 다음 레벨에서 방문할 수 있도록 합니다.
</details>

---

## 문제 15: QuickSort - Pivot 선택과 Swap
```java
private int partition(int[] arr, int low, int high) {
    // 중간 요소를 pivot으로 선택
    int pivot_index = ___________________;  // low와 high의 중간 인덱스
    swap(arr, __________, __________);      // pivot을 맨 앞으로 이동

    int pivot = arr[low];
    int i = low + 1;
    int j = high;
    // ... 나머지 코드
}
```
**힌트**: 중간 pivot 전략에서는 중간 인덱스를 계산하고 pivot을 첫 위치로 이동시킵니다.

<details>
<summary>정답 보기</summary>

```java
int pivot_index = (low + high) / 2;
swap(arr, pivot_index, low);
```

중간 요소를 pivot으로 선택하기 위해 중간 인덱스를 계산하고, 선택된 pivot을 배열의 맨 앞(low)으로 swap합니다.
</details>

---

## 문제 16: QuickSort - Partition의 i 증가 조건
```java
private int partition(int[] arr, int low, int high) {
    int pivot = arr[low];
    int i = low + 1;
    int j = high;

    while (true) {
        // pivot보다 큰 요소를 찾을 때까지 i 증가
        while (i <= j && __________________) {  // i를 증가시키는 조건
            i++;
        }
        // ... 나머지 코드
    }
}
```
**힌트**: i는 pivot보다 작거나 같은 요소를 건너뜁니다.

<details>
<summary>정답 보기</summary>

```java
arr[i] <= pivot
```

i 포인터는 왼쪽에서 오른쪽으로 이동하며 pivot보다 작거나 같은 요소들을 건너뜁니다. pivot보다 큰 요소를 만나면 멈춥니다.
</details>

---

## 문제 17: QuickSort - Partition의 j 감소 조건
```java
private int partition(int[] arr, int low, int high) {
    int pivot = arr[low];
    int i = low + 1;
    int j = high;

    while (true) {
        while (i <= j && arr[i] <= pivot) {
            i++;
        }
        // pivot보다 작은 요소를 찾을 때까지 j 감소
        while (i <= j && __________________) {  // j를 감소시키는 조건
            j--;
        }
        // ... 나머지 코드
    }
}
```
**힌트**: j는 pivot보다 크거나 같은 요소를 건너뜁니다.

<details>
<summary>정답 보기</summary>

```java
arr[j] >= pivot
```

j 포인터는 오른쪽에서 왼쪽으로 이동하며 pivot보다 크거나 같은 요소들을 건너뜁니다. pivot보다 작은 요소를 만나면 멈춥니다.
</details>

---

## 문제 18: QuickSort - i와 j 교차 확인
```java
private int partition(int[] arr, int low, int high) {
    int pivot = arr[low];
    int i = low + 1;
    int j = high;

    while (true) {
        while (i <= j && arr[i] <= pivot) {
            i++;
        }
        while (i <= j && arr[j] >= pivot) {
            j--;
        }
        // i와 j가 교차하면 종료
        if (____________________) {  // 루프 종료 조건
            break;
        }
        swap(arr, i, j);
    }
    // ... 나머지 코드
}
```
**힌트**: i가 j를 넘어서면 partition이 완료된 것입니다.

<details>
<summary>정답 보기</summary>

```java
i > j
```

i가 j보다 커지면 두 포인터가 교차한 것이므로 partition 과정을 종료합니다.
</details>

---

## 문제 19: QuickSort - Pivot 최종 위치로 이동
```java
private int partition(int[] arr, int low, int high) {
    int pivot = arr[low];
    int i = low + 1;
    int j = high;

    while (true) {
        while (i <= j && arr[i] <= pivot) {
            i++;
        }
        while (i <= j && arr[j] >= pivot) {
            j--;
        }
        if (i > j) {
            break;
        }
        swap(arr, i, j);
    }
    // pivot을 올바른 위치로 이동
    swap(arr, __________, __________);  // pivot을 j 위치로 이동
    System.out.print(pivot + ", ");
    return j;
}
```
**힌트**: pivot은 j 위치로 이동해야 합니다.

<details>
<summary>정답 보기</summary>

```java
swap(arr, low, j);
```

partition이 끝나면 pivot(현재 low 위치)을 j 위치로 이동시킵니다. 이때 j의 왼쪽은 pivot보다 작거나 같고, 오른쪽은 pivot보다 크거나 같습니다.
</details>

---

## 문제 20: QuickSort - 재귀 호출 범위
```java
private void sort(int[] arr, int low, int high) {
    if (low < high) {
        int pivotIndex = partition(arr, low, high);

        // pivot 기준 왼쪽 부분 정렬
        sort(arr, __________, __________);

        // pivot 기준 오른쪽 부분 정렬
        sort(arr, __________, __________);
    }
}
```
**힌트**: pivot을 기준으로 왼쪽과 오른쪽 부분을 재귀적으로 정렬합니다.

<details>
<summary>정답 보기</summary>

```java
sort(arr, low, pivotIndex - 1);
sort(arr, pivotIndex + 1, high);
```

pivot의 최종 위치(pivotIndex)를 기준으로:
- 왼쪽 부분: `low`부터 `pivotIndex - 1`까지
- 오른쪽 부분: `pivotIndex + 1`부터 `high`까지

를 재귀적으로 정렬합니다. pivot은 이미 올바른 위치에 있으므로 제외합니다.
</details>

---

## 문제 21: 괄호 타입 검사 - isOpenBracket 구현
```java
private static boolean isOpenBracket(char ch) {
    return ch == '(' || ch == ___________①___________ || ch == ___________②___________;
}
```
**힌트**: 여는 괄호는 총 3종류입니다.

<details>
<summary>정답 보기</summary>

```java
// ① '['
// ② '{'
```

여는 괄호의 종류: `(`, `[`, `{`
</details>

---

## 문제 22: 괄호 타입 검사 - isCloseBracket 구현
```java
private static boolean isCloseBracket(char ch) {
    return ch == ___________①___________ || ch == ']' || ch == '}';
}
```
**힌트**: 닫는 괄호는 여는 괄호에 대응됩니다.

<details>
<summary>정답 보기</summary>

```java
// ① ')'
```

닫는 괄호의 종류: `)`, `]`, `}`
</details>

---

## 문제 23: 괄호 매칭 검사 - isMatchingPair 구현
```java
private static boolean isMatchingPair(char open, char close) {
    return (open == '(' && close == ___________①___________) ||
           (open == '[' && close == ']') ||
           (open == ___________②___________ && close == '}');
}
```
**힌트**: 각 여는 괄호는 대응하는 닫는 괄호와 쌍을 이룹니다.

<details>
<summary>정답 보기</summary>

```java
// ① ')'
// ② '{'
```

괄호 쌍: `()`, `[]`, `{}`
</details>

---

## 문제 24: 이진 트리 시각화 - printTreeHelper 구조
```java
private void printTreeHelper(Node<T> node, String prefix, boolean isTail) {
    if (node == null) return;

    System.out.println(prefix + (isTail ? ___________①___________ : "├── ") + node.data);

    if (node.left != null || node.right != null) {
        if (node.right != null) {
            printTreeHelper(node.right, prefix + (isTail ? "    " : "│   "), ___________②___________);
        }
        if (node.left != null) {
            printTreeHelper(node.left, prefix + (isTail ? "    " : "│   "), true);
        }
    }
}
```
**힌트**: 트리 구조를 시각적으로 표현하기 위한 문자열입니다.

<details>
<summary>정답 보기</summary>

```java
// ① "└── "
// ② false
```

마지막 자식은 `└── `로, 중간 자식은 `├── `로 표현합니다.
</details>

---

## 문제 25: 이진 트리 노드 구조 - Node 클래스
```java
private static class Node<T> {
    T data;
    Node<T> ___________①___________;  // 왼쪽 자식
    Node<T> ___________②___________;  // 오른쪽 자식

    Node(T data) {
        this.data = data;
    }
}
```
**힌트**: 이진 트리는 각 노드가 최대 두 개의 자식을 가집니다.

<details>
<summary>정답 보기</summary>

```java
// ① left
// ② right
```

이진 트리의 각 노드는 왼쪽(left)과 오른쪽(right) 자식을 가집니다.
</details>

---

## 문제 26: QuickSort - swap 메서드 구현
```java
private void swap(int[] arr, int i, int j) {
    int temp = ___________①___________;
    arr[i] = ___________②___________;
    arr[j] = temp;
}
```
**힌트**: 두 요소의 위치를 교환하는 표준적인 방법입니다.

<details>
<summary>정답 보기</summary>

```java
// ① arr[i]
// ② arr[j]
```

임시 변수(temp)를 사용하여 두 요소를 교환합니다.
</details>

---

## 문제 27: QuickSort - 배열 정렬 시작
```java
public void sort(int[] arr) {
    if(arr.length < 2 ) return;
    else {
        System.out.println("=====Pivot list =====");
        sort(arr, ___________①___________, ___________②___________);
        System.out.println("\n=====");
    }
}
```
**힌트**: 배열의 전체 범위를 정렬합니다.

<details>
<summary>정답 보기</summary>

```java
// ① 0
// ② arr.length - 1
```

배열의 시작 인덱스(0)부터 마지막 인덱스(arr.length - 1)까지 정렬합니다.
</details>

---

## 문제 28: QuickSort - 재귀 종료 조건
```java
private void sort(int[] arr, int low, int high) {
    if (___________①___________) {
        int pivotIndex = partition(arr, low, high);
        sort(arr, low, pivotIndex - 1);
        sort(arr, pivotIndex + 1, high);
    }
}
```
**힌트**: 정렬할 범위가 유효한지 확인합니다.

<details>
<summary>정답 보기</summary>

```java
// ① low < high
```

low가 high보다 작을 때만 정렬을 계속합니다. 같거나 크면 정렬할 요소가 없거나 하나뿐입니다.
</details>

---

## 문제 29: 이진 트리 - 빈 트리 확인 (BFS)
```java
List<T> bfs() {
    List<T> result = new ArrayList<>();

    if (___________①___________) return result;

    Queue<Node<T>> queue = new LinkedList<>();
    queue.offer(root);
    // ... 나머지 코드
}
```
**힌트**: 트리가 비어있으면 순회할 노드가 없습니다.

<details>
<summary>정답 보기</summary>

```java
// ① root == null
```

루트가 null이면 트리가 비어있으므로 빈 리스트를 반환합니다.
</details>

---

## 문제 30: 이진 트리 - Preorder 메서드 호출
```java
List<T> preorder() {
    List<T> result = new ArrayList<>();
    preorderHelper(___________①___________, result);
    return result;
}
```
**힌트**: 순회는 루트 노드부터 시작합니다.

<details>
<summary>정답 보기</summary>

```java
// ① root
```

전위 순회는 루트 노드에서 시작하여 재귀적으로 모든 노드를 방문합니다.
</details>

---

## 문제 31: 이진 트리 - Inorder 메서드 호출
```java
List<T> inorder() {
    List<T> result = new ArrayList<>();
    inorderHelper(root, ___________①___________);
    return ___________②___________;
}
```
**힌트**: 결과를 저장할 리스트를 전달하고 반환합니다.

<details>
<summary>정답 보기</summary>

```java
// ① result
// ② result
```

헬퍼 메서드에 결과 리스트를 전달하여 순회 결과를 수집한 후 반환합니다.
</details>

---

## 문제 32: 이진 트리 - Postorder 메서드 호출
```java
List<T> postorder() {
    List<T> result = new ArrayList<>();
    ___________①___________(root, result);
    return result;
}
```
**힌트**: 후위 순회를 수행하는 헬퍼 메서드를 호출합니다.

<details>
<summary>정답 보기</summary>

```java
// ① postorderHelper
```

후위 순회 헬퍼 메서드를 호출하여 순회를 시작합니다.
</details>

---

## 문제 33: BFS - 큐가 비었는지 확인
```java
List<T> bfs() {
    List<T> result = new ArrayList<>();
    Queue<Node<T>> queue = new LinkedList<>();
    queue.offer(root);

    while (___________①___________) {
        var current = queue.poll();
        result.add(current.data);
        // ... 나머지 코드
    }

    return result;
}
```
**힌트**: 큐에 노드가 있는 동안 계속 처리합니다.

<details>
<summary>정답 보기</summary>

```java
// ① !queue.isEmpty()
```

큐가 비어있지 않은 동안 계속해서 노드를 꺼내서 처리합니다.
</details>

---

## 문제 34: BFS - 현재 노드 처리
```java
List<T> bfs() {
    List<T> result = new ArrayList<>();
    Queue<Node<T>> queue = new LinkedList<>();
    queue.offer(root);

    while (!queue.isEmpty()) {
        var current = ___________①___________;
        ___________②___________(current.data);

        if (current.left != null) {
            queue.offer(current.left);
        }
        if (current.right != null) {
            queue.offer(current.right);
        }
    }

    return result;
}
```
**힌트**: 큐에서 노드를 꺼내고 결과에 추가합니다.

<details>
<summary>정답 보기</summary>

```java
// ① queue.poll()
// ② result.add
```

큐에서 현재 노드를 poll하여 꺼내고, 그 데이터를 결과 리스트에 추가합니다.
</details>

---

## 문제 35: QuickSort - Pivot 값 설정
```java
private int partition(int[] arr, int low, int high) {
    int pivot_index = (low + high) / 2;
    swap(arr, pivot_index, low);

    int pivot = ___________①___________;

    int i = low + 1;
    int j = high;
    // ... 나머지 코드
}
```
**힌트**: Pivot을 맨 앞으로 이동시킨 후 그 값을 저장합니다.

<details>
<summary>정답 보기</summary>

```java
// ① arr[low]
```

Pivot을 low 위치로 이동시켰으므로 arr[low]가 pivot 값입니다.
</details>

---

## 문제 36: QuickSort - 포인터 초기화
```java
private int partition(int[] arr, int low, int high) {
    int pivot = arr[low];

    int i = ___________①___________;  // 왼쪽에서 시작
    int j = ___________②___________;  // 오른쪽에서 시작

    while (true) {
        // ... 나머지 코드
    }
}
```
**힌트**: i는 pivot 다음부터, j는 끝에서 시작합니다.

<details>
<summary>정답 보기</summary>

```java
// ① low + 1
// ② high
```

i는 pivot(low) 다음 위치부터, j는 배열의 끝(high)에서 시작합니다.
</details>

---

## 문제 37: QuickSort - 요소 교환
```java
private int partition(int[] arr, int low, int high) {
    int pivot = arr[low];
    int i = low + 1;
    int j = high;

    while (true) {
        while (i <= j && arr[i] <= pivot) {
            i++;
        }
        while (i <= j && arr[j] >= pivot) {
            j--;
        }
        if (i > j) {
            break;
        }
        ___________①___________(arr, i, j);
    }
    // ... 나머지 코드
}
```
**힌트**: i와 j 위치의 요소를 교환합니다.

<details>
<summary>정답 보기</summary>

```java
// ① swap
```

arr[i]와 arr[j]를 교환하여 작은 값은 왼쪽, 큰 값은 오른쪽으로 이동시킵니다.
</details>

---

## 문제 38: 괄호 검사기 - 테스트 케이스 실행
```java
public static void main(String[] args) {
    System.out.println("=== 괄호 검사기 테스트 ===");
    char[][] testCases = {
        {'(', ')'},
    };
    IISEStackSol2025 sol = new ___________①___________();

    for (int i = 0; i < testCases.length; i++) {
        char[] brackets = testCases[i];
        boolean result = sol.___________②___________(brackets);
        // ... 출력 코드
    }
}
```
**힌트**: 솔루션 객체를 생성하고 isPair 메서드를 호출합니다.

<details>
<summary>정답 보기</summary>

```java
// ① IISEStackSol2025
// ② isPair
```

솔루션 클래스의 인스턴스를 생성하고 isPair 메서드를 호출하여 괄호 쌍을 검사합니다.
</details>

---

## 문제 39: 이진 트리 - 제네릭 타입 선언
```java
class BinaryTree<___________①___________> {

    private Node<___________②___________> root;

    private static class Node<T> {
        T data;
        Node<T> left;
        Node<T> right;

        Node(T data) {
            this.data = data;
        }
    }
}
```
**힌트**: 제네릭 타입 파라미터를 사용하여 다양한 타입을 저장할 수 있습니다.

<details>
<summary>정답 보기</summary>

```java
// ① T
// ② T
```

제네릭 타입 파라미터 `T`를 사용하여 Integer, String 등 다양한 타입의 데이터를 저장할 수 있습니다.
</details>

---

## 문제 40: 이진 트리 - 생성자 초기화
```java
BinaryTree() {
    this.root = ___________①___________;
}
```
**힌트**: 빈 트리는 루트가 없습니다.

<details>
<summary>정답 보기</summary>

```java
// ① null
```

빈 이진 트리를 생성할 때 루트를 null로 초기화합니다.
</details>

---

**문제 끝! 총 40개 완성**
