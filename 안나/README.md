# 🔖 **Red Black Tree ?**

- 이진 트리(BST)의 한 종류
- 스스로 균형을 잡는 트리
- BST의 wort case 의 단점을 개선하기 위해 등장
    - 최악의 상황에 시간복잡도가 O(N)이 아니라 O(logN)이 나오도록 개선
- 특이점 : 모든 노드에 색을 부여
  <br><br>
  <br>
<hr>

## 🔍 **RB Tree의 속성**

<span style="color:orange">**📌 #1 속성**</span>. 모든 노드에는 red 혹은 black 이다.

<span style="color:orange">**📌 #2 속성**</span>. 루트 노드는 black 이다.

<span style="color:orange">**📌 #3 속성**</span>. 모든 NIL노드는 black 이다.

    💡 NIL 노드 ?
        - 존재하지 않음을 의미
        - 자녀가 없을 때 자녀를 NIL 노드로 표기하므로  RB 트리의 모든 단말 노드는 NIL 노드이다.

<span style="color:orange">**📌 #4 속성**</span>. red 의 자녀들은 black 이고 red인 두 노드가 부모, 자식 관계를 맺을 수 없다.

<span style="color:orange">**📌 #5 속성**</span>. 임의의 노드에서 자식 NIL 노드 까지 가는 각 경로들의 black의 수는 모두 같다.
(이때 자기 자신은 카운트에서 제외한다.)

    💡 노드 x의 black height ?
        - 노드 x에서 임의의 자손 NIL 노드까지 내려가는 경로에서의 black의 수


    💡 색을 바꾸면서 #5속성 유지하기 (삽입, 삭제시 이용하는 기법)
        - 두 자녀의 색이 같을 때 부모와 두 자녀의 색을 바꿔주어도 #5속성 를 여전히 만족한다.
        - 부모의 입장에서는 black 노드가 더 추가되거나 삭제된 게 아니기 때문에 당연한 것.

<br>
<hr>

## 🔍 **RB Tree의 삽입**

### 🎁 들어가기 전

- 삽입하는 노드의 색은 항상 red 이다. 왜 삽입하는 노드의 색이 항상 red 여야 할까 ❓
  ![Untitled](https://user-images.githubusercontent.com/99172832/234583161-82c2426b-85a4-40c4-be3c-bb330fbadf07.png)

    - #5속성 을 만족 시키기 위해서이다.
    - 단말노드에 노드가 삽입되었을 때 양 NIL노드까지의 black의 수에 영향을 미치지 않기 때문.

### 🎁 삽입하는 노드의 위치에 따라 발생하는 문제
* ### case 0 : 삽입하는 노드의 위치가 루트인 경우 (⇒  **#2 속성**를 위반의 경우)
  ##### 📌 해결 방법
       1. 삽입한 노드를 루트로 지정
       2. 자녀 노드를 NIL로 지정
       3. #2속성으로 인해 삽입한 노드의 색을 black으로 변경
  ##### 📌 결론
    - 노드를 삽입한 후에  **#2 속성**를 위반한다면 루트 노드를 black으로 바꿔준다.


* ### case 1 : 삽입하는 노드의 부모가 red이고 삽입 후 모양이 LL이거나 RR인 경우  (⇒  #4 속성를 위반의 경우)
  ##### 📌 해결 방법
  ![1](https://user-images.githubusercontent.com/99172832/234583273-ad8af8b2-09f1-4333-99e0-fb8b2abcb458.png)



      1. 삽입할 노드의 부모와 조부모의 색을 바꿔준다. (20을 black으로 50을 red로)
      2. 조부모 노드를 기준으로 회전
##### 📌 결론
- 노드를 삽입한 후에 삽입한 노드의 부모가 red, 부모의 형제가 black 이고 LL이거나 RR 이라면 부모와 조부모의 색을 바꾼 후 조부모를 기준으로 회전한다.

* ### case 2 : 삽입하는 노드의 부모가 red이고 삽입 후 모양이 LR이거나 RL인 경우  (⇒  **#4 속성**를 위반의 경우)
  ##### 📌 해결 방법
  ![2](https://user-images.githubusercontent.com/99172832/234583306-999efd90-f22a-4a61-bafa-1549f380e1ee.png)



        1. 삽입할 노드의 부모를 기준으로 회전한다.( 꺾여 있는 부분을 회전하기 위함)

           (이후 삽입하는 노드의 부모가 red이고 삽입 후 모양이 LL이거나 RR인 경우에 균형을 맞추는 작업과 동일하게 진행)

        2. 부모와 조부모의 색을 바꿔준다. (40을 black으로 50을 red로)
        3. 조부모 노드를 기준으로 회전
##### 📌 결론
* 노드를 삽입한 후에 삽입한 노드의 부모가 red, 부모의 형제가 black 이고 LR이거나 RL 이라면 부모와 조부모의 색을 바꾼 후 조부모를 기준으로 회전한다.

* ### case 3 : 삽입하는 노드의 부모가 red이고 부모의 형제가 red인경우 (⇒  **#4 속성**를 위반의 경우)
  ##### 📌 해결 방법
    - 30 노드 삽입
      <br>![3](https://user-images.githubusercontent.com/99172832/234583361-49a3e1b8-67f6-4fe7-aea2-ef737782c90f.png)



        1. 편향되지 않았지만 RB의 규칙을 지켜주어야 한다.
        2. 삽입한 노드의 부모와 형제들의 색을 blakc 으로 바꾸고 조부모는 red로 변경한다.(20을 red로 10과 50은 black 으로) (**#5 속성**를 “최대한” 유지하기 위해)  (⇒  #2 속성를 위반)
        
        3-1. 조부모가 루트 노드라면 black로 바꿔준다. (20을 black으로 ) (**#2 속성**를 유지하기 위해)
        3-2. 조부모가 부모가 존재하고 그 부모의 색이 red라면 다시 확인한다.
##### 📌 결론
- 노드를 삽입한 후에 삽입한 노드의 부모가 red, 부모의 형제가 red 이면 부모와 부모형제 노드를 black으로 변경 후 조부모가 RB 규칙이 맞는지 다시 확인한다.

<br>
<hr>

## 🔍 **RB Tree의 삭제**

### 🎁 들어가기 전

- 삭제되는 노드의 색이 어떤 색인지에 따라 속성의 위반 여부가 판별된다.

      💡 삭제되는 색 ?
        - 삭제하려는 노드가 자식이 없거나 하나인 경우 (NIL 노드는 포함하지 않음)삭제되는 색은 삭제되는 "노드의 색"이다.
        - 삭제하려는 노드가 자식이 둘인 경우, 삭제되는 색은 삭제되는 "노드와 대체되는 노드의 색"

-  삭제되는 색에 따라 속성 위반 여부를 어떻게 확인할까 ❓
    - 삭제되는 색이 **red**라면 어떠한 속성도 위반하지 않는다.
      <br>👉 black 색의 수에 영향이 없기 때문에
    - 삭제되는 색이 **black**이라면 #2, #4,#5 속성을 위반할 수 있다.
        - 삭제되는 노드의 색은 black 이고 부모와 자식이 red 인 경우
          ![4](https://user-images.githubusercontent.com/99172832/234583546-1a414919-b2eb-472f-bd2c-d0cafd9ce2db.png)

          <br>👉 노드를 삭제하고 그 노드의 부모와 자식을 이어주게 되는데 그러면 red-red 인 경우가 생긴다. (⇒  **#4, #5속성**를 위반)
        - 삭제하려는 노드가 root이고 자식의 자식이 존재하지 않으며 자식이 red 인 경우
          <br>👉 루트인 노드가 삭제되면 자식노드가 루트가 되니까 루트가 red가 된다.(⇒  **#2 속성**를 위반)
          <br>
<hr>

### 🎁 삭제 되는 색이 blcak일 때 **#2, #4 ,#5속성**을 만족 시키는 방법
* ### **#2 속성**을 위반할 때
    ![5](https://user-images.githubusercontent.com/99172832/234583629-4c9cfad4-6056-4c82-901f-f9427b7e2c2a.png)

  ##### 📌 해결 방법
      - 루트 노드의 색을 black으로 바꿔준다.
  ##### 📌 결론
    - 노드를 삽입한

* ### **#4, #5 속성**을 위반할 때
    - black인 노드를 삭제하게 되면 NIL노드까지의 black height가 같지 않게 변할 수 있다.
    - 이러한 문제를 해결하기 위해 삭제된 색의 위치를 대체한 노드에 extra black을 부여하여 black height 를 동일하게 유지한 후 #4 속성을 유지하며 extra black을 제거한다.

          💡 extra black  : 루트에서 NIL노드로의 black 의 수를 유지 시키기 위해서 부여하는 가상의 black

          💡 doubly black : black 노드에 extra black이 부여된 노드
          
          💡 red and black :  red 노드에 extra black이 부여된 노드
    - ![6](https://user-images.githubusercontent.com/99172832/234583660-9df8ed61-ad04-4eb3-a24d-0c38ec27210e.png)

    - ![7](https://user-images.githubusercontent.com/99172832/234583684-776c334b-80b5-4879-942c-34bbb135f703.png)

        - 다음은 extra black을 제거하는 방법이다.

### 🎁  red 노드에 부여된 extra black 제거 ( red and black 해결하기)
##### 📌 해결 방법

      - red 였던 노드를 black 으로 바꿔주면 해결
      - #5 속성을 만족하기 위해 black을 부여했던 것이기 때문에 색을 바꾸어 주면된다.
      - 만약 바꿔준 후 #4 속성을 위반한다면 주변의 red를 black으로 바꿔주면 된다.

<br>
<br>
<br>

### 🎁  black 노드에 부여된 extra black 제거 ( doubly black 해결하기)
* ### case 1 : doubly black의 오른쪽(왼쪽) 형제가 black 이고 그 형제의 오른쪽(왼쪽) 자녀가 red일 때
  ![8](https://user-images.githubusercontent.com/99172832/234583763-db0651f0-b1af-4934-9aa8-19027b9907b4.png)


##### 📌 해결 방법
      - red 였던 노드를 black 으로 바꿔주면 해결
      - #5 속성을 만족하기 위해 black을 부여했던 것이기 때문에 색을 바꾸어 주면된다.
      - 만약 바꿔준 후 #4 속성을 위반한다면 주변의 red를 black으로 바꿔주면 된다.
       
      💡 오른쪽(왼쪽) 형제는 부모의 색으로. 오른쪽(왼쪽) 형제의 오른쪽(왼쪽)자녀는 black으로 , 부모는 black으로 바꾼 후에 부모를 기준으로 왼쪽(오른쪽)으로 회전하면 해결
##### 📌 접근 방법
- red인 E 노드를 doubly 노드인 A의 위로 보내서 extra black을 E에 부여하면 red and black 으로 변경하면 쉽게 해결할 수 있지 않을까 ?
- 그러면 A 노드 위에 red 노드를 두기 위해서는 “두 자녀의 색이 같을 때 부모와 두 자녀의 색을 바꿔주어도 **속성 5**를 여전히 만족한다.” 것을 이용하여 D를 red로
  바꾸고 E를 black 으로 바꾸고 C에게 extra black 을 부여한다.
  <br>![9](https://user-images.githubusercontent.com/99172832/234583798-fa19517f-1891-4946-9436-26fcd06bff2f.png)



- 그렇게 되면 B를 기준으로 왼쪽 회전을 했을때 A위로 B가 넘어가고 그 노드의 색이 red일 수 있도록 만들어주기 위해서 B와 D의 색을 바꾼다.
- B를 기준을 왼쪽 회전을 한다.
  <br>![10](https://user-images.githubusercontent.com/99172832/234583835-07189b39-ddd5-4d25-92eb-c23961272e0f.png)



- A와 C는 모두 색을 black을 가지고 있으므로 “두 자녀의 색이 같을 때 부모와 두 자녀의 색을 바꿔주어도 **속성 5**를 여전히 만족한다.”을 이용하여 B는
  black으로 A와 C는 black이 부과되기 이전의 색으로 바꾸어 준다.
<br>![11](https://user-images.githubusercontent.com/99172832/234583874-872123ae-9930-4622-8887-e6d1edc4ab3c.png)



- 그러면 B는 red and black 이 되므로 “red and black 해결하기”를 참고해 black으로 바꿔 주면 된다.



<br>
<br>
<br>

* ### case 2 : doubly black의 오른쪽(왼쪽) 형제가 black 이고 그 형제의 왼쪽(오른쪽)  자녀가 red, 오른쪽(왼쪽)자녀가 black일때
  ![12](https://user-images.githubusercontent.com/99172832/234583894-64642115-6377-4351-be18-e0702a8e9b70.png)


##### 📌 해결 방법
      💡 오른쪽(왼쪽) 형제는 부모의 색으로. 오른쪽(왼쪽) 형제의 오른쪽(왼쪽)자녀는 black으로 , 부모는 black으로 바꾼 후에 부모를 기준으로 왼쪽(오른쪽)으로 회전하면 해
##### 📌 접근 방법
- E 위치가 red가 되도록 만들면 case1 과 동일한 케이스가 되니까 그렇게 바꿔도 되지 않을까?
  ![13](https://user-images.githubusercontent.com/99172832/234583911-221b2203-d4ee-4347-99f1-cebdf3c29908.png)



- 그러면 C와 E의 색을 바꿔준후 오른쪽 회전을 하면 .E위치의 노드가 red 이다.
  <br>
  <br>
  <br>

* ### case 3: doubly black과 그 형제가 black이고 그 형제의 두 자녀가 모두 black 일 경우
  <br>![14](https://user-images.githubusercontent.com/99172832/234583935-80a07eb3-0b9e-40da-ba55-7a321bfef770.png)


  ##### 📌 해결 방법
      💡 doubly black 과 그 형제의 black을 모아서 부모에게 전달해서 부모가 extra black을 해결하도록 위임한다.
  ##### 📌 접근 방법
- C, E가 모두 black이므로 D는 red가 될 수 있으니 A와 D의 색을 바꾸면 A는 extra black을 떼고 D는 red로 바꾸고 B에 extra black을 부여할
  수 있지 않을까?
- 그렇게 extra black을 부여한 B노드가 red and black 이면 black을 바꾸어 해결하고 doubly black이고 루트노드가 아니라면 case 1,2,3,4
  중에 하나로 해결한다.
- 만약 B가 루트노드라면 black으로 변경하여 해결한다.

<br>
<br>
<br>

* ### case 4: doubly black의 형제가 red 인 경우
  <br>![15](https://user-images.githubusercontent.com/99172832/234583978-1159c4ef-557c-4e82-8b44-2d9b70ad186e.png)


##### 📌 해결 방법
      💡 부모와 형제의 색을 바꾸고 부모를 기준으로 왼쪽(오른쪽) 회전한뒤 doubly black을 기준으로 case 1,2,3 중에 하나로 해결한다.
##### 📌 접근 방법
- 위 case 1,2,3은 모두 doubly black의 형제가 black인 경우이므로 A의 형제를 black으로 만들면 해결할 수 있지 않을까?
- 그러면 B노드를 기준으로 왼쪽 회전을 하게 되면 D의 왼쪽 자식노드 C가 B의 오른쪽 자식이 되므로 A의 형제노드가 black이 된다. 그러면 case 1,2,3 중에 하나로
  해결가능하다.
- 그치만 이 과정에서 왼쪽 회전을 하게되면 D 노드가 루트가 되므로 black으로 만들어쥐 위해 B와 D의 색을 바꾸고 회전한다.
