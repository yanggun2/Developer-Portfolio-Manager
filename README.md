# Developer Portfolio Manager

Flutter와 Firebase로 만든 **개발자 포트폴리오 등록·관리·공유 앱**입니다. 앱프로그래밍 1학기 프로젝트로, 프로젝트 설명과 기술 스택, 링크, 썸네일을 한곳에서 관리합니다.

## 주요 기능

- 이메일·비밀번호 회원가입 및 로그인: Firebase Authentication 연동
- 포트폴리오 등록·수정·삭제, Firestore 실시간 목록 갱신
- 이름 검색과 기술 스택 필터, 검색 입력 300ms 디바운스
- 썸네일 선택 및 이미지 리사이즈·JPEG 압축 후 Base64 저장
- 프로젝트 링크 복사 및 QR 코드 표시
- 다크 테마 UI

## 기술 스택

Flutter · Dart · Firebase Authentication · Cloud Firestore · file_picker · image · qr_flutter

`pubspec.yaml`의 Dart SDK 조건은 `^3.8.1`입니다. Firebase Storage 의존성도 포함되어 있으나 현재 등록 화면은 이미지를 Base64로 Firestore 문서에 저장합니다.

## 프로젝트 구조

```text
lib/
├── main.dart                       # Firebase 초기화 및 인증 상태에 따른 화면 전환
├── auth_screen.dart                # 로그인·회원가입
├── firebase_options.dart           # 플랫폼별 Firebase 설정
├── screens/home_screen.dart        # 실시간 목록·검색·필터·삭제
└── services/
    ├── portfolio_form_screen.dart  # 등록·수정 및 이미지 처리
    ├── portfolio_card.dart         # 카드·링크 복사·QR 코드
    └── firestore_service.dart      # 사용자별 데이터 접근 보조 코드
android/ ios/ web/                  # 플랫폼 프로젝트
docs/                             # 원본에 포함된 웹 빌드 산출물
```

## 실행 준비

1. Dart 3.8.1 이상을 제공하는 호환 Flutter SDK를 설치합니다.
2. Firebase 프로젝트에서 이메일/비밀번호 인증과 Cloud Firestore를 설정합니다.
3. 본인 Firebase 프로젝트로 FlutterFire 설정을 생성합니다. Android 등 플랫폼 설정도 함께 확인합니다.

```bash
flutter pub get
dart pub global activate flutterfire_cli
flutterfire configure
flutter run -d chrome
```

웹 대신 Android 또는 iOS 기기를 선택할 수도 있습니다. 현재 Firebase 설정에는 macOS·Linux가 구성되어 있지 않습니다. Firebase CLI 및 로그인 등 FlutterFire CLI의 사전 준비가 필요합니다.

## 데이터 및 구현 참고

현재 화면은 `portfolios` 컬렉션의 `name`, `description`, `stack`, `link`, `thumbnailBase64`, `createdAt` 필드를 사용합니다. 별도 `FirestoreService`의 사용자별 하위 컬렉션 구조와 화면의 데이터 접근 방식은 다릅니다. 사용자별 비공개 포트폴리오로 운영하려면 소유자 필드·조회 방식·Firestore 규칙을 함께 맞춰야 합니다.

원본의 `docs/`는 이전 빌드 결과이므로 새 저장소 주소에 맞는 재빌드·배포 설정이 필요합니다. 저장소 분리 과정에서 앱 동작 코드는 변경하지 않았으며 실제 Firebase 연결·기기 실행은 별도 확인이 필요합니다.

## 출처

[3Class-App](https://github.com/yanggun2/3Class-App)의 `앱프로그래밍 1학기 프로젝트/portfolio_manager` 폴더에서 분리했습니다. 원본 저장소는 유지합니다.
