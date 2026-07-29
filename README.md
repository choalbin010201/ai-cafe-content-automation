# 동네 카페를 위한 AI 멀티채널 홍보 콘텐츠 자동 생성 시스템

## 1. 프로젝트 개요

본 프로젝트는 동네 카페가 하나의 홍보 주제를 입력하면, AI가 인스타그램, 블로그, X용 홍보 콘텐츠를 자동으로 생성하고 Notion 데이터베이스에 저장하는 자동화 시스템이다.

Google Form을 통해 홍보 주제, 가게 종류, 타겟 고객, 콘텐츠 목적, 톤앤매너, 필수 포함 내용, 금지 표현, A/B 테스트 여부를 입력받는다. 입력된 값은 Google Sheets에 저장되고, Make 자동화 시나리오를 통해 Gemini AI에 전달된다.

Gemini는 플랫폼별 특성에 맞춰 인스타그램 콘텐츠, 블로그 콘텐츠, X 콘텐츠, 대표 이미지 생성 프롬프트, A/B 테스트 결과를 생성한다. 최종 결과는 Notion 데이터베이스에 플랫폼별 컬럼으로 구분되어 저장된다.

---

## 2. 주요 기능

- Google Form을 통한 홍보 정보 입력
- Google Sheets에 입력값 자동 저장
- Make를 통한 자동화 시나리오 실행
- Gemini를 활용한 플랫폼별 콘텐츠 생성
- Notion 데이터베이스에 결과 자동 저장
- 대표 이미지 생성 프롬프트 생성
- A/B 테스트 결과 생성

---

## 3. 사용 도구

| 도구 | 역할 |
|---|---|
| Google Form | 홍보 콘텐츠 생성에 필요한 입력값 수집 |
| Google Sheets | Google Form 응답 저장 |
| Make | 전체 자동화 워크플로우 연결 |
| Gemini | 플랫폼별 홍보 콘텐츠 생성 |
| Notion | 생성 결과 저장 및 팀 프로젝트 정리 |
| 이미지 생성 AI | 대표 이미지 생성 |
| GitHub | 최종 보고서, 프롬프트, 결과물 정리 |

---

## 4. 전체 워크플로우

```text
Google Form
→ Google Sheets
→ Make: Watch New Rows
→ Gemini 1: Instagram 콘텐츠 생성
→ Gemini 2: Blog 콘텐츠 생성
→ Gemini 3: X 콘텐츠 생성
→ Gemini 4: Image Prompt 및 A/B Test 생성
→ Notion: Data Source Item 생성
```

자동화 흐름은 다음과 같다.

1. 사용자가 Google Form에 카페 홍보 정보를 입력한다.
2. 입력된 응답은 Google Sheets에 자동 저장된다.
3. Make의 Google Sheets 모듈이 새 행을 감지한다.
4. Gemini 1 모듈이 인스타그램용 캡션과 해시태그를 생성한다.
5. Gemini 2 모듈이 블로그용 제목과 본문을 생성한다.
6. Gemini 3 모듈이 X용 280자 이내 게시글을 생성한다.
7. Gemini 4 모듈이 대표 이미지 생성 프롬프트와 A/B 테스트 결과를 생성한다.
8. Notion 모듈이 생성 결과를 Notion 데이터베이스에 플랫폼별로 저장한다.

---

## 5. 폴더 구조

```text
ai-cafe-content-automation/
├─ README.md
├─ prompts/
│  ├─ instagram_prompt.md
│  ├─ blog_prompt.md
│  ├─ x_prompt.md
│  └─ image_ab_prompt.md
├─ results/
│  └─ sample_output.md
└─ assets/
   ├─ google_form.png
   ├─ google_sheets.png
   ├─ make_workflow.png
   ├─ notion_result.png
   └─ generated_image.png
```

---

## 6. Google Form 입력 항목

| 입력 항목 | 설명 |
|---|---|
| 홍보 주제 | 생성할 콘텐츠의 핵심 주제 |
| 가게 종류 | 홍보 대상 업종 |
| 타겟 고객 | 콘텐츠를 전달할 주요 고객층 |
| 콘텐츠 목적 | 신메뉴 홍보, 이벤트 안내, 신규 고객 유입 등 |
| 톤앤매너 | 친근한 톤, 감성적인 톤, 전문적인 톤 등 |
| 반드시 포함해야 할 내용 | 콘텐츠에 꼭 들어가야 하는 정보 |
| 사용하면 안 되는 표현/주의사항 | 과장 표현, 임의 정보 생성 방지 조건 |
| A/B 테스트 여부 | 두 가지 톤의 콘텐츠 비교 여부 |

---

## 7. Gemini 프롬프트 구성

본 프로젝트에서는 플랫폼별 결과물 품질을 높이기 위해 Gemini 프롬프트를 4개로 분리하였다.

| 파일 | 목적 |
|---|---|
| [instagram_prompt.md](./prompts/instagram_prompt.md) | 인스타그램 캡션 및 해시태그 생성 |
| [blog_prompt.md](./prompts/blog_prompt.md) | 블로그 제목 및 본문 생성 |
| [x_prompt.md](./prompts/x_prompt.md) | X용 280자 이내 게시글 생성 |
| [image_ab_prompt.md](./prompts/image_ab_prompt.md) | 대표 이미지 프롬프트 및 A/B 테스트 결과 생성 |

---

## 8. Notion 데이터베이스 구조

생성 결과는 하나의 긴 텍스트로 저장하지 않고, 플랫폼별로 구분하여 저장하였다.

| 컬럼명 | 저장 내용 |
|---|---|
| 제목 | 콘텐츠 생성 결과 제목 |
| 홍보 주제 | Google Form에서 입력한 홍보 주제 |
| 가게 종류 | 홍보 대상 업종 |
| 타겟 고객 | 주요 고객층 |
| 콘텐츠 목적 | 콘텐츠 제작 목적 |
| 톤앤매너 | 원하는 문체와 분위기 |
| 인스타그램 콘텐츠 | 인스타그램 캡션 및 해시태그 |
| 블로그 콘텐츠 | 블로그 제목 및 본문 |
| X 콘텐츠 | X에 게시할 280자 이내 문구 |
| 대표 이미지 프롬프트 | 이미지 생성 AI에 사용할 영어 프롬프트 |
| A/B 테스트 결과 | A안/B안 비교 및 추천 사용처 |
| 상태 | 생성 완료 여부 |
| 생성일 | 결과 생성 날짜 |

---

## 9. 실행 결과

실행 결과 예시는 [sample_output.md](./results/sample_output.md)에 정리하였다.

또한 `assets/` 폴더에는 Google Form, Google Sheets, Make 워크플로우, Notion 결과, 생성 이미지 등의 증빙 이미지를 저장한다.

---

## 10. 문제 해결 과정

초기 구현에서는 Gemini가 생성한 전체 결과를 Notion의 단일 텍스트 컬럼에 저장하려고 하였다. 그러나 Make 실행 과정에서 Notion 저장 단계에서 다음과 같은 오류가 발생하였다.

```text
body.properties.생성 결과.rich_text[0].text.content.length should be <= 2000
```

이는 Gemini가 생성한 전체 결과가 Notion의 단일 텍스트 속성 제한을 초과했기 때문이다.

이를 해결하기 위해 생성 결과를 하나의 컬럼에 몰아서 저장하지 않고, 인스타그램 콘텐츠, 블로그 콘텐츠, X 콘텐츠, 대표 이미지 프롬프트, A/B 테스트 결과로 분리하였다.

또한 Gemini 모듈도 하나의 통합 프롬프트가 아니라 플랫폼별 4개 모듈로 나누어 구성하였다. 이를 통해 각 플랫폼에 맞는 결과물을 더 명확하게 생성하고, Notion 데이터베이스에서도 결과를 쉽게 확인할 수 있도록 개선하였다.

---

## 11. 팀원 역할

| 이름 | 역할 |
|---|---|
| 조영경 | 전체 자동화 설계, Make-Gemini-Notion 연결, 최종 보고서 정리 |
| 정인용 | Google Form 및 Google Sheets 입력 구조 설계 |
| 이현경 | 플랫폼별 프롬프트 초안 작성 및 콘텐츠 검수 |
| 고한결 | Notion 페이지 정리, 이미지 생성 결과 정리, 스크린샷 수집 |

---

## 12. 개선 가능성

1. 이미지 생성 AI까지 Make에 직접 연결하여 대표 이미지 생성도 완전 자동화한다.
2. Notion에 저장된 콘텐츠를 실제 SNS 예약 발행 도구와 연결한다.
3. A/B 테스트 결과를 실제 반응 데이터와 비교하여 성과 기반 추천이 가능하도록 확장한다.
4. 업종을 카페뿐만 아니라 음식점, 미용실, 소매점 등으로 확장한다.
5. 사용자가 원하는 브랜드 톤을 더 세분화하여 프롬프트에 반영한다.
