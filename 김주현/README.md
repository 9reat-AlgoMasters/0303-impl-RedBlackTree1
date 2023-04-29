# Redblack Tree
- 이진 탐색 트리(BST)의 한 종류
- self-balancing tree
    - 편향된 트리가 나오지 않는다.
    - 편향된 트리가 나올 시 조회할 때 O(N) 의 시간복잡도

# RedBlack Tree의 속성
## 1. 모든 노드는 red 또는 black

## 2. 루트노드는 black

## 3. 모든 nil(leaf) 노드는 black

## 4. red의 자녀들을 black
- red가 연속적으로 존재할 수 없다.

## 5. 임의의 노드에서 자손 nil 노드들까지 가는 경로들의 black 수는 같다.
- 자기 자신은 카운트에서 제외


# RedBlckTree 만의 특징
## nil 노드
- 존재하지 않음을 의미하는 노드
- 자녀가 없을 때 자녀를 nil 노드로 표기
- 값이 있는 노드와 동등하게 취급
- RB 트리에서 leaf 노드는 nil 노드

## 노드 X의 black height
- 노드 x에서 임의의 자손 nil 노드까지 내려가는 경로에서의 black 수
- 자기 자신 카운트에서 제외
- 5번 속성을 만족해야 성립하는 개념

## 색을 바꾸면서도 #5 속성 유지하기
- RB 트리가 5번 속성을 만족하고 있고 두 자녀가 같은 색을 가질 때 부모와 두 자녀의 색을 바꿔줘도 5번 속성은 여전히 만족한다.

## 회전시 5번 속성 만족하려면
- 색을 바꿔주며 회전한다. -> 원래 루트 색을 유지하도록

# RedBlack Tree 삽입
## 순서
0. 삽입 전 RB 트리 속성 만족한 상태
1. 삽입 방식은 일반적인 BST와 동일
2. 삽입 후 RB 트리 위반 여부 확인
3. RB 트리 속성을 위반했다면 재조정
4. RB 트리 속성을 다시 만족

## 삽입 노드의 색
- 삽입하는 노드는 항상 red 이다.
    - #5 속성을 만족하기 위해
    - 즉 삽입하기 전과 후에 nil 노드 까지 내려가는데 거치는 black 노드 수는 같다.

## Insert Case Study
### case1: 맨 처음 루트 노드 삽입시
- 루트 노드를 black 으로 바꾸어준다. (#2 루트 노드는 black 속성 만족)

### case2: 레드 두개가 연속으로 붙어있을 때
- 레드 중 부모가 검은 색인 레드의 색을 검은색으로 바꿔주고 그 부모는 레드로 바꾼다.
- 회전한다.
- example
    - 루트 노드 일경우
        |Before|After1|After2|After3|
        |---|---|---|---|
        |![case1-1](https://user-images.githubusercontent.com/95271588/234247532-88e97397-bdec-4a01-9dab-9c1840b9476a.png)|![case1-1-2](https://user-images.githubusercontent.com/95271588/234248474-54f2a0e7-6808-4435-8354-576e1bb8db05.png)|![case1-1-3](https://user-images.githubusercontent.com/95271588/234248972-9fc0ff7e-ed0a-406e-94ff-a8946588e0b7.png)|![case1-1-4](https://user-images.githubusercontent.com/95271588/234248982-dc4471ef-350f-4a8a-a088-3c707b7ef726.png)
        ||5 추가|오른쪽 회전|색 교환|

    - 루트노드가 아닐 경우

        |Before|After1|After2|After3|
        |---|---|---|---|
        |![case1-2-1](https://user-images.githubusercontent.com/95271588/234259322-f0d08f85-f280-427f-bf2a-eb1e4ea7ec50.png)|![case1-2-2](https://user-images.githubusercontent.com/95271588/234259337-f236769a-a401-4193-80b2-6cf8c6160bf5.png)|![case1-2-3](https://user-images.githubusercontent.com/95271588/234259351-c9e471cb-2fa1-437c-a8d8-03f789ec9e3c.png)|![case1-2-4](https://user-images.githubusercontent.com/95271588/234259373-1649a3e2-fa0e-4459-b49e-9440e798a1ca.png)
        ||70 추가|왼쪽 회전|색 교환|

### case3: case2에서 경로가 꺾인 상태
- 회전 2번
- example
    - 루트 노드 일경우
        |Before|After1|After2|After3|
        |---|---|---|---|
        |![case2-1-1](https://user-images.githubusercontent.com/95271588/234260214-4c9f301f-13de-4a7c-8412-b3065d469338.png)|![case2-1-2](https://user-images.githubusercontent.com/95271588/234260221-8064ab29-c479-461f-bd53-4218ae267a36.png)|![case2-1-3](https://user-images.githubusercontent.com/95271588/234260225-95e99359-9a3f-4038-b150-4d3f17c28fdb.png)|![case2-1-4](https://user-images.githubusercontent.com/95271588/234260229-4433cd1c-b9f9-4fc8-a2bd-5693b751f7d0.png)
        ||40 추가|50에서 오른쪽 회전|30에서 왼쪽 회전 및 색교환 (case2)|
    
    - 루트 노드가 아닐 경우
        - 루트 노드 일때와의 차이가 case2 와 비슷하다.

### case4: 레드가 한쪽으로 몰려있지 않을 때, 레드가 붙는 경우
- 색을 바꿔준다
- 할아버지에서 다시 확인을 시작
- example
    - 루트 노드 일 경우
        |Before|After1|After2|After3|
        |---|---|---|---|
        |![case3-1-1](https://user-images.githubusercontent.com/95271588/234261780-4048a9b8-82db-4aaf-9703-8074869ef5f7.png)|![case3-1-2](https://user-images.githubusercontent.com/95271588/234261789-5770fa93-5bef-496c-aefe-66a20a3349cf.png)|![case3-1-3](https://user-images.githubusercontent.com/95271588/234261793-ca07a256-e185-48f7-a1e6-1c9129c51c67.png)|![case3-1-4](https://user-images.githubusercontent.com/95271588/234261803-dcdbf5f2-61e8-4e2b-9260-7c6dbb55925a.png)
        ||45 추가|추가한 노드 기준 할아버지 노드와 그 자식 노드의 색을 바꿔준다.|루트 노드의 색을 검은색으로 바꾼다.|
    
    - 루트 노드가 아닐 경우

        |Before|After1|After2|After3|After4|
        |---|---|---|---|---|
        |![case3-2-1](https://user-images.githubusercontent.com/95271588/234263414-434cd96a-393b-41c0-83a7-11c887406091.png)|![case3-2-2](https://user-images.githubusercontent.com/95271588/234263433-a5750953-626f-431c-8cda-57616247b25f.png)|![case3-2-3](https://user-images.githubusercontent.com/95271588/234263443-09164aa1-e4ca-412a-b572-f329ccd431d3.png)|![case3-2-4](https://user-images.githubusercontent.com/95271588/234263455-99898b75-f765-4ff2-b6a0-0c02f05a61c6.png)|![case3-2-5](https://user-images.githubusercontent.com/95271588/234263496-56c8279f-5bcb-453d-89af-e8ef11ae14a6.png)
        ||46 추가|추가한 노드 기준 할아버지 노드와 그 자식 노드의 색을 바꿔준다.|45와 그 부모 노드가 연속된 red -> case3 처리 -> 50 기준 오른쪽 회전| 40기준 왼쪽 회전 및 색 교환

# Delete
## 주목할 점
- 삭제된 색이 Red 일 경우 일반 BST와 같다.
    - 어떤 조건도 위반하지 않기 때문

- 삭제된 색이 black일 경우 black height를 유지하기 위해 doubly black이 생긴다.
    - doubly black을 해결해주기 위해 4가지 케이스로 나누어서 처리한다.

- 루트 노드가 doubly black --> 그냥 black으로 바꿔도 됨
    - 루트 노드의 doubly black은 모든 트리에 적용되는 것이기 때문에 하나 그냥 빼도 상관 없음

## Case Study
### Case1
- Case1의 조건
    - doubly black의 형제가 black
    - doubly black의 형제의 먼 쪽 자식이 red 일 경우
        - ex) 만약 doubly black이 왼쪽 자식일 경우 형제의 오른쪽 자식이 red

- example
    - full 과정
        |Before|After1|After2|
        |---|---|---|
        |![case1-1-1](https://user-images.githubusercontent.com/95271588/234269082-9522eb48-3928-4d7c-bcee-30c54a29804c.png)|![case1-1-2](https://user-images.githubusercontent.com/95271588/234269092-00eae841-6be3-4020-8381-4a3954151504.png)|![case1-1-3](https://user-images.githubusercontent.com/95271588/234269098-a44f0426-2c50-4178-8216-8aa90dac9970.png)|
        ||1 삭제|3의 black을 자식들로 보내준다. (이때 왼쪽 오른쪽 자식 모두에게 보내야 RB tree 속성을 만족한다.)|

        |After3|After4|After5|
        |---|---|---|
        |![case1-1-4](https://user-images.githubusercontent.com/95271588/234269107-f3552256-b696-4971-9296-0dff60402138.png)|![case1-1-5](https://user-images.githubusercontent.com/95271588/234269116-d7a2b7d3-2c49-4cdf-a00b-3c9ddacd5030.png)|![case1-1-6](https://user-images.githubusercontent.com/95271588/234269130-356de752-8d6d-4e8c-80f5-bee80285109f.png)|
        |2 기준 왼쪽 회전 및 색 교환|2의 자식의 모든 doubly black을 2가 받는다.|2의 doubly black을 검은색으로 바꾸며 처리한다.|


### Case2 - Case4의 꺾인 형태
- 한번 회전으로 Case1의 형태를 만들어서 처리한다.

### Case3 - 형제 black & 형제의 자식 모두 black
- 자신과 형제의 black을 부모로 올려서 부모에서 doubly black을 처리하도록 위임한다.
- 만약 doubly black이 root 까지 올라간다면 root에서는 그냥 doubly black을 없애주어도 된다.

### Case4 - 형제 red
- 회전시켜서 형제를 black으로 만들자
- Red의 자식으로 반드시 black이 있음이 보장되기 때문에 한번 회전으로 doubly black의 형제를 black으로 바꿀 수 있다.
