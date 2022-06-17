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
### 5-2 삽입 정렬(Insertion Sort)
- 데이터 집합을 순회하면서 정렬이 필요한 요소를 뽑아내 다시 적당한 곳에 삽입해 나가는 정렬. 트럼프 카드를 순서대로 정리하는 모습을 생각하자 
- 버블 정렬과 마찬가지로 구현이 간단해서 많이 쓰지만 성능도 비슷하다..
- 정렬이 되어있을 경우에는 비교 연산을 수행하지 않기 때문에 비교 연산을 반드시 수행하는 버블 정렬과 달리 상황에 따라 더 나은 성능을 내기도 한다. 데이터 집합의 크기가 작다면 삽입 정렬을 쓰자
- 삽입 정렬의 과정
  - 1. 정렬 대상이 되는 요소들을 선택한다. -> 왼쪽에서부터 선택해나가며 범위가 처음에는 2개지만 반복 횟수가 늘어날 때마다 1개씩 커진다. 최대 범위는 '데이터 집합의 크기 -1'이 된다.
  - 2. 정렬 대상의 가장 오른쪽에 있는 요소가 정렬 대상 중 가장 큰 값을 갖고 있는지 확인한다. 만약 그렇지 않다면 이 요소를 정렬 대상에서 뽑아 위치할 적절한 곳을 정렬 대상 내에서 찾는다.  여기서 적절한 곳이란 데이터 집합의 가장 왼쪽을 기준으로 했을 때 자신보다 더 작은 요소가 없는 위치를 말한다.
  - 3. 요소를 삽입할 적절한 곳을 찾았다면 정렬 대상 내에서 삽입할 값보다 큰 값을 갖는 모든 요소를 한 자리씩 오른쪽으로 이동시키고 새로 생긴 빈 자리에 삽입한다.
  - 4. a~c의 과정을 반복

```
void InsertionSort(int DataSet[], int Length){
   int i = 0;
   int j = 0;
   int value = 0;
   
   for(i = 1;i<Length;i++){
     /*정렬할 필요가 없다면 비교 연산을 수행하지 않음*/
     if(DataSet[i-1] <= DataSet[i])
       continue;
      
     value = DataSet[i];
     
     /*요소를 삽입할 공간을 찾는다*/
     for(j=0;j<i;j++){
       if(DataSet[j] > value){
         memmove(&DataSet[j+1], &DataSet[j], sizeof(DataSet[0]) * (i-j)); //메모리의 내용을 이동시키는 함수. 순환문으로 대체 가능하다
         DataSet[j] = value;
         break;
       }
     }
   }
}
```

### 5-3 퀵 정렬(Quick Sort)
- 전쟁 전략 중 하나인 분할 정복(Divide and Conquer)에 기반한 알고리즘
- 퀵 정렬의 과정
  - 1. 데이터 집합 내에서 임의의 기준 요소를 선택하고 기준 요소보다 작은 요소들은 순서에 관계없이 기준 요소의 왼편, 큰 값은 오른편에 위치시킨다.
  - 2. 이렇게 나눈 데이터 집합들을 다시 a와 마찬가지로 임의의 기준 요소를 선택해 같은 방법으로 데이터 집합을 분해한다.
  - 3. a와 b의 과정을 데이터 집합을 나눌 수 없을 때까지 반복한다.
- 기준 요소를 선택할때 무작위로 선택 하는 방식이 있으나 난수를 뽑는 과정에서 성능 저하가 있을 수 있다. 그래서 그냥 중간값을 지정하는 것이 제일 낫다.
- 퀵 정렬은 데이터 집합이 어떻게 정렬 돼있느냐에 따라 성능이 달라지는데 데이터가 이미 정렬되어 있거나 역순으로 정렬되어 있을땐 최악의 성능을 보이지만 무작위로 흩어져 있을 경우엔 최고의 정렬이다.(최악일 땐 버블 정렬, 삽입 정렬과 비슷하다)

```
/*요소를 바꾸는 함수*/
void Swap(int* A, int* B){
  int Temp = *A;
  *A = *B;
  *B = Temp;
}

/*인덱스를 받아 정렬하는 함수*/
int Partition(int DataSet[], int Left, int Right){
  int First = Left;
  int Pivot = DataSet[First]; //피벗은 배열의 가장 첫 번째 값으로 지정
  
  ++Left;
  
  while(Left <= Right){
    while(DataSet[Left] <= Pivot && Left < Right)
      ++Left;
    while(DataSet[Right] > Pivot && Left < Right)
      --Right;
    
    if(Left < Right)
      Swap(&DataSet[Left], &DataSet[Right]);
    else
     break;
  }
  
  Swap(&DataSet[First], &DataSet[Right]);
  
  return Right;
}

void QuickSort(int DataSet[], int Left, int Right){
  if(Left<Right){
    int Index = Partition(DataSet, Left, Right);
    
    /*재귀 호출*/
    QuickSort(DataSet, Left, Index-1);
    QuickSort(DataSet, Index+1, Right);
  }
}
```
## 6. 탐색
### 6-1 순차 탐색(Sequential Search)
- 데이터 집합의 처음부터 끝까지 차례대로 모든 요소를 비교해서 데이터를 찾는 탐색 알고리즘
- 한쪽 방향으로만 탐색을 수행한다고 해서 선형 탐색(Linear Search)이라고 부르기도 한다.
- 처음부터 모든 요소를 검사하기 때문에 효율이 나쁘다.
- 하지만 정렬되어 있지 않은 데이터 집합 속에서 원하는 데이터를 찾을 수 있는 유일한 방법이며 구현이 간단해 버그가 생길 가능성이 적기 때문에 높은 성능이 필요치 않거나 데이터 집합의 크기가 작은 곳에 자주 사용된다.
- 배열이나 링크드 리스트일 때 모두 사용 가능한 알고리즘이다.

```
/*링크드 리스트를 이용한 순차 탐색*/
Node* SLL_SeqeuntialSearch(Node* Head, int Target){
  Node* Current = Head;
  Node* Match = NULL;
  
  /*노드를 순회하며 찾는 값을 가진 노드를 탐색해 반환*/
  while(Current != NULL){
    if(Current->Data == Target){
      Match = Current;
      break;
    }
    else
      Current = Current->NextNode;
  }
  
  return Match;
}
```

### 6-2 자기 구성 순차 탐색(Self-Organizing Sequential Search)
- 자주 사용하는 항목을 데이터 집합의 앞쪽에 배치하여 순차 탐색의 효율을 올리는 방법
- 자주 사용 되는 항목을 어떻게 선별하는가는 3가지 방법이 있다.
#### 6-2 a. 전진 이동법(Move To Front)
- 한 번 탐색된 항목을 데이터 집합의 가장 앞에 위치시키는 방법
- '최근 문서' 기능과 동일한 원리로 작동한다.
- 특정한 항목들이 집중적으로 탐색 대상이 되는 것은 흔한 일이 아니기 때문에 모든 경우에 적합한 것은 아니다.
- 한 번 탐색된 항목이 곧 이어서 또 다시 검색될 가능성이 높은 데이터 집합에서만 사용해야 한다.

```
Node* SLL_MoveToFront(Node** Head, int Target){
  Node* Current = (*Head);
  Node* Previous = NULL;
  Node* Match = NULL;
  
  while(Current != NULL){
    /*찾는 값을 갖고 있는 노드를 검색해 Match에 저장/
    if(Current->Data == Target){
      Match = Current;
      
      if(Previous != NULL){
        /*자신의 앞 노드와 다음 노드를 연결*/
        Previous->NextNode = Current->NextNode; //찾은 노드의 다음 노드를 이전 노드와 연결
        
        /*자신을 리스트의 가장 앞으로 이동/
        Current->NextNode = (*Head); //찾은 노드를 헤드의 앞으로 이동
        (*Head) = Current; //헤드를 찾은 노드로 설정
      }
      break;
    }
    else{
      Previous = Current; //이전 노드를 저장
      Current = Current->NextNode;
    }
  }
  return Match;
}
```

#### 6-2 b. 전위법(Transpose)
- 탐색된 항목을 바로 이전 항목과 교환한다는 것 말고는 기본적으로 전진 이동법과 같은 알고리즘
- 전진 이동법과 다르게 '자주' 탐색된 항목을 점진적으로 앞으로 옮긴다.

```
Node* SLL_Transpose(Node** Head, int Target){
  Node* Current = (*Head);
  Node* PPrevious = NULL;
  Node* Previous = NULL;
  Node* Match = NULL;
  
  while(Current != NULL){
    /*해당 노드를 찾았을 경우*/
    if(Current->Data == Target){
      Match = Current;
      /*헤드 노드가 찾는 노드일 경우를 위한 if문*/
      if(Previous != NULL){
        if(PPrevious != NULL)
          PPrevious->NextNode = Current; //전전노드의 다음 노드를 현재 노드로 가리킴
        /*2번째 노드가 찾는 노드일 경우*/
        else
          (*Head) = Current; //찾는 노드를 헤드로 변경
          
        Previous->NextNode = Current->NextNode; //전노드가 가리키는 노드를 찾는 노드의 다음 노드로 변경
        
        Current->NextNode = Previous; //찾는 노드의 다음 노드를 전노드로 변경
        }
        break; //수행할 경우 탈출. 헤드면 노드만 찾고 바로 탈출한다
    }
    /*찾지 못했을 경우*/
    else{
      if(Previous != NULL)
        PPrevious = Previous; //이전 노드를 더 앞으로
      Previous = Current; //현재 노드를 이전 노드로
      Current = Current->NextNode; //다음 노드를 현재 노드로
    }
  }
  return Match;
}
```

#### 6-2 c. 빈도 계수법(Frequency Count)
- 집합 내의 각 요소들이 탐색된 횟수를 별도의 공간에 저장해 두고 탐색된 횟수가 높은 순으로 데이터 집합을 재구성하는 알고리즘
- 계수 결과를 저장하는 별도의 공간을 유지해야 하고 계수 결과에 따라 데이터 집합을 재배치해야 하는 등 비용이 더 많이 소모된다.

### 6-4 이진 탐색(Binary Search)
- 정렬된 데이터 집합에서 사용할 수 있는 고속 탐색 알고리즘
- 이진 탐색이라는 이름이 붙은 이유는 탐색 범위를 1/2씩 줄여나가는 방식이라 그런 것
- 수행 과정
  - 1. 데이터 집합의 중앙에 있는 요소를 선택
  - 2. 중앙 요소의 값과 찾고자 하는 목표 값을 비교
  - 3. 목표 값이 중앙 요소의 값보다 작다면 중앙을 기준으로 데이터 집합의 왼편에 대해 새로 검색을 수행하고 크다면 오른편에 대해 새로 검색을 수행한다.
  - 4. 찾을때까지 a~c를 반복한다.
- 뛰어난 성능에 비해 구현이 굉장히 간단한 편이다.
```
ElementType BinarySearch(ElementType DataSet[], int Size, ElementType Target){
  int Left, Right, Mid;
  
  Left = 0;
  Right = Size - 1;
  
  /*찾을때까지 반복*/
  while(Left <= Right){
    /*미드를 배열의 중앙값으로 설정*/
    Mid = (Left + Right)/2;
    
    /*데이터 일치시 반환*/
    if(Target == DataSet[Mid])
      return DataSet[Mid];
    
    /*오른쪽에 있다면 Left 값을 재설정*/
    else if(Tatget > DataSet[Mid])
      Left = Mid + 1;
    
    /*왼쪽에 있다면 Right 값을 재설정*/
    else
      Right = Mid - 1;
  }
  return NULL;
}
```

### 6-5 이진 탐색 트리(Binary Search Tree)
- 이진 탐색을 위한 이진 트리다.
- 이진 탐색은 데이터 집합이 배열인 경우에만 사용할 수 있기에 해당 사항이 없다.
- 동적으로 크기가 달라지는 데이터 집합인 링크드 리스트로 이루어진 이진 트리는 한 번에 데이터의 중앙 요소에 접근할 수 없기에 이진 탐색이 불가능하다.
- 이진 탐색 트리가 다른 이진 트리와 다른 점은 '왼쪽 자식 노드는 나보다 작고, 오른쪽 자식 노드는 나보다 크다.'라는 규칙을 갖고 있다는 것이다.
```
/*이진 탐색 트리에서 이진 탐색*/
BSTNode* BST_SearchNode(BSTNode* Tree, ElementType Target){
  if(Tree == NULL) return NULL;
  
  if(Tree->Data < Target) //작다면 왼쪽으로
    return BST_SearchNode(Tree->Left, Target);
  else if(Tree->Data > Target) //크다면 오른쪽으로
    return BST_SearchNode(Tree->Right, Target);
  else
    return Tree;
}
```

```
/*이진 탐색 트리에서 노드 삽입*/
void BST_InsertNode(BSTNode** Tree, BSTNode *Child){
  /*새 노드가 현재 노드보다 큰 경우*/
  if((*Tree)->Data < Child->Data){
    if((*Tree)->Right == NULL)
      (*Tree)->Right = Child;
    else
      BST_InsertNode(&(*Tree)->Right), Child);
  }
  /*새 노드가 현재 노드보다 작은 경우*/
  else if((*Tree)->Data > Child->Data){
    if((*Tree)->Left == NULL)
      (*Tree)->Left = Child;
    else
      BST_InsertNode(&(*Tree)->Left, Child);
  }
}
```

- 노드 삭제는 2가지 경우의 수가 있기 때문에 조금 까다로운 편이다.
- 첫 번째로 양쪽 자식 노드를 모두 갖고 있는 경우는 삭제된 노드의 하위 트리에서 가장 작은 값을 가진 노드를 삭제된 노드의 위치에 옮겨 놓는다.
- 두 번째로 한쪽 자식 노드만 갖고 있는 경우는 삭제되는 노드의 자식을 삭제되는 노드의 부모에게 연결 시켜준다.
```
/*이진 탐색 트리에서 노드 삭제*/
BSTNode* BST_RemoveNode(BSTNode* Tree, BSTNode* Parent, ElementType Target){
  BSTNode* Removed = NULL;
  
  if(Tree == NULL) return NULL; //트리가 비었다면 바로 종료
  
  /*찾는 노드보다 더 크다면 왼쪽으로*/
  if(Tree->Data > Target)
    Removed = BST_RemoveNode(Tree->Left, Tree, Target);
  /*찾는 노드보다 더 작다면 오른쪽으로*/
  else if(Tree->Data < Target)
    Removed = BST_RemoveNode(Tree->Right, Tree, Target);
  /*찾았을 경우*/
  else{
    Removed = Tree;
    
    /*찾은 노드가 자식이 없는 경우*/
    if(Tree->Left == NULL && Tree->Right == NULL){
      if(Parent->Left == Tree) Parent->Left = NULL; //부모의 왼쪽 노드일 경우 초기화
      else Parent->Right = NULL; //부모의 오른쪽일 경우 초기화
    }
    /*자식이 있는 경우*/
    else{
      /*양쪽 다 있을 경우*/
      if(Tree->Left != NULL && Tree->Right != NULL){
        BSTNode* MinNode = BST_SearchMinNode(Tree->Right);
        Removed = BST_RemoveNode(Tree, NULL, MinNode->Data); //MinNode에 대해 BST_RemoveNode() 함수를 호출하는 이유는 이 노드에 대해서도 제거 후의 뒤처리가 필요하기 때문
        Tree->Data = MinNode->Data;
      }
      /*한쪽만 있을 경우*/
      else{
        BSTNode* Temp = NULLl
        if(Tree->Left != NULL) Temp = Tree->Left;
        else Temp = Tree->Right;
        
        if(Parent->Left == Tree) Parent->Left = Temp;
        else Parent->Right = Temp;
      }
    }
  }
  return Removed;
}
```

### 6-6 레드 블랙 트리(Red Black Tree)
- 자가 균형 이진 탐색 트리(Self-Balancing Binary Search Tree)라고도 부른다.
- 노드를 빨간색 또는 검은색으로 표시하기 때문에 색깔을 위한 필드를 따로 필요로 한다. 삽입과 삭제 연산을 위해 부모 노드를 기리키는 포인터도 필요하다.
- 레드 블랙 트리가 균형을 유지하는 방법
 - 모든 노드는 빨간색 아니면 검은색이다.
 - 루트 노드는 검은색이다.
 - 잎 노드는 검은색이다.
 - 빨간 노드의 자식들은 모두 검은색이다. 하지만 검은색 노드의 자식이 빨간색일 필요는 없다.
 - 루트 노드에서 모든 잎 노드 사이에 있는 검은색 노드의 수는 모두 동일하다.
- NIL 노드는 아무 데이터도 갖고 있지 않지만 색깔만 검은색인 더미 노드다. 굳이 사용하는 이유는 '모든 잎 노드는 검은색'이라는 규칙은 확실하게 지킬 수 있기 때문이다.
- 레드 블랙 트리는 이진 탐색 트리이기 때문에 이진 탐색을 그대로 사용하면 된다. 하지만 삽입과 삭제에서 규칙이 무너지기 때문에 삽입과 삭제가 구현이 핵심이 된다.
- 삽입과 삭제 연산 이전에 회전을 먼저 알아야한다.
 - 회전(Rotate)
  - 부모와 자식 노드의 위치를 서로 바꾸는 연산이며 방향에 따라 우회전(Right-Rotate), 좌회전(Left-Rotate)으로 나뉜다.
  - 우회전은 왼쪽 자식과 부모의 위치를 바꾸는 것, 좌회전은 오른쪽 자식과 부모의 위치를 바꾸는 것이다.(방향은 자식이 기준이다.)
  - 왼쪽 자식 노드는 부모 노드보다 작고, 오른쪽 자식은 부모보다 커야 하기 때문에 단순히 바꾸기만 해서는 규칙이 무너져 버린다. 그러므로 다음과 같이 처리한다.
   - 우회전을 할때는 왼쪽 자식 노드의 오른쪽 자식 노드를 부모 노드의 왼쪽 자식으로 연결한다.
   - 좌회전을 할때는 오른쪽 자식 노드의 왼쪽 자식 노드를 부모 노드의 오른쪽 자식으로 연결한다.

## 7. 우선순위 큐와 힙
### 7-1 우선순위 큐
- 우선순위 큐도 큐와 같이 동작하지만 이름처럼 '우선순위' 속성을 갖는 데이터를 다룬다.
- 똑같이 삽입과 제거 연산을 수행하지만 새 요소에 우선순위를 부여해서 큐에 삽입하고 가장 높은 우선순위를 갖는 요소부터 빠져나오도록 한다.
- 우선순위의 기준에 절대적인 것은 없다. 프로그래머의 결정에 따른다.

- 우선순위 큐의 삽입 연산
 - 각 요소는 우선순위를 가지며 요소의 우선순위 오름차순으로 연결된다.
 - 새로 추가되는 요소는 마지막 노드에 추가 되는 것이 아닌 우선순위 값에 따라 순차 탐색으로 삽입된다.
- 우선순위 큐의 제거 연산
 - 전단만 제거해서 반환하면 된다. 정말 별거 없음

### 7-2 힙(Heap)
- 자유 저장소의 그 힙 아님
- 힙 순서 속성(Heap Order Property)을 만족하는 **완전 이진 트리**
- 힙 순서 속성이란 트리 내의 모든 노드가 부모 노드보다 커야 한다는 규칙이다.
- 힙은 루트 노드가 트리 내에서 가장 작은 노드라는 것을 확실히 보장한다. 그러나 자식이 부모보다 커야한다는 조건만 만족하면 되기 때문에 이진 탐색이 되지 않으며 모든 노드를 순회해야 한다.
- 힙에는 새 노드를 삽입하는 연산과 루트 노드를 없애는 최소값 삭제 연산이 있다.
- 새 노드 삽입
 - 힙의 삽입 연산은 3단계를 거친다.
  - 1. 힙의 최고 깊이, 최 우측에 새 노드를 추가한다. 하지만 완전 이진 트리는 유지할 수 있도록 한다.
  - 2. 삽입한 노드를 부모 노드와 비교한다. 삽입한 노드가 부모 노드보다 크면 연산을 종료. 부모 노드보다 작다면 다음 단계를 진행한다.
  - 3. 부모 노드와 삽입한 노드의 위치를 바꾼다. 바꾼 후 2를 다시 진행한다.
 - 새로 추가한 노드가 힙 속성 순서를 만족시킬 때까지 부모 노드와 계속해서 교환해 나가는 것이 핵심.
- 최소값 삭제
 - 힙에서 가장 작은 값은 루트 노드이므로 최소값 삭제는 곧 루트 노드의 삭제를 의미한다.
 - 루트 노드를 삭제한 후의 과정은 다음과 같다.
  - 1. 힙의 루트에 최고 깊이, 최 우측에 있던 노드를 루트 노드로 옮겨오는데 이때 힙의 순서 속성이 파괴된다.
  - 2. 힙 순서 속성 유지를 위해 옮겨온 노드의 양쪽 자식을 비교하여 작은 쪽 자식과 위치 교환을 한다.
  - 3. 옮겨온 노드가 더 이상 자식이 없는 잎 노드가 되거나 양쪽 자식보다 작은 값을 가지는 경우엔 삭제 연산을 종료한다. 그렇지 않다면 2의 과정을 반복한다.
```

```
## 8. 해시 테이블(Hash Table)
- 해시 테이블에서의 해시는 입력 받은 데이터를 완전히 다른 모습의 데이터로 바꾸는 작업이며 주로 해시 테이블이라는 탐색 알고리즘, 암호화(대표적으로 SHA), 데이터 축약에 사용된다.
### 8-1 해시 테이블
- 데이터를 해시해서 테이블 내의 주소로 바꾸는 개념
- 데이터를 담을 테이블을 미리 크게 확보해 놓은 후 입력받은 데이터를 해시하여 테이블 내의 주소를 계산하고 이 주소에 데이터를 담는다.
- 주소값을 얻는 과정만 필요하기 때문에 테이블의 크기와 성능은 전혀 상관이 없고 배열과 동일한 수준의 접근 속도가 나온다.
- 데이터가 입력되지 않은 여유 공간이 많아야 제 성능을 유지할 수 있다.(공간을 팔아 시간을 산다는 개념)
### 8-2 해시 함수(Hash function)
#### 8-2 a. 나눗셈법(Division Method)
- 해시 함수중에서도 가장 간단한 알고리즘으로 *입력 값을 테이블의 크기로 나누고 그 나머지를 테이블의 주소로 사용*한다.
- *주소 = 입력 값 % 테이블의 크기*로 수식을 표현할 수 있다.
- 어떤 값이든 테이블의 크기로 나누면 나머지는 절대 테이블의 크기를 넘지 않는다. 만약 입력 값이 테이블의 크기의 배수 또는 약수인 경우 해시 함수는 0을 반환한다.
- 나눗셈법으로 구현된 해시 함수가 테이블 내의 공간을 효율적으로 사용하기 위해서는 테이블의 크기 n을 소수로 정하는 것이 좋은 성능을 낸다. 특히 2의 제곱수와 거리가 먼 소수.
- 서로 다른 입력 값에 대해 동일한 해시 값(해시 테이블 내의 동일한 주소)을 반환할 가능성이 있는데 이것을 충돌(Collision)이라고 한다.
- 테이블 내의 일부 지역의 주소들을 집중적으로 반환하는 결과로 데이터들이 한 곳에 모이는 문제를 클러스터(Cluster)라고 하는데 나눗셈법은 이 두 문제가 발생할 가능성이 높다.
#### 8-2 b. 자릿수 접기(Digits Folding)
- 자릿수 접기 알고리즘은 충돌과 클러스터 문제를 일으킬 가능성을 줄인 알고리즘이다.
- 자릿수 접기는 종이처럼 각 자릿수 숫자를 접어 일정한 크기 이하의 수의 해시 값으로 만드는 방법이다.
- 문자열을 키로 사용하는 해시 테이블에 잘 어울리는데 문자열의 각 요소를 아스키 코드 번호로 바꾸고 이 값들을 각각 더하여 접으면 문자열을 깔끔하게 해시 테이블 내의 주소로 바꿀 수 있기 때문이다.
- 자릿수 접기 알고리즘으로 해시 값을 만드는 코드는 다음과 같다
```
int Hash(char* Key, int KeyLength, int TableSize){
  int i = 0;
  int HashValue = 0;
  
  /*문자열의 각 요소를 아스키 코드 번호로 변환하여 더한다*/
  for(i = 0 ; i < KeyLength ; i++)
    HashValue += Key[i];
  
  return HashValue % TableSize;
}
```
- 자릿수 접기는 한 가지 문제가 있는데 테이블의 크기에 비해 문자열 키의 최대 길이가 짧다면 너무 많은 수의 주소가 활용되지 않는다는 것이다.
- 이와 같은 문제를 사용되지 않는 비트의 숫자를 계산해 그만큼 왼쪽으로 밀어올린 다음 아스키 코드 번호를 더하는 것으로 해결한다.
- 예시 코드는 해시 테이블 크기가 14비트로 이루어져 있고 해시 함수의 최대 주소는 11비트만 활용하는 것으로 가정한다.
```
int Hash(char* Key, int KeyLength, int TableSize){
  int i = 0;
  int HashValue = 0;
  
  for(i = 0 ; i < KeyLength ; i++)
    HashValue = (HashValue << 3) + Key[i];
  
  return HashValue % TableSize;
```

### 8-3 해시 함수의 충돌 해결
- 해시 함수는 아무리 정교하게 설계되었다고 해도 모든 입력 값에 대해 고유한 해시 값을 만들 수는 없으므로 충돌을 피할 순 없다.
- 이에 대한 해결책으로는 크게 2가지가 있는데 해시 테이블의 바깥에 새로운 공간을 할당해서 해결하는 방법과 주어진 공간 내에서 해결을 하는 것이다.
- 전자를 개방 해싱(Open Hashing), 후자를 폐쇄 해싱(Closed Hashing)이라고 부른다.
#### 8-3 a. 체이닝(Chaining)은 개방 해싱 기반의 충돌 해결 기법
- 해시 함수가 서로 다른 키에 대해 같은 주소값을 반환해서 충돌이 발생하면 각 데이터를 해당 주소에 있는 링크드 리스트에 삽입하여 문제를 해결하는 방식
- 충돌이 일어나면 링크드 리스트에 사슬처럼 주렁주렁 엮는다는 의미에서 붙여진 이름이다.
- 해시 함수가 만들어낸 주소값을 데이터가 직접 사용하지 않고 링크드 리스트가 사용한다는 것 말고는 해시 함수의 역할이 똑같기 때문에 해시 함수를 딱히 수정할 필요는 없다.
- 하지만 삽입 연산은 충돌이 앞으로 '발생할 것'을 고려해서, 삭제 연산과 탐색 연산은 충돌이 이미 '발생했을 것'을 고려해서 설계해야 한다.
- 체이닝 기반 해시 테이블의 탐색
 - 다음과 같은 순서로 탐색을 수행한다.
  - a. 찾고자 하는 목표값을 해싱하여 링크드 리스트가 저장되어 있는 주소를 찾는다.
  - b. 이 주소를 이용하여 해시 테이블에 저장되어 있는 링크드 리스트에 대한 포인터를 생성한다.
  - c. 링크드 리스트의 앞에서부터 뒤까지 차례대로 이동하며 목표값이 저장되어 있는지 비교한다. 목표값과 링크드 리스트 내의 노드 값이 일치하면 해당 노드의 주소를 반환한다.
- 체이닝 기반 해시 테이블의 삽입
 - 해시 함수를 이용해서 데이터가 삽입될 링크드 리스트의 주소를 얻어낸 후에, 링크드 리스트가 비어 있으면 데이터를 바로 삽입하고 그렇지 않은 경우에는 링크드 리스트의 '헤드 앞에' 삽입한다.
 - 헤드 앞에 삽입하는 이유는 만약 새로운 충돌 데이터를 테일로 사용할 경우 순차 탐색으로 테일 노드를 찾아 삽입해야하기 때문이다
 - 만약 충돌 데이터가 많을 경우 탐색 시간이 오래 걸리므로 있던 노드를 밀어내고 새로운 노드를 헤드로 정한다.
 - 체이닝의 성능을 끌어올리는 방법으로 해시 테이블 + 이진 탐색 트리의 결합이 있다.
### 8-3 b. 개방 주소법(Open Addressing)
- 충돌이 일어날 때 해시 함수에 의해 얻어진 주소가 아니더라도 얼마든지 다른 주소를 사용할 수 있도록 허용하는 충돌 해결 알고리즘
- 해시 함수에 의해 얻어진 주소만 사용하는 체이닝은 오픈 해싱 기법인 동시에 폐쇄 주소법(Closed Addressing) 알고리즘
- 개방 주소법은 충돌이 일어나면 해시 테이블내의 새로운 주소를 탐사(Probe)하여 충돌된 데이터를 입력하는 방식으로 동작
-선형 탐사(Linear Probing)
 - 가장 간단한 탐사 방법으로 해시 함수로부터 얻어진 주소에 이미 다른 데이터가 있다면 현재 주소에서 고정 폭으로 다음 주소로 이동한다.
 - 그 주소에도 다른 데이터가 있다면 또 그 다음 주소로 이동하고 이렇게 비어 있는 주소를 찾아내면 그곳에 데이터를 입력한다.
 - 선형 탐사는 클러스터가 매우 잘 발생하며 클러스터가 발생하면 새로운 주소를 찾기 위해 수행하는 선형 탐사 시간이 길어져 해시 테이블 성능이 매우 저하된다.
---끝
