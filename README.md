## Next.js App Router Course - Starter
This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.
For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.

## Nextjs step 별 진행
https://nextjs.org/learn?utm_source=next-site&utm_medium=homepage-cta&utm_campaign=home

## 개인 스터디 작업물(자유롭게)
   김혜남: https://nextjs.org/learn
   시작일: 2026-03-05


## 셋팅관련 정리

### 시스템 요구사항
- 최소 Node.js 20.9 버전 이상
- 운영 체제: maxOS, Windows(WSL 포함), Linux
### 지원되는 브라우저
- 크롬 111+, 엣지 111+, 파이어폭스 111+, 사파리 16.4 이상
### 필요한 패키지 설치 (예제 포함 설치는 진행요약꺼 참고)
>_ pnpm i next@latest react@latest react-dom@latest
### 패키지 스크립트 (npm run dev -> :3000 서버실행)
- next dev: Turbopack(기본 번들러)을 사용하여 개발 서버 시작
- next buil: 프로덕션용 애플리케이션 빌드
- next start 프로덕션용 서버 시작
- eslint: ESLint 실행
### 라우팅 구조 및 public폴더
- /app/ :파일 시스템 라우팅을 사용, 라우트 root경로
- /app/layout.tsx: 루트 레이아웃 파일. 필수. <html><body> 태그 포함
- /app/page/tsx: 루트에 포함될 컨텐츠.
- /src/app/구조는 선택적 (지원함)
- /public/: 정적파일(이미지,폰트 등), Image(img) 컴포넌트 사용, import Image from 'next/image;
### 타입스크립트 vscode 설정: ctrl/command + shift + p -> TypeScript: Select TypeScrirpt Version -> Use Workspace Version
### 린팅셋팅 (최신형 권장.eslint.config.mjs / 기존형 .eslintrc.)
- ESLint (포괄적인 규칙) "lint": "eslint", "lint:fix": "esling --fix" 
- Biome (빠른린터+포맷터) "lint": "biome check", "format": "biome format --write"
- Next.js 16버전부터는 next build 린터가 자동으로 실행 안됨
### 파일 import 경로 
- 상대경로 (before): import { Button } from '../../../components/button'
- 절대경로 (after): import { Button } from '@/components/button'
- 설정은 tsconfig.json 또는 jsconfig.json 파일에서 설정



## 진행관련 정리

### step1. 시작하기 : 스타터 예제를 사용하여 Next.js 애플리케이션을 생성하고 개발 서버를 실행
>_ npm i -g pnpm // npm 관리자
>_ npx create-next-app@latest nextjs-dashboard --example "https://github.com/vercel/next-learn/tree/main/dashboard/starter-example" --use-pnpm 
ㄴ 예제사용을 위한 셋팅 및 설치, --exmple, --starter 사용

>_ cd nextjs-dashboard 
ㄴ 폴더 구조
/app: 애플리케이션의 모든 경로, 구성요소 및 로직 포함, 주로 이 영역에서 작업
/app/lib: 애플리케이션에서 사용되는 함수들 (재사용 가능한 유틸리티 함수 및 데이터 가져오기 함수 등)
/app/ui: 애플리케이션에 필요한 카드, 테이블, 폼 등의 모든 UI 구성 요소를 포함함 (시간 절약을 위해 해당 프로젝트엔 미리 스타일링 되어있음)
/public: 애플리케이션에 필요한 이미지 등의 모든 정적 자산을 포함
next.config.ts: 설정파일, 'npm i' 명령어 사용할때 (새프로젝ㅈ트 시작할때 생성), 현재는 미리 설정되어있음, 수정X 

사용자 인터페이스를 구축할 때 임시 데이터 사용: JSON형식(app/lib/...data.ts), (mockAPI 라이브러리 사용해도됨)
타입스크림트: 오류 및 실수 방지 (/app/lib/definitions.ts)
ㄴ Prisma (ORM): Node js 및 TypeScript 환경에서 데이터 베이스 작업을 간소화하고 휴율화하는 강력한 도구, 타입스크립트 지원 ORM(객체관계매핑)
ㄴ Drizzle (ORM): Next.js에서 Neon, PostgreSQL 등과 연동하여 가벼운 SQL 친화적 데이터베이스 작업을 가능하게 하는 라이브러리

>_ pnpm i
>_ pnpm dev


### step2. CSS 스타일링 : 홈페이지 작업을 함께 진행하면서 애플리케이션 스타일을 지정하는 다양한 방법
- Tailwind: create-next-app 으로 next 새프로젝트 생성시, Tailwind 사용여부 물어봄 (react랑 다르게 설정을 안해도 되서 편함)
- CSS Modules: 고유한 클래스 이름을 자동을 생성하여 CSS를 구성 요소로 제한할 수 있으며 스타일 충돌 걱정 없음
- clsx: 라이브러리로 조건부 스타일 및 클래스 선언에 용이, className={clsx('inline-flex items-center rounded-full px-2 py-1 text-sm', { 'bg-gray-100 text-gray-500': status == 'pending', 'bg-green-500 text-white': status === 'paid' })} => status값에 따라 스타일 조건부 처리 
- Sass(.scss) 파일을 기본적으로 지원함?
- CSS-in-JS (styled-jsx, styled-components, emotion)


### step3. 폰트 및 이미지 최적화 : 사용자 지정 폰트 및 히어로 이미지 추가
- 폰트 최적화 (next/font): 사용자 지정 폰트일 경우 지정폰트를 다운받고 적용할려면 폰트의 레이아웃이 변동되는 문제 (시스템폰트->지정폰트, 딜레이)를 Next.js모듈에서 자동으로 최적화 해줌
ㄴ 이 프로젝트에서는 /app/ui/fonts.ts 파일에사 불러 오고, html > body에 인라인으로 적용 (해당파일에서 임포트는 해야함)
- 이미지 최적화 (/public): 정적 자산 최상의 폴더
ㄴ 수동 시: 반응형화면에 맞췄는지, 기기별 이미지 크기 지정, 이미지 로드시 레이아웃 변경 됨을 방지, 사용자 화면 밖의 이미지 지연 로드 등으로 이미지 최적화를 수동으로
ㄴ 자동 시: next/image 컴포넌트를 사용하여 이미지를 자동으로 최적화
- 자동, Image(next/image) 컴포넌트 - html img 태그의 확장 기능
  ㄴ 이미지 로딩 시 레이아웃이 자동으로 변경되는 것을 방지, 화면  크기가 작은 기기에 큰 이미지를 전송하지 않도록 이미지 크기를 조정
  ㄴ 기본적으로 이미지 지연로딩(이미지가 뷰포트에 들어올때 로드), WebP와 같은 최신 형식으로 이미지 제공(AVIF 브라우저 지원 하는 경우만)
  ㄴ import Image next/font; <Image src="url" className="hidden md:block" /> <Image src="url" className="block md:hidden" />


### step4. 레이아웃 및 페이지 생성 (프로젝트 구조)
- 중첩 라우팅: Next.js는 폴더를 사용하여 라우팅 (app폴더가 root / Root Segment/Segment/leaf Segment), 해당 경로 폴더내 page.tsx가 index.
- /app/(경로명)/page.tsx -> /(경로명), /app/api/route.js -> /api, /app/_(폴더명) -> 비공개폴더(page.tsx접근x) 
- app 폴더안에 경로에 영향을 주지 않고 그룹으로 나누려면 (괄호)사용. /app/(shop)/account/page.js -> /account
- 로딩 스켈레톤 처리: 해당경로 내 loading.js. -> /app/dashboard/(overview)/loading.tsx, page.tsx 
- (특이구조) 여러 루트 레이아웃 생성 (각 라우트 그룹 내에 layout.js생성), layout.js파일에는 <root><html> 또는 <root><body> 태그 추가 
  ㄴ /app/layout.js -> /app/(marketing/layout.js),(shop/layout.js)

- 구조방법1: (app에는 라우팅만) /app 폴더는 라우팅을 목적으로만 사용 -> 프로젝트root/components,lib,app 등으로 사용
- 구조방법2: (app에 모두포함) /app 폴더에 모두 포함 -> 프로젝트root/app/components,lib,(라우트 세그먼트) 등으로 사용
- 구조방법3: 기능 및 경로별로 프로젝트 파일을 분리, (전역용이 있고 각 세그먼트에도 세그먼트용 폴더및파일 존재) -> app/components,lib,(라우트 세그먼트)/(components,lib,page.js)
- 구조방법4: Next.js에서는 app폴더를 src폴더 내에 저장하는 것을 지원. -> /src/app

- 대시보드 + 대시보드 레이아웃 만들기 + 고객페이지, 청구서 페이지 추가 
  ㄴ /app/dashboard/customers/page.tsx 만들기 -> /dashboard/customers 
  ㄴ /app/dashboard/invoices/page.tsx 만들기 -> /dashboard/invoices 
  ㄴ /app/dashboard/layout.tsx 만들기 -> ({children}: {children: ReactNode})

- Next.js에서 Layout.tsx를 사용하면 레이아웃은 렌더링되지 않고 페이지 구성 요소만 업데이트 -> 부분 렌더링 (페이지 전환시, 클라이언트 측 리액트 상태 유지)
- 루트 레이아웃 (/app/layout.tsx): Next.js애플리케이션에서 필수, 이곳에서 추가하는 요소는 애플리케이션 모든페이지에서 공유
  ㄴ <head><html><body> 태그 수정 및 메타데이터를 추가


### step5. 페이지간 이동 (네비게이션 구성)
- 네비게이션 최적화: SPA 프레임워크로 페이지 이동이 아닌 하나의 페이지에서 변경된 부분만 업데이트 가능함, 전체새로고침 안되고 좀더 쾌적하게 작동 -> <Link />
- <Link href="이동할페이지"><Link>: import Link next/link; 임포트 후 사용
- 자동 코드 분활: 기존 React SPA와는 다르게, 경로별로 자동 코드 분활하여, 다른페이지에서 오류가 나도 해당페이지에서는 정상작동, 또한 코드양도 줄어서 속도도 빠름
- 사전 로드: <Link> 컴포넌트가 뷰포트에 보이게 되면, 연결된 경로의 코드를 백그라운드 로드되어, 페이지 전환이 거의 즉각적으로 빠름

- use client : 서버사이드렌더링이 필요 없는 페이지에서 선언 (v13=<), 모든페이지 모든 인터랙션이 필요한 컴포넌트에서만 제한적 사용하는 것이 좋음 
  ㄴ 컴포넌트가 브라우저 환경에서 상화 작용이 필요할때, useState, useEffect를 사용하여 버튼클릭/폼제출 등 이벤트 처리
  ㄴ 브라우저 api접근 (window, document), 브라우저 환경에서만 제공되는 api를 사용할때
  ㄴ 컴포넌트 하이드레이션(Hydration): 서버에서 렌더링 된 html측 js를 연결하여 동적인 페이지로 활성화 시키는 과정이 필요할때
  ㄴ 스타일링 라이브러리: styled-components 등의 일부 스타일링 라이브러리는 클라이언트 환경에서 작동

- usePathname() : import { usePathname } from 'next/navigation'; import 후 사용, 현재 경로를 가져옴 -> 현재 위치 표시
  ㄴ clsx라이브러리: 조건부 className 처리 import clsx from 'clsx';

### step6. 데이터베이스 설정
- 데이터베이스 설정 및 배포: GitHub https://docs.github.com/en/repositories/creating-and-managing-repositories/quickstart-for-repositories
- Vercel: https://vercel.com/signup
- bash: npm i -g vercel / vercel login / vercel link (연결및생성) / vercel --prod (배포)







