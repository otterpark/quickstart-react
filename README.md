# quickstart-react

`Setting`

React + TypeScript + Jest + Parcel + ESLint

## 가능한 스크립트 동작

```bash
npm ci

npm test

npm start
```

<http://localhost:8000>

## 처음부터 시작하기

GitHub 저장소에 있는 코드를 참고하여, 아래 내용을 따라하면 됩니다.

### npm 프로젝트 생성

폴더를 만든 후, 생성한 폴더에 접근합니다.

```bash
mkdir my-react-project

cd my-react-project
```

npm 프로젝트 생성을 진행합니다.

```bash
npm init -y
```

### .gitignore 생성

`.gitignore` 파일을 생성합니다.

```bash
touch .gitignore
```

생성 후 밑에 두 가지 방법에 따라 `.gitignore`을 작성합니다.

**방법1:** <https://github.com/github/gitignore> 로 접속하여 개발 환경을 찾아 복사 후 붙여넣기 합니다.

**방법2:** 위 처럼 파일을 생성한 후 <https://toptal.com/developers/gitignore> 로 접속하여 자신이 만들고자 하는 개발 환경을 검색하여 내용을 긁어옵니다. (예제에서는 `node`로 세팅을 진행)

### TypeScript 설치 및 세팅

`TypeScript` 패키지를 설치합니다.

```bash
npm install --save-dev typescript

npx tsc --init
```

설치가 완료 후 `npx tsc --init`을 실행하면 `tsconfig.json` 파일이 생성 된 것을 확인할 수 있습니다.

`package.json` 파일에 의존성이 추가된 걸 확인할 수 있습니다.

```json
{
  "devDependencies": {
    "typescript": "^5.0.4"
  }
}
```

JSX 사용을 위해 `tsconfig.json` 파일을 열어 옵션을 수정해 줍니다.

```json
{
  "compilerOptions": {
    // ...(전략)...
    "jsx": "react-jsx",
    // ...(후략)...
  }
}
```

추가적으로 TypeScript 컴파일을 통해 문법 오류를 확인하는 `check` 명령을 `package.json` 파일에 추가합니다.

```json
{
  "script": {
    // ...(전략)...
    "check": "tsc --noEmit"
    // ...(후략)...
  }
}
```

다음 명령어를 입력해서 문법 오류가 있는지 체크할 수 있으며, 이 명령을 자주 실행하고, CI 등에 포함시킵니다.

```bash
npm run check
```

### ESLint 설치 및 세팅

`ESLint` 패키지를 설치합니다.

```bash
npm install --save-dev eslint
npx eslint --init
```

설치가 완료 후 `npx eslint --init`을 실행하면 아래와 같이 질문들이 뜹니다. 내용을 전체적으로 확인 후에 자신의 프로젝트에 맞춰서 설정을 완료합니다. (아래 내용은 현재 프로젝트에 세팅된 내용입니다.)

```bash
You can also run this command directly using 'npm init @eslint/config'.
✔ How would you like to use ESLint?
> style

✔ What type of modules does your project use?
> esm

✔ Which framework does your project use?
> react

✔ Does your project use TypeScript?
> Yes

✔ Where does your code run?
> browser

✔ How would you like to define a style for your project?
> guide

✔ Which style guide do you want to follow?
> xo-typescript

✔ What format do you want your config file to be in?
> JavaScript

Checking peerDependencies of eslint-config-xo-typescript@latest
Checking peerDependencies of eslint-config-xo@latest

The config that you have selected requires the following dependencies:

eslint-plugin-react@latest eslint-config-xo@latest eslint@>=8.0.0 eslint-config-xo-typescript@latest @typescript-eslint/eslint-plugin@>=5.57.0 @typescript-eslint/parser@>=5.57.0 typescript@>=4.4

✔ Would you like to install them now?
> Yes

✔ Which package manager do you want to use?
> npm

Installing eslint-plugin-react@latest, eslint-config-xo@latest, eslint@>=8.0.0, eslint-config-xo-typescript@latest, @typescript-eslint/eslint-plugin@>=5.57.0, @typescript-eslint/parser@>=5.57.0, typescript@>=4.4

added 105 packages, and audited 204 packages in 8s

86 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
Successfully created .eslintrc.js file in ...
```

위와 같이 설치를 완료하면 `package.json` 파일에 의존성이 포함된다.

```json

{
  "devDependencies": {
    ...(전략)...
    "@typescript-eslint/eslint-plugin": "^5.58.0",
    "@typescript-eslint/parser": "^5.58.0",
    "eslint": "^8.38.0",
    "eslint-config-xo": "^0.43.1",
    "eslint-config-xo-typescript": "^0.57.0",
    "eslint-plugin-react": "^7.32.2",
    ...(후략)...
  }
}
```

`.eslintrc.js` 파일에 설정 추가

```js
module.exports = {
  env: {
    browser: true,
    es2021: true,
    jest: true,
  },
  extends: [
    'plugin:react/recommended',
    'plugin:react/jsx-runtime',
    'xo',
  ],
  overrides: [
    {
    extends: [
      'xo-typescript',
    ],
    files: [
      '*.ts',
      '*.tsx',
    ],
    },
  ],
  parserOptions: {
    ecmaVersion: 'latest',
    sourceType: 'module',
  },
  plugins: [
    'react',
  ],
  rules: {
  },
};
```

`package.json` 파일에 `lint` 명령을 추가합니다.

```json
  {
    "scripts": {
      // ...(전략)...
      "lint": "eslint --fix --ext .js,.jsx,.ts,.tsx ."
    }
  }
```

`.eslintignore` 파일을 생성합니다.

```bash
touch .eslintignore
```

`.eslintignore` 파일을 작성합니다.

```eslintignore
/node_modules/
/dist/
```

앞서 설치했던 `lint` 명령어를 입력 시, 설정했던 파일에 `lint`가 실행되고 자동으로 `lint`에 맞게 수정합니다.

```bash
npm run lint
```

### React 설치

```bash
npm install react react-dom
npm install --save-dev @types/react @types/react-dom
```

### React 기본 코드 작성

```bash
mkdir src
touch src/index.tsx
touch src/App.tsx
```

`src/App.tsx` 파일:

```tsx
export default function App() {
  return (
    <p>Hello, world!</p>
  );
}
```

`src/index.tsx` 파일:

```tsx
import * as ReactDOM from 'react-dom';
import App from './App';

const container = document.getElementById('app');
ReactDOM.render(<App />, container);
```

### Jest(테스팅 도구) 설치

```bash
npm i -D jest @types/jest @swc/core @swc/jest \
    jest-environment-jsdom \
    @testing-library/react @testing-library/jest-dom
```

### `jest.config.js` 파일 생성 후 작성하기

```bash
touch jest.config.js
```

```js
module.exports = {
  testEnvironment: 'jsdom',
  setupFilesAfterEnv: [
    '@testing-library/jest-dom/extend-expect',
    './jest.setup',
  ],
  transform: {
    '^.+\\.(t|j)sx?$': ['@swc/jest', {
      jsc: {
        parser: {
          syntax: 'typescript',
          jsx: true,
          decorators: true,
        },
        transform: {
          react: {
            runtime: 'automatic',
          },
        },
      },
    }],
  },
  testPathIgnorePatterns: [
    '<rootDir>/node_modules/',
    '<rootDir>/dist/',
  ],
};
```

`.eslintrc.js` 파일에 설정 추가:

```javascript
module.exports = {
  env: {
    // ...(전략)...
    jest: true,
  },
  // ...(후략)...
};
```

`src/App.test.tsx` 파일 작성:

```tsx
import { render } from '@testing-library/react';
import App from './App';

describe('App', () => {
  it('renders greeting message', () => {
    const { container } = render(<App />);
    expect(container).toHaveTextContent('Hello, world!');
  });
});
```

`package.json` 파일에 `jest` 명령을 추가합니다.

```json
  {
    "scripts": {
      // ...(전략)...
      "test": "jest",
      "coverage": "jest --coverage --coverage-reporters html",
      "watch:test": "jest --watchAll"
    }
  }
```

방금 만든 `test` 명령어로 테스트를 시작합니다.

```bash
npm test
```

### Parcel 설치

```bash
npm install --save-dev parcel
```

`package.json` 파일에 `parcel` 명령을 추가합니다.

```json{
  "scripts": {
    "start": "parcel index.html --port 8080",
    // ...(후략)...
  }
```

`.gitignore` 파일과 `.eslintgnore` 파일에 각각 Parcel 캐시 추가:

```txt
/.parcel-cache/
```

### index.html 생성

`index.html` 파일을 생성합니다.

```bash
touch index.html
```

`index.html` 파일:

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>Sample</title>
</head>
<body>
  <div id="app">
    Loading...
  </div>
  <script type="module" src="./src/index.tsx"></script>
</body>
</html>
```

### Run web server for development

```bash
npm start
```

웹 브라우저로 확인: <http://localhost:8080>

### 여기서부터는 꿀팁 👍

`.vscode/settings.json` 파일을 추가해 JS/TS 파일을 저장할 때마다 ESLint를 실행하고 문제점을 고치게 설정할 수 있다.

- <https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint>
- <https://marketplace.visualstudio.com/items?itemName=shardulm94.trailing-spaces>

```json
{
    "editor.rulers": [
        80
    ],
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    },
    "trailing-spaces.trimOnSave": true
}
```
