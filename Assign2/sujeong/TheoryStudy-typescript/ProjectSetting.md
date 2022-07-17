# TODO 프로젝트 해보기

# 첫번째 실습 프로젝트

## 1) project setting

### tsconfig.json

: ts파일을 js파일로 변환할때의 설정값을 지정하는 파일

```tsx
{
  "compilerOptions": {
    "allowJs": true,
    "checkJs": true,
    "noImplicitAny": false // true면 any있을 때 에러 발생
  },
  "include": ["./src/**/*"]
}
```

### .eslintrc.js

: eslint라는게 타입스크립트 문법을 보조함. 에러를 발생할 수 있도록 규칙을 작성해둔 파일

```tsx
module.exports = {
  root: true,
  env: {
    browser: true,
    node: true,
    jest: true,
  },
  extends: [
    'plugin:@typescript-eslint/eslint-recommended',
    'plugin:@typescript-eslint/recommended',
  ],
  plugins: ['prettier', '@typescript-eslint'],
  rules: {
    'prettier/prettier': [
      'error',
      {
        singleQuote: true,
        semi: true,
        useTabs: false,
        tabWidth: 2,
        printWidth: 80,
        bracketSpacing: true,
        arrowParens: 'avoid',
      },
    ],
    '@typescript-eslint/no-explicit-any': 'off',
    'prefer-const': 'off',
  },
  parserOptions: {
    parser: '@typescript-eslint/parser',
  },
};
```

## 2) API Introduce

### filter API

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/10dafb01-884e-440e-8577-a36af20247be/Untitled.png)

- 다음은 showCompleted내의 return내용은 동일하다