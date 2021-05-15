# ts-compilation-context
컴파일할 파일, 컴포넌트들의 모음. 해당 컨텍스트에서 컴파일러가 어떠한 에러도 없이 컴파일 하는데 필요한 모든 것을 포함하고 있다는 것을 뜻함

## tsconfig schema

최상위 프로터피

- files - 어떤 파일을 컴파일 할건지 결정
- exclude - 어떤 파일을 컴파일 할건지 결정
- include - 어떤 파일을 컴파일 할건지 결정
- compileOnSave
- extends
- compileOptions
- references

### files, include, exclude

- 셋다 설정이 없으면 전부다 컴파일
- files
    - 상대 혹은 절대 경로의 리스트 배열
    - exclude보다 강하다
- include, exclude
    - glob 패턴 (.gitignore 처럼)
    - inlcude
        - exclude보다 약하다
        - * 같은걸 사용하 .ts / .tsx / .d.ts 만 include (JS도 컴파일 하고 싶으면 allow JS 사용)
    - exclude
        - 설정 안하면 4가지(node_modules, bower_components, jspm_packages, <outDir>)를 default로 제외
        - <outDir>은 항상 제외한다. (include에 있어도)

### typeRoots, types

@types

- TypeScript 2.0부터 사용 가능해진 내장 type definition 시스템
- 아무 설정을 안한다면?
    - node_modules/@types 라는 모든 경로를 찾아서 사용
- typeRoots를 사용하면?
    - 배열 안에 들어있는 경로들 아래서만 가져온다.
- types를 사용하면?
    - 배열 안의 모듈 혹은 ./node_modules/@types/ 안의 모듈 이름에서 찾아온다.
    - 빈 배열 [ ]을 넣는다는 건 이 시스템을 이용하지 않겠다는 것
- typeRoots와 types를 같이 사용하지 않는다.

### target, lib

- target
    - 빌드의 결과물을 어떤 버전으로 할 것이냐?
    - 지정을 안하면 es3
- lib
    - 기본 type definition 라이브러리를 어떤 것을 사용할 것인가
    - lib를 지정하지 않을 때
        - target이 es3이고 디폴트로 lib.d.ts를 사용
        - target이 es5이면 디폴트로 dom, es5, scripthost를 사용
        - target이 es6이면 디폴트로 dom, es6, dom.iterable, scripthost를 사용
    - lib를 지정하면 그 lib배열로만 라이브러리를 사용한다.
        - 빈 [ ] ⇒ 'no definition found error..'
