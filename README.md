# Expo Todo

React Native + Expo 기반의 Todo 애플리케이션입니다.

## 기술 스택

| 분류 | 라이브러리 | 버전 | 설명 |
|------|-----------|------|------|
| 프레임워크 | Expo | 54 | React Native 개발 플랫폼 |
| 언어 | TypeScript | 5.9 | 정적 타입 지원 |
| 라우팅 | Expo Router | 6 | 파일 기반 라우팅 |
| 스타일링 | NativeWind | 4 | Tailwind CSS for React Native |
| 스타일링 | Tailwind CSS | 3.4 | 유틸리티 기반 CSS 프레임워크 |
| 린터 | Biome | 2 | 코드 포맷팅 및 린팅 |

## 프로젝트 구조

```
expo-todo/
├── src/
│   ├── app/                  # Expo Router 파일 기반 라우팅
│   │   ├── _layout.tsx       # 루트 레이아웃 (global.css import)
│   │   └── index.tsx         # 홈 화면 (/ 경로)
│   └── styles/
│       └── global.css        # Tailwind CSS 디렉티브
├── babel.config.js           # Babel 설정 (nativewind/babel 프리셋)
├── metro.config.js           # Metro 번들러 설정 (withNativeWind)
├── tailwind.config.js        # Tailwind CSS 설정 (nativewind/preset)
├── nativewind-env.d.ts       # NativeWind TypeScript 타입 선언
├── tsconfig.json             # TypeScript 설정
├── biome.json                # Biome 린터/포맷터 설정
└── package.json
```

## 주요 라이브러리 설정

### Expo Router (파일 기반 라우팅)

`src/app/` 디렉토리 구조가 곧 라우트가 됩니다.

- `_layout.tsx` — 레이아웃 파일 (Stack, Tabs 등 네비게이션 구조 정의)
- `index.tsx` — `/` 경로의 화면
- 엔트리포인트: `package.json`의 `"main": "expo-router/entry"`

### NativeWind v4 (Tailwind CSS for React Native)

React Native 컴포넌트에서 `className` prop으로 Tailwind 유틸리티 클래스를 사용할 수 있게 해줍니다.

**필수 설정 파일 4개:**

1. **`metro.config.js`** — `withNativeWind`로 Metro 번들러를 래핑하여 CSS 처리 활성화
2. **`tailwind.config.js`** — `nativewind/preset` 프리셋 포함, `content` 경로에 소스 파일 지정
3. **`src/global.css`** — `@tailwind base/components/utilities` 디렉티브 선언
4. **`nativewind-env.d.ts`** — `className` prop에 대한 TypeScript 타입 지원

**추가 설정:**

- `babel.config.js` — `nativewind/babel`을 **presets** 배열에 추가 (plugin이 아님)
- `src/app/_layout.tsx` — `import '../global.css'`로 글로벌 스타일 로드

**사용 예시:**

```tsx
import { Text, View } from 'react-native'

export default function HomeScreen() {
  return (
    <View className="flex-1 items-center justify-center">
      <Text className="text-red-500 text-lg font-bold">Hello!</Text>
    </View>
  )
}
```

### 경로 별칭 (`@/`)

`@/`를 `./src/`로 매핑하여 깊은 상대 경로 없이 import할 수 있습니다.

- `tsconfig.json` — `paths: { "@/*": ["./src/*"] }`
- `babel.config.js` — `module-resolver` 플러그인으로 런타임 경로 해석

```tsx
import { something } from '@/utils/helper'
```

### Biome (린터/포맷터)

ESLint + Prettier를 대체하는 통합 도구입니다.

```bash
yarn lint          # 코드 검사 및 자동 수정
```

## 실행 방법

```bash
# 의존성 설치
yarn install

# 개발 서버 시작 (캐시 초기화 포함)
yarn start

# 플랫폼별 실행
yarn android
yarn ios
yarn web
```
