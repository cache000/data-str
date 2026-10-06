# 신동훈 202630111

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