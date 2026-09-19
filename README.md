# 필라테스 시퀀스 빌더

회원 프로필과 메인 기구·집중 부위를 고르면 수업 시퀀스를 만드는 웹앱입니다.
Google 로그인과 Cloud Firestore를 사용해 아이패드·컴퓨터 사이에서 데이터를 실시간 동기화합니다.

## 수업 구성

1. 서서 하는 스트레칭: 5분
2. 박스/보수 스텝업, 빠르게 걷기, 니킥, 런지 조합 유산소: 3~5분
3. 매트 복부: 최대 5분
4. 선택 기구 메인: 힙/하체/상체/코어/전신 중 한 부위를 중심으로 구성
5. 쿨다운: 5분

메인 파트는 비교적 쉬운 동작부터 강한 동작 순서로 정렬됩니다. 회원의 주의사항과 초급 레벨도 후보 필터에 반영하지만, 자동 생성 결과는 반드시 강사가 최종 확인해야 합니다.

## 새 동작 추가

`동작 데이터 편집` 탭에서 기구를 선택한 뒤 새 동작명, 카테고리, 집중 부위, 시간을 입력하고 `+ 동작 추가`를 누르세요.

수업 준비 중에는 `시퀀스 만들기` 결과 상단의 `+ 새 동작 바로 추가`를 사용할 수 있습니다. 동작명만 입력하면 현재 기구·현재 집중 부위·3분·`빠른 추가` 카테고리로 현재 시퀀스와 동작 DB에 동시에 저장됩니다. 이름·카테고리·집중 부위·시간·스프링은 나중에 `동작 데이터 편집`에서 바꿀 수 있습니다.

- 추가한 동작은 즉시 시퀀스 생성 후보에 포함됩니다.
- 직접 추가한 동작만 완전히 삭제할 수 있습니다.
- 기본 동작과 직접 추가한 동작 모두 시간·스프링·제외 여부를 수정할 수 있습니다.
- 직접 추가한 데이터와 수정·제외 설정은 로그인한 Google 계정에 저장됩니다.

## Firebase 설정

1. Firebase Authentication의 `Sign-in method`에서 Google 로그인을 활성화합니다.
2. Firestore Database는 Standard edition으로 생성합니다.
3. `firestore.rules`의 내용을 Firebase Console → Firestore Database → Rules에 붙여넣고 게시합니다.
4. GitHub Pages 배포 후 Firebase Console → Authentication → Settings → Authorized domains에 `깃허브아이디.github.io`를 추가합니다.

## GitHub Pages 배포

1. GitHub에서 Public 저장소를 생성합니다. 예: `pilates-sequencer`
2. 이 폴더 안의 모든 파일을 저장소 루트에 업로드합니다.
3. 저장소 `Settings → Pages`에서 `Deploy from a branch`, `main`, `/ (root)`를 선택합니다.
4. `https://깃허브아이디.github.io/pilates-sequencer/`에 접속합니다.
5. 동생분이 아이패드와 컴퓨터에서 같은 Google 계정으로 로그인하면 됩니다.

## 동기화 범위

- 회원 프로필
- 직접 추가한 동작
- 동작 시간·스프링·제외 설정
- 저장한 시퀀스

기본 교재 동작은 `data.js`에서 읽고, 변경 데이터만 Firestore에 저장합니다. 브라우저 `localStorage`는 네트워크 오류에 대비한 로컬 캐시로 유지됩니다. 기존 버전에서 저장한 로컬 데이터는 최초로 로그인한 Google 계정에 한 번 자동 이전됩니다.

## 파일 구성

- `index.html`: 화면, 시퀀스 생성 규칙, Google 로그인·동기화 기능
- `data.js`: Barrel, Cadillac, Chair, Mat, Reformer 교재 기반 동작 목록
- `firebase-config.js`: Firebase 웹 앱 연결 설정
- `firestore.rules`: 로그인한 본인의 데이터만 허용하는 보안 규칙

교재의 손글씨 표시는 오인식 가능성이 있으므로, 제외 동작과 세팅은 강사가 최종 검수해야 합니다.
