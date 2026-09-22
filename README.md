# 신동훈 202630111

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