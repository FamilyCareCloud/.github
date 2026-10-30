# CareBridge

**다국어 음성·텍스트 기반 돌봄 기록 생성 및 검토 지원 AI**

영남대학교 **YU42**팀이 개발한 CareBridge는 돌봄 관찰 메모를 한국어 기록 초안으로 정리하고, 담당자가 원문과 대조하여 수정·확정한 뒤 공개 내용과 수신자를 선택하도록 지원하는 웹서비스입니다.

**[서비스 접속](https://develop.db2l4u9y804jp.amplifyapp.com/)** · 2026 AI 라이프 솔루션 챌린지 · 13번 아이디어 케어브릿지

## 서비스 흐름

**음성·텍스트 메모 → 원문 확인·AI 초안 → 담당자 검토·수정·확정 → 내용·수신자 선택 → 공개 기록 열람**

| 역할 | 주요 기능 |
|---|---|
| 작성자 | 대상자 선택, 메모 입력·음성 전사, AI 초안 생성·편집·제출 |
| 검토자 | 기관 참여 승인, 대상자 관리, 원문 대조·수정·보류·확정, 수신자 지정 공개 |
| 열람자 | 자신에게 공개된 기록과 기록 시각·공개 시각 확인 |

로그인과 업무 화면은 한국어·영어·베트남어·인도네시아어를 지원합니다. 화면 언어는 메모 작성 언어와 별도로 선택합니다. 기록 확정과 공개는 별도 단계이며, AI 결과만으로 자동 공개하지 않습니다.

## 핵심 저장소

| 저장소 | 구성과 역할 | 제출 기준 |
|---|---|---|
| [carebridge-frontend](https://github.com/FamilyCareCloud/carebridge-frontend) | React·TypeScript·Vite 기반 역할별 업무 화면, 다국어 UI, 음성 입력·AI 연동 | `main` |
| [carebridge-backend](https://github.com/FamilyCareCloud/carebridge-backend) | Node.js·AWS Lambda·Cognito·DynamoDB 기반 인증, 기관 권한, 검토·공개 API | `main` |
| [carebridge-ai](https://github.com/FamilyCareCloud/carebridge-ai) | FastAPI·Whisper·LoRA·Qwen3 기반 음성 전사, 한국어 초안, 원문 대조 QA | `main` |

프론트·백엔드의 서비스 자동 배포 기준은 `develop`입니다. 각 저장소 README에 실행 방법, 설정, 검증 자료를 안내합니다.

## 구현과 검증

- 프론트엔드: 현재 화면·권한·세션·전송·언어 테스트 91개, 린트·빌드 통과.
- 백엔드: 인증·기관 권한·검토·공개·실시간 접근 등 테스트 113개 통과.
- AI: 합성 메모 생성 94건·QA 131건 평가 후, 수정 관련 생성 22건과 QA 41건을 최종 GPU 서버에서 재검증했습니다. 변조 QA 19건은 모두 보류됐습니다.
- [AI 최종 평가 해석과 한계](https://github.com/FamilyCareCloud/carebridge-ai/blob/main/docs/REMAINING_QUALITY_2026-10-30.md)에 원본 실행 결과와 별도 원문 대조 기록을 연결했습니다.

현재 시제품은 합성·비식별 사례로 검증했습니다. AI 초안은 담당자 검토 보조용이며 공식 기록·의료 판단을 자동 확정하지 않습니다. 위 결과는 원어민·현장 검증이나 전체 번역 정확도 100%, 시간 절감 효과를 뜻하지 않습니다. AI 기능은 별도 AI 서버와 연결 환경의 가동 상태에 의존합니다.

## YU42

| 팀원 | 담당 |
|---|---|
| 임현승 | 대표·프론트엔드 |
| 전채영 | 백엔드 |
| 김우주 | AI |