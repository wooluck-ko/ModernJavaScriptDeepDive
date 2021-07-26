## 11장. 원시 값과 객체의 비교

**변수**(variable)는 하나의 값을 저장하기 위해 확보한 **메모리 공간 자체** 또는 그 **메모리 공간을 식별하기 위해 붙인 이름**

변수 이름을 식별자(identifier)라고 한다. 식별자는 값이 아니라 메모리 주소를 기억하고 있다. 식별자는 메모리 주소에 붙인 이름이라고 할 수 있다.

### 원시 값

- 변수 값을 변경하기 위해 원시 값을 재할당하면 새로운 메모리 공간을 확보하고 재할당한 값을 저장한 후, 변수가 참조하던 메모리 공간의 주소를 변경한다. 값의 이러한 특성을 **불변성**(immutability)이라 한다. ([예전에 정리해놓은 글](https://velog.io/@dyongdi/JS-%ED%97%B7%EA%B0%88%EB%A6%AC%EB%8A%94-%EB%B3%B5%EC%82%AC-%EC%A0%95%EB%A6%AC%EC%A0%95%EB%A6%AC))
- ECMAScript 사양에 문자열 타입(2바이트), 숫자 타입(8바이트) 이외의 원시 타입은 크기를 명확히 규정하고 있지 않다. → 브라우저 제조사의 구현에 따라 원시 타입의 크기는 다를 수 있다.
- 문자열의 독특한 특징 (다른 원시 값과 비교할 때)
    - 문자열이란, 0개 이상의 문자(character)로 이뤄진 집합
    - 1개의 문자는 2바이트의 메모리 공간에 저장
    - 따라서 몇 개의 문자로 이뤄졌느냐에 따라 필요한 메모리 공간의 크기가 결정
    - (참고) C언어에는 하나의 문자를 위한 데이터 타입(char)만 있고, 문자열은 문자의 배열로 처리, Java에서는 문자열을 String 객체로 처리
- 문자열은 유사 배열 객체이면서 이터러블이므로 배열과 유사하게 각 문자에 접근할 수 있다.
    - 유사 배열 객체: 인덱스로 프로퍼티 값에 접근할 수 있고, length 프로퍼티를 갖는 객체
- 가독성을 위해 문자열을 줄바꿈 할 때에는 `\` 사용하면 된다. [MDN 참고](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String#%EA%B8%B4_%EB%AC%B8%EC%9E%90%EC%97%B4_%EB%A6%AC%ED%84%B0%EB%9F%B4)
- `str.length` 와 같이 문자열을 객체처럼 쓴다는 걸 한 번도 이상하게 생각해본 적이 없는데 아무튼 객체처럼 동작한다. (문맥 안의 메서드에서 프로퍼티 조회 또는 원형의 문자열 호출이 발생하면, JavaScript는 자동으로 문자열 원형을 감싸고 프로퍼티 조회를 수행 하거나 메서드를 호출합니다. - [MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String#%EB%AC%B8%EC%9E%90%EC%97%B4_%EC%9B%90%ED%98%95%EA%B3%BC_string_%EA%B0%9D%EC%B2%B4%EC%9D%98_%EC%B0%A8%EC%9D%B4)) - 21.3절 "원시 값과 래퍼 객체"에 나온다고 함
- 문자열은 유사 배열이므로 인덱스를 사용해 접근할 수 있지만, 값을 변경할 수는 없다. 이 때 에러가 발생하지 않는다.

    ```jsx
    var str = 'string';
    str[0] = 'S';
    console.log(str); // string
    ```

### 값에 의한 전달

"값에 의한 전달"이라는 용어는 ECMAScript 사양에 등장하지 않는다. 공유에 의한 전달(pass by sharing)이라고 표현하는 경우도 있다. **사실은 값을 전달하는 것이 아니라 메모리 주소를 전달한다.**

### 객체

- 프로퍼티의 개수가 정해져 있지 않고 동적으로 추가, 삭제할 수 있다.
- 프로퍼티의 값에도 제약이 없다.
- 따라서 확보해야 할 메모리 공간의 크기를 사전에 정해둘 수 없다.
- 객체의 구현 방식은 브라우저 제조사마다 다를 수 있다.
- 대부분의 자바스크립트 엔진은 해시 테이블과 유사하지만 높은 성능을 위해 일반적인 해시 테이블보다 나은 방법으로 객체를 구현한다.
- V8 엔진에서는 프로퍼티에 접근하기 위해 동적 탐색(dynamic lookup) 대신 히든 클래스(hidden class) 방식을 사용해 성능을 보장 (p.147의 링크들 참고)