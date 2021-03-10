

## TDD

## 3주차 수업

- 클린코드 왜 중요한가?

  - 컴퓨터가 실행할정도로 엄힐하고 정확하고 상세하게...

  - 비즈니스

  - 클린코드는 생산성을 일정하게 유지하는 것.

  - 클린코드를 지양하는건 초반유지생산성을 일관되게 유지하는 방법

  - 작은수정하는데 2~3일하는게 많이 걸림. 수정하고 테스트하는데 엄청 오래 걸리고 대부분의 팀들은 전면 재개발... 새로운 기존에 코드보다 깔끔하게 짤것 같지만 그렇지 않음

  - 가능한 곳을 레거시를 없애가야함.

  - [ ] 리팩토링하고 클린코드하는 연습을 해야함

  - [ ] 레거시코드를 리팩토링하는 개발자를 요구

  - [ ] 너무 빠르게 만드는 것보다 어떻게 리팩토링해야할지 고민하기

    

  - [ ] UI동작프로세스 보기
  - [ ] 마지막에 안되는부분 보기
  - 내가 클린코드를 어떻게 만들어가는지 알아야지 추후에 개선이 가능함. 모르는 것보다 클린코드에 관심을 가졌으면 좋겠다.
  - 매주마다 1주미션이 이상적. 현실적으로 힘듦 만약 로또를 진행하고있다 우리의 속도가 안된다 그럼 여러분 속도대로 하지. 마지막 5주차에 못했던 미션하기. 남은 기간도 달리면되니깐...
  - 로또를 가지고 TDD로 하라고하면 일단 막막함.
  - 어떻게 접근할 수 있는가? 내가 역량이 쌓이니깐 이부분은 티디디로 구현해야지. 객체지향설계.. 단위테스트... 스텝바이스텝으로 어떻게 할지 그래도 이렇게하면 수월하지 않을까... 
  - Q. 이 로또문제는 몇번째 풀고계신건가요? 피드백을 주면서 라이브코딩하면서 이사이클로 왔다갔다 함. 앞에 코드를 이해해야됨 자고싶다면 이론강의할때 자기. 라이브코딩은
  - TDD설계하기
    - 기능 목록을 작성하기. 기능을 작은 단위로 분리하기 
    - 단위테스트 이런거 하지 말고 막 구현하기.
    - 그러면 프로그램 요구사항능력이 올라감
    - 이렇게되면 기능을 구현하려고할때 기능에대한 이해도가 올라가면 분리를해서 훨씬더 좋아짐.
    - 구현다하고 코드 버리고
    - 기능 목록을 추출
      - 대략적인 초보자일떈 이렇게라도 해야함.
      - ex)구매할 로ㅗㄸ의 매수구하기
        - 1000->1
        - 1500->1
        - 500->error
      - 한장의 로또구하기
      - 당첨 번호 생성
        - 정상적인 당첨번호 입력
        - 유효하지 않은 당첨번호
      - 한장의 Lotto에 대한 당첨 결과 구하기
      - n장의 Lotto에 대한 당첨 결과 구하기
      - Lotto  결과에 따른 수익률 구하기
    - 테스트가 어떤의도로 만든지 알려주는게 더 중요해서 한글 사용.
    - 테스트 가능할 거 같아. 테스트 쉬워보여. 리팩토링 연습하다보면 이런코드하는게 어렵제 않음.



step2 코드리뷰

RacingResult는 "경주가 완료된 자동차들의 리스트를 통해 우승자를 선정하기" 의 역할로 충분하다고 생각합니다.
RacingResult 는

1. 경주가 완료된 자동차의 리스트로
2. 가장 먼 지점의 위치를 찾고
3. 이를 바탕으로 우승자(여러명일 수 있음)를 찾는 것
   이 이상의 역할이 필요하지는 않을 것 같습니다!
   기존 RacingGame에서 하던 createRacingCar와 같이 "자동차 경주"와 관련된 역할을 RacingResult가 하는게 맞을까요? 관련해서 한번 고민해보면 좋을것 같습니다.
   현재 RacingResult 클래스를 다시 설계하기 위해 고민해보는 것이 가장 중요할 것 같습니다!

궁금한점에 대해 코멘트 드리겠습니다!
해당 부분에 대해서는 스택, 힙영역과 같은 자바 메모리 구조에 대해 한번 찾아보는 것은 어떨까요?
과연 자동차 1000대로 인해 성능에 이슈가 생길까요?



1단계의 핵심이 move에 대한 테스트를 구현하는 것이라면, 2단계에서 빠져서는 안되는 부분은 우승자를 구하는 로직에 대한 테스트에요!
해당 부분에 대한 테스트가 없는데 우승자를 구하는 로직에 대한 테스트 케이스 작성을 추가해주세요!
코멘트 어려운점에 대해 답변을 드리자면, 당연히 기능이 추가 되거나, 변화가 생기면 테스트 코드가 깨질수 있다고 생각합니다!
하지만, 테스트가 깨진다고 전반적인 구조를 변경하는 것을 두려워하면 안될것 같아요!
깨지는 테스트 코드에 대해서는 충분히 수정 및 반영이 가능하다고 생각합니다.



### 1주차 레이싱카 2단계

```
@Test
public void 우승자의_좌표가_5일때_우승자인지_이름구하기() {
    assertThat(racingGame.getWinnerName()).contains("minsu");
}
```

### 2주차강의

- [ ] by javajigi cimmit


  ```
  implement calculator (#114)
  refactor: upgrade gradle version to 5.2.1
  remove maven build config
  add .mvn folder
  initial commit
  Initial commit
  
  ```

- [ ] ## [IntelliJ 디버깅 해보기](https://jojoldu.tistory.com/149)

- [ ] [final을 쓰는이유](https://youtu.be/lcPfxmn0otA)

```
//가독성해치면 변수로선언하고 아니면 메서드나열함.
//로컬변수가 필요하지 않는이상 최대한 만들지 말자가 주의이심.
//toInts
//isBlack 메서드가 한눈에 들어와서 어떤 일을 하는지 한눈에 볼 수 있다.
//극단적인 연습, 메서드를 작은 단위로 쪼개기
//        split
//StringAddingCalculator
//package calculator
class Positive {
    public Positive add(int no) {
        return Positive(this.no + no);//vo 한번생성된 후에 변경되지 않는것.
    }
}
```

- code convention, format 맞추기

  - static(하나만 만들어져셔!!) final로 해야함. 설명 들었는데 모르겠음.??

- 변수생성위치

  - 상수, 인스턴스변수 생성자, 메서드

- 공백라인은 문맥달라질때!!

- space도 컨벤션이다. 

- [ ] 인텔리제이 템블릿나오는거 공부하기.

- 이름 지을때 자식 이름만큼 공들여서 짓기

  - 변수명이 바꿔야할때 데이터타입이 바뀔수있기때문에 데이터타입이나 자료구조명은 붙이지 말고 복수형으로 쓰기.

- final 사용해 값 변경 막기

- setter/getter 

  - 변수명을 public으로 하기

  - setter/getter안에 기능이 아무 것도 없다.

  - 상태값 변경은 상태값 변경가능한 객체가 담당하는게 좋음.

    ```
    Car car =  new Car();
    int position = car.getPosition();
    for(int i = 0 ; i<10 ; i++)
    	position++;
    car.setPosition(position);(x)
    ```

- 인스턴스 변수는 private 쓰기

- Enum

- 테스트하기 쉬운코드와 어려운 코드를 분리해야한다.

  - 메서드 구조를 변경
  - interface

- 인스턴스변수는 최고화한다.

  - 인스턴스변수가 필요한것인가
  - 다른곳에서 구할수 있는건 아닌가 고민하기.

- 상태 데이터를 get하지 말고 메세지를 보내라

  - 중복코드 발생

  - 객체메세지를 보내 데이터를 가지는 객체가 일하도록하라.

  - 데이터 꺼내올때만 쓰기

  - car.isMaxPosition()이라고 해보기.

    ```
    if(maxCarPosition === car.getPosition)(x)
    ```

- 테스트하기 쉬운부분과 어려운 부분을 분리하기

- UI로직도 "-"값을 비교해서 테스트할수있기 때문에 테스트하기.

- CollectionAPI로 해결방법 찾기

  - 자바에 있는 리스트 콜렉션이랑 셋 맵을 잘 활용하기.
  - 방법 찾았는데 해결 방법 몿찾느 경우만 직즙 구현

- 테스트도 유지보수해야하는 코드이다.

  - 테스트가 많다고 무조건 좋은게 아니다.
  - 테스트는 경계값을 넣어서 코딩하기
  - 이동과 정지..

- Text Fixture 생성

  - 세대의 자동차가 있고 각 자동차가 특정 포지션갖도록하는게 Fixture생성이라고함.

  - 여러개의 피쳐메서드를 사용할 수 있는데 모든 테스트 메서드에서 공통적으로 사용하는 거면 상관 없는데 A라는 텍스트메서드는 2개, B라는 것에서는 C,D 입력하면 유지보수 힘듦

  - ```
    다른방ㅂ접은 없을까?
    new Car("pobi", 2);
    new Car("pobi", 3); (O)
    
    car1.move();
    car2.move();
    car2.move();(x)
    ```

  - [ ] AssertJ 다양한 콜렉션 사용하기

- 테스트는 하나만 아니면 가능한 문법활용해서 하기.

- 일단 도메인에(Model)이 mvc로 분리되서 보이는지 확인하기.

### 2주차 수업질문

- 작은단위로 쪼개서 커밋하게되면 추천받을때 이익있음
- 코드리뷰 후 커밋시 코멘트 별 커밋이 좋은가?
- 일일커밋
  - [커밋 메시지에 대해 | 매일 성장하기 - 김용균](https://edykim.com/ko/post/about-commit-messages/)
- 사업확장을 위해 지속적으로 구인
- 카카오 50명 백엔드 채용계획
- SI 갑(은행, 제조업)에서 소프트웨어 경쟁력 
- 유지보수에서 인하우스로 개발자 모집
- 연봉 및 문화
  - 개발자 연봉이 빠르게 높아짐-> 돈은 있는데 역량있는 개발자가 적어지고있음.
  - 네이버나 카카오보다 스타트업에서도 계속해서 높은 연봉줌.
  - 2018년 상반기엔 이런 움직임이 없었는데 작년 하반기부터 괜찮은 신입들을 모아서 키우자라는 본인들이 원하는 개발자들이 적음
  - 카카오, 네이버 이런데 돌아다니다보니깐 괜찮은 신입뽑는방향으로 가고있음.
  - 좋은 개발자 채용하기 위해 좋은 문화를 만드는데 관심이 높아지는 상태
  - 개발자에대한 처우가 좋은시기다.
  - 앞으로 오년이상은 백엔드기간의 부흥기간아닐까.
  - 대용량서비스가 대부분 자바기반임.
- 신입
  - 프로그래머로 일을 하려는 신입 개발자들이 넘쳐나고 있는 상태
  - 성장할 수 있는 서비스 개발회사(스타트업 포함)로 취업하고 싶어함.
  - SI는 기피하지만 서비스 개발 회사에 취업하지 못하는 경우 다수가 SI로 시작
  - 주니어도 그렇고 우아한에 합격못해 SI로 가는 경우가 많음 80%가 SI개발자다 
  - 환경이 열악하고 기술적인 격차가 커지고 있다.
  - SI문화를 개선하는게 좋은 방법
- 경력
  - SI프로그래머의 다수가 좋은 회사
- 최근 요구하는 역량
  - 다른사람이 읽기 좋은 클린코드(V)
    - 효과적인 연습 방법을 학습하는 것이 더 중요함.
  - 소통원활, 팀워크 만들어 갈 수 있는 협업 능력
    - 주니어일때
  - 자기 주도적으로 문제를 해결하려는 능력
    - 프로그래밍을 대하는 자세, 삶을 대하는 자세에 변화
    - 난 어떤 종류의 사람이고 어떤 소신이 있고 그런게 좀 더 자기 주도적인성향을 만들지 않을까.
    - 과거처럼 시키는 일만 잘하는 사람.



### RacingCar - step2

- 어려운점  : 기존코드는 차량대수만 받았는데 이름으로 바꾸느 구조로 되다보니깐 테스트가 다깨질때 어려움.
- [Naming-특수문자](http://blog.naver.com/PostView.nhn?blogId=skybels&logNo=221118981019&parentCategoryNo=&categoryNo=7&viewDate=&isShowPopularPosts=true&from=search)

### RacingCar - step1

- 상수는 

  - static final로 선언하기
  - 변수 이름을 모두 대문자로 구현하는 것

- 변수명과 메소드이름에는 자료구조가 아닌 복수형으로 쓰기

- 초기값은 생성자로 진행하기

- [x] 불필요한 메서드 제거하기

- [x] 불필요한 공백 제거

- 차에대한 위치 출력은 자동차 스스로 하도록 하기

- mvc 패턴형태로 구현하기

  ```
  사용자에게 값을 입력받고, 결과를 출력하고, 로직을 구현하고.. 너무 많은 일을 하고 있다. 객체가 한가지 역할만 가지도록 분리한다. MVC 패턴 기반으로 구현하는 연습을 해보는건 어떨까요?
  
  힌트:
  도메인 로직과 View 로직을 구분하기 위해 다음과 같은 구조로 도전해 보면 어떨까?
  
  public static void main(String[] args) {
  String carNames = InputView.getCarNames();
  int tryNo = InputView.getTryNo();
  
  RacingGame racingGame = new RacingGame(carNames, tryNo);
  RacingResult result = null;
  while(!racingGame.isEnd()) {
      result = racingGame.race();
      ResultView.printResult(result);
  }
  ResultView.printWinners(result);
  }
  GameResult에 이동한 위치 정보가 포함되어 있고요. 이 위치 정보를 활용해 출력하는 구조로 구현해 보면 좋을 것 같아요.
  
  위 코드에서 힌트를 얻어 본인의 코드에 개선할 부분이 있는지 검토해 보고 리팩토링 해보세요.
  ```

  - Car에서 움직임을 담당하는 move(int randomNumber) 와 같은 메서드를 통해 차의 움직임을 제어해보고, 이를 바탕으로 테스트 코드도 다시 작성해보면 어떨까요?

  - setFormatMix 네이밍 변경

  - start  꼭 필요한 메서드인가?

  - ```
    //테스트 독립된 관계 만들기
    //의존관계 가지지 않고 독립된 관계 만듦
    //순서 보장하면서 테스트 만들지 말기.
    ```



- 프로그래밍 공부법
- 단위테스트와   TDD는 다르다.
- 이직추천은 웹쪽만 추천해주시는것인가?
- JUnit을 활용한 단위 테스트 이론 및 실습
- 온라인 코드 리뷰 방식 공유
- 초간단 자동차 경주 게임 구현 및 코드 리뷰
- spark.java
- 미션 새벽2시까지하심. 이렇게해놓으면 다음날 아침,저녁에 피드백하심
- 피드백기간동안 설계 고민하기.
- 내가 어떻게 하는게 클린한지 고민하기.
- 한 사람당 4명을 리뷰
- 의식적인 연습
  - 1만 시간의 재발견
  - 목적의식 있는 연습에 얼마나 많은 시간을 투자했는가?
  - 첫째, 효과적인 훈련 기법이 수립되어 있는 기술 연마
  - 둘째, 개인의 컴포트 존을 벗어난 지점에서 진행, 자신의 현재 능력을 살짝 넘어가는 작업을 지속적으로 시도
  - 셋째, 명확하고 구체적인 목표를 가지고 진행
    - 이번에 연습할땐 어떤목표를 받을지.
    - 이 연습 후엔 피드백이 굉장히 중요함.
    - 그 다음 단계엔 무슨연습을 할지 앎.
    - 한번에 다 하는게 아니라 특정부분 연습함.
  - 넷째, 신중하고 계획적이다.
- 주변 정리 및 우선순위 조정
  - 시간확보
    - 애인과의 만남 시간 조정.
    - 친구들과의 관계 끊기
  - 우선순위 조정
- 매일 1,2시간씩 미션 진행하기
  - 한번에 모두 구현하기 보다 매일 일정한 시간 투자하는 것이 정말 중요함.
  - 일주일에 최소 4회 이상 코드리뷰 요청을 보내 코드 리뷰 받기
  - 이전 과정의 경우 최소 하루에 2시간이상 
- 가진것을 비우기
  - 요구사항 규모에 비해 극단적인 리팩토링 요구
  - 자신이 가진것을 가장 많이 비울 때 가장 많은 것을 배움
- main method  테스트 문제점

질문

- 어떤분들이 피드백해주시나?