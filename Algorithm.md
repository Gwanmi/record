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
- 먼저 들어간 데이터가 마지막에 나오는 First In Last Out, 마지막에 들어간 데이터가 먼저 나오는 Last In First Out 구조이며 데이터의 삽입과 삭제가 한쪽 끝에서만 이뤄진다.
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


- 순환 큐 생성, 소멸
```
/*큐 생성*/
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

```
/*큐 소멸*/
void CQ_DestroyQueue(CircularQueue* Queue){
     free(Queue->Node); //노드 먼저 해제
     free(Queue);       //큐를 해제
}
```

- 공백 확인, 포화 확인

```
/*공백 확인*/
int CQ_IsEmpty(Circular* Queue){
    return (Queue->Front) == (Queue->Rear); //전단과 후단이 동일한 인덱스면 비어있다는 뜻
}
```

```
/*포화 확인*/
int CQ_IsFULL(Circular* Queue){

    /*Front가 Rear보다 작을 경우*/
    if((Queue->Front) < (Queue->Rear)){
       return ((Queue->Rear) - (Queue->Front)) == Queue->Capacity;
    }
    
    /*Rear가 Front보다 작을 경우*/
    else return (Queue->Rear + 1) == Queue->Front;
}
```

- 삽입(Enqueue) 연산

```
void CQ__Enqueue(CircularQueue* Queue, int Data){
     int Position = 0;
     
     //가득 차지 않았을 경우
     if(!CQ_IsFull(Queue)){
          /*Rear가 용량과 같다면 끝에 도달했다는 의미이므로 0으로 옮겨준다*/
          if(Queue->Rear == Queue->Capacity){
             Position = Queue->Rear;
             Queue->Rear = 0;
           }
          
          /*Rear를 옮겨주고 값을 넣을 해당 위치 데이터를 넣을 인덱스로 사용*/
          else{
               Position = Queue->Rear++;
          }
     
     /*가득 찼을 경우 안내 문구를 출력하고 종료*/
     else{
         printf("큐가 가득 찼습니다.\n");
         return;
     }
     
     }
     
     Queue->Nodes[Position].Data = Data;
}
```

- 제거(Dequeue) 연산

```
int CQ_Dequeue(CircularQueue* Queue){
    int Position = Queue->Front;
    
    /*큐가 비어있지 않다면*/
    if(!CQ_IsEmpty(Queue)){
       /*전단이 배열의 끝이라면*/
       if(Queue->Front == Queue->Capacity){
         Queue->Front = 0; //전단을 배열의 앞으로 초기화
       }
       else{
        Queue->Front++;
       }
       return Queue->Nodes[Position].Data;
    }
    
    /*큐가 비어있다면*/
    else{
         printf("큐가 비어있습니다.\n");
         return 0;
    }
}
```

### 3-2 링크드 큐
- 순환 큐와 다르게 구현이 쉽고 포화 상태인지 확인할 필요가 없으며 용량에 제한이 없다.
- 하지만 성능은 순환 큐가 더 빠르다.

- 자료형 선언
```
/*노드 선언*/
typedef struct tagNode{
         int Data;
         struct tagNode* NextNode;
} Node;
```

```
/*링크드 큐 선언*/
typedef struct tagLinkedQueue{
         Node* Front;
         Node* Rear;
         int Count; //노드의 숫자
} LinkedQueue;
```

- 링크드 큐 생성, 소멸
```
/*생성*/
void LQ_CreateQueue(LinkedQueue** Queue){
     (*Queue) = (LinkedQueue)malloc(sizeof(LinkedQueue));
     (*Queue)->Front = NULL;
     (*Queue)->Rear = NULL;
     (*Queue)->Count = 0;
}
```

```
/*소멸*/
void LQ_DestroyQueue(LinkedQueue* Queue){
     /*모든 노드를 먼저 해제 후 큐를 해제*/
     while(!LQ_IsEmpty(Queue)){
         Node* Popped = LQ_Dequeue(&Queue);
         LQ_DestroyNode(Popped);
     }
     free(Queue);
}
```

- 삽입(Enqueue) 연산
```
void LQ_Enqueue(LinkedQueue* Queue, Node* NewNode){
     /*헤드 노드가 없다면*/
     if(Queue->Front == NULL){
         Queue->Front = NewNode;
         Queue->Rear  = NewNode;
         Queue->Count++;
     }
     else{
         Queue->Rear->NextNode = NewNode; //후단에 노드를 연결
         Queue->Rear = NewNode; //후단 갱신
         Queue->Count++;
     }
}
```

- 제거(Dequeue) 연산
```
Node* LQ_Dequeue(LinkedQueue* Queue){
      /*제거 할 최상위 노드*/
      Node* Front = Queue->Front;
      
      /*최상위 노드 제거 이후 아무 것도 없다면*/
      if(Queue->Front->NextNode == NULL){
         Queue->Front = NULL;
         Queue->Rear  = NULL;
      }
      
      else{
         Queue->Front = Queue->Front->NextNode;
      }
      
      Queue->Count--;
      
      return Front;
}
```

## 4. 트리
- 이름처럼 나무를 닮은 자료구조이며 활용범위가 아주 넓다(OS의 파일시스템, 검색 엔진, DB 등)
- 뿌리(Root), 가지(Branch), 잎(Leaf) 3가지 요소로 이루어져 있다.
  - 뿌리는 가장 위에 있는 노드를 가리키며 가지는 뿌리와 잎 사이에 있는 모든 노드, 가지의 끝에 있는 노드를 잎이라 하며 잎은 단말(Terminal) 노드라고 부르기도 한다.
  - 어떤 노드의 상위 노드를 부모(Parent)라고 하며 하위 노드를 자식(Children)이라고 한다. 그리고 한 부모에서 나온 노드를 형제(Sibling)다.
  - 경로(Path)는 한 노드에서부터 다른 한 노드까지 이르는 길 사이에 놓여있는 노드들의 순서이며 거쳐가는 노드의 갯수인 길이(Length)라는 속성을 가진다.
  - 깊이(Depth)는 뿌리 노드에서 해당 노드까지의 경로의 길이를 뜻한다.
  - 레벨(Level)은 깊이가 같은 노드의 집합이다.(뿌리는 0이다)
  - 높이(Height)는 가장 깊은 곳에 있는 잎 노드까지의 깊이를 말한다.
  - 차수(Degree)에서 노드의 차수는 해당 노드의 자식 노드 개수를 말하는 것이며 트리의 차수는 트리 내의 노드들 가운데 자식 노드가 가장 많은 노드의 차수를 말한다.
- 트리의 표현 방법으로는 3가지가 있다.
  - 중첩된 괄호(Nested Parenthesis) 표현법: 같은 레벨의 노드들을 괄호로 같이 묶어 표현하는 방법이다. 읽기는 어렵지만 트리를 하나의 공식처럼 표현할 수 있는 장점이 있다.
  - 중첩된 집합(Nested Set) 표현법: 트리가 하위 트리의 집합이라는 관계를 잘 표현할 수 있는 장점이 있다.(그림은 검색해보자)
  - 들여쓰기(Indentation): 자료의 계층적인 특징을 잘 나타낸다. 좋은 예시로 윈도우 탐색기의 폴더 트리가 있다.
- 노드의 표현 방법으로는 2가지가 있다.
  - N-링크(N_Link) 표현법: 노드의 차수가 N개일 때 노드는 N개의 링크를 가지고 있고 이 링크는 각각 자식 노드를 가리키도록 구성된다. 쓸만해 보이지만 차수가 노드마다 달라지는 트리에서는 적용하기 어려운 단점이 있다.
  - 왼쪽 자식-오른쪽 형제(Left Child-Right Sibling) 표현법: 위의 문제를 해결한 표현법으로 이름 그대로 왼쪽에는 자식, 오른쪽에는 형제에 대한 포인터를 갖고 있는 노드의 구조다. 한 노드의 자식 노드를 구하려면 왼쪽 자식의 포인터를 따라서 오른쪽 형제의 포인터를 얻어나가면 모두 얻어낼 수 있다.


### 4-1 기본 트리
- 왼쪽 자식-오른쪽 형제(LCRS) 표현법 사용

- 자료형 선언
```
typedef struct tagLCRSNode{
        struct tagLCRSNode* LeftChild;
        struct tagLCRSNode* RightSibling;
        
        int Data;
} LCRSNode;
```

- 노드 생성, 소멸
```
/*노드 생성*/
LCRSNode* LCRS_CreateNode(int NewData){
          LCRSNode* NewNode = (LCRSNode*)malloc(sizeof(LCRSNode));
          NewNode->LeftChild = NULL;
          NewNode->RightSibling = NULL;
          NewNode->Data = NewData;
          
          return NewNode;
}
```

```
/*노드 소멸*/
void LCRS_DestroyNode(LCRS* Node){
     free(Node);
}
```

- 자식 노드 연결
```
void LCRS_AddChildNode(LCRSNode* Parent, LCRSNode* Child){
     if(Parent->LeftChild == NULL){
        Parent->LeftChild = Child; //자식 노드가 없다면 바로 붙인다
     }
     /*자식 노드가 있다면 NULL을 찾아서 붙인다*/
     else{
         LCRSNode* TempNode = Parent->LeftChild;
         while(TempNode->RightSibling != NULL)
               TempNode = TempNode->RightSibling;
               
         TempNode->RightSibling = Child;
     }
}
```

- 트리 출력
  - 깊이에 따라 들여쓰기를 해서 노드를 출력하면 트리를 표현할 수 있다.
```
void LCRS_PrintTree(LCRSNode* Node, int Depth){
     int i = 0;
     
     /*깊이만큼 들여쓰기*/
     for(i = 0 ; i<Depth ; i++)
         printf(" ");
     
     /*데이터 출력*/
     printf("%c\n", Node->Data);
     
     /*자식 노드가 있다면 출력*/
     if(Node->LeftChild != NULL)
        LCRS_PrintTree(Node->LeftChild, Depth+1);
     
     /*형제가 있다면 출력*/
     if(Node->RightSibling != NULL)
        LCRS_PrintTree(Node->RightSibling, Depth);
}
```
### 4-2 이진 트리(Binary Tree)
- 모든 노드가 최대 2개의 자식을 가질 수 있는 트리
- 데이터를 담는 용도로는 적합하지 않으며 컴파일러나 검색 등에 사용되는 특수 자료구조다.
- 대표적으로 수식을 트리 형태로 표현하여 계산하게 하는 수식 이진 트리(Expression Binary Tree), 아주 빠른 데이터 검색을 가능하게 하는 이진 탐색 트리(Binary Search Tree)가 있다.
- 이진 트리의 종류
  - 포화 이진 트리(Full Binary Tree): 잎 노드를 제외한 모든 노드가 자식 노드를 둘씩 갖고 있는 트리
  - 완전 이진 트리(Complete Binary Tree): 잎 노드들이 왼쪽부터 모두 채워진 트리(일부가 비었어도 잎 노드 **사이**가 빠지지 않았다면 완전 이진 트리)
  - 높이 균형 트리(Height Balanced Tree): 뿌리 노드를 기준으로 왼쪽 하위 트리와 오른쪽 하위 트리의 높이가 1이상 차이나지 않는 이진 트리
  - 완전 높이 균형 트리(Complete Height Balanced Tree): 뿌리 노드를 기준으로 왼쪽 하위 트리와 오른쪽 하위 트리의 높이가 같은 이진 트리
- 이진 트리의 순회에는 3가지가 있다.
  - 전위 순회(Preorder Traversal): (1)뿌리 노드부터 방문 (2)왼쪽 하위 트리 방문 (3) 오른쪽 하위 트리 방문. 이진 트리를 중첩된 괄호로 표현할 수 있다.
  - 중위 순회(Inorder Traversal): (1)왼쪽 하위 트리부터 방문 (2)뿌리를 방문 (3)오른쪽 하위 트리 방문. 대표적으로 수식 트리(Expression Tree)가 있다.
  - 후위 순회(Postorder Traversal): (1)왼쪽 하위 트리부터 방문 (2)오른쪽 하위 트리 방문 (3) 뿌리를 방문. 중위 순회로 중위 표기식이 나오는 노드에 후위 순회를 적용하면 후위 표기식이 나온다.

- 자료형 선언
```
typedef struct tagSBTNode{
        struct tagSBTNode* Left;
        struct tagSBTNode* Right;
        char Data;
} SBTNode;
```

- 노드 생성, 소멸
```
/*노드 생성*/
SBTNode* SBT_CreateNode(char NewData){
         SBTNode* NewNode = (SBTNode*)malloc(sizeof(SBTNode));
         NewNode->Left  = NULL;
         NewNode->Right = NULL;
         NewNode->Data = NewData;
         
         return NewNode;
}
```

```
/*노드 소멸*/
void SBT_DestroyNode(SBTNode* Node){
     free(Node);
}
```

- 전위 순회를 이용한 트리 출력
```
void SBT_PreorderPrintTree(SBTNode* Node){
     if(Node==NULL) return;
     
     /*루트 노드 출력*/
     printf(" %c", Node->Data);
     
     /*왼쪽 하위 트리 출력*/
     SBT_PreorderPrintTree(Node->Left);
     
     /*오른쪽 하위 트리 출력*/
     SBT_PreorderPrintTree(Node->Right);
}
```

- 중위 순회를 이용한 트리 출력
```
void SBT_InorderPrintTree(SBTNode* Node){
     if(Node == NULL) return;
     
     /*왼쪽 하위 트리 출력*/
     SBT_InorderPrintTree(Node->Left);
     
     /*루트 노드 출력*/
     printf(" %c", Node->Data);
     
     /*오른쪽 하위 트리 출력*/
     SBT_InorderPrintTree(Node->Right);
}
```
- 후위 순회를 이용한 트리 출력
```
void SBT_PostorderPrintTree(SBTNode* Node){
     if(Node == NULL) return;
     
     /*왼쪽 하위 트리 출력*/
     SBT_PostorderPrintTree(Node->Left);
     
     /*오른쪽 하위 트리 출력*/
     SBT_PostorderPrintTree(Node->Right);
     
     /*루트 노트 출력*/
     printf(" %c", Node->Data);
}
```

- 후위 순회를 응용한 트리 소멸 함수
  - 트리를 생성할 때의 순서는 상관 없지만 소멸할 때는 반드시 잎 노드부터 해제해야 한다.
  - 잎 노드부터 방문하여 루트까지 거슬러 올라가며 방문하는 후위 순회를 이용하면 이진 트리를 문제 없이 소멸시킬 수 있다.
```
/*트리 소멸 함수*/
void ET_DestroyTree(SBTNode* Node){
     if(Node == NULL) return;
     
     /*왼쪽 하위 트리 소멸*/
     ET_DestroyTree(Node->Left);
     
     /*오른쪽 하위 트리 소멸*/
     ET_DestroyTree(Node->Right);
     
     ET_DestroyNode(Node);
}
```
```
/*노드 소멸 함수*/
void ET_DestroyNode(SBTNode* Node){
     free(Node);
}
```
# 알고리즘
## 5. 정렬
### 5-1 버블 정렬(Bubble Sort)
- 데이터를 정렬하는 과정이 수면을 올라오는 거품의 모습과 비슷해서 붙여진 이름
- 집합 내의 이웃 요소들끼리의 교환을 통해 정렬을 수행
- 비교 연산이 많아 비효율적이기 때문에 실제로 사용하기에는 조금 무리가 있다.
- 하지만 구현이 간단해서 버그가 생길 가능성이 적기 때문에 쓰는 경우도 있다.

```
/*버블 정렬 구현*/
void BubbleSort(int DataSet[], int Length){
     int i = 0;
     int j = 0;
     int temp = 0;
     
     /*길이보다 1회 적게 루프를 돈다*/
     for(i=0;i<Length-1;i++){
     
       /*정렬을 할때마다 한 번씩 줄어든다*/
       for(j=0;j<Length-(i+1);j++){
         
         /*값을 비교해서 바꾼다*/
         if(DataSet[j]>DataSet[j+1]){
           temp = DataSet[j+1];
           DataSet[j+1] = DataSet[j];
           DataSet[j] = temp;
         }
       }
     }   
}
```
