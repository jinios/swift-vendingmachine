## 미션 진행과정 - Daily

- 2018.01.26 - step1 요구사항에 대한 구현 : Beverage클래스와 각 음료 클래스(Milk, Soft Drink…)생성, 상속관계로 구현
- 2018.01.27 - 피드백에 따른 수정 : MyDate 객체 생성
  - `Date`타입을 입력하거나 출력할때마다 `DateFormatter()`객체를 사용해야하고, 매번 같은 문자열 `"yyyyMMdd"`포맷을 사용해야하기때문에 객체로 만들어서 입력은 `String`으로만 입력하면 `Date`가 생성되고 그 포맷에 따라 출력되도록 설계.
- 2018.01.28 - step2 요구사항에 대한 구현 : Attribute 프로토콜 구현, UnitTest코드 추가
    - Attribute 프로토콜 : 음료 객체들이 구현해야할 음료의 특징을 나타내는 함수 추가하고 Beverage가 Attribute를 준수하도록 설계
    - Package enum 추가 - Attibute 프로토콜의 package()함수의 리턴값으로 사용하기위해 enum타입 생성
    - Beverage extension 에 Attribute표시하고 오버라이드하려고했더니 안됨ㅠ 스택오버플로우 참고 https://stackoverflow.com/questions/38213286/overriding-methods-in-swift-extensions
    - 유통기한을 계산해서 valid한 상품인지 아닌지를 판단하기 위해, 음료 구조체에 expiration() 함수를 구현, MFDDate타입인 MyDate 객체 내부에서 '오늘(프로그램 실행일)'의 날짜와 MFDDate비교하는 함수 구현함


- 2018.02 - step3, 4 요구사항에 대한 구현: 코드스쿼드 방학기간이라 혼자 단계별로 미션 진행함
  - 어려웠던 부분 : 클래스 상속 관계설정, 슈퍼클래스와 서브클래스 간의 init()활용,
                음료수를 콘솔에 표시하는 과정에서 번호와 함께 표시하는 기능(음료수를 구매하거나 삭제하는 기능을 위해서는 번호로 입력받은 값을 음료수 객체와 연결해야하는데 그 번호를 음료와 함께 표시하고 매칭하는 기능)
- 2018.03.05 - step4 피드백에 따른 수정 :
  - Attribute 프로토콜 제거
    - 음료 속성(칼로리,용기 등)을 Attribute 프로토콜로 속성을 묶어서 표현했는데, 슈퍼클래스가 프로토콜을 구현하고 있어도 서브클래스가 해당 속성을 구현하도록 강제할 수도 없는 문제.(슈퍼클래스가 Attribute를 구현하고 있으니 컴파일 에러나지않음.)  
    - `init()` / `super.init()`에 속성을 넣고 서브클래스도 해당 속성을 갖게 강제하게 만들었고, 그 속성들을 각 클래스에서 `private`으로 감쌀 수 있음
  - 음료 속성들을 단순 `Bool`에서 `Int`로 변경
  - Controller에서의 사용자 입력값 수정
    - Controller에서 실행되는 모든 mode와 동작옵션 선택을 enum으로 변경함
    - 사용자 input값 튜플로 변경
- 2018.03.06 - step4 피드백에 따른 수정 :
  - itemCode, matchKey() 제거 : 음료수와 번호를 매칭하기위해 음료 객체에 추가한 속성 itemCode를 제거하고, Stock이 가지는 inventory의 key값만 배열로 따로 관리하고 그 배열의 인덱스를 이용해서 번호 표시 & 번호 매칭
  - Shelf()구조체 추가 : inventory의 key값만 배열로 따로 관리하는 객체 추가, `[Objectidentifier]`의 index값을 입출력에 사용한다.
- 2018.03.07 - step4 피드백에 따른 수정 :
  - admin모드 동작 수정 : 음료 추가와 삭제때 사용되는 index가 사용자 모드와 다르기때문에 분리
  - AdminController분리해서 구현. admin모드에서 필요한 코드가 길어져서 분리.
  - 프로그램에서 사용하는 Enum과 Description을 파일을 분리하여 관리- CustomEnum, ProgramDescription 파일
  - OutputView에서 ProgramDescription파일에 저장된 문자열만 출력 할 수 있도록 수정
- 2018.03.08 - step4 피드백에 따른 수정 : Money/History/Stock객체 생성 & 리팩토링
  - 의미있는 속성이라면 최대한 객체를 분리하는 구조로 짜야함. 객체 자기 자신의 속성일지라도, 그 속성에 접근해서 그 속성을 조작하는 동작을 많이 하고있으면 해당 속성도 다른 객체로 분리해야함.
  - Stock 객체를 Stock(기존 Stock의 inventory)과 StockController로 나눔.
  - SwiftLint적용
