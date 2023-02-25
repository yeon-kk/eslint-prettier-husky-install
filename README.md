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
  arrowParens: "avoid", // arrow function parameter가 하나일 경우 괄호 생략
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

### 실습
```
npm init -y
npm install eslint prettier eslint-config-prettier --save-dev
