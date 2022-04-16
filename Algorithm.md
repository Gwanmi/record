# 자료구조
## 1. 리스트
### 1-1 링크드 리스트(Linked List)
- 리스트 내의 각 요소는 노드(Node)라고 부르는데 링크드 리스트는 노드를 연결해 만드는 리스트라 해서 붙여진 이름이다.
- 링크드 리스트의 노드는 데이터를 보관하는 필드와 다음 노드와의 연결고리 역할을 하는 포인터로 이루어져 있다.
- 리스트의 첫 번째 노드를 헤드(head), 마지막 노드를 테일(tail)이라고 부른다.
- 필요할 때마다 노드를 추가하면 되기 때문에 다뤄야 하는 데이터 집합의 크기를 몰라도 된다.
- 새로운 노드의 추가, 삽입, 삭제가 빠르지만 특정 위치에 있는 노드를 찾는 연산은 느리다. 그러므로 추가, 삽입, 삭제가 잦고 조회는 드문 곳에 적합하다.
- 링크드 리스트의 연산에는 생성, 소멸, 추가, 탐색, 삭제, 삽입이 있다.
- 자료형 선언
```
/*typedef로 선언하지 않으면 노드를 생성할 때마다 struct를 적어야 한다*/
typedef struct tagNode {
         int Data;
         struct tagNode* NextNode;
         } Node;
Node l_Node;
```
-생성, 소멸
  - 링크드 리스트는 전역 변수와 정적 변수가 저장되는 스태틱 메모리와 지역 변수가 저장되는 오토매틱 메모리가 아닌 자유 저장소(Free Memory)에 저장된다.
```
/*노드 생성*/
Node* SLL_CreateNode(ElementType NewData) {
      Node* NewNode = (Node*)malloc(sizeof(Node)); //자유 저장소에 생성하여 주소값을 반환
      
      NewNode->Data = NewData; //데이터 저장
      NewNode->NextNode = NULL; //주소 초기화
      
      return NewNode; //생성한 노드의 주소 반환
      }
```
```
/*노드 제거*/
void SLL_DestroyNode(Node* Node){
     free(Node);
     }
```

- 노드 추가
  - 테일 노드 뒤에 새로운 노드를 만들어 연결한다.
  - List를 전달할 때 이중포인터를 쓰는 이유: List 변수 그 자체는 아무값이 아닌 NULL을 갖고 있기 때문에 Node 자료형의 포인터로 선언된 List의 주소값을 전달하려면 포인터의 주소를 담는 이중포인터를 사용해야한다.
```
void SLL_AppendNode(Node** Head, Node* NewNode){
     /*헤드가 없다면 새로운 노드를 헤드로 한다.*/
     if((*Head) == NULL){
     *Head = NewNode;
     ]
     
     /*테일을 찾아 새로운 노드를 연결*/
     else{
     Node* Tail = *Head;
     while(Tail->NextNode!=NULL){
     Tail = Tale->NextNode;
     }
     Tail->NextNode = NewNode;
     }
}
```
-노드 탐색
  - *Array와 달리 리스트는 헤드부터 시작해 노드를 세어나가야만 원하는 자료에 접근할 수 있다.
```
Node* SLL_SearchNode(Node* Head, int Location){
      Node* Current = Head;
      
      whlie(Current != NULL && (--Location)>=0){
      Current = Current->NextNode;
      }
      return Current;
}
```

-노드 삭제: 리스트 내에 있는 임의의 노드를 찾아 삭제함
```
/*헤드가 삭제해야할 노드일 수도 있으므로 헤드의 주소를 넘기기 위해 이중포인터를 사용*/
void SLL_RemoveNode(Node** Head, Node* Remove){
     if(*Head == Remove){
     *Head = Remove->NextNode;
     }
     
     else{
     Node* Current = *Head;
     
     /*테일을 만나거나 삭제할 노드를 만날때까지 반복문*/
     while(Current != NULL && Current->NextNode != Remove){
     Current = Current->NextNode;
     }
     /*삭제할 노드 이전의 노드가 가리키는 값을 삭제할 노드의 다음 노드의 주소값으로 치환*/
     if(Current != NULL){
     Current->NextNode = Remove->NextNode;
     }
     }
}
```

-노드 삽입
```
/*해당 노드의 뒤에 삽입*/
void InsertNode(Node* Current, Node* NewNode){
     NewNode->NextNode = Current->NextNode;
     Current->NextNode = NewNode;
}
```
