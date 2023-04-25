# Red Black Tree
## Red Black Tree 성질
- 각 노드는 red 혹은 black의 색을 가짐
- 루트 노드는 반드시 black
- red 노드의 자식은 반드시 black (red가 연속적으로 나올 수 없음)
- 모든 말단 노드(NIL Node)는 black이라 가정 
- 루트 노드에서 리프 노드로의 경로 사이의 black 노드 수(black height)는 어느 곳에서나 같음

## NIL Node
![image](https://user-images.githubusercontent.com/67370317/233995852-e6f741c6-e38c-4da8-871e-36f69c95e468.png)
- 자식 노드가 없는 자리는 NIL 노드라는 가상의 노드가 있다고 가정
- 레드 블랙 트리에서 NIL 노드들은 항상 리프 노드가 됨

## Insert
- 새로 삽입되는 노드는 red
- red 노드의 자식으로 삽입되면 위의 3번째 조건 만족 X
- 삼촌 노드의 색에 따라 Restructuring or Recoloring

### Restructuring
![image](https://user-images.githubusercontent.com/67370317/234003913-6f4b9a16-886c-4fb0-b95e-e4e1d12837f7.png)
- 새로운 노드 삽입 시 부모 노드가 red, 삼촌 노드 black
- 삼촌 노드란 부모 노드의 형제 노드

- 이 경우, (조부모 노드, 부모 노드, 새 노드) 셋을 정렬한 후 가운데 노드를 black, 나머지 둘을 red로 바꾸어 재구축
- AVL 트리 때의 삽입처럼 LL/LR/RL/RR에 따라 회전시키면 될 듯
![image](https://user-images.githubusercontent.com/67370317/234004944-c131475d-ee70-4b24-b1dd-eb71d93c9187.png)


### Recoloring
![image](https://user-images.githubusercontent.com/67370317/233999384-732e5783-bc56-43e2-8d0e-2186e86e5482.png)
- 새로운 노드 삽입 시 부모 노드가 red, 삼촌 노드도 red
- 이 경우 조부모 노드를 red, 부모 노드와 삼촌 노드를 black으로 색 변경
- 조부모 노드가 루트 노드인 경우 red가 될 수 없으므로 다시 black으로 바꿔줌
- 조부모 노드가 red로 바뀐 후 조부모 노드의 조상 노드들이 red일 수 있으므로 위로 올라가며 확인 과정 필요
![image](https://user-images.githubusercontent.com/67370317/234006263-45504d50-681e-4c8a-b631-24741924a32d.png)

### Delete
- 삭제 노드가 red라면 문제없이 삭제 가능
- 삭제 노드가 black이라면 리프 노드들의 black height가 바뀌거나, red가 연속으로 나올 수 있으므로 처리 필요 
  - 삭제 노드를 대체할 노드가 red?
    => 대체할 노드를 black으로 바꿔주면 해결
  - 삭제 노드를 대체할 노드가 black?
    => 대체할 노드 : 이중흑색노드가 됨(이미 black인 애를 또 black처리)

#### 이중흑색노드가 삭제된 노드의 왼쪽 자식이라 가정 시
- 형제 노드가 red : 부모를 red, 형제를 black으로 변경 후 부모를 기준으로 left rotation => 형제가 black이 됨, 아래 케이스에 따라 다시 균형잡기 수행
- 형제 노드가 black 이고 그의 두 자식이 모두 black : 형제를 red로, 부모를 black으로 => 부모가 이중흑색노드가 되면 부모의 형제 탐색
- 형제 노드가 black 이고 왼쪽 자식만 red : 형제를 red로, 왼쪽 자식을 black으로 변경 후 형제를 기준으로 right rotation => 형제가 black이 됨, 다시 균형잡기 수행
- 형제 노드가 black 이고 오른쪽 자식이 red : 형제의 색을 부모의 색으로, 부모와 오른쪽 자식을 black으로 변경 후 부모를 기준으로 left rotation
- 형제 탐색 불가(이중흑색노드가 루트라 형제가 없음) : 끝

#### 삭제된 노드의 자식이 오른쪽
- 위의 방식에서 방향 반대
