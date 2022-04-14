# 1. 객체지향이란
- 1:1로 대응하는 개념은 아니지만 실세계의 모방
- 시스템을 상호작용 하는 자율적인 객체들의 공동체이다.
- 역할, 책임, 협력은 객체지향에서 가장 중요한 개념이다.
  - 협력은 요청(request)과 응답(response)으로 구성 돼있다.
- 객체의 역할
  - 여러 사람이 동일한 역할을 수행할 수 있다.
  - 역할은 대체 가능성을 의미 한다.
  - 책임을 수행하는 방법은 자율적으로 선택할 수 있다
  - 한 사람이 동시에 여러 역할을 수행할 수 있다.
- 객체는 협력적이고 자율적이어야 한다.
- 객체는 상태(state)와 행동(behavior)을 함께 지녀야 한다.
- 객체의 유일한 의사소통 수단 '메시지'
- 객체지향은 클래스 지향이 아니다.
- 중요한건 어떤 클래스가 필요한가가 아니라 **어떤 메시지를 주고 받으며 협력하는가**다.

---

# 2. 객체란
- 객체는 현실의 무언가와 비슷하지만 명백히 다르다.
- 객체는 상태(state), 식별(behavior), 식별자(identity)를 지닌 실체다.
  - 식별자가 없는 단순값들은 객체가 아니다.
  - Property는 객체의 상태를 구성하는 모든 특징을 통틀어 칭하는 것이며, 정적이다.
  - Property value는 상태의 값이며 동적이다.
  - 프로퍼티는 Attribute라는 단순값과 다른 객체를 가리키는 Link로 구분할 수 있다.
- 객체는 자율적인 존재로 다른 객체에 직접적으로 접근할 수도, 상태를 변경할 수도 없다.
  - 캡슐화로 인해 객체내에서 어떤 일이 일어나는지 외부에선 알 수 없다.
  - 노출하는 것은 객체의 행동뿐이며 접근할 수 있는 방법 또한 행동뿐이다.
- 값은 대체로 불변 상태이며 인스턴스의 상태가 같다면 같은 것으로 판단한다.
  - 상태로 두 값이 같은지 판단할 수 있는 성질을 동등성(equality)이라 한다.
- 객체는 가변 상태를 가지며 시간에 따라 변경되는 상태를 포함. 행동을 통해 상태를 변경한다.
  - 식별자를 기반으로 객체가 같은지 판단하는 것을 동일성(identical)이라 한다.
- 객체의 행동을 먼저 결정한 후 상태를 결정하자. 상태를 먼저 결정할 경우 객체의 캡슐화와 재사용성이 저해된다.
  - 객체의 행동에 초점을 맞추자
  - 행동이 상태를 결정한다.
 - 현실 객체의 은유를 적절하게 사용하면 소프트웨어의 구조를 쉽게 예측 가능하고 이해하기 쉬워진다.
- 단, 실제와는 다르다는 사실을 잊지말것

---

# 3. 추상화와 타입
- 추상화란 목적과 부합하지 않는 불필요한 것들을 제거하고 **단순화** 하는 것이다.
  - 공통점을 취하고 차이점을 버려 일반화를 하거나 중요한 부분을 강조하기 위해 불필요한 세부사항을 단순화하는 방법이 있다. 
  - 사람은 현실을 그대로 받아들일만큼 인지능력이 그렇게 뛰어나지 않다.
  - 객체지향에서는 현실의 복잡성을 극복하기 위해 추상화를 한다.
- 그룹으로 나눠 단순화 하라.
  - 공통점을 기반으로 객체를 묶는 그릇을 개념(concept)이라 한다.
  - 개념을 사용하면 객체를 여러 그룹으로 분류할 수 있다.(분류란 객체에 특정한 개념을 적용하는 작업이다.)
- 객체의 정의: **특정한 개념을 적용할 수 있는 구체적인 사물**을 의미하며 개념이 객체에 적용 됐을떄 객체를 개념의 인스턴스라 한다.
- 개념은 특정한 객체가 어느 그룹에 속할 것인지를 결정한다.(아래는 세 가지 관점)
  - 심볼(symbol): 개념을 가리키는 이름이나 명칭
  - 내연(intension): 개념의 정의
  - 외연(extension): 개념에 속하는 모든 객체의 집합
- 타입은 개념이다.
  - 객체가 어떤 타입인지를 결정하는 것은 객체의 행동이다.
  - 객체의 내부표현은 외부로부터 철저하게 감춰진다.
  - 데이터의 표현 방식이나 보유 데이터는 타입에 영향을 미치지 않는다.
- 일반화/특수화 관계
  - 일반적 타입은 포괄적인 개념, 특수한 타입은 일반적 타입보다 특화된 행동을 하는 개념이다.
  - 특수한 타입은 일반적 타입의 부분집합이지만 행동의 가짓수는 더 많다.
  - 따라서 특수한 타입은 일반적 타입이 할 수 있는 행동을 모두 할 수 있다.
  - 객체지향에서 일반적 타입은 슈퍼타입(Supertype), 특수한 타입은 서브타입(Subtype)이라 한다.
  - 서브타입은 슈퍼타입을 대체할 수 있어야 하며 표기시 중복된 행동은 생략이 가능하다.
- 타입의 목적(정적 모델과 동적 모델)
  - 인간의 인지능력으로는 객체의 복잡성을 극복하기 어렵다.
  - 타입은 결국 추상화다.
  - 동적 모델: 객체가 특정 시점에 어떤 상태를 가지는지를 표현하는 것
  - 정적 모델: 객체가 가질 수 있는 모든 상태와 모든 행동을 시간에 독립적으로 표현하는 것
  - 적절히 혼용해서 써라
- 클래스와 타입은 다르다.
  - 클래스는 타입을 구현하는 방식중 하나일 뿐.

---

# 4. 역할, 책임, 협력
- 객체지향의 세계는 동일한 목적을 달성하기 위해 협력하는 객체들의 공동체다.
  - 요청과 응답은 협력에 참여하는 객체가 수행할 책임을 정의한다.
- 어떤 객체가 어떤 요청에 대해 대답해 줄 수 있거나 적절한 행동을 할 의무가 있는 경우 해당 객체가 책임을 가진다고 말한다.
  - 어떻게 구현할 것인가는 객체와 책임을 할당한 뒤에 생각해도 늦지 않다.
  - 객체의 책임은 무엇을 아는가(knowing), 무엇을 할 수 있는가(doing)로 구성된다.
  - 책임은 설계의 품질을 결정하는 가장 중요한 요소다.
  - 책임은 객체의 공용 인터페이스를 구성한다.(캡슐화)
- 역할은 협력 내에서 다른 객체로 대체할 수 있다.
  - 역할은 협력의 추상화라 할 수 있다.
  - 역할을 수행만 가능하다면 어떤 객체라도 참여할 수 있다.
  - 객체지향에서 역할 대체가 가능한 객체는 동일한 메시지를 이해할 수 있는 객체라는 뜻이다.
  - 따라서 역할은 본질적으로 다른 객체에 의해 대체 가능함을 의미한다.(행위 호환성)
  - 그러나 주어진 책임 이외에 다른 책임도 수행할 수 있다.
- 데이터나 클래스 중심으로 설계를 하는 것은 바람직하지 않다.
  - 책임(행동)을 결정한 뒤에 데이터를 고민하라.
  - 클래스 구현 방법은 이보다 더 뒤다.
  - 먼저 협력을 설계하고 어떤 책임이 필요한지 고려하라. 그리고 객체에게 책임을 할당하라.
- 설계 기법
  - 책임-주도 설계(Responsibility-Driven Design): 협력에 필요한 책임들을 식별하고 적합한 객체에게 책임을 할당하는 방식
    - 시스템의 책임을 객체의 책임으로. 각 객체는 협력자를 찾아 다시 책임을 할당하는 순차적인 방식으로 협력 공동체를 구축
    - 객체의 개별적인 상태가 아니라 객체의 책임과 상호작용에 집중
  - 디자인 패턴(Design Pattern): 자주 사용하는 해결 방법인 설계 템플릿을 모아놓은것
    - 해결하려는 문제가 무엇인지를 명확하게 서술하고 패턴을 적용할 수 있는 상황과 적용할 수 없는 상황을 함께 설명한다.
  - 테스트-주도 개발: 테스트를 통과하기 위한 최소한의 코드를 작성한뒤에 테스트를 통과하면 성공한 코드를 리팩토링을 한다.
    - 초보 개발자들이 어렵다고 느끼는 이유는 객체지향에 대한 심도 깊은 이해(역할, 책임, 협력에 대한)가 부족한 것
    - 근데 이해가 있어도 경험이 없으면 어려운게 맞다.
    - 책임-주도 설계의 기본적인 개념을 따른다.
    - 결과적으로 객체지향의 깊은 이해와 감각, 경험이 있어야만 적용할 수 있는 설계 기법이다.

---

# 5. 책임과 메시지
- 적절하게 자율적인 책임의 분배가 설계의 품질을 결정한다.
  - 지나치게 상세한 책임은 객체의 자율성을 저해한다.
  - 그렇다고 의도가 흐릿할만큼 포괄적이고 추상적인 책임 또한 좋지 않다.
  - *상황에 따라 적절하게 선택하자.
- **메시지는 객체의 유일한 소통 수단**이며 이 메시지를 수신한다는건 해당 객체가 이 메시지에 대한 책임을 수행할 수 있다는걸 의미한다.
- 자율적인 책임의 특징은 어떻게(how) 해야하는가가 아니라 무엇이(what) 해야하는가를 설명하는 것.
  - 어떻게 하는지는 객체가 자율적으로 할 수 있게 해야한다.
  - 책임을 수행하는 것을 메서드고 이 메서드를 객체가 스스로 선택할 수 있게 하는것이 자율성이다.
- 다형성은 서로 다른 유형의 객체가 동일한 메시지에 대해 서로 다르게 반응하는 것을 말한다.
  - 하나의 메시지와 하나 이상의 메서드 사이의 관계로도 볼 수 있다.
  - 쉽게 말해 하나의 요청에 각각의 객체가 서로 다르게 반응하는 것이다.
  - 다형성은 곧 동일한 역할을 수행하는 객체들 사이의 대체 가능성을 의미한다.
  - 설계를 유연하고 재사용 가능하게 만드는게 이 특징이 객체지향 패러다임을 강력하게 한다.
- 메시지를 중심으로 협력 설계를 하라
  - 훌륭한 객체지향 설계는 어떤 객체가 어떤 메시지를 전송할 수 있는가와 어떤 객체가 어떤 메시지를 이해할 수 있는가를 중심으로 객체 사이의 협력 관계를 구성하는 것이다.
  - 독립된 객체의 상태와 헹위에 대해 고민하지말고 객체가 다른 객체에게 제공해야 하는 메시지에 대해 고민하라.
- What/Who 사이클은 책임-주도 설계에서 필요한 기법으로 어떤 행위(메시지)가 필요한지 먼저 결정한 후에 수행할 객체를 선택하는 것이다.
- **'묻지말고 시켜라'** 스타일
  - 송신자는 수신자가 어떤 객체인지는 모르지만 잘 처리할 것이라 믿고 메시지를 전송한다.
  - 객체는 다른 객체의 결정에 간섭하지 말아야하고 모든 객체는 자신의 상태를 기반으로 결정을 내려야 한다.
  - 이 스타일은 객체를 자율적으로 만들고 캡슐화를 보장하며 결합도를 낮게 유지해주어 설계를 유연하게 만든다.
- 인터페이스: 어떤 두 사물이 마주치는 경계지점에서 서로 상호작용할 수 있게 이어주는 방법이나 장치를 의미한다.
  - 특징 1: 사용법만 익히면 내부구조나 동작 방식을 몰라도 상관 없다.
  - 특징 2: 내부 구성이나 작동 방식을 변경하는 것은 사용자에게 어떤 영향도 미치지 않는다.
  - 특징 3: 인터페이스만 동일하면 어떤 대상과도 상호작용할 수 있다.
  - 객체끼리의 상호작용에 유일한 수단은 메시지이므로 메시지가 인터페이스를 결정한다.
  - 공용 인터페이스는 내부에서 접근 가능한 인터페이스와 구별하기 위하여 외부에 공개된 인터페이스를 말한다.
  - 공용 인터페이스를 구성하는 것은 객체가 외부로부터 수신할 수 있는 메시지의 목록
- 구현(Implementation): 객체를 구성하지만 공용 인터페이스에 포함되지 않는 모든 것
- 인터페이스와 구현의 분리 원칙: 객체 외부에 노출되는 인터페이스와 객체 내부에 숨겨지는 구현을 명확하게 분리해서 고려해야 함
  - 이는 변경을 관리하기 위한 것이며 변경이 될만한 부분을 객체의 내부에 숨겨 놓는다는 것을 의미한다.
  - 이 원칙을 수행하기 위한 객체 설계 방법을 캡슐화라 한다.
- 캡슐화: 객체의 자율성을 보존하기 위해 구현을 외부로부터 감추는 것
  - 정보 은닉(Information hiding)이라 부르기도 한다.
  - 상태와 행위의 캡슐화(데이터 캡슐화): 상태와 행동을 객체 내부에 보관. 인터페이스와 구현을 분리하기 위한 전제조건
  - 사적인 비밀의 캡슐화: 외부의 객체가 자신의 내부 상태를 직접 관찰하거나 제어할 수 없도록 하기 위해 공용 인터페이스로만 노출한다.

---

# 6. 객체지도
- 기능 측면의 설계: 제품이 사용자를 위해 무엇을 할 수 있는지
- 구조 측면의 설계: 제품의 형태가 어떠해야 하는지
- 변경을 수용할 수 있는 유연한 소프트웨어를 위해 기능이 아닌 안정적 객체 구조를 중심으로 설계하라
- 구조와 기능이라는 두 가지 재료
  - 구조: 사용자나 이해관계자들이 도메인에 관해 생각하는 개념과 개념들간의 관계
  - 기능: 사용자의 목표를 만족 시키기 위해 책임을 수행하는 시스템의 행위
- 도메인 모델링: 구조를 수집하고 표현하기 위한 기법
  - 도메인은 사용자가 프로그램을 사용하는 대상 분야를 말한다.
  - 모델링 활동의 결과물을 도메인 모델이라고 하며 사용자가 프로그램을 사용하는 대상영역에 관한 지식을 선택적으로 단순화하고 의식적으로 구조화한 형태다.
  - 도메인 모델은 사람들의 머릿속에 있는 공유된 멘탈 모델이다.
  - 도메인 모델과 코드는 밀접한 연관이 있는데 객체지향은 변경된 코드로부터 자연스럽게 도메인 모델의 변경을 유추할 수 있게 한다.

- 유스케이스 모델링: 기능을 수집하고 표현하기 위한 기법
  - 사용자의 목표를 달성하기 위해 사용자와 시스템 간에 이뤄지는 상호작용의 흐름을 텍스트로 정리한 것을 유스케이스라 한다.
  - 모델링 활동의 결과물을 유스케이스 모델이라고 한다.
  - 사용자의 목표를 중심으로 시스템의 기능적인 요구사항들을 이야기 형식으로 묶을 수 있다.
  - 하나가 아닌 여러 시나리오의 집합이다. 여기서 시나리오를 유스케이스 인스턴스라고 한다.
  - 인터페이스와 관련된 세부 정보, 내부설계와 관련된 정보를 포함하지 않는다.
- 도메인 모델이 안정적인 이유는 비즈니스가 없어지거나 완전히 개편되지 않는 한 안정적으로 유지되기 때문이다.
- 연결완전성: 도메인 모델링에서 사용한 객체와 개념을 프로그래밍 설계의 객체와 클래스로 변환이 가능한 것.
- 가역성(reversibility): 연결완전성과 반대로 코드에서 모델로 전환이 가능한 것.

---

# 7. 정리
- 객체지향 안에 존재하는 세 가지 상호 연관된 관점
  - 개념 관점(Conceptual Perspective): 설계는 도메인 안에 존재하는 개념과 개념들 사이의 관계를 표현한다.
  - 명세 관점(Specification Perspective): 소프트웨어로 옮겨가 객체가 '무엇'을 할 수 있는가에 초점을 맞춘다.
  - 구현 관점(Implementation Perspective): 객체들이 책임을 수행하는데 필요한 동작하는 코드를 작성하는 것
  - *인터페이스와 구현을 분리하라
- 추상화 기법
  - 분류와 인스턴스화: 객체의 구체적인 세부사항을 숨기고 인스턴스 간에 공유하는 공통적인 특성을 기반으로 범주를 형성하는 과정. 역은 범주로부터 객체를 생성하는 인스턴스화(예시) 과정이다.
    - ex) 바퀴가 네 개 달린 운송수단을 자동차라고 칭하는 것.
    - 범주로 묶는 것은 객체들의 특정 집합에 공통의 개념을 적용하는 것. 객체에 개념을 적용하는 과정을 분류라고 한다.
    - 객체지향에서 타입은 곧 개념을 의미한다.
    - 객체가 어느 한 시점에 하나의 타입에만 속할 경우 단일 분류(single classification), 여러 타입에 속할 경우 다중 분류(multiple classification)라고 한다.(하지만 대부분의 객체지향 언어는 단일 분류만 지원한다.)
    - 객체가 한 집합에서 다른 집합의 원소로 자신이 속하는 타입을 변경할 수 있는 경우 동적 분류(dynamic classfication)라 하고 변경할 수 없는 경우 정적 분류(static classfication)라고 한다.(하지만 대부분의 언어는 정적 분류만 가능하다.)
    - 객체에는 핵심적이고 필수불가결한 본질적인 속성(essence)과 본질적이지 않은 우연적인 속성(accidental)이 존재한다. (하지만 대부분의 객체지향 언어는 우연적인 속성은 표현할 수 없다.)
  - 일반화와 특수화: 범주 사이에 차이를 숨기고 범주 간에 공유하는 공통적인 특성을 강조. 역을 특수화라고 한다.
    - ex) 고양이를 포유류의 육식동물과로 분류하는 것.
    - 어떤 타입이 다른 타입보다 일반적이라면 슈퍼타입(supertype), 어떤 타입이 다른 타입보다 특수하다면 서브타입(subtype)이라고 부른다.
    - 서브타입은 슈퍼타입이 가진 본질적인 속성과 함께 추가적인 속성을 가진다.
    - 일반화의 원칙에 따르면 한 타입이 다른 타입의 서브타입이 되기 위해서는 슈퍼타입에 순응해야하는데 순응은 서브타입의 슈퍼타입에 대한 대체가능성을 의미하며 이는 2가지가 있다.
      - 구조적인 순응(structural conformance): 서브타입은 슈퍼타입이 갖고 있는 속성과 연관관계 면에서 100% 일치해야 한다. Person이 name 속성을 갖고 있다면 서브타입인 Employee 역시 name 을 갖고 있다고 기대할 수 있으며 따라서 대체할 수 있다.
      - 행위적인 순응(behavioral conformance): 서브타입은 슈퍼타입을 행위적으로 대체 가능해야 한다. Person이 getAge()에 대한 메세지로 나이를 반환한다면 Employee 역시 해당 메소드에 대해 나이를 반환해야하고 따라서 대체할 수 있다.
    - 상속은 서브타이핑(subtyping)과 서브클래싱(subclassing) 2가지 용도로 사용될 수 있다.
      - 서브클래스가 슈퍼클래스를 대체할 수 있을 경우 이를 서브타이핑이라 부르며 설계의 유연성이 목표이다. 인터페이스 상속(interface inheritance)이라고 한다.
      - 서브클래스가 슈퍼클래스를 대체할 수 없을 경우 이를 서브클래싱이라 부르며 코드 중복 제거와 재사용이 목적이다. 구현 상속(implementation inheritance)이라고 한다.
      - 이에 대한 여부는 상속만으로는 알 수 없고 클라이언트 관점에서 실제로 어떻게 사용되는가로 구분할 수 있다.
    - 어떤 객체의 클래스가 수신된 메세지를 이해할 수 없다면 메세지를 클래스의 부모 클래스로 위임하는데 이는 이해될때까지 상위 클래스로 위임된다. 이를 delegation(위임)이라 한다.
  - 집합과 분해: 부분과 관련된 세부 사항을 숨기고 부분을 사용해서 전체를 형성하는 과정. 반대는 전체를 부분으로 분리하는 분해 과정이다.
