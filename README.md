# 신동훈 202630111

## 11월 26일
### 1. 재귀 호출(Recursion)의 개념과 동작 원리
재귀 호출이란 함수 내부에서 자기 자신을 다시 호출하는 프로그래밍 기법입니다. 큰 문제를 동일한 구조의 더 작은 하위 문제로 쪼개어 해결할 때 유용하게 사용됩니다.
- 기저 조건(Base Case): 재귀 호출이 무한히 반복되어 스택 오버플로우(Stack Overflow)가 발생하는 것을 막기 위한 종료 조건입니다.
- 재귀 단계(Recursive Step): 문제를 더 작은 단위로 줄여가며 자기 자신을 다시 호출하는 구간입니다.
- 호출 스택(Call Stack)의 흐름: 함수가 호출될 때마다 메모리 스택에 실행 정보가 쌓이며, 기저 조건에 도달해 값을 반환하기 시작하면 가장 마지막에 호출된 함수부터 역순으로 빠져나오며 나머지 코드를 실행합니다.

#### 재귀 호출의 진입과 복귀 흐름 확인 (callback)
재귀 호출 코드의 앞과 뒤에 출력문을 배치하면, 기저 조건(num == 0)에 도달할 때까지 함수가 안쪽으로 깊어지는 과정과 반환 후 바깥쪽으로 빠져나오는 과정을 직관적으로 확인할 수 있습니다.
```py
def callback(num):
    num -= 1
    if num == 0:
        print("Count reached zero. Stopping execution.")
        return
    print("Callback function executed. count", num) # 재귀 진입 시 실행
    callback(num)
    print("Callback function executed. count", num) # 재귀 복귀 시 실행

callback(3)
```

### 2. 수학적 연산의 재귀 구현
#### 1) 1부터 N까지의 합 구하기 (add_numbers)
end에서 시작하여 1씩 감소시키며 자기 자신을 호출하고, 기저 조건(end <= start)에 도달하면 1을 반환하며 역순으로 누적 합계를 계산합니다.
```py
def add_numbers(start, end):
    if end <= start:
        return 1
    return end + add_numbers(start, end - 1)

print(add_numbers(1, 10)) # 출력: 55
```

#### 2) 팩토리얼(Factorial) 계산 (factorial)
n이 1 이하가 될 때까지 재귀적으로 내려갔다가, 반환된 값(foo)에 현재의 n을 곱해 올라오며 $5! = 120$을 계산합니다.
```py
def factorial(n):
    if n <= 1:
        print("n:", n)
        return 1
    print("n:", n)
    foo = factorial(n - 1)
    print("n:", n)
    return n * foo

print(factorial(5)) # 출력: 120
```

#### 3) 거듭제곱 계산 (power)
모든 수의 0제곱은 1이므로 exponent == 0일 때 1을 반환합니다.
```py
def power(base, exponent):
    if exponent == 0:
        return 1
    return base * power(base, exponent - 1)

print(power(2, 4)) # 출력: 16
```

### 3. 반복 구조와 패턴 출력의 재귀 및 반복문 구현
#### 1) 카운트다운 (countdown)
n부터 1까지 숫자를 출력한 뒤 0 이하가 되면 "발사!!!"를 출력합니다. for 반복문과 재귀 호출이 서로 동일한 로직으로 변환될 수 있음을 보여줍니다.

```py
# 재귀 호출 방식
def countdown(n):
    if n <= 0:
        print("발사!!!")
        return
    print(n)
    countdown(n - 1)

# 반복문 방식 비교
# def countdown(n):
#     for i in range(n, 0, -1):
#         print(i)
#     print("발사!!!")

countdown(5)
```

#### 2) 별 찍기 (print_starts)
재귀 호출(print_starts(n - 1))을 출력문(print("*" * n))보다 먼저 배치하여, n=1인 기저 조건에 도달한 뒤 복귀하는 과정에서 별이 1개부터 5개까지 오름차순으로 출력되도록 구현했습니다.
```py
def print_starts(n):
    if n <= 0:
        return
    print_starts(n - 1) # 먼저 가장 작은 단계(1)까지 들어간 후
    print("*" * n)      # 복귀하면서 1개부터 n개까지 순서대로 출력

print_starts(5)
```

#### 3) 2중 반복문을 이용한 구구단 출력 (multiplication_table)
바깥쪽 for 문으로 단(1~9)을 제어하고, 안쪽 for 문으로 곱하는 수(1~9)를 제어하여 전체 구구단을 출력합니다. 포맷 문자열({i * j:2})을 사용해 결과값이 한 자리 수일 때도 두 칸 폭으로 정렬되도록 처리했습니다.
```py
def multiplication_table():
    for i in range(1, 10):
        for j in range(1, 10):
            print(f"{i} x {j} = {i * j:2}")
        print()

multiplication_table()
```

### 4. 배열(리스트) 요소의 합계 구하기 (arr_sum)
배열 arr과 원소 개수 n을 전달받아 뒤쪽 원소(arr[n - 1])부터 하나씩 더해가며 전체 배열의 합을 구하는 재귀 함수입니다. n이 0 이하가 되면 더 이상 더할 원소가 없으므로 0을 반환합니다.
```py
def arr_sum(arr, n):
    if n <= 0:
        return 0
    return arr[n - 1] + arr_sum(arr, n - 1)

arr = [1, 2, 3, 4, 5]
print(arr_sum(arr, 5)) # 출력: 15
```

## 11월 19일
### 1. 그래프(Graph) 자료구조와 인접 행렬(Adjacency Matrix) 구현
그래프는 정점(Vertex)과 간선(Edge)으로 이루어진 비선형 자료구조입니다. 이번 실습에서는 정점 간의 연결 관계를 2차원 배열(size × size)로 표현하는 인접 행렬 방식을 사용하여 그래프를 구현했습니다.

#### 1. 그래프 클래스 정의 (graph) 및 출력 함수 (print_graph)
정점의 개수(size)를 입력받아 모든 요소가 0으로 초기화된 2차원 리스트를 생성하는 graph 클래스를 정의합니다. print_graph 함수는 이중 반복문을 통해 2차원 배열 형태의 인접 행렬을 행과 열에 맞춰 출력합니다.
```py
# 클래스 선언부
class graph:
    def __init__(self, size):
        self.SIZE = size
        self.graph = [[0 for _ in range(size)] for _ in range(size)]

def print_graph(graph):
    print("===" + " 그래프 출력 " + "===")
    for row in range(graph.SIZE):
        for col in range(graph.SIZE):
            print(graph.graph[row][col], end=' ')
        print()
```

#### 2. 무방향 그래프(G1) 구성
정점 4개(0, 1, 2, 3)를 가진 무방향 그래프 G1을 생성하고, 간선으로 연결된 정점 쌍의 행렬 값을 1로 설정합니다. 무방향 그래프는 방향성이 없으므로 (0, 1)과 (1, 0)처럼 대칭되는 위치에 모두 1을 저장합니다.
```py
G1 = graph(4)
G1.graph[0][1] = 1
G1.graph[0][2] = 1
G1.graph[0][3] = 1
G1.graph[1][0] = 1
G1.graph[1][2] = 1
G1.graph[2][0] = 1
G1.graph[2][1] = 1
G1.graph[2][3] = 1
G1.graph[3][0] = 1
G1.graph[3][2] = 1

print_graph(G1)
```

#### 3. 방향 그래프(G3) 구성 및 출력
정점 4개를 가진 그래프 G3을 생성하고, 특정 출발 정점에서 도착 정점으로 향하는 단방향 간선(0→1, 0→2, 3→0, 3→2)만 1로 설정하여 인접 행렬을 직접 순회하며 출력합니다.
```py
G3 = graph(4)
G3.graph[0][1] = 1
G3.graph[0][2] = 1
G3.graph[3][0] = 1
G3.graph[3][2] = 1

print('=== G3 무방향 그래프 ===')
for row in range(G3.SIZE):
    for col in range(G3.SIZE):
        print(G3.graph[row][col], end=' ')
    print()
```

## 11월 12일
### 1. 이진 트리(Binary Tree) 자료구조의 구현
이진 트리는 각 노드가 최대 두 개의 자식 노드(왼쪽 자식, 오른쪽 자식)를 가질 수 있는 계층형 비선형 자료구조입니다. 이번 실습에서는 노드의 데이터와 좌우 링크를 포함하는 클래스를 정의하고, 각 노드를 수동으로 연결하여 트리 구조를 구성했습니다.

#### 1. 트리 노드 클래스 정의 (tree_node)
실제 값을 저장하는 data와 왼쪽 자식 노드를 가리키는 left, 오른쪽 자식 노드를 가리키는 right 링크로 구성된 tree_node 클래스를 정의합니다.
```py
class tree_node:
    def __init__(self):
        self.data = None
        self.left = None
        self.right = None
```

#### 2. 노드 생성 및 계층 구조 연결
루트 노드(node1)부터 시작하여 각 노드의 left와 right 속성에 자식 노드를 할당함으로써 계층적인 트리 구조를 만듭니다.
```
        커피 (node1)
        /          \
   우유 (node2)    주스 (node3)
    /       \         /
물 (node4) 콜라 (node5) 사이다 (node6)
```
```py
node1 = tree_node()
node1.data = "커피"

node2 = tree_node()
node2.data = "우유"
node1.left = node2   # 커피의 왼쪽 자식 -> 우유

node3 = tree_node()
node3.data = "주스"
node1.right = node3  # 커피의 오른쪽 자식 -> 주스

node4 = tree_node()
node4.data = "물"
node2.left = node4   # 우유의 왼쪽 자식 -> 물

node5 = tree_node()
node5.data = "콜라"
node2.right = node5  # 우유의 오른쪽 자식 -> 콜라

node6 = tree_node()
node6.data = "사이다"
node3.left = node6   # 주스의 왼쪽 자식 -> 사이다
```

#### 3. 이진 트리 레벨별 출력
루트 노드(node1)에서 시작하여 .left와 .right 참조를 연속으로 따라가며 트리의 각 깊이(레벨)에 위치한 노드들의 데이터를 순서대로 출력합니다.
```py
print("=== 이진 트리 구조 ===")
print(node1.data, end="")
print()
print(node1.left.data, node1.right.data, end="")
print()
print(node1.left.left.data, node1.left.right.data, node1.right.left.data)
```

## 11월 5일
### 1. 큐(Queue) 자료구조의 구현 및 활용
큐(Queue)는 먼저 들어간 데이터가 먼저 나오는 선입선출(FIFO, First In First Out) 방식의 자료구조입니다. 파이썬의 리스트(print_q)와 데이터의 앞/뒤 인덱스를 추적하는 전역 변수(front, rear)를 활용하여 큐의 주요 연산을 구현했습니다.

#### 1. 큐 초기화 (init_queue) 및 상태 출력 (print_queue)
지정한 크기(size)만큼 비어있는(None) 리스트를 생성하고, 데이터의 맨 앞쪽을 가리키는 front와 맨 뒤쪽을 가리키는 rear를 모두 -1로 초기화합니다. print_queue 함수는 리스트의 처음부터 끝까지 순회하며 전체 큐의 상태와 현재 front, rear의 위치를 출력합니다
```py
def init_queue(size):
    global print_q, front, rear
    print_q = [None] * size
    front = -1
    rear = -1
    return print("큐 초기화 완료! 큐의 크기: " + str(size))

def print_queue():
    print("=== 큐 상태 ===")
    print("큐의 크기: " + str(len(print_q)))
    for i in range(len(print_q)):
        print(print_q[i])
    print("현재 front: " + str(front))
    print("현재 rear: " + str(rear))
    print("=================")
```

#### 2. 큐 꽉 참/비어있음 확인 (is_queue_full, is_queue_empty)
데이터를 삽입하거나 추출하기 전에 큐의 상태를 확인하는 함수입니다.
- `Full`: 마지막 데이터가 들어간 위치(rear)가 리스트의 맨 끝 인덱스(len(print_q) - 1)에 도달하면 꽉 찬 상태로 판단합니다.
- `Empty`: 데이터를 추출한 위치(front)와 마지막 데이터가 들어간 위치(rear)가 같아지면 큐가 비어있는 것으로 판단합니다.
```py
def is_queue_empty():
    global front, rear
    if front == rear:
        return True
    else:
        return False

def is_queue_full():
    global rear
    if rear == len(print_q) - 1:
        return True
    else:
        return False
```

#### 3. 큐 데이터 삽입(enqueue), 추출(dequeue), 확인(peek)
- `Enqueue`: 큐가 꽉 차지 않았다면 rear를 1 증가시키고, 해당 위치에 새로운 데이터를 삽입합니다.
- `Dequeue`: 큐가 비어있지 않다면 front를 1 증가시키고 해당 위치의 데이터를 임시 변수(temp)에 담은 뒤, 원래 자리를 None으로 비우고 데이터를 반환합니다.
- `Peek`: 큐에서 데이터를 빼내지 않고, 다음에 나올 데이터(front + 1 위치의 데이터)를 확인만 합니다.
```py
def enqueue(data):
    global rear
    if is_queue_full():
        return print("큐가 가득 찼습니다!")
    else:
        rear += 1
        print_q[rear] = data
        return print("현재 rear: " + str(rear))

def dequeue():
    global front, temp
    if is_queue_empty():
        return print("큐가 비어있습니다! 삭제할 데이터가 없습니다.")
    front += 1
    temp = print_q[front]
    print_q[front] = None
    return temp

def peek():
    global front
    if is_queue_empty():
        return print("큐가 비어있습니다! Peek 불가!")
    else:
        temp = print_q[front + 1]
        return temp
```

#### 4. 큐 동작 테스트
작성한 함수를 바탕으로 크기가 5인 큐를 초기화한 후 데이터를 삽입하고 확인하는 테스트 코드입니다. 5개의 요소를 모두 삽입하여 큐를 가득 채운 후, peek() 함수를 통해 가장 앞에 있는(다음에 추출될) 데이터를 확인합니다.
```py
init_queue(5)
enqueue("커피")
enqueue("우유")
enqueue("주스")
enqueue("물")
enqueue("콜라")

print("======peek() 함수 호출 전======")
print(peek()) # 큐의 가장 맨 앞(front+1)에 있는 데이터 확인
print("======peek() 함수 호출 후======")

print_queue()
```

## 10월 29일
### 1. 파이썬 웹 브라우저 제어 (webbrowser 모듈)
파이썬의 내장 모듈인 webbrowser를 활용하여 기본 웹 브라우저를 열고 특정 URL로 접속하는 간단한 실습입니다.
```py
import webbrowser

webbrowser.open("https://naver.com")
```

### 2. 스택(Stack) 자료구조의 구현 및 활용
스택은 나중에 들어간 데이터가 먼저 나오는 후입선출(LIFO, Last In First Out) 구조의 자료구조입니다. 파이썬의 리스트와 전역 변수(top)를 활용하여 스택의 주요 기능들을 함수로 구현했습니다.

#### 1. 스택 초기화 (init_stack) 및 상태 출력 (print_stack)
지정한 크기(size)만큼 비어있는(None) 리스트를 생성하고, 스택의 현재 위치를 나타내는 top 변수를 -1로 초기화합니다. 스택 상태 출력 함수는 리스트의 마지막 인덱스부터 역순으로 데이터를 차례대로 출력하여 실제 데이터가 쌓여있는 구조를 직관적으로 보여줍니다.
```py
def init_stack(size):
    global stack, top
    stack = [None] * size
    top = -1
    return print("스택 초기화 완료! 스택의 크기: " + str(size))

def print_stack():
    print("=== 스택 상태 ===")
    # range(start, end, step) : start부터 end까지 step만큼 감소하며 역순 출력
    for i in range(len(stack) -1, -1, -1):
        print(stack[i])
    print("=================")
```

#### 2. 스택 꽉 참/비어있음 확인 (is_stack_full, is_stack_empty)
데이터를 넣거나 빼기 전에 스택의 상태를 검사하는 함수입니다. top 인덱스가 리스트의 마지막 인덱스(len(stack) - 1)와 같으면 꽉 찬 상태(Full)로, -1이면 완전히 비어있는 상태(Empty)로 판단하여 참(True)을 반환합니다.
```py
def is_stack_full():
    global top
    if top == len(stack) - 1:
        return True
    else:
        return False

def is_stack_empty():
    global top
    if top == -1:
        return True
    else:
        return False
```

#### 3. 스택 데이터 삽입(push), 추출(pop), 확인(peek)
`Push`: 스택이 꽉 차지 않았다면 top을 1 증가시키고 해당 위치에 새로운 데이터를 저장합니다.

`Pop`: 스택이 비어있지 않다면 현재 top 위치의 데이터를 꺼내어 출력하고, 해당 자리를 비운(None) 뒤 top을 1 감소시킵니다.

`Peek`: 스택 최상단(top)에 있는 데이터를 삭제하지 않고 읽기만 하여 어떤 값이 들어있는지 확인합니다.
```py
def push(data):
    global top
    if is_stack_full():
        return print("스택이 가득 찼습니다!")
    else:
        top += 1
        stack[top] = data
        return print("현재 top: " + str(top))

def pop():
    global top
    if is_stack_empty():
        return print("스택이 비어있습니다! 삭제할 데이터가 없습니다.")
    else:
        data = stack[top]
        stack[top] = None
        top -= 1
        return print("Pop된 데이터: " + str(data) + ", 현재 top: ", top)

def peek():
    global top
    if is_stack_empty():
        return print("스택이 비어있습니다! Peek 불가!")
    else:
        data = stack[top]
        return print("Peek 데이터: " + str(data) + ", 현재 top", top)
```

#### 4. 스택 동작 테스트
작성한 함수들을 바탕으로 스택을 생성하고 데이터를 넣고 빼는 전체 테스트 과정입니다. 스택의 크기인 7을 초과하여 데이터를 push하거나, 비어있는 스택에서 pop 또는 peek을 시도할 때 조건문에 의해 안전하게 방어되는 것을 확인할 수 있습니다.
```py
# 크기가 7인 스택 초기화
init_stack(7)
print_stack()

# Push 연산 수행
push("커피")
push("녹차")
push("꿀물")
push("레몬차")
push("오렌지주스")
push("밀크티")
push("아이스티")

push("콜라") # 스택이 가득 찼습니다! (크기 7 초과 방어)

print_stack()

peek() # 최상단 데이터 확인 (아이스티)

# Pop 연산 수행
pop()
pop()
pop()
pop()
pop()
pop()
pop()

pop() # 스택이 비어있습니다! 삭제할 데이터가 없습니다.

peek() # 스택이 비어있습니다! Peek 불가

print_stack()
```

## 10월 15일(6주차)
### 1. 원형 연결 리스트의 기본 개념
원형 연결 리스트는 마지막 노드가 다시 첫 번째 노드를 가리키는(회전하는) 구조의 자료구조입니다.

#### 단순 연결 리스트와 비교
| 구분 | 단순 연결 리스트 | 원형 연결 리스트 |
|---|---|---|
| 마지막 노드 | `None`을 가리킴 | 첫 번째 노드를 가리킴 |
| 구조 | 일직선 | 원형 |
| 순회 | 마지막에서 종료 | 반복 순회 가능 |
| 종료 조건 | `current is None` | `current == head` |

> **구조 다이어그램**
> ```text
>          ┌─────────────────────────────┐
>          ↓                             │
> 다현 → 정연 → 쯔위 → 사나 → 지효 ──────┘
> ```

### 2. 기본 클래스 구조 (Node)
원형 연결 리스트에서도 단순 연결 리스트와 동일한 `Node` 클래스를 사용합니다.
```py
class Node:
    def __init__(self):
        self.data = None
        self.link = None
```
- `self.data`: 노드에 저장되는 데이터
- `self.link`: 다음 노드를 가리키는 참조값

### 3. 핵심 연산 및 코드 패턴
#### 1. 노드 하나로 원형 리스트 만들기
노드가 하나만 있어도 자기 자신을 가리키게 하여 원형 구조를 유지합니다.
```py
node1.link = node1
```

#### 2. 첫 번째 노드 지정 (초기화)
```py
head = node
node.link = head
```

#### 3. 두 번째 이후 노드 추가
```py
pre = node
node = Node()
node.data = data
pre.link = node
node.link = head
```

#### 4. 중간 노드 삽입 (정연 뒤에 재남 삽입)
반드시 새로운 노드의 링크를 먼저 연결한 뒤, 이전 노드의 링크를 변경해야 참조를 잃지 않습니다.
```py
newNode.link = pre.link
pre.link = newNode
```

#### 5. 중간 노드 삭제 (쯔위 삭제)
```py
pre.link = current.link
del(current)
```

#### 6. 순회 및 종료 조건
원형 연결 리스트는 None이 없으므로, 시작 노드로 다시 돌아왔는지 확인하는 조건이 필수입니다.
```py
current = head
while True:
    print(current.data, end=" ")
    current = current.link
    
    if current == head:
        break
```



## 10월 8일(5주차)
### 1. 단순 연결 리스트의 출력 및 노드 삽입 함수 구현
이번 주차에서는 연결 리스트를 처음부터 끝까지 순회하며 출력하는 기능과, 원하는 데이터를 찾아 그 앞에 새로운 노드를 삽입하는 기능을 함수로 모듈화하여 구현했습니다.

#### 1) 노드 출력 함수 (printNodes)
시작 노드(start)를 매개변수로 받아, 링크(link)를 따라가며 리스트의 끝(None)에 도달할 때까지 모든 노드의 데이터를 출력하는 함수입니다.
```py
def printNodes(start):
    current = start
    if current == None:
        return
    print(current.data, end = ' ')
    
    while current.link != None:
        current = current.link
        print(current.data, end = ' ')
    print()
```
#### 2) 노드 삽입 함수 (insertNode)
찾고자 하는 데이터(findData) 앞 위치에 새로운 데이터(insertData)를 삽입하는 함수입니다. 삽입 위치에 따라 크게 세 가지 상황으로 나누어 처리합니다.
```py
def insertNode(findData, insertData):
    global memory, head, current, pre
    current = head
    
    # 1. 첫 번째 노드 앞에 삽입
    if current.data == findData:
        node = Node()
        node.data = insertData
        node.link = head
        head = node
        return

    # 2. 중간 노드 삽입
    current = head
    while current.link != None:
        pre = current
        current = current.link
        if current.data == findData:
            node = Node()
            node.data = insertData
            node.link = current
            pre.link = node
            return

    # 3. 마지막 노드 삽입 (찾는 데이터가 없는 경우)
    node = Node()
    node.data = insertData
    current.link = node
```
#### 3) 배열 기반 초기화 및 함수 활용 실습
초기 데이터가 담긴 배열(dataArray)을 반복문으로 순회하며 기본 연결 리스트를 구성하고, insertNode 함수를 활용해 다양한 위치에 데이터를 삽입해 보는 테스트 코드입니다.
```py
# 전역 변수 선언
memory = []
head, current, pre = None, None, None
dataArray = ['다현', '정연', '쯔위', '사나', '지효']

if __name__ == "__main__":
    # 첫 번째 노드 생성
    node = Node()
    node.data = dataArray[0]
    head = node
    memory.append(node)

    # 나머지 노드 생성 및 연결
    for data in dataArray[1:]:
        pre = node
        node = Node()
        node.data = data
        pre.link = node
        memory.append(node)

    printNodes(head) # 초기 리스트 출력

    insertNode("다현", "화사") # 맨 앞 위치(다현 앞)에 '화사' 삽입
    printNodes(head)
    
    insertNode("사나", "솔라") # 중간 위치(사나 앞)에 '솔라' 삽입
    printNodes(head)
    
    insertNode("재남", "문별") # 찾는 데이터가 없으므로 맨 끝에 '문별' 삽입
    printNodes(head)
```

## 10월 1일(4주차)
### 1. 배열을 이용한 선형 리스트 생성 및 출력
배열(리스트)을 먼저 생성하고 append() 함수를 사용하여 데이터를 리스트의 맨 뒤에 순차적으로 추가하는 방법입니다.

```py
kakao = []
kakao_len = len(kakao)
kakao.append("다현")
kakao.append("정연")
kakao.append("쯔위")
kakao.append("사나")
kakao.append("지효")

for i in range(len(kakao)):
    print(kakao[i], end=', ')
```

### 2. 단순 연결 리스트 (Simple Linked List)
단순 연결 리스트는 실제 데이터를 저장하는 공간과 다음 데이터를 가리키는 링크(Link)로 구성된 노드(Node)들의 연결로 이루어진 자료구조입니다.

#### 1) Node 클래스 정의 및 노드 연결
실제 데이터를 저장하는 data와 다음 노드를 가리키는 link를 가진 클래스를 생성합니다. 앞노드.link = 다음노드 형태로 노드들을 연결해 줍니다.

```py
class Node:
    def __init__(self):
        self.data = None
        self.link = None

# 노드 생성 및 연결
node1 = Node()
node1.data = "다현"

node2 = Node()
node2.data = "정연"
node1.link = node2  # node1과 node2 연결

node3 = Node()
node3.data = "쯔위"
node2.link = node3  # node2와 node3 연결

node4 = Node()
node4.data = "사나"
node3.link = node4  # node3과 node4 연결

node5 = Node()
node5.data = "지효"
node4.link = node5  # node4와 node5 연결
```

#### 2) 연결 리스트 전체 출력
첫 번째 노드(node1)부터 시작하여 링크(link)가 None이 아닐 때까지 반복문을 통해 다음 노드로 이동하며 데이터를 출력합니다.
```py
print("\n\n연결리스트 출력")
current = node1
print(current.data, end=', ')
while current.link is not None: # is not None > != None
    current = current.link
    print(current.data, end=', ')
```

#### 3) 노드 삽입 (중간 삽입)
정연 노드(node2)와 쯔위 노드(node3) 사이에 '재남' 노드를 새로 삽입하는 과정입니다. 기존 데이터의 이동 없이 새 노드가 쯔위를 가리키게 하고, 정연이 새 노드를 가리키게 링크만 수정합니다.
```py
new_node = Node()
new_node.data = "재남"

new_node.link = node3 # 새 노드가 쯔위 노드를 가리킴
node2.link = new_node # 정연 노드가 새 노드를 가리킴
```

#### 4) 노드 삭제 (중간 삭제)
삽입했던 '재남' 노드를 삭제하는 과정입니다. 정연 노드(node2)의 링크가 삭제할 노드를 건너뛰고 쯔위 노드(node3)를 바로 가리키게 변경한 뒤, del()을 이용해 노드를 삭제합니다.
```py
node2.link = node3 # 정연 노드가 쯔위 노드를 바로 가리킴
del(new_node)
```

## 9월17일(3주차)
### 파이썬 기본 출력과 리스트 인덱싱·임시 변수를 활용한 데이터 삽입 및 요소 스왑 실습

### 파이썬 기본 출력
```py
print("Hello, World")
```

### 리스트 요소의 이동과 데이터 삽입
```py
kakao = ["가나", "다라", "마바", "사아", "자차"]
print(kakao)
kakao.append(None)
print(kakao)
kakao[5] = kakao[4]
kakao[4] = None
print(kakao)
kakao[4] = kakao[3]
kakao[3] = None
print(kakao)
kakao[3] = "쌈밥"
print(kakao)
kakao[3] = None
print(kakao)
kakao[3] = kakao[4]
kakao[4] = None
print(kakao)
kakao[4] = kakao[5]
kakao[5] = None
print(kakao)
```

### 임시 변수(temp)를 활용한 리스트 요소 스왑
```py
kakao = ["가나", "다라", "마바", "사아", "자차"]
temp = kakao[4]
print(kakao)
kakao.append("쌈밥")
print(kakao)
kakao[4] = kakao[5]
kakao[5] = temp
temp = kakao[3]
print(kakao)
kakao[3] = kakao[4]
kakao[4] = temp
print(kakao)
```

## 9월10일(2주차)
### 마크다운 문법
# h1 태그
## h2 태그
### h3 태그
...
###### h6 태그

*이텔릭체*

**볼드체**

***이텔릭+볼드***

~~취소선~~

밑줄
---

1. 감자
2. 옥수수
3. 배추

* 감자
* 옥수수
* 배추
    * 배추 김치
        * 신김치

### 코드 블럭
```java
public class HelloWorld {
    public static void main(String[] args) {
        // 화면에 문장을 출력합니다
        System.out.println("Hello, Java!");
        
        int age = 20;
        String name = "홍길동";
        
        System.out.println(name + "의 나이는 " + age + "살입니다.");
    }
}

```

```py
score = 85

if score >= 80:
    print("A등급입니다.")
else:
    print("B등급 이하입니다.")
```

복사는 `Ctrl + C` 입니다.

### 링크

[구글 바로가기](https://google.com "구글 사이트")

[코드 블럭](#코드-블럭 "코드블럭 예제")

![깃 로고](./image.png "git logo")
