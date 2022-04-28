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
- 생성, 소멸
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
/*노드 소멸*/
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
- 노드 탐색
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

- 노드 삭제: 리스트 내에 있는 임의의 노드를 찾아 삭제함
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

- 노드 삽입
```
/*해당 노드의 뒤에 삽입*/
void InsertNode(Node* Current, Node* NewNode){
     NewNode->NextNode = Current->NextNode;
     Current->NextNode = NewNode;
}
```

### 1-2 더블 링크드 리스트(Double Linked List)
- 링크드 리스트의 단방향 탐색 기능을 개선하여 양방향 탐색이 가능한 자료구조다.
- 링크드 리스트는 다음 노드의 주소만 갖고 있는 반면 더블 링크드 리스트는 이전 노드의 주소도 갖고 있다.(그래서 구현상 링크드 리스트와 큰 차이는 없다)

- 자료형 선언
```
typedef struct tagNode {
        int Data;
        struct tagNode* PrevNode;
        struct tagNode* NextNode;
} Node;
```
- 노드 생성, 소멸

```
/*노드 생성*/
Node* SLL_CreateNode(ElementType NewData){
     Node* NewNode = (Node*)malloc(sizeof(Node));
     
     NewNode->Date = NewData;
     NewNode->PrevNode = NULL;
     NewNode->NextNode = NULL;
     
     return NewNode;
}
```

```
/*노드 소멸*/ 
void DLL_DestroyNode(Node* Node){
     free(Node);
}
```

- 노드 추가
```
void DLL_AppendNode(Node** Head, Node* Node){
     if(*Head == NULL){
     *Head = Node;
     }
     
     else{
     Node* Tail = Node;
     
     while(Tail->NextNode != NULL){
     Tail = Tail->NextNode;
     }
     Tail->NextNode = Node;
     Node->PrevNode = Tail;
     }
}
```

-노드 탐색
```
Node* DLL_SearchNode(Node* Head, int Location){
      Node* Current = Head;
      
      while(Current != NULL && (--Location) >= 0){
      Current = Current->NextNode;
      }
      return Current;
}
```

- 노드 삭제
  - *삭제 노드가 가진 앞뒤 노드의 주소값 초기화가 꼭 필요한지, 언제 필요한건지 잘 모르겠다
```
void DLL_Remove(Node** Head, Node* Remove){
     if(*Head == Remove){
         *Head = Remove->NextNode;
         if(*Head != NULL) (*Head)->PrevNode = NULL; //어차피 헤드는 이전 노드가 없는데 꼭 해야하나?
         
         Remove->PrevNode = NULL;
         Remove->NextNode = NULL;
     }
     
     else{
         Remove->PrevNode->NextNode = Remove->NextNode;
     
         if(Remove->NextNode != NULL) Remove->NextNode->PrevNode = Remove->PrevNode;
     
          Remove->PrevNode = NULL;
          Remove->NextNode = NULL;
     }
}
```
- 노드 삽입
```
void DLL_InsertNode(Node* Current, Node* NewNode){
     /*새로운 노드에 주소값을 대입*/
     NewNode->NextNode = Current->NextNode;
     NewNode->PrevNode = Current;
     
     /*기존 노드들의 주소값을 변경*/
     if(Current->NextNode != NULL){
     Current->NextNode->PrevNode = NewNode;
     }
     Current->NextNode = NewNode;
}
```

### 1-3 환형 링크드 리스트(Circular Linked List)
- 테일의 다음 노드가 헤드를 가리키는 형태의 링크드 리스트로 나머지는 다른 링크드 리스트와 거의 동일하다.
- 테일에 접근하는 비용이 거의 없어서 노드를 추가하는 함수의 성능 개선도 가능하고 뒤에서부터 노드를 찾아나가는 루틴도 구현할 수 있다.

- 노드추가
```
void CLL_AppendNode(Node** Head, Node* NewNode){
     /*헤드가 없으면 새로운 노드를 헤드로*/
     if((*Head) == NULL){
       *Head = NewNode
       (*Head)->PrevNode = *Head
       (*Head)->NextNode = *Head
     }
     
     else{
       Node* Tail = (*Head)->PrevNode;
       
       Tail->NextNode->PrevNode = NewNode;
       Tail->NextNode = NewNode;
       
       NewNode->PrevNode = Tail;
       NewNode->NextNode = (*Head);
     }
}
```

- 노드 삭제
```
void CLL_RemoveNode(Node** Head, Node* Remove){
     if((*Head) == Remove){
        (*Head)->PrevNode->NextNode = Remove->NextNode;
        (*Head)->NextNode->PrevNode = Remove->PrevNode;
        
        *Head = Remove->NextNode;
        
        Remove->PrevNode = NULL;
        Remove->NextNode = NULL;
     }
     else{
         Remove->PrevNode->NextNode = Remove->NextNode;
         Remove->NextNode->PrevNode = Remove->PrevNode;
         
         Remove->PrevNode = NULL;
         Remove->NextNode = NULL;
     }
}
```
## 2. 스택
- 가장 먼저 들어간 데이터가 가장 마지막에 나오는 First In Last Out, 가장 마지막에 들어간 데이터가 가장 먼저 나오는 Last In First Out 구조이며 데이터의 삽입과 삭제가 한쪽 끝에서만 이뤄진다.
- 메모리, 네트워크 프로토콜도 스택으로 구성되어 있다.
- 주기능으로 삽입(Push)와 제거(Pop)가 있다.
- 배열과 링크드 리스트로 구현하는 방법이 있다.

### 2-1 배열로 구현
- 동적으로 용량을 조절하기가 어렵다는 단점이 있지만 구현이 간단하다는 장점이 있다.

- 자료형 선언
```
/*노드 선언*/
typedef struct tagNode{
        int Data;
} Node;
```

```
/*스택 선언*/
typedef struct tagArrayStack{
        int Capacity;
        int Top;
        Node* Nodes; //C언어 특성상 포인터를 배열로 사용할 수 있기 때문에 가능한 선언이다.
} ArrayStack;
```
- 스택 생성, 소멸
```
/*스택 생성*/
void AS_CreateStack(ArrayStack** Stack, int Capacity){
     /*스택을 자유저장소에 생성*/
     (*Stack) = (ArrayStack*)malloc(sizeof(ArrayStack));
     
     /*입력된 Capacity만큼의 노드를 자유 저장소에 생성*/
     (*Stack)->Nodes = (Node*)malloc(sizeof(Node)*Capacity);
     
     /*값 초기화*/
     (*Stack)->Capacity = Capacity;
     (*Stack)->Top = 0;
}
```
```
/*스택 소멸*/
void AS_DestroyStack(ArrayStack* Stack){
     free(Stack->Nodes); //스택 내에 있는 노드를 먼저 해제해준다.
     free(Stack); //스택 해제
}
```

- Push 연산
```
void AS_Push(ArrayStack* Stack, int Data){
     int Position = Stack->Top;
     Stack->Nodes[Position] = Data;
     Stack->Top++;
}
```

- Pop 연산
```
/*빼는 연산이기 떄문에 반드시 호출자에게 값을 반환한다.*/
int AS_Pop(ArrayStack* Stack){
    int Position = --(Stack->Top); //Top의 값은 실제 배열 내의 최상위 값보다 1이 크기 때문에 위치로 사용할때 유의할 것
    
    return Stack->Nodes[Position].Data;
}
```

### 2-2 링크드 리스트로 구현
- 스택과 달리 용량에 제한이 없다.
- 배열과 다르게 인덱스로 노드에 접근할 수 없기 때문에 자신의 위에 있는 노드 위치에 대한 포인터가 있어야한다.

- 자료형 선언
```
/* 선언*/
typedef struct tagNode{
        char* Data;
        struct tagNode* NextNode; //자신의 위에 쌓일 노드의 주소
} Node;
```

```
/*스택 선언*/
typedef struct tagLinkedListStack{
        Node* List; //용량 제한이 없기 때문에 Capacity는 필요 없지만 헤드부터 접근 할 주소는 필요
        Node* Top;
} LinkedListStack;
```

- 스택 생성, 소멸
```
/*스택 생성*/
void LLS_CreateStack(LinkedListStack** Stack){
     (*Stack) = (LinkedListStack*)malloc(sizeof(LinkedListStack));
     (*Stack)->List = NULL;
     (*Stack)->Top = NULL;
}
```

```
/*스택 소멸*/
void LLS_DestroyStack(LinkedListStack* Stack){
     /*스택이 빌 때까지 반복*/
     while(!LLS_IsEmpty(Stack)){
          Node* Popped = LLS_Pop(Stack); //노드를 스택에서 제거
          LLS_DestroyNode(Popped); //메모리 해제
     }
     free(Stack); //
}
```

```
/*노드 생성*/
Node* LLS_CreateNode(char* NewData){
      /*자유저장소에 노드 할당*/
      Node* NewNode = (Node*)malloc(sizeof(Node));
      
      /*문자열을 자유 저장소에 할당*/
      NewNode->Data = (char*)malloc(strlen(NewData)+1);
      
      /*자유 저장소에 문자열 복사*/
      strcpy(NewNode->Data, NewData);
      
      NewNode->NextNode = NULL;
      
      return NewNode;
}
```

```
/*노드 소멸*/
void LLS_DestroyNode(Node* Node){
     free(Node->Data); //데이터를 먼저 해제
     free(Node); //노드를 해제
}
```

```
/*Push 연산*/
void LLS_Push(LinkedListStack* Stack, Node* NewNode){
     /*헤드일 경우*/
     if(Stack->List == NULL){
         Stack->List = NewNode;
     }
     else{
     /*최상위 노드를 찾아서 연결*/
     Node* OldTop = Stack->List;
     while(OldTop->NextNode != NULL){
         OldTop = OldTop->NextNode;
     }
     OldTop->NextNode = NewNode;
     }
     
     Stack->Top = NewNode;
}
```

```
/*Pop 연산*/
Node* LLS_Pop(LinkedListStack* Stack){
      /*Pop 하려는 Top 노드를 복사*/
      Node* TopNode = Stack->Top;
      
      /*헤드라면 바로 초기화*/
      if(Stack->Top == Stack->List){
         Stack->List == NULL;
         Stack->Top == NULL;
      }
      
      else{
         Node* CurrentTop = Stack->List;
         
         /*기존 Top 이전 노드가 나올때까지 반복문 수행 후 Top을 교체*/
         while(CurrentTop != NULL && CurrentTop->NextNode != Stack->Top){
                  CurrentTop = Current->NextNode;
         }
         Stack->Top = CurrentTop;
         CurrentTop->NextNode = NULL;
      }
      
      return TopNode;
}
```

### 2-3 사칙 연산 계산기
- 수식의 중위 표기법과 후위 표기법

## 3. 큐
- 먼저 들어가고 먼저 나오는 First In First Out 구조이며 우리말로 대기행렬이라고도 한다.
- 큐의 가장 앞요소를 전단(Front), 마지막 요소를 후단(Rear)이라고 한다.
- 주기능으로 삽입(Enqueue)과 제거(Dequeue)가 있다.
- 배열로 구현하는 순환 큐와 링크드리스트로 구현하는 링크드 큐가 있다.

### 3-1 순환 큐
- 개념과 구현이 다른 자료구조에 비해 비교적 까다롭다..
- 배열의 시작과 끝을 잇는 개념이지만 실제로 그런 기능은 없기 때문에 논리적인 구현을 해야한다.
- 공백과 포화 상태를 구분 하기 위해 후단의 값은 실제 후단보다 1을 더한 값을 가진다.
   - 같은 곳을 가리키면 비어 있고 후단이 전단보다 1 작은 값을 가지면 가득 찬 것.

- 자료형 선언
```
/*노드 선언*/
typedef struct tagNode {
        int Data;
} Node;
```

```
/*순환 큐 선언*/
typedef struct tagCircularQueue{
        int Capacity; //용량 -> 공백 상태와 포화 상태를 구분하기 위해 더미 노드가 하나 더 있기 때문에 실제 용량보다 하나 적다.
        int Front;    //전단의 위치
        int Rear;     //후단의 위치 -> Capacity와 마찬가지로 공백/포화상태 구분을 위해 실제 후단보다 1 큰 값을 갖는다.
        Node* Nodes;
} CircularQueue;
```


- 순환 큐 생성
```
void CQ_CreateQueue(CircularQueue** Queue, int Capacity){
     /*큐를 생성*/
     (*Queue) = (Queue*)malloc(sizeof(CircularQueue));
     
     /*Capacity+1 만큼의 노드를 생성*/
     (*Queue)->Nodes = (Node*)malloc(sizeof(Node)*Capacity+1);
     
     (*Queue)->Capacity = NULL;
     (*Queue)->Front = 0;
     (*Queue)->Rear = 0;
}
```
