## init-project(출처: wanted-pre-onboarding-frontend-9th)

1. eslint: CRA의 경우 내장되어 있음

```
npm install eslint --save-dev
```

2. prettier

```
npm install prettier --save-dev
```

3.eslint-config-prettier

- config
  다른 사람이 미리 만들어 놓은 설정 파일.(내가 가져와서 쓰려고 다운)

3-1. Prettier 설정

- .prettierrc.확장자

```javascript
// .prettierrc.js

module.exports = {
  printWidth: 100, // printWidth default 80 => 100 으로 변경
  singleQuote: true, // "" => ''
  arrowParens: 'avoid', // arrow function parameter가 하나일 경우 괄호 생략
};
```

- 참고자료
  [https://prettier.io/docs/en/options.html](https://prettier.io/docs/en/options.html)

3-2. ESLint 설정

- eslint에서 기본적으로 제공되지 않는 규칙을 추가하고 싶을때는 plugin을 활용
- js 라이브러리이기 때문에 React 관련 문법이 없다.
  - plugin: 기능 추가
  - config: 미리 설정해둔 세팅 공유

```
// .eslintrc

{
  "extends": ["react-app", "eslint:recommended"], //react-app이라는 config를 그대로 쓰겠다. eslint:recommended라는 config를 쓰겠다
  "rules": { // config에 덧붙여서 추가
    "no-var": "error", // var 쓰면 eslint error 뜨게 하자
    "no-multiple-empty-lines": "error", // 여러 줄 공백 금지
    "no-console": ["error", { "allow": ["warn", "error", "info"] }], // console.log() 금지
    "eqeqeq": "error", // 일치 연산자 사용 필수
    "dot-notation": "error", // 가능하다면 dot notation 사용
    "no-unused-vars": "error" // 사용하지 않는 변수 금지
  }
}
```

- 참고자료  
  [https://eslint.org/docs/latest/rules/](https://eslint.org/docs/latest/rules/)  
  [https://eslint.org/docs/latest/use/configure/configuration-files#using-a-shareable-configuration-package](https://eslint.org/docs/latest/use/configure/configuration-files#using-a-shareable-configuration-package)  
  [https://eslint.org/docs/latest/use/configure/plugins](https://eslint.org/docs/latest/use/configure/plugins)

### prettier 실습

```
npm init -y //package.json 생성
npm install eslint prettier eslint-config-prettier --save-dev //package-lock.json, node_modules 생성
```

index.js 파일 생성  
.prettierrc.js //설정파일 생성, module.exports 입력

```
npx prettier . //적용은 안된 상태. 포매팅 하면 이렇게 될거야.
npx prettier --write . //포맷팅 된 다음 저장해줘
```

만약 vscode에서 이미 저장하면 자동 수정되게 만든 경우,
메모장 또는 다른 프로그램을 index.js 파일을 열어서 수정후 저장하면 된다.
그런다음 위 명령어 npx prettier --write . 를 다시 터미널에서 실행해주면 됨

```
npx prettier --write --cache .
```

- 이미 포맷팅 되었고 변화 없는 파일은 캐시파일로 남겨두겠다. 변한 파일만 포맷팅 하겠다.
- prettier의 cache 파일은 node_modules 안에 있음

```javascript
"scripts":{

}
```

- npm run [커스텀 스크립트 명령어]
- node_modules 안에 있다면 npx, npm 명령어 입력하지 않아도 됨
  ![image](https://user-images.githubusercontent.com/86847564/221353404-dc2460e8-ed2a-497c-8d6f-020069704678.png)
- 캐시된 파일은 (cached)

### eslint 실습

- .eslintrc 파일 생성(json)

```
{
  "env":{
    "es6":true //es5가 기본이기 때문에 es6라는 것을 알림
  },
  "rules": {
    "no-var": "error", // var 금지
    "eqeqeq": "error" // 일치 연산자 사용 필수
  }
}
```

```
npx eslint .
```

![image](https://user-images.githubusercontent.com/86847564/221353784-e7502e4d-b405-416e-86de-6bd2f20d7290.png)

- var는 쓰지 못합니다, let을 쓰세요. no-var라는 설정에 걸립니다.
- no-var 참고자료 https://eslint.org/docs/rules/no-var
- 만약 다른 파일을 extends 해서 쓰고싶다면, .eslintrc 파일에 extends와 경로를 적어주면 된다.

```
// .eslintrc

{
  "env": {
    ...
  },
  "extends":["./eslintrc.base.js", "..."],
  "plugin":[],
  "rules": {
  ...
  }
}


```

![image](https://user-images.githubusercontent.com/86847564/221354051-bce49e70-697b-4456-9793-e3e3e2dd0193.png)

```
history | grep "init"
npm init @eslint/config //eslint setting 파일을 만드는걸 도와준다.
```

(1) syntex? syntex and problems(0)? code styling?  
(2) module? JS modules(import export 모듈 사용)  
(3) React?  
(4) TypeScript?  
(5) browser, node  
(6) JSON  
(7) react plugin  
(8) npm

```
npx eslint --cache . // .eslintcache 생성
```

- .eslintcache파일은 local에만 필요하기 때문에 .gitignore에 포함

```
//.gitignore

node_modules/
.eslintcache
```

```
// package.json

  "scripts": {
    "lint":"eslint --cache ."
  },
```

### husky: 자동화

- git hook: 특정 단계에서 hook 동작 실행

```
npm install husky --save-dev //프로그램 돌리는데 필요없고 개발하는데만 필요하기 때문에 dev dependency
npx husky install // husky를 돌리려면 이 과정을 통해 git hook을 실제 등록(처음 husky 세팅하는 사람만 실행 필요)
```

- 이후 clone 받아서 실행하는 사람들은 husky install 이 자동 실행되도록 설정

```
  "scripts": {
    "post install":"husky install" //npm이 모두 install된 후, 실행
  },
```

- 그런 다음 husky hook 추가

```
npx husky add .husky/pre-commit "npm run format"
npx husky add .husky/pre-push "npm run lint"
```

### husky 실습

```
npm install husky --save-dev
```

- package.json 파일의 devDependency에 설치된 모습

![image](https://user-images.githubusercontent.com/86847564/221358385-8ef67d97-5f53-4b51-8c5e-fac242c4cbd9.png)

- git hook이 되려면 git이 되어야 한다(깃으로 관리 안된 경우)

```
git init -y
```

- husky Git hooks 설치

```
npx husky install
```

- husky추가, commit 전에, "npm run format" 하기 추가
  - format: package.json의 script인 "prettier --write --cache ." 실행

```
npx husky add .husky/pre-commit "npm run format"
```

├─.husky  
│ │ pre-commit

- 확인 메시지 추가 echo "format finish"

```
//.husky/pre-commit

#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

echo "pre commit start" //추가
npm run format
echo "format finish" //추가
```

- push 전에 eslint 다 통과 후 push
- pre-push hook

```
npx husky add .husky/pre-push "npm run lint"
```

### lint warning level 설정

```
// .eslintrc
"rules":{
  "no-var":"warn"
}
```

```
//index.js

var c
```

```
npm run lint
```
