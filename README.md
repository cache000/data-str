# 신동훈 202630111

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