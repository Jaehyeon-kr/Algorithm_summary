# 자료구조 빈칸 채우기 문제 (4week ~ 9week)

## 문제 1: ArrayList 동적 배열 크기 조정 (4week)

다음은 `MyArrayList` 클래스의 `ensureCapacity` 메서드입니다. 배열의 크기가 부족할 때 자동으로 확장하는 로직을 구현하세요.

```java
// Ensures that the array has at least the minimum capacity.
private void ensureCapacity(int minCapacity) {
    if (minCapacity > elements.length) {
        int newCapacity = _________①_________;
        if (newCapacity < minCapacity) {
            newCapacity = minCapacity;
        }
        elements = _________②_________;
    }
}
```

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `elements.length * 2`
- ② `Arrays.copyOf(elements, newCapacity)`

</details>

---

## 문제 2: LinkedStack의 Push 연산 (5week)

다음은 `MyLinkedStack` 클래스의 `push` 메서드입니다. 연결 리스트 기반 스택에 새로운 요소를 추가하는 코드를 완성하세요.

```java
@Override
public void push(T newEntry) {
    top = _________①_________;
    _________②_________;
}
```

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `new Node<>(newEntry, top)`
- ② `size++`

</details>

---

## 문제 3: 원형 큐의 isEmpty 확인 (6week)

다음은 `ArrayQueue` 클래스의 `isEmpty` 메서드입니다. 원형 배열 기반 큐가 비어있는지 확인하는 조건을 작성하세요.

```java
public boolean isEmpty() {
    checkIntegrity();
    return _________①_________;
}
```

**힌트:** `first`와 `last`는 큐의 앞과 뒤를 가리키는 인덱스이며, 원형 배열 구조입니다.

**빈칸 채우기:**
- ① _______________

<details>
<summary>정답 보기</summary>

- ① `first == (last + 1) % queue.length`

</details>

---

## 문제 4: 하노이 탑 재귀 알고리즘 (7week)

다음은 하노이 탑 문제를 해결하는 재귀 메서드입니다. 재귀 호출을 완성하세요.

```java
public void hanoi(int num, String source, String target, String spare) {
    // base case
    if(num == 1)
        System.out.println("Move one disk from " + source + " to "+ target);
    else {
        _________①_________;
        System.out.println("Move one disk from " + source + " to "+ target);
        _________②_________;
    }
}
```

**힌트:** n개의 원판을 옮기려면:
1. (n-1)개를 source에서 spare로 이동
2. 가장 큰 원판을 source에서 target으로 이동
3. (n-1)개를 spare에서 target으로 이동

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `hanoi(num-1, source, spare, target)`
- ② `hanoi(num-1, spare, target, source)`

</details>

---

## 문제 5: 이진 탐색 트리 삽입 연산 (8week)

다음은 `BST` 클래스의 재귀적 `insert` 메서드입니다. 올바른 위치에 노드를 삽입하는 코드를 완성하세요.

```java
private boolean insert(TreeNode<T> node, T x) {
    boolean result = true;
    int comp = x.compareTo(node.getData());

    if (comp == 0) {
        result = false; // Duplicate key
    } else if (comp < 0) {
        // Insert in left subtree
        if (node.hasLeftChild()) {
            result = insert(_________①_________, x);
        } else {
            node.setLeftChild(_________②_________);
        }
    } else {
        // Insert in right subtree
        if (node.hasRightChild()) {
            result = insert(node.getRightChild(), x);
        } else {
            node.setRightChild(new TreeNode<T>(x));
        }
    }
    return result;
}
```

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `node.getLeftChild()`
- ② `new TreeNode<T>(x)`

</details>

---

## 문제 6: 힙을 이용한 Top-K 추적 (kpop 폴더)

다음은 `DebutTracker_Heap` 클래스의 `updateVote` 메서드입니다. 최소 힙을 사용하여 상위 K명을 추적하는 로직을 완성하세요.

```java
@Override
public void updateVote(Trainee update) {
    Trainee oldData = null;
    for (Trainee trainee : minHeap) {
        if (trainee.name().equals(update.name())) {
            oldData = trainee;
            break;
        }
    }

    if (oldData != null) {
        minHeap.remove(oldData);
        minHeap.offer(update);

    } else {
        if (minHeap.size() < k) {
            _________①_________;

        } else if (_________②_________) {
            minHeap.poll();
            minHeap.offer(update);
        }
    }
}
```

**힌트:** 최소 힙에서 `peek()`은 최솟값(커트라인)을 반환합니다.

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `minHeap.offer(update)`
- ② `update.totalVotes() > minHeap.peek().totalVotes()`

</details>

---

## 문제 7: Comparable과 Comparator 정렬 (sort 폴더)

다음은 `SortingLab` 클래스의 정렬 예제입니다. 빈칸을 채워 정렬 기능을 완성하세요.

### 7-1: Student 클래스의 자연적 순서 정의

```java
@Override
public int compareTo(Student other) {
    // 점수 기준 내림차순
    return _________①_________;
}
```

### 7-2: 다중 조건 Comparator 구현

```java
// 점수 내림차순 -> 이름 오름차순
Comparator<Student> multiComparator = Comparator
    ._________②_________
    .reversed()
    ._________③_________;
```

**빈칸 채우기:**
- ① _______________
- ② _______________
- ③ _______________

<details>
<summary>정답 보기</summary>

- ① `Integer.compare(other.score, this.score)`
- ② `comparingInt(Student::getScore)`
- ③ `thenComparing(Student::getName)`

</details>

---

## 문제 8: LinkedList의 linkLast 메서드 (4week)

다음은 `MyLinkedList` 클래스의 `linkLast` 메서드입니다. 이중 연결 리스트의 마지막에 요소를 추가하는 코드를 완성하세요.

```java
private void linkLast(E e) {
    final Node<E> l = last;
    final Node<E> newNode = new Node<>(l, e, null);
    last = newNode;
    if (_________①_________) {
        _________②_________;
    } else {
        l.next = newNode;
    }
    size++;
}
```

**힌트:** 리스트가 비어있는 경우와 아닌 경우를 구분해야 합니다.

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `l == null`
- ② `first = newNode`

</details>

---

## 문제 9: LinkedList의 unlink 메서드 (4week)

다음은 `MyLinkedList` 클래스의 `unlink` 메서드입니다. 이중 연결 리스트에서 특정 노드를 제거하는 코드를 완성하세요.

```java
private E unlink(Node<E> x) {
    final E element = x.item;
    final Node<E> next = x.next;
    final Node<E> prev = x.prev;

    if (prev == null) {
        first = next;
    } else {
        _________①_________;
        x.prev = null;
    }

    if (next == null) {
        _________②_________;
    } else {
        next.prev = prev;
        x.next = null;
    }

    x.item = null;
    size--;
    return element;
}
```

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `prev.next = next`
- ② `last = prev`

</details>

---

## 문제 10: LinkedList의 node 탐색 최적화 (4week)

다음은 `MyLinkedList` 클래스의 `node` 메서드입니다. 인덱스 위치에 따라 앞에서부터 또는 뒤에서부터 탐색하는 최적화 코드를 완성하세요.

```java
private Node<E> node(int index) {
    if (index < _________①_________) {
        Node<E> x = first;
        for (int i = 0; i < index; i++)
            x = x.next;
        return x;
    } else {
        Node<E> x = last;
        for (int i = size - 1; i > index; i--)
            x = _________②_________;
        return x;
    }
}
```

**힌트:** `size >> 1`은 size를 2로 나눈 값입니다.

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `(size >> 1)` 또는 `size / 2`
- ② `x.prev`

</details>

---

## 문제 11: LinkedQueue의 enqueue 연산 (6week)

다음은 `LinkedQueue` 클래스의 `enqueue` 메서드입니다. 연결 리스트 기반 큐에 새로운 요소를 추가하는 코드를 완성하세요.

```java
public void enqueue(T newEntry) {
    if (_________①_________)
        first = last = new Node(newEntry, null);
    else
        _________②_________;
    size++;
}
```

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `isEmpty()`
- ② `last = last.next = new Node(newEntry, null)`

</details>

---

## 문제 12: LinkedQueue의 dequeue 연산 (6week)

다음은 `LinkedQueue` 클래스의 `dequeue` 메서드입니다. 큐에서 요소를 제거하고 반환하는 코드를 완성하세요.

```java
public T dequeue() {
    if(isEmpty()) return null;
    T result = _________①_________;
    if(first == last)
        first = last = null;
    else
        _________②_________;
    size--;
    return result;
}
```

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `first.data`
- ② `first = first.next`

</details>

---

## 문제 13: 피보나치 수열 - 꼬리 재귀 (7week)

다음은 피보나치 수열을 꼬리 재귀로 구현한 코드입니다. 재귀 호출을 완성하세요.

```java
public long tailRecursion(int n, long preFibo, long prePreFibo) {
    long currentFibo;
    if (n < 3) return preFibo + prePreFibo;

    currentFibo = _________①_________;
    prePreFibo = preFibo;
    preFibo = currentFibo;
    return _________②_________;
}
```

**힌트:** 꼬리 재귀는 현재 값을 계산한 후 재귀 호출로 전달합니다.

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `preFibo + prePreFibo`
- ② `tailRecursion(n-1, preFibo, prePreFibo)`

</details>

---

## 문제 14: 피보나치 수열 - 반복문 (7week)

다음은 피보나치 수열을 반복문으로 구현한 코드입니다. 빈칸을 채워 완성하세요.

```java
public long iteration(int n) {
    long currentFibo = 1;
    long preFibo = 1, prePreFibo = 1;
    for(int i = n; i > 1; i--) {
        currentFibo = _________①_________;
        _________②_________;
        preFibo = currentFibo;
    }
    return currentFibo;
}
```

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `preFibo + prePreFibo`
- ② `prePreFibo = preFibo`

</details>

---

## 문제 15: BST 삭제 연산 - 최댓값 찾기 (8week)

다음은 `BST` 클래스의 `findMax` 메서드입니다. 서브트리에서 최댓값을 찾는 재귀 코드를 완성하세요.

```java
private T findMax(TreeNode<T> node) {
    if (_________①_________) {
        return findMax(_________②_________);
    } else {
        return node.getData();
    }
}
```

**힌트:** BST에서 최댓값은 가장 오른쪽 노드에 있습니다.

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `node.hasRightChild()`
- ② `node.getRightChild()`

</details>

---

## 문제 16: BST 순회 - Inorder (8week)

다음은 `BST` 클래스의 `inorderTraversal` 메서드입니다. 중위 순회(Inorder)를 완성하세요.

```java
private void inorderTraversal(TreeNode<T> node) {
    if (node != null) {
        _________①_________;
        System.out.print(node.getData() + " ");
        _________②_________;
    }
}
```

**힌트:** 중위 순회는 왼쪽 → 루트 → 오른쪽 순서입니다.

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `inorderTraversal(node.getLeftChild())`
- ② `inorderTraversal(node.getRightChild())`

</details>

---

## 문제 17: BST 트리 높이 계산 (8week)

다음은 `BST` 클래스의 `height` 메서드입니다. 트리의 높이를 재귀적으로 계산하는 코드를 완성하세요.

```java
private int height(TreeNode<T> node) {
    if (node == null) {
        return 0;
    }
    return 1 + _________①_________;
}
```

**힌트:** 높이는 왼쪽과 오른쪽 서브트리 중 더 큰 높이에 1을 더한 값입니다.

**빈칸 채우기:**
- ① _______________

<details>
<summary>정답 보기</summary>

- ① `Math.max(height(node.getLeftChild()), height(node.getRightChild()))`

</details>

---

## 문제 18: Trainee의 compareTo 구현 (kpop 폴더)

다음은 `Trainee` 레코드 클래스의 `compareTo` 메서드입니다. 득표수 내림차순으로 정렬하되, 동점일 경우 이름 오름차순으로 정렬하는 코드를 완성하세요.

```java
public int compareTo(Trainee other) {
    if (this.totalVotes == other.totalVotes) {
        return _________①_________;
    }
    return _________②_________;
}
```

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `this.name.compareTo(other.name)`
- ② `Integer.compare(other.totalVotes, this.totalVotes)`

</details>

---

## 문제 19: DebutTracker_Naive 정렬 (kpop 폴더)

다음은 `DebutTracker_Naive` 클래스의 `getDebutGroup` 메서드입니다. 전체 리스트를 정렬한 후 상위 K명을 추출하는 코드를 완성하세요.

```java
public String getDebutGroup() {
    _________①_________;

    int limit = Math.min(k, allTrainees.size());
    List<Trainee> topK = _________②_________;

    return topK.toString();
}
```

**힌트:** Collections 클래스의 sort 메서드와 List의 subList 메서드를 사용합니다.

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `Collections.sort(allTrainees)`
- ② `allTrainees.subList(0, limit)`

</details>

---

## 문제 20: ArrayList의 remove 연산 (4week)

다음은 `MyArrayList` 클래스의 `remove` 메서드입니다. 특정 인덱스의 요소를 제거하고 배열을 왼쪽으로 이동시키는 코드를 완성하세요.

```java
@Override
public E remove(int index) {
    checkIndex(index);
    E oldValue = (E) elements[index];
    int numMoved = _________①_________;
    if (numMoved > 0) {
        System.arraycopy(elements, _________②_________, elements, index, numMoved);
    }
    elements[--size] = null;
    return oldValue;
}
```

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `size - index - 1`
- ② `index + 1`

</details>

---

## 문제 21: MySortedArrayList의 정렬된 삽입 (4week)

다음은 `MySortedArrayList` 클래스의 `add` 메서드입니다. 정렬을 유지하면서 요소를 삽입하는 코드를 완성하세요.

```java
@Override
public boolean add(E element) {
    int insertionPoint = 0;
    for (int i = 0; i < internalList.size(); i++) {
        if (_________①_________) {
            insertionPoint = i;
            break;
        }
        insertionPoint = _________②_________;
    }
    internalList.add(insertionPoint, element);
    return true;
}
```

**힌트:** `compareTo()` 메서드를 사용하여 삽입 위치를 찾습니다. compareTo() < 0이면 현재 요소가 더 작습니다.

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `element.compareTo(internalList.get(i)) < 0`
- ② `i + 1`

</details>

---

## 문제 22: ArrayQueue의 enqueue 연산 (6week)

다음은 `ArrayQueue` 클래스의 `enqueue` 메서드입니다. 원형 배열 큐에 요소를 추가하는 코드를 완성하세요.

```java
public void enqueue(T newEntry) {
    checkIntegrity();
    ensureCapacity();
    last = _________①_________;
    _________②_________;
}
```

**힌트:** 원형 배열에서는 `(index + 1) % length`를 사용합니다.

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `(last + 1) % queue.length`
- ② `queue[last] = newEntry`

</details>

---

## 문제 23: ArrayQueue의 dequeue 연산 (6week)

다음은 `ArrayQueue` 클래스의 `dequeue` 메서드입니다. 원형 배열 큐에서 요소를 제거하는 코드를 완성하세요.

```java
public T dequeue() {
    checkIntegrity();
    if(isEmpty()) return null;
    else {
        T result = _________①_________;
        queue[first] = null;
        first = _________②_________;
        return result;
    }
}
```

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `queue[first]`
- ② `(first + 1) % queue.length`

</details>

---

## 문제 24: ArrayQueue의 size 계산 (6week)

다음은 `ArrayQueue` 클래스의 `size` 메서드입니다. 원형 배열 큐의 크기를 계산하는 공식을 완성하세요.

```java
public int size() {
    return _________①_________;
}
```

**힌트:** 원형 배열에서 size = (last - first + 1 + length) % length 형태입니다.

**빈칸 채우기:**
- ① _______________

<details>
<summary>정답 보기</summary>

- ① `(last + queue.length + 1 - first) % queue.length`

</details>

---

## 문제 25: BST의 find 메서드 (8week)

다음은 `BST` 클래스의 재귀적 `find` 메서드입니다. 특정 값을 찾는 코드를 완성하세요.

```java
private T find(TreeNode<T> n, T x) {
    T result = null;
    if (n != null) {
        T data = n.getData();
        if (data.compareTo(x) == 0) {
            result = data;
        } else if (_________①_________) {
            result = find(_________②_________, x);
        } else {
            result = find(n.getLeftChild(), x);
        }
    }
    return result;
}
```

**힌트:** BST에서 찾는 값이 현재 노드보다 크면 오른쪽으로, 작으면 왼쪽으로 이동합니다.

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `data.compareTo(x) < 0`
- ② `n.getRightChild()`

</details>

---

## 문제 26: BST의 findMin 메서드 (8week)

다음은 `BST` 클래스의 재귀적 `findMin` 메서드입니다. 서브트리에서 최솟값을 찾는 코드를 완성하세요.

```java
private T findMin(TreeNode<T> node) {
    if (_________①_________) {
        return findMin(_________②_________);
    } else {
        return node.getData();
    }
}
```

**힌트:** BST에서 최솟값은 가장 왼쪽 노드에 있습니다.

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `node.hasLeftChild()`
- ② `node.getLeftChild()`

</details>

---

## 문제 27: BST 순회 - Preorder (8week)

다음은 `BST` 클래스의 `preorderTraversal` 메서드입니다. 전위 순회(Preorder)를 완성하세요.

```java
private void preorderTraversal(TreeNode<T> node) {
    if (node != null) {
        _________①_________;
        _________②_________;
        preorderTraversal(node.getRightChild());
    }
}
```

**힌트:** 전위 순회는 루트 → 왼쪽 → 오른쪽 순서입니다.

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `System.out.print(node.getData() + " ")`
- ② `preorderTraversal(node.getLeftChild())`

</details>

---

## 문제 28: BST 순회 - Postorder (8week)

다음은 `BST` 클래스의 `postorderTraversal` 메서드입니다. 후위 순회(Postorder)를 완성하세요.

```java
private void postorderTraversal(TreeNode<T> node) {
    if (node != null) {
        postorderTraversal(node.getLeftChild());
        _________①_________;
        _________②_________;
    }
}
```

**힌트:** 후위 순회는 왼쪽 → 오른쪽 → 루트 순서입니다.

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `postorderTraversal(node.getRightChild())`
- ② `System.out.print(node.getData() + " ")`

</details>

---

## 문제 29: BST의 size 계산 (8week)

다음은 `BST` 클래스의 재귀적 `size` 메서드입니다. 트리의 노드 개수를 계산하는 코드를 완성하세요.

```java
private int size(TreeNode<T> node) {
    if (node == null) {
        return 0;
    }
    return _________①_________;
}
```

**힌트:** 현재 노드(1) + 왼쪽 서브트리 크기 + 오른쪽 서브트리 크기

**빈칸 채우기:**
- ① _______________

<details>
<summary>정답 보기</summary>

- ① `1 + size(node.getLeftChild()) + size(node.getRightChild())`

</details>

---

## 문제 30: BST의 remove 메서드 - 삭제 로직 (8week)

다음은 `BST` 클래스의 `remove` 메서드의 핵심 부분입니다. 삭제 대상 노드를 찾았을 때의 처리 로직을 완성하세요.

```java
// Found the node to remove
result = new NodeData(node, node.getData());

if (!node.hasLeftChild()) {
    // Case 2: No left child
    result.node = _________①_________;
} else if (!node.hasRightChild()) {
    // Case 3: No right child
    result.node = node.getLeftChild();
} else {
    // Case 4: Two children
    T temp = findMax(node.getLeftChild());
    node.setData(temp);
    node.setLeftChild(_________②_________.node);
}
```

**힌트:** 자식이 없거나 하나일 때는 자식 노드로 대체하고, 둘 다 있으면 왼쪽 서브트리의 최댓값으로 대체합니다.

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `node.getRightChild()`
- ② `remove(node.getLeftChild(), temp)`

</details>

---

## 문제 31: 피보나치 - Stack을 이용한 구현 (7week)

다음은 피보나치 수열을 스택으로 구현한 `usingStack` 메서드입니다. 빈칸을 채워 완성하세요.

```java
public long usingStack(int n) {
    ArrayDeque<Record> programStack = new ArrayDeque<>(100);
    programStack.push(new Record(n, 1, 1));
    long currentFibo = n;
    while(!programStack.isEmpty()) {
        Record topRecord = _________①_________;
        currentFibo = topRecord.n;
        long preFibo = topRecord.pre;
        long prePreFibo = topRecord.prePre;
        if(currentFibo < 3)
            currentFibo = preFibo + prePreFibo;
        else
            _________②_________;
    }
    return currentFibo;
}
```

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `programStack.pop()`
- ② `programStack.push(new Record(currentFibo - 1, preFibo + prePreFibo, preFibo))`

</details>

---

## 문제 32: 피보나치 - Memoization (7week)

다음은 피보나치 수열을 메모이제이션으로 구현한 코드입니다. 빈칸을 채워 완성하세요.

```java
public long memorize(int n) {
    if(n < num) return fibonacci[n];
    else if(n == num) {
        fibonacci[n] = _________①_________;
        num++;
        return fibonacci[n];
    }
    else return _________②_________;
}
```

**힌트:** 이미 계산된 값은 배열에서 가져오고, 새로운 값은 계산 후 저장합니다.

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `fibonacci[n-1] + fibonacci[n-2]`
- ② `memorize(n-1) + memorize(n-2)`

</details>

---

## 문제 33: ArrayList의 indexOf 메서드 (4week)

다음은 `MyArrayList` 클래스의 `indexOf` 메서드입니다. 특정 객체의 인덱스를 찾는 코드를 완성하세요.

```java
@Override
public int indexOf(Object o) {
    if (o == null) {
        for (int i = 0; i < size; i++) {
            if (_________①_________) {
                return i;
            }
        }
    } else {
        for (int i = 0; i < size; i++) {
            if (_________②_________) {
                return i;
            }
        }
    }
    return -1;
}
```

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `elements[i] == null`
- ② `o.equals(elements[i])`

</details>

---

## 문제 34: LinkedList의 linkBefore 메서드 (4week)

다음은 `MyLinkedList` 클래스의 `linkBefore` 메서드입니다. 특정 노드 앞에 새 노드를 삽입하는 코드를 완성하세요.

```java
void linkBefore(E e, Node<E> succ) {
    final Node<E> pred = _________①_________;
    final Node<E> newNode = new Node<>(pred, e, succ);
    succ.prev = newNode;
    if (pred == null) {
        first = newNode;
    } else {
        _________②_________;
    }
    size++;
}
```

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `succ.prev`
- ② `pred.next = newNode`

</details>

---

## 문제 35: ArrayQueue의 ensureCapacity (6week)

다음은 `ArrayQueue` 클래스의 `ensureCapacity` 메서드입니다. 큐가 가득 찼을 때 용량을 확장하는 코드를 완성하세요.

```java
private void ensureCapacity() {
    if(first == (last + 2) % queue.length) {
        T[] oldQ = queue;
        int newSize = _________①_________;
        integrityOK = false;
        if(newSize - 1 < MAX_CAPACITY) {
            @SuppressWarnings("unchecked")
            T[] tempQueue = (T[]) new Object[newSize];
            queue = tempQueue;
            for(int i = 0; i < oldQ.length - 1; i++) {
                queue[i] = oldQ[first];
                first = _________②_________;
            }
            first = 0;
            last = oldQ.length - 2;
            integrityOK = true;
        }
    }
}
```

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `2 * oldQ.length`
- ② `(first + 1) % oldQ.length`

</details>

---

## 문제 36: PriorityQueue를 이용한 최소 힙 생성 (kpop 폴더)

다음은 `DebutTracker_Heap` 클래스의 생성자입니다. 최소 힙(Min-Heap)을 생성하는 코드를 완성하세요.

```java
public DebutTracker_Heap(int k) {
    super(k);
    this.minHeap = new PriorityQueue<>(k,
        _________①_________
    );
}
```

**힌트:** Comparator.comparingInt()를 사용하여 totalVotes를 기준으로 오름차순 정렬합니다.

**빈칸 채우기:**
- ① _______________

<details>
<summary>정답 보기</summary>

- ① `Comparator.comparingInt(Trainee::totalVotes)`

</details>

---

## 문제 37: 람다를 이용한 이름 역순 정렬 (sort 폴더)

다음 코드는 Student 배열을 이름 역순(내림차순)으로 정렬합니다. 람다 표현식을 완성하세요.

```java
// 이름 내림차순 정렬 (Z -> A)
Arrays.sort(students, _________①_________);
```

**힌트:** s1과 s2의 이름을 비교하되, 순서를 반대로 합니다.

**빈칸 채우기:**
- ① _______________

<details>
<summary>정답 보기</summary>

- ① `(s1, s2) -> s2.getName().compareTo(s1.getName())`

</details>

---

## 문제 38: Comparator의 thenComparing 사용 (sort 폴더)

다음 코드는 점수 오름차순 → 이름 내림차순으로 정렬하는 Comparator입니다. 빈칸을 채우세요.

```java
Comparator<Student> comparator = Comparator
    .comparingInt(Student::getScore)
    ._________①_________;
```

**힌트:** thenComparing에 reversed()를 적용합니다.

**빈칸 채우기:**
- ① _______________

<details>
<summary>정답 보기</summary>

- ① `thenComparing(Comparator.comparing(Student::getName).reversed())`

</details>

---

## 문제 39: Collections.reverseOrder() 사용 (sort 폴더)

다음은 Integer 배열을 내림차순으로 정렬하는 코드입니다. 빈칸을 채우세요.

```java
Integer[] scoresBoxed = new Integer[scores.length];
for(int i = 0; i < scores.length; i++) {
    scoresBoxed[i] = scores[i];
}
Arrays.sort(scoresBoxed, _________①_________);
```

**빈칸 채우기:**
- ① _______________

<details>
<summary>정답 보기</summary>

- ① `Collections.reverseOrder()`

</details>

---

## 문제 40: DebutTracker_Heap의 힙 갱신 로직 (kpop 폴더)

다음은 `DebutTracker_Heap`에서 힙에 이미 있는 후보자의 득표수를 갱신하는 코드입니다. 빈칸을 채우세요.

```java
if (oldData != null) {
    // 이미 힙에 있는 후보자 갱신
    _________①_________;
    _________②_________;
}
```

**힌트:** 기존 데이터를 제거하고 새 데이터를 추가합니다.

**빈칸 채우기:**
- ① _______________
- ② _______________

<details>
<summary>정답 보기</summary>

- ① `minHeap.remove(oldData)`
- ② `minHeap.offer(update)`

</details>
