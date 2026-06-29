<div align="center">

<img width="100%" height="100%" alt="munaro mockup" src="https://github.com/user-attachments/assets/0eac95fb-c3e4-447e-9237-cbf61f73278f" />

### 위치기반 문화유산 탐방 게임

**공공 관광지 데이터 × AI 퀴즈 자동 생성 × 시즌 랭킹**

[![Flutter](https://img.shields.io/badge/Flutter-3.x-02569B?logo=flutter)](https://flutter.dev)
[![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.5.0-6DB33F?logo=springboot)](https://spring.io/projects/spring-boot)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Supabase-4169E1?logo=postgresql)](https://supabase.com)
[![OpenAI](https://img.shields.io/badge/OpenAI-gpt--4.1--mini-412991?logo=openai)](https://platform.openai.com)
[![AWS](https://img.shields.io/badge/AWS-Elastic_Beanstalk-FF9900?logo=amazonaws)](https://aws.amazon.com/elasticbeanstalk)

</div>

---

## 프로젝트 소개

전국 161개 지자체가 제공하는 공공 관광지 정보를 활용하여, 사용자가 관광지를 직접 방문하고 AI가 생성한 퀴즈를 풀며 문화·역사를 체험 학습하는 위치기반 모바일 게임입니다.

```
탐색 → 관광지 방문 → AI 퀴즈 풀이 → 점수 획득 → 시즌 랭킹 경쟁
```

기존 지도 앱은 정보 조회에 그치고, 위치 기반 게임은 공공 문화데이터와 무관합니다. Munaro는 **문화체육관광부 전국관광지정보표준데이터**를 지도·퀴즈 생성의 공통 원천으로 활용하여 이 둘의 한계를 동시에 해소합니다.

---

## 서비스 핵심 화면

| 로그인 및 회원가입 |
|:---:|
| <img width="80%" height="80%" alt="로그인 및 회원가입 사진" src="https://github.com/user-attachments/assets/a87cd06e-cfb8-49bc-87de-973864cd2592" /> |

| 홈 화면 및 관광지 상세 |
|:---:|
| <img width="80%" height="80%" alt="홈 화면 및 관광지 상세 사진" src="https://github.com/user-attachments/assets/1eba531d-ec3d-47d4-a71a-8b3e0ff7eee0" /> |

| 퀴즈 풀이 및 퀴즈 결과 |
|:---:|
| <img width="80%" height="80%" alt="퀴즈 풀이 및 퀴즈 결과" src="https://github.com/user-attachments/assets/23a6764a-e373-42ed-9d58-40e13a415544" /> |

| 시즌 랭킹 및 마이페이지 |
|:---:|
| <img width="80%" height="80%" alt="시즌 랭킹 및 마이페이지" src="https://github.com/user-attachments/assets/f3c0dd3b-691d-4bc8-b2a9-2dbd0c4c2095" /> |

---

## 주요 기능

| 기능 | 설명 |
|------|------|
| **GPS 기반 관광지 탐색** | 사용자 위치 기준 주변 관광지를 카카오맵 마커로 표시. 이동 시 자동 재요청 |
| **공공데이터 상세 화면** | 관광지소개·주소·편의시설·수용인원·연락처 등 표준데이터 직접 표시 |
| **AI 퀴즈 자동 생성** | OpenAI gpt-4.1-mini가 관광지소개 원문으로 3문항·4지선다 퀴즈 생성 |
| **서버 채점 · 점수 적립** | 정답 정보는 서버에서만 보관. 문항당 15점, 60점 이상 시 시즌 점수 반영 |
| **월간 시즌 랭킹** | 매시간 자동 롤오버. 현재/과거 시즌 조회, 포디엄 1~3위, 내 순위 고정 |
| **퀴즈 이력 · 복습** | 관광지별 정답률·획득 점수·문항별 정답/오답 이력 보관 |
| **소셜 로그인** | 카카오 OAuth, Google OAuth, 이메일+비밀번호 지원 |
| **마이페이지** | 누적 점수·완료 장소·뱃지·최근 탐험 지역 한 페이지 요약 |

---

## 시스템 아키텍처

<img width="100%" alt="시스템 아키텍쳐" src="https://github.com/user-attachments/assets/2bbb2ef7-f51f-4817-bfec-2a940dc9702f" />

---

## 기술 스택

| 영역 | 기술 |
|------|------|
| **Client** | Flutter 3, Riverpod, Dio, Kakao Map Plugin, Geolocator, flutter_secure_storage |
| **Server** | Spring Boot 3.5.0, Java 17, Spring Security, JPA, JWT |
| **DB** | PostgreSQL (Supabase 호스팅) |
| **AI** | OpenAI Responses API — gpt-4.1-mini, JSON Schema strict |
| **Infra** | AWS Elastic Beanstalk |
| **인증** | Kakao OAuth, Google OAuth, 이메일(BCrypt), JWT Access/Refresh |

---

## 데이터 모델 (ERD)

<img width="100%" alt="ERD" src="https://github.com/user-attachments/assets/c30eb632-0dcd-4a0a-bcf7-81d6c28ecbd4" />


`tourist_spots`를 중심으로 퀴즈 콘텐츠(`quizzes → quiz_questions → quiz_choices`), 사용자 제출 이력(`quiz_submissions`), 점수·시즌·랭킹이 연결되는 구조입니다.

---

## 레포지토리 구조

```
munaro/
├── Munaro_front/          # Flutter 클라이언트
│   ├── lib/
│   │   ├── layouts/       # 로그인 · 회원가입
│   │   ├── models/        # 데이터 모델
│   │   ├── repositories/  # API 호출 (Riverpod Provider)
│   │   ├── screens/       # 화면 (홈·퀴즈·랭킹·마이페이지 …)
│   │   └── utils/         # JWT 파싱, 위치, 에러 처리
│   └── pubspec.yaml
│
└── munaro_backend/        # Spring Boot API 서버
    └── backend/
        └── src/main/java/com/carrot/munaro/
            ├── auth/          # 인증 · JWT
            ├── tourist_spot/  # 관광지 도메인
            ├── quiz/          # 퀴즈 생성·채점·이력
            ├── score/         # 점수·시즌·랭킹·스케줄러
            ├── user/          # 사용자·프로필·뱃지
            ├── security/      # JwtFilter · SecurityConfig
            └── global/        # 공통 응답·예외 처리
```

---

## 로컬 실행

### 백엔드

환경 변수를 설정한 뒤 실행합니다.

```bash
cd munaro_backend/backend

# 환경 변수 예시 (IDE Run Configuration 또는 .env 주입)
# DB_URL / DB_USERNAME / DB_PASSWORD
# KAKAO_REST_API_KEY / OPENAI_API_KEY / JWT_SECRET

./gradlew bootRun
# → http://localhost:5000
# → Swagger UI: http://localhost:5000/swagger-ui/index.html
```

### 프론트엔드

```bash
cd Munaro_front

# .env 파일 생성
echo "API_BASE_URL=http://localhost:5000" > .env
echo "KAKAO_NATIVE_APP_KEY=your_key" >> .env
echo "KAKAO_JAVASCRIPT_KEY=your_key" >> .env

flutter pub get
flutter run
```

---

## Team

| [NE7K](https://github.com/NE7K) | [장태훈](https://github.com/Thjanga) | [박연희](https://github.com/h2st0ry) |
| :--: | :--: | :--: |
| ![NE7K](https://github.com/NE7K.png) | ![장태훈](https://github.com/Thjanga.png) | ![박연희](https://github.com/h2st0ry.png) |
| **Project Lead** | **Frontend-Flutter** | **Backend-SpringBoot** |

---

## 데이터 출처

| 데이터명 | 제공기관 | 출처 |
|----------|----------|------|
| 전국관광지정보표준데이터 | 문화체육관광부 (161개 지자체) | [공공데이터포털](https://www.data.go.kr/data/15021141/standard.do) |

관광지소개 텍스트는 상세 화면 노출과 AI 퀴즈 생성 프롬프트 입력에 동시에 활용됩니다.

