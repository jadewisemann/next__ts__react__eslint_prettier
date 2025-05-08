# 네이밍 컨벤션

## basic
- `camelCase`
- 알파벳, `_`, `$`으로 시작하도록 권장
	- 객체의 키로 다룰때 안전하게
	- 숫자로 시작하거나 기타 특수문자로 시작하면 안됨
	
## 파일 이름
- 컴포넌트: `PascalCase`
- 일반 파일: `camelCase`
```
// 컴포넌트 파일 이름 (PascalCase) UserProfile.jsx 

// 일반 파일 이름 (camelCase) apiService.js
```

## 폴더 이름
- `kebab-case`

```
src/
├── components/
│   ├── user-profile/
│   └── navigation-bar/
```


## static 파일
- 대분류:
	- `btn`
	- `ico`
	- `img`
	- (추후 추가)
	- 축약어로
	- 축약어가 애매한 경우 일반 명사 카멜케이스
- 대분류-소분류 구분자: `__`
- 소분류-속성 구분자: `_`
- 띄어쓰기가 있는 단어: `camelCase`
- 순서
	- `대분류__이름_크기_색상`
	- `대분류__이름_색상`
	- `대분류__이름_크기`

```
btn__primary_24_large
ico__arrow_12_black
ico__arrowLeft_12_black

img__background_1920*1080
```

## 변수
### boolean
- `is`, `has`, `can`, `should`로 시작

### 그 외
- 동사로 시작하지 **않기**

```js
// Boolean 변수
const isActive = true;
const hasPermission = false;


// 일반 변수 (동사로 시작하지 않음)
const userName = 'John';
const itemCount = 5;
```

## 함수
- `camelCase`
- 동사로 시작

### boolean 반환
- `is`, `has`, `can`, `should`로 시작

### 특정 케이스
- 이벤트 헨들러: `handle__`
- 폼 서브밋: `submit__`
- 패칭: `get__`
	- `fetch`보다 권장
	- 서버 요청과 일관성을 지키기 위함
- 훅: `use`

# 주석
- 간결하게 적기
- 존댓말 사용하지 않기

## 필수
- 상수 선언 바로 위에 주석 달기
- 함수 주석

# 임포트
- 임포트 구문 사이 개행 없음
- 모든 임포트가 끝난후 필수 개행

## 임포트 순서
- 'builtin',
	- `node.js` || `js 내장`
- 'external',
	- `react`
	- `react-*`
- 'internal',
	- `routes`
	- `pages`
	- `store`
	- `context`
	- `provider`
	- `components`
	- `hooks`
	- `services`
- `uitll`
- `parent`
- `sibling`
- `index`
- `object`
- `type`

# js 포매팅

## 일반
### 인덴트
- space 2개

### 세미콜론
- 무조건

### 네이밍
- 일반: `camelCase`
- 상수: `SCREAMMING_SNAKE_CASE`

```js
const foo =  "foo"

const BAR = 12345;
```

### 공백
- 함수, 예약어, 쉼포, 연산자 뒤에 공백

```js
// 함수 뒤에 공백 없음 => bad
function foo(){
  ...
}
// 함수 뒤에 공백 있음 => good
function bar () {
  ...
}

// 예약어 뒤에 공백 없음 => bad
if(false){
	...
}
// 예약어 뒤에 공백 있음 => good
if (true) {
	...
}


// 쉼표 뒤에 공백 없음 => bad
const a = [1,2, 3,4]
// 쉼표 뒤에 공백 있음 => good
const b = [1, 2, 3, 4]

// 연산자 뒤에 공백 없음 => bad
const foo = 1+2*4
// 연산자 뒤에 공백 있음 => good
const bar = 1 + 2 * 4
```

### 비교 연산자
- 일치 비교 연산자 사용(`===`, `!==`), 동등 연산자 (`==`, `!=`) **금지**

```js
const foo = 'foo'
const bar = 'bar'

// 동등 비교 연산자 사용  => never
if (foo == bar) {
	...
}

// 일치 비교 연산자 사용  => good
if (foo === bar) {
  ...
}
```

## 변수

- `var`: 금지
- `const`: **강력히** 권장
	- 불가피할때만 `let` 사용
	
```js
// never
var foo = 1;

// good
const bar = 2;

// ok
let baz = 3;
baz += 1;
```


- 사용안하는 변수는 선언도 하지 말 것
	- commit, pr 전에 정리하기


## 문자열
- `'`(작은 따옴표)만 사용

```js
// bad
const foo = "string"

// good
const bar = 'string'
```

## 긴 문자열
- 한 줄에 작성(개행없이 처리)

## 가변 문자열 
- 템플릿 리터럴 사용

```js
const foo = 'apple';
const bar = 'red';

// bad
const foobar = foo + 'is' + bar; 

// good
const foobar = `${foo} is ${bar}`
```

## 순회
- `for ... in ...` : 비권장
- `for ... of ...` : 권장
- 고급 순회 메소드 : 아주 좋음
- 순회 불가능한 경우: 순회 가능한 객체로 변경

```js
// bad
for (let i in items) {
  console.log(items[i]);
}

// good
const items = [1, 2, 3];
for (const item of items) {
  console.log(item);
}

// best
items.forEach(item => {
  console.log(item);
});
```


```js
// 순회 가능 객체로 변환
const user = {name: 'John', age: 30};

Object.keys(user).forEach(key => {
  console.log(`${key}: ${user[key]}`);
});

```

## 객체
### 생성
- 리터럴 선언 사용, 가급적 생성자 사용 금지

```js
// bad
const obj = new Object();

// good
const obj = {};
```

### 식별자
- 유효한 식별자 권장
	- 알파벳, 언더바(`_`), 달러사인(`$`)으로 시작하는 단어
- 유효하지 않은 식별자의 경우 `'`으로 감싸기

```js
const alice = {
  foo: 1,
  'bar-baz': 2,
  `123qux`: 3,
  _quxx: 4,
  $fie: 5,
}
```

### 속성
- 단축 구문 사용

```js
const foo = 'foo';

// bad
const bar = {
	foo:  foo,
}

// good
const baz = {
  foo,
}
```

- 단축 구문은 시작에 모으기

```js
const foo = 'foo';
const bar = 'bar';
const baz = 'baz';

// bad
const alice = {
  foo,
  qux:  'qux',
  bar,
  quux: 'quux',
  baz
}

// good
const bob = {
  foo,
  bar,
  baz,
  qux:  'qux',
  quux: 'quux',  
}
```


### 메서드 
- 단축 구문 사용

```js
// bad
const obj = {
  addValue: function (value) {
    return obj.value + value;
  }
};

// ok
const obj = {
  addValue (value) {
    return obj.value + value;
  }
};

// good
const obj = {
  addValue: (value) => obj.value + value;
};

```

### 여러줄
- 배열을 여러 줄로 작성할 때는 요소를 한 줄씩 작성하세요.

### 얉은 복사
- 전개 구문(`...`) 사용

```js
const alice = {foo: 1, bar: 'bar'};
const aliceCopy = {...alice, baz: 3};

const { foo, ...aliceWithOutFoo } = alice; 
```

### 깊은 복사
- `sturcturedClone()` 강력히 권장
- `JSON.parse(JSON.stringify())` 강력히 권장되지 않음
	- 손실이 있을 수 있음


```js
const alice = {foo: 1, bar: 'bar'};

// ok, but mostly bad,
const deepCopyOfAlice = JSON.parse(JSON.stringify(alice));

// good
const deepCopyOfAlice = structuredClone(alice);

```

## 배열
### 생성
- 리터럴 사용

```js
// bad
const foo = new Array();

// good
const bar = [];
```

### 값 할당
- 생성 시: 리터럴
- 그 외: `Array.prototype.push()`

```js
const foo = 1;

// good
const alice = [foo];

// good
const bob = [];
bob.push(foo);
```

### 얉은 복사
- 스프레드 연산자(`...`) 사용

```js
const foo = [1, 2, 3];

const foz = [...foo];
```

> 스프레드 연산자 + 템플릿 리터럴은 사실 깊은 복사임.
> 단, 배열 안의 모든 원소가 원시 값일때만.
> 참조 값이면 참조를 그대로 가져옴.

### 깊은 복사
- `structuredClone()` 권장

```js
const foo = [1, 2, 3];

const foz = structuredClone(foo);
```

> 참조 값도 복사는 해오나, 함수, DOM은 가져오지 못함.

### 순회 가능 객체로 변환
- `Array.from()`보다는 전개 구문(`...`) 사용

```js
const foo = document.querySelectorAll('.foo');

// good
const nodes = Array.from(foo);

// best
const nodes = [...foo];
```

### 유사 배열 변환
- `Array.prototype.from()` 사용
- 스프레드 연산자(`...`) 금지
	- 유사배열은 전개 구문을 사용하면 안되는 경우가 존재 (이터러블하지 않은 경우)

### `map()`
- `Array.prototype.from()` 권장
	- 전개 구문(`...`)은 성능적으로 유리하지 않음
	- 중간 배열을 만들기 때문
```js
const foo =  [1, 2, 3];
const bar = el =>  el + 1; 

// ok
const baz = [...foo].map(bar);

// good
const baz = Array.from(foo, bar);
```

### 배열 메소드 콜백
- return 반드시 포함

```js
// good
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x * y;
});

// good (Implicit Return)
[1, 2, 3].map(x => x + 1);
```

## 객체 + 속성 공통
### 여러줄
- 여러 줄로 작성할때는 한 줄 씩
- 요소가 3개 이상이면 개행 권장

```js
// bad
const foo = [
  [0, 1], [2, 3], [4, 5],
];

// bad
const objectInArray = [{
  id: 1,
}, {
  id: 2,
}];

// bad
const numberInArray = [
  1, 2,
];

// good, 한 줄이면 모두 한 줄에
const arr = [[0, 1], [2, 3], [4, 5]];

// good, 여러 줄이면 요소별로 줄바꿈
const objectInArray = [
  {
    id: 1,
  },
  {
    id: 2,
  },
]; 

// ok
const numberInArray = [
  1,
  2,
]; 

// good 
const numberInArray = [1, 2];
```

### 구조 분해
- **객체**
	- 여러 속성에서는 구조 분해 사용
		- 임시 참조를 만들지 않음
		- 불필요한 접근을 막음

```js
// bad
function foo (bar) {
  const baz = bar.baz;
  const qux = bar.qux;

  return `${baz} ${qux}`;
}

// good
function foo(bar) {
  const { baz, qux } = bar;
  return `${baz} ${qux}`;
}

// best
function foo({ baz, qux }) {
  return `${baz} ${qux}`;
}
```

- **배열**
	- 구조 분해 사용

```js
const foo = [1, 2, 3, 4];

// bad
const bar = foo[0];
const baz = foo[1];

// good
const [bar, baz] = foo;
```

### 함수 반환값
- 여러 값을 반환한다면 배열보다는 객체 사용 강력히 권장

```js
// bad
function foo(bar) {
  // ...
  return [qux, quxx, quxxx, quxxxx];
}

// 순서를 고려해야 한다
const [qux, __, quxxxx] = foo(baz); 

// good
function foo(bar) {
  // ...
  return { qux, quxx, quxxx, quxxxx };
}

// 필요한 데이터만 선택할 수 있음
const { qux, quxxx } = foo(baz);
```

## 함수
- 화살표 함수 선언
	- this 바인딩, 호이스팅

```js
const foo = () => {
  // ...
};
```

# react
## 파일 확장자
- `.jsx`, `.tsx`

## 컴포넌트
### 이름
- `PascalCase`
- 파일이름은 컴포넌트이름과 동일하게 작성

### 선언
- 함수형 컴포넌트 사용
- 화살표 함수 사용

### props
- `camelCase`
- 구조분해 활당 권장
	- RORO 패턴

## JSX 문법
### 태그 닫기
- 항상 태그 닫기
- 자식요소가 없으면 자체 닫는 태그


### 속성 줄 바꿈
- 3개 이상일때 줄 바꿈

```jsx
// 한 두개의 속성
<Button type="submit" disabled={isLoading}>Submit</Button>

// 여러 속성
<Button
  type="submit"
  className="btn-primary"
  disabled={isLoading}
  onClick={handleSubmit}
>
  Submit
</Button>
```

### 조건부 렌더링
- 조건이 짧으면: 삼항 연사자 권장
- 조건이 복잡하면: 분리해서 처리
	- 컴포넌트의 리턴문안에 쑤셔넣지 않기
	
```jsx
// 짧은 조건
{isLoggedIn ? <UserProfile /> : <LoginButton />}

// 복잡한 조건
const renderContent = () => {
  if (isLoading) {
    return <Loader />;
  }
  
  if (error) {
    return <ErrorMessage message={error} />;
  }
  
  return <UserProfile data={data} />;
};

return (
  <div className="container">
    {renderContent()}
  </div>
);
```

### 복잡한 요소
- 괄호로 감싸서 리턴하기

```jsx
// good
return (
  <div>
    <Header />
    <MainContent>
      <ArticleList items={articles} />
    </MainContent>
    <Footer />
  </div>
);
```

## Hook
- 항상 `use`로 시작
- 컴포넌트 최상위에서만 호출
- 조건문, 반복문에서 호출 금지

## 상태관리
### 상태 분리
- 관련 있는 상태는 함께 관리
- 독립 상태 독립 관리

```jsx
// bad,  관련된 상태가 분리됨
const [firstName, setFirstName] = useState('');
const [lastName, setLastName] = useState('');
const [email, setEmail] = useState('');

// good, 관련된 상태를 함께 관리
const [formData, setFormData] = useState({
  firstName: '',
  lastName: '',
  email: ''
});

// 또는 useReducer 사용
```

### 불변성
- 상태 업데이트 시 항상 불변성을 유지
	- 리액트의 상태 업데이트에 따른 리렌더링 기준은 참조
	- 새로운 객체를 생성해서 할당함이 타당
```jsx
// bad
const handleChange = (e) => {
  formData.firstName = e.target.value; // 직접 수정
  setFormData(formData);
};

// good
const handleChange = (e) => {
  setFormData({
    ...formData,
    firstName: e.target.value
  });
};
```

## 이벤트 헨들러
### 이름
- 핸들(`handle`)로 시작
- props로 전달할때는 `on` 접두어 권장
	- 관습적 => 다른 사람들이 읽기 쉬워짐

```jsx
// 컴포넌트 내부
const handleSubmit = (e) => {
  e.preventDefault();
  // ...
};

// Props로 전달
<Form onSubmit={handleSubmit} />
```

### 인라인 함수 
- 지양할 것
	- 매 랜더링마다 재생성, 성능에 악영향

```jsx
// bad
<button onClick={() => handleClick(id)}>Click me</button>

// good
const handleButtonClick = () => {
  handleClick(id);
};

<button onClick={handleButtonClick}>Click me</button>
``` 

## 성능 최적화
- `memo`, `useMemo`, `useCallback`
	- 남용하지 말기
	- 꼭 필요할때만 사용하기

## 스타일링
- tailwind 사용

## 에러처리
### 비동기 작업
- 에러처리 필수

## 접근성
- ARIA 속성 권장
- 인터렉티브 요소는 키보드로 접근 가능해야 함

## 의존성
### `useEffect`
- 의존성 배열 명시
- 필요한 의존성 모두 포함
	- 모든 변수에 의존성을 포함할 필요는 없음(워닝도 없음)

## 커스텀 훅
- 컴포넌트 간에 공유되는 로직은 커스텀훅으로 분리 권장
- 범용적인 함수는 유틸

# next.js
## 라우팅
- 앱 라우터

## 이미지
- 내장 요소말고 `@next/image` 사용
- `<Image />`

# tailwind
## basic
- 가능한 적게 쓰기
	- 영향력이 없는 유틸리티 사용 금지
 
## 중복 요소
- `@apply` 사용
	- 그러나 피치 못할 상황에만 사용하기
- 반복문 사용
- 컴포넌트로 분리
## 포매팅
- `prettier/tailwind`로 순서 통일



# misc
## 파일 구조
- `src/` 추후에
- assets
- components
- pages
- routes
- services
- store
- hooks

- ../public

# 형상관리
## github flow
- 이슈 발행 => 브런치 => 개발
- 작업 후 이슈의 상태 변경 필수

# commit
## 제목
- 80자 이하
- 메시지와 내용 모두 한글로 작성

# Pull Request
## 승인
### 승인 인원
- 전원

### 리뷰어
- 2(과반수)
- 랜덤이나 임의 선정이 아니라 돌아가면서

## 템플릿
```
# 설명
_pr에 대한 설명_

# 이유
_이 변경이 필요한 이유_

# 변경 내용
- _변경 사항 1_
- _변경 사항 2_

# 커밋
_관련 커밋 1_, _관련 커밋 2_, ...

#(?) 테스트 방법
_테스트 방법_

#(?) 스크린 샷
_스크린 샷 1_
_스크린 샷 2_

# 관련 이슈
_관련 이슈 1_, _관련 이슈 2_, ...
```

## 리뷰
- 아래 체크리스트를 활용 할 것
- **설명/주석**:
    - 수정 설명이 명확하게 작성되었는가? 변경 사항과 의도가 충분히 설명되었는가?
- **의도**:
    - 왜 이렇게 설계했는가?
- **기능**:
    - 코드가 의도한 대로 동작하는가? 사용자에게 적절한가?
- **복잡성**:
    - 코드를 더 단순하게 만들 수 있는가? 다른 개발자가 쉽게 이해하고 사용할 수 있는가?
- **?테스트**: 코드에 올바르고 잘 설계된 자동화 테스트가 포함되어 있는가?
- **문서화**: 관련 문서가 업데이트되었는가?

