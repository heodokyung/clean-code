# clean-code(좋은 코드)는 무엇인가?에 대해 고민하고 작성한 글입니다.

## 목차 ##
- [좋은 코드란 무엇인가?](#1)
- [그렇다면 좋은 코드에서 가독성은 왜 중요할까요?](#2)
- [가독성이 좋으려면 주석을 사용하면 되지 않나요?](#3)
- [좋은 코드를 작성하기 위한 방법](#4)
  - [예측(검색)이 가능한 이름](#4-1)
  - [함수명은 반드시 기능을 명시](#4-2)
  - [함수는 하나의 동작만 구현되게 작성](#4-3)
  - [함수의 인수는 명확하게 값을 전달](#4-4)
  - [변수명은 명확한 이름을 사용](#4-5)
  - [일관된 코딩 스타일을 적용](#4-6)

# clean-code

<a name="1"></a>
## 좋은 코드란 무엇인가?
이 질문은 IT업무를 하고 개발을 하는 사람이라면 누구나 한 번쯤 고민하고 나아가서 그렇게 하기 위해 노력합니다. 하지만 true/false처럼 명쾌한 답이 있지 않고 좋은 코드는 무엇인가요라고 동료들에게 물어본다면 '버그 없이 잘 돌아가는 코드', '이해하기 쉬운 코드', '재사용성이 좋은 코드' 정도의 추상적인 답변을 들을 가능성이 높습니다.

다시 처음의 질문으로 돌아가 봅시다. 좋은 코드란 무엇일까요?

정말 사람들의 말처럼 코드가 우아하고 섹시하다면 그 코드는 좋은 코드일까요? 정말 코드의 재 사용성만 높다면 그 코드는 좋은 코드일까요?  코드가 최신 기술 스펙에 맞게 구현되어 있으면 그 코드는 좋은 코드일까요?

어찌 보면 모두 맞는 말이지만 그 코드가 어떻게 구현되었나에  좋은 코드가 될 수도 있고 좋지 못한 코드가 될 수 있습니다.

분명히 말할 수 있는 건 좋은 코드란 모두가 쉽게 이해 가능하고 가독성이 용이한 코드가 좋은 코드라는 점입니다.

<a name="2"></a>
## 그렇다면 좋은 코드에서 가독성은 왜 중요할까요?

개발을 하면서 코드를 구현한다는 것은 협업을 전제로 작업을 한다는 점입니다. 협업은 다른 팀원과의 협력을 의미하기도 하지만  미래의 나 혹은 과거의 나와의 작업도 협업의 한 파트입니다. 가독성이 좋지 않으면 코드를 분석하는데 너무 많은 시간과 비용을 소모하게 되고 시간이 지나면 사람의 기억력은 그리 오래 지속되지 않으며 자신의 작성한 코드라 할지라도 기억하지 못하고 왜곡이 발생할 수도 있습니다.


<a name="3"></a>
## 가독성이 좋으려면 주석을 사용하면 되지 않나요?
```javascript
❌
// 이름: 유저 정보 반환
// 설명: 유저 정보 요청이 있을 때 해당 정보에 따라서 보여주는 정보를 반환
// 인자1: b: 요청자에 대한 정보 (신용도 함수로 전달되는 데이터 객체)
// 인자2: c: 요청자에 대한 정보를 가져오지 못하면 보여지는 텍스트

function a(b, c) {
  const u = send(b)
  const t = view(c)

  if (u) {
    return b
  } else {
    return c
  }
}
```


위의 코드는 네이밍도 간결하고 주석도 충분히 설명되어 있습니다.

그렇지만 정말 저 코드는 좋은 코드일까요? 무엇을 의미하는지 명확하지 않고 코드를 읽기 위해 주석을 다시 읽고 이해하고 코드를 다시 이해하는 과정이 지속적으로 반복됩니다.  물론 위의 코드는 조금 극단적인 예시이긴 하지만 중요한 포이트는 바로 이것입니다.

주석문은 그 코드가 무슨 역할을 수행하는가? 가 아니라 왜 이 코드가 이곳에 존재하는가에 대한 이유를 설명해합니다.


좋은 코드를 작성하지 않는다면?
누군가는 이렇게 반문할지도 모릅니다.

개발을 진행할 시간도 턱없이 부족한데 어떻게 좋은 코드 구현까지 생각하면서 작업을 할 수 있는가? 그것은 너무 이상이지 않은가? 현실과 이상은 다르다고 말이죠.


한번 상상해 봅시다.

매우 위급한 환자가 있습니다. 당장 수술을 받아야 하며 조금의 시간도 지체할 수 없습니다. 그 환자에게 1분은 누군가에도 1시간 아니 천금과도 같은 일촉즉발의 시간입니다. 의사는 환자의 상태를 보고 당장 수술을 진행하려고 합니다.

이때 환자의 수술이 시급하다고 하여 손을 씻는 행위를 생략하거나 수술에 반드시 필요한 과정 등을 생략하고 바로 수술을 한다면 그 환자의 결과는 어떻게 될까요?  성공적으로 수술을 끝마쳐도 여러 가지 후유증으로 인해 재수술 또는 더 안 좋은 상황으로 진행될 것은 조금의 상식만 있다면 누구나 예측할 수 있습니다.


우리의 코드도 마찬가지입니다.

좋은 코드 구현을 하는 게 귀찮고 시간이 걸린다고 해서 당장 개발 구현에만 집중하고 코드를 작성하게 된다면 이는 이후 우리 속담에도 있듯 '호미로 막을 것을 가래로 막는다'와 같은 일이 벌어지게 될 것입니다.



<a name="4"></a>
## 좋은 코드를 작성하기 위한 방법
그렇다면 어떻게 하는 것이 좋은 코드를 구현하는 방법일까요?

아래에 명시한 6가지 규칙에 따라서 코드를 작성합니다. (해당 규칙은 상황에 따라 간소화되거나 추가될 수 있습니다.)

예측(검색)이 가능한 이름을 사용합니다.
함수명은 반드시 기능을 명시합니다.
가급적 함수는 하나의 동작만 구현되게 작성합니다. (재사용성이 용이해집니다.)
함수의 인수는 3개 이하가 적당하며 많을 경우에는 Object로 정리해서 param 값을 전달합니다.
변수명은 모두에게 명확한 이름을 사용합니다.
일관된 코딩 스타일을 적용합니다.

<a name="4-1"></a>
### 1. 예측(검색)이 가능한 이름
#### -bad ####
아래 코드를 처음 접하는 사람은 86400이 무엇을 의미하지는 바로 이해하기가 쉽지 않습니다.
```javascript
returnData('hello', 86400)
```
#### -good ####
변수명에 검색(예측)이 가능한 이름으로 86400이라는 값을 넣어서 사용합니다. 변수명으로 하루의 총 시간 중 초를 의미한다는 것을 예측할 수 있습니다.
```javascript
const TOTAL_DAY_SECOND = 86400;
returnData('hello', TOTAL_DAY_SECOND)
```

<a name="4-2"></a>
### 2. 함수명은 반드시 기능을 명시
#### -bad ####
아래의 함수는 정확히 무엇을 의미하는지 알 수 없습니다.
```javascript
function userData () {
 ...
}
```
#### -good ####
함수에 get, delete, load와 같은 기능을 명시하면 함수명만 보고도 기능을 예측할 수 있습니다.
```javascript
function getUserData () {
 ...
}
```

<a name="4-3"></a>
### 3. 함수는 하나의 동작만 구현되게 작성
#### -bad ####
하나의 함수에서 매개변수에 따라 기능을 구분해서 코드를 작성하게 되면 코드의 가독성도 좋지 않을 뿐 아니라 기능의 재사용성 측면에서도 좋지 않습니다.
```javascript
function detailView (param) {
  if(param) {
    ...
  }
  else {
    ...
  }
}
detailView(true)
```
#### -good ####
함수의 코드가 기능으로 나뉘어서 분리되어 있으면 해당 코드를 상황에 맞게 호출해서 사용할 수 있으므로 재사용성이 높아지고 가독성도 좋아지게 됩니다.
```javascript
function showDetailView () {
   ...
}

function hideDetailView () {
   ...
}
```

<a name="4-4"></a>
### 4. 함수의 인수는 명확하게 값을 전달
#### -bad ####
예시에서는 함수와 전달하는 매개변수가 바로 붙어있기 때문에 큰 불편함을 못 느낄 수도 있지만 코드의 길이가 길어지고 해당 함수와 매개 변수만 보게 되면 각각의 매개변수가 무엇을 의미하는지 이해하기가 쉽지 않습니다.
```javascript
function readUserData (userName, age, email, job, userId) {
    ...
}
```
readUserData('홍길동', 24, 'test@gmail.com', 'programmer', 'badCode')
#### -good ####
함수의 역할을 파악하기 쉽고 전달하는 매개변수가 각각 무엇을 의미하는지 가독성과 이해가 용이합니다.
```javascript
function readUserData ({userName, age, email, job, userId}) {
   ...
}
readUserData({
  userName:'홍길동',
  age: 24,
  email: 'test@gmail.com',
  job: 'programmer',
  userId: 'goodCode'
})
```

<a name="4-5"></a>
### 5. 변수명은 명확한 이름을 사용
코드를 작성하는 자신에게는 명확하고 분명한 의미라고 해서 그 의미가 다른 사람 모두에게도 분명한 것은 아닙니다.
#### -bad ####
```javascript
userData.forEach((u, i) => {
  getUserId(u);
  addCount(i);
});
```
#### -good ####
```javascript
userData.forEach((user, currentIndex) => {
  getUserId(user);
  addCount(currentIndex);
});
```

<a name="4-6"></a>
### 6. 일관된 코딩 스타일을 적용
협업에서 가독성을 보장하는 방법 중 하나는  일관성 있는 코드를 작성하는 것입니다.
코드의 규칙을 정하고 정의된 규칙(그라운드 룰:Ground Rule)은 코드를 작성하는 모두 준수하면 작성합니다.
코드에 일관성이 지켜진다면 예측이 가능하다. 예측이 가능하다는 것은 어느 곳에 어떤 코드가 위치하는지 예상할 수 있다는 것이다. 프로젝트 팀원 간의 그라운드 룰(Ground Rule)이 필요한 이유이다.

- 네이밍(Naming):  변수명이나 함수명 등 작명을 할 때 규칙이 명확이 있으면 좋습니다.
- 디렉터리 구조 정의(Directory) : 디렉터리 구조는 프로젝트의 규모나 성격에 따라서 논의하고 정의합니다. 일반적으로 아래 2가지 방법을 가장 많이 사용합니다.
  - 역할에 따라 디렉터리를 분리
  - 페이지(도메인 영역)에 따라 디렉터리를 분리
#### -bad ####
```javascript
function eventbuttonclick() {
   ...
}
```
#### -good ####
```javascript
// camelCase
// action: get, delete, post, read....
// data : userInfo, chart...
// event: click

function readUserInfoClick() {
    ...
}
```

