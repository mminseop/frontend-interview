1. React를 왜 사용하나요?

- React는 컴포넌트 기반으로 UI를 재사용 가능하게 만들어 개발 속도를 높입니다. 가상 DOM을 사용해 필요한 부분만 효율적으로 업데이트하고, 방대한 커뮤니티와 라이브러리 생태계 덕분에 문제 해결이 빠릅니다

2. React.memo는 언제 사용하나요?

- React.memo는 props가 변경되지 않으면 컴포넌트 리렌더링을 건너뛰어 성능을 최적화합니다. 예를 들어 리스트에서 특정 아이템만 업데이트 될 때 나머지 아이템들의 불필요한 리렌더링을 방지할 수 있습니다. 다만 최초 렌더링에서는 약간 느릴 수 있으므로 리렌더링이 자주 발생하거나 연산 비용이 큰 컴포넌트에 사용하는 것이 효과적입니다

3. useCallback과 useMemo의 차이는?
- useCallback은 함수 자체를 캐싱하고 useMemo는 함수의 반환값을 캐싱합니다. useCallback은 자식 컴포넌트에 props로 전달되는 함수가 매번 새로 생성되는 것을 방지하고 useMemo는 계산 결과를 캐싱합니다. 둘 다 의존성 배열이 변경될 때만 재생성되며 리렌더링이 빈번한 경우에 사용하면 효과적입니다

4. 커스텀 훅을 왜 사용하나요?
- 커스텀 훅은 로직과 UI를 분리하여 코드 재사용성을 높이고 가독성을 개선합니다. 연관된 상태와 로직을 하나의 훅으로 묶어서 여러 컴포넌트에서 사용할 수 있습니다

5. CSR과 SSR 중 어떤 것을 선택하나요?
- 프로젝트 특성에 따라 다릅니다. SEO가 중요하고 초기 로딩 속도가 중요한 마케팅 페이지는 SSR이 적합하고 로그인 후 사용하는 인트라넷처럼 인터랙션이 많고 SEO가 덜 중요한 경우 CSR이 유리합니다. 기기 성능이 낮고 페이지 전환이 빈번한 경우에도 CSR이 더 나을 수 있습니다. Next.js를 사용하면 페이지별로 렌더링 방식을 선택할 수 있습니다

6. Virtual DOM이 무엇이고 작동 원리를 설명해주세요
- Virtual DOM은 실제 DOM을 자바스크립트 객체로 복사한 것으로 메모리에 저장됩니다. React는 state가 변경되면 새로운 Virtual DOM을 만들고 이전 Virtual DOM과 비교(diffing)해서 변경된 부분만 실제 DOM에 적용합니다. React 18부터는 Auto Batching으로 여러 변경사항을 모아서 한 번에 DOM에 반영하기 때문에 효율적입니다. DOM 조작이 적을 때는 오히려 기존 방식이 더 빠를 수 있습니다. Virtual DOM은 대규모 UI 업데이트가 많을때 사용하면 좋습니다

7. JSX가 무엇이고 왜 사용하나요?
- JSX는 JavaScript에 XML을 추가한 문법으로 HTML과 JS를 한 파일에서 작성할 수 있게 해줍니다. React는 JSX를 일반 JavaScript로 변환합니다 (React.createElement()).
- JSX 규칙은 반드시 하나의 부모 요소로 감싸야 합니다 (Fragment < > < / > 사용 가능) -> Virtual DOM이 변화를 효율적으로 비교하려면 하나의 DOM 트리 구조여야 하기 때문입니다

8. props와 state의 차이는?
- props : 부모에서 받는 읽기 전용 데이터. 변경 불가능
- state : 컴포넌트 자신이 관리하는 데이터. 변경 가능 (useState, setState)

9. state를 직접 바꾸지 않고 useState를 사용하는 이유는?
- React는 메모리 주소 비교로 변경 감지를 합니다. state를 직접 수정하면 메모리 주소가 바뀌지 않아서 React가 변경을 감지하지 못합니다. useState의 setter 함수는 새로운 값으로 새 메모리 주소를 만들어서 리렌더링을 트리거합니다.

10. 제어 컴포넌트와 비제어 컴포넌트의 차이는?
- 제어 컴포넌트 : state로 입력값을 관리 (value와 onChange 사용)
- 비제어 컴포넌트 : DOM이 직접 값을 관리 (ref 사용)
- 제어 컴포넌트는 실시간 유효성 검사가 필요할 때, 비제어 컴포넌트는 파일 업로드처럼 단순 제출만 필요할 때 사용합니다.

11. useEffect와 useMemo의 차이?
- useEffect : 부수효과(side effect) 처리용 (API 호출, DOM 조작)
- useMemo : 순수 함수의 결과값 캐싱용

12. useEffect와 useLayoutEffect의 차이는?
- useEffect : 화면 렌더링(paint) 후 비동기 실행
- useLayoutEffect : 화면 렌더링(paint) 전 동기 실행
- useLayoutEffect는 DOM 측정이나 애니메이션 구현처럼 즉시 반응이 필요한 경우에 사용합니다. 대부분의 경우 useEffect로 충분합니다.

13. React에서 메모이제이션은 어떻게 하나요?
- React.memo: 컴포넌트 메모이제이션 (props 비교)
- useMemo: 값 메모이제이션 (dependency 배열 비교)
- useCallback: 함수 메모이제이션 (dependency 배열 비교)
```tsx
// React.memo : props 변경시만 리렌더링
const MemoizedComponent = React.memo(ChildComponent);

// useMemo : a, b 변경시만 재계산
const sum = useMemo(() => a + b, [a, b]);

// useCallback : aaa 변경시만 함수 재생성
const onClick = useCallback(() => {}, [aaa]);
```

14. 렌더링 성능을 향상시키는 방법은?
- 메모이제이션 : React.memo, useMemo, useCallback 사용
- Key 최적화 : 배열 map에서 index 대신 고유한 id 사용
- 함수형 업데이트 : setState(prev => prev + 1) 형태 사용
- 객체 참조 유지 : 자식에게 props 전달 시 매번 새 객체 생성 방지
- 디바운싱/쓰로틀링 : 검색창 입력 같은 빈번한 이벤트 처리

15. Key Props를 왜 사용하나요?
- React가 리스트에서 어떤 항목이 변경/추가/삭제되었는지 식별하기 위해서입니다. key가 없으면 React는 모든 항목을 다시 렌더링합니다.
- index를 key로 사용하면 항목 순서가 바뀔 때 버그가 발생할 수 있습니다. 고유한 id를 사용해야 합니다
```tsx
// index 사용 (순서 변경시 문제)
{list.map((item, index) => <Item key={index} />)}

// 고유 id 사용
{list.map((item) => <Item key={item.id} />)}
```

16. React Query(TanStack Query)란 무엇인가요?
- 서버 상태를 관리하는 라이브러리로, 비동기 데이터 fetching, 캐싱, 동기화를 자동화합니다.
간략히 장점
- 자동 캐싱으로 중복 요청 방지
- isLoading, error 객체로 상태 분기 간편
- 서버 상태와 클라이언트 상태 분리 (서버 : TanStack Query, 클라이언트 : Zustand)

17. Context API가 무엇인가요?
- props drilling 없이 컴포넌트 간 값을 공유하는 React 기능입니다. 주로 전역 상태(테마, 로그인 정보)를 다룰 때 사용합니다.
- Context API는 성능 최적화 도구가 아닙니다. 값이 자주 변경되면 하위 컴포넌트가 모두 리렌더링되므로, 이런 경우 Zustand 같은 상태 관리 라이브러리가 더 적합합니다.

18. React 18의 주요 변경사항은?
- Auto Batching: Promise, setTimeout에서도 여러 상태 업데이트를 자동으로 묶어서 리렌더링 최소화
- 새로운 Root API: ReactDOM.createRoot() 사용 (기존 render() 대체)
- Concurrent Features: Suspense, useTransition으로 더 부드러운 UX
- Streaming SSR: Suspense로 페이지 일부를 먼저 보여주고 나머지는 로딩

19. Hydration이 무엇인가요?
- SSR에서 서버가 보낸 정적 HTML에 클라이언트 측 JavaScript를 연결하는 과정입니다. 서버 HTML + 클라이언트 JS를 매칭해서 인터랙티브하게 만듭니다. Next.js에서 자동으로 처리되며 초기 로딩 속도와 SEO를 개선합니다.

20. 클래스형과 함수형 컴포넌트의 차이는?
- 클래스형: Lifecycle API, this.props 사용
- 함수형: Hooks 사용, this 없음
- 함수형이 더 간결하고 최신 React에서 권장됩니다.

21. 생명주기 메서드란? (레거시)
- 클래스형 컴포넌트의 생명주기 메서드는 크게 세 단계입니다.
- Mount: constructor -> render -> componentDidMount
- Update: shouldComponentUpdate -> render -> componentDidUpdate
- Unmount: componentWillUnmount
- 함수형에서는 useEffect로 대체합니다.