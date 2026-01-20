# Pull Request (PR) 전략 계획

이 문서는 완성된 프로젝트(`runpod_stt`)를 논리적인 기능 단위로 나누어 PR을 생성하기 위한 가이드입니다.
Git 히스토리를 깔끔하게 유지하고, 리뷰어가 코드를 쉽게 파악할 수 있도록 4단계로 구성했습니다.

---

## 1. 단계: 프로젝트 초기 세팅 (Infrastructure & Skeleton)
**목표**: 프로젝트의 뼈대를 잡고, 실행 환경(Docker)을 구성합니다.

- **포함 내용**:
    - `README.md` (초기 버전)
    - `.gitignore`
    - `stt_server/Dockerfile` (Base Image, 패키지 설치 등)
    - `stt_server/builder/download_model.py` (모델 다운로드 스크립트)
    - `ai_server/requirements.txt` (서버용)
    - `stt_server/requirements.txt` (워커용)
    - `TROUBLESHOOTING.md` (초기 트러블 슈팅 로그)

- **PR 제목 예시**: `chore: Initial project setup and Docker configuration`

---

## 2. 단계: RunPod Worker 구현 (STT Server)
**목표**: 실제 AI 추론을 담당하는 Worker의 핵심 로직을 구현합니다.

- **포함 내용**:
    - `stt_server/config.py` (설정)
    - `stt_server/utils/audio_loader.py` (오디오 다운로드 유틸)
    - `stt_server/services/model_service.py` (모델 로딩)
    - `stt_server/services/inference_service.py` (추론 로직)
    - `stt_server/handler.py` (RunPod 핸들러 진입점)

- **PR 제목 예시**: `feat(stt): Implement Whisper inference worker for RunPod`

---

## 3. 단계: AI Server 구현 (FastAPI Client)
**목표**: 클라이언트 요청을 받아 Worker로 전달하는 FastAPI 서버를 구현합니다.

- **포함 내용**:
    - `ai_server/.env` (템플릿 또는 예시)
    - `ai_server/app/core/config.py` (서버 설정)
    - `ai_server/app/schemas/transcription.py` (Pydantic 스키마)
    - `ai_server/app/services/runpod_client.py` (RunPod 연동 클라이언트)
    - `ai_server/app/api/v1/endpoints/transcription.py` (API 엔드포인트)
    - `ai_server/app/api/v1/router.py` (라우터 설정)
    - `ai_server/app/main.py` (메인 앱 실행)

- **PR 제목 예시**: `feat(ai): Implement FastAPI server and RunPod client`

---

## 4. 단계: 문서화 및 최종 안정화 (Documentation & Polish)
**목표**: 최종적으로 발견된 버그를 수정하고 문서를 보완합니다.

- **포함 내용**:
    - `README.md` (배포 가이드, 실행 방법 업데이트)
    - `TROUBLESHOOTING.md` (최종 트러블 슈팅 내용 반영)
    - 코드 리팩토링 및 버그 픽스 반영 (예: `handler.py`의 `model_dump` 제거 등)

- **PR 제목 예시**: `docs: Update documentation and apply final fixes`
