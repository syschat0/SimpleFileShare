# Simple File Share

**Simple File Share**는 로컬 네트워크에서 파일을 업로드·관리·공유할 수 있는 독립형 파일 공유 서비스입니다. Apple에서 영감을 받은 사진 중심의 디자인으로 구성되어 있으며, 내장 서버와 데스크톱 앱으로 동작합니다. 같은 네트워크에 연결된 기기에서는 웹 브라우저로도 접속할 수 있습니다.

> **테스트 환경**: Windows 11에서 개발·실행·빌드가 검증되었습니다.

[English README](README_en.md)

---

## ✨ 주요 기능

- **Apple 스타일 UI/UX**: Apple 디자인 시스템을 기반으로 한 인터페이스. 엣지 투 엣지 타일, SF Pro 타이포그래피, Action Blue 단일 강조색을 사용합니다.
- **드래그 앤 드롭 업로드**: 브라우저 또는 데스크톱 앱 창에 파일을 끌어다 놓아 업로드할 수 있습니다.
- **독립형 데스크톱 앱**: Pywebview로 빌드된 `.exe`로 실행 가능합니다. 최종 사용자 PC에 Python 설치가 필요 없습니다.
- **로컬 네트워크 공유**: 같은 네트워크의 모든 기기에서 접속할 수 있는 웹 서버를 자동으로 띄웁니다.
- **실시간 시스템 로그**: 서버 상태, 연결, 내부 로그를 앱 화면에서 확인할 수 있습니다.
- **관리자 대시보드**: 포트 번호, 최대 업로드 크기, 관리자 비밀번호 등 설정을 관리할 수 있습니다.

---

## 🛠️ 기술 스택

- **백엔드**: Python 3.12, FastAPI, SQLAlchemy (SQLite), Uvicorn
- **프론트엔드**: HTML5, Vanilla CSS (Apple 디자인 시스템), Vanilla JavaScript
- **데스크톱 GUI**: Pywebview
- **패키징**: PyInstaller

---

## 🚀 빠른 시작 (Windows — BAT 파일)

이 프로젝트는 Windows 환경에서 `.bat` 스크립트로 실행·빌드할 수 있습니다.

### 사전 요구 사항

- Windows 11 (테스트 완료)
- Python 3.12 이상 ([python.org](https://www.python.org/downloads/)에서 설치, **Add to PATH** 옵션 체크)

### 1. 개발 모드 실행 — `run.bat`

소스 코드를 수정하며 앱을 실행할 때 사용합니다.

1. 저장소를 클론한 뒤 프로젝트 루트로 이동합니다.
2. `run.bat`을 더블클릭하거나, 명령 프롬프트에서 실행합니다.

   ```cmd
   run.bat
   ```

**동작 방식**
- `venv` 가상 환경이 있으면 자동으로 활성화한 뒤 `python run.py`를 실행합니다.
- `venv`가 없으면 오류 메시지를 표시합니다. 이 경우 아래 `build.bat`을 먼저 실행하거나, [수동 설치](#수동-설치-개발-환경) 절차를 따르세요.

> 최초 실행 시 `config.json`이 없으면 포트 `8000`, 기본 관리자 비밀번호 `admin`으로 자동 생성됩니다.

### 2. 환경 설정 및 빌드 — `build.bat`

가상 환경 생성, 의존성 설치, 독립 실행 파일(`.exe`) 빌드를 한 번에 수행합니다.

1. 프로젝트 루트에서 `build.bat`을 더블클릭하거나 실행합니다.

   ```cmd
   build.bat
   ```

**동작 방식**
1. Python 설치 여부 확인
2. `venv` 가상 환경이 없으면 생성
3. `requirements.txt` 의존성 설치/업데이트
4. 이전 빌드 산출물(`build`, `dist`, `.spec`) 정리
5. PyInstaller로 단일 실행 파일 빌드

**빌드 결과**
- `dist\SimpleFileShare.exe` — Python 없이 실행 가능한 독립 실행 파일

빌드가 끝나면 `dist\SimpleFileShare.exe`를 더블클릭하여 배포·실행할 수 있습니다.

### BAT 파일 요약

| 파일 | 용도 |
|------|------|
| `run.bat` | 개발 모드 실행 (`venv` 활성화 → `run.py`) |
| `build.bat` | `venv` 생성, 의존성 설치, `SimpleFileShare.exe` 빌드 |

---

## 🛠️ 수동 설치 (개발 환경)

BAT 파일 대신 직접 설정하려면 다음 절차를 따르세요.

1. **저장소 클론 및 가상 환경 생성**

   ```bash
   git clone <your-repo-url>
   cd SimpleFileShare
   python -m venv venv
   ```

2. **가상 환경 활성화 (Windows)**

   ```cmd
   venv\Scripts\activate
   ```

3. **의존성 설치**

   ```bash
   pip install -r requirements.txt
   ```

4. **앱 실행**

   ```bash
   python run.py
   ```

---

## 🎨 디자인 철학

프론트엔드는 CSS 프레임워크 없이 처음부터 작성되었으며, Apple에서 영감을 받은 디자인 언어를 따릅니다. (`DESIGN.md` 참고)

**주요 디자인 특징**
- **사진 중심**: UI 크롬을 최소화하고 콘텐츠가 돋보이도록 구성
- **타이포그래피**: `SF Pro Display`, `SF Pro Text`와 디스플레이 크기용 음수 자간
- **색상**: Pure White / Parchment / Near-Black 타일 교차, 인터랙션은 `Action Blue` (#0066cc) 단일 사용
- **입체감**: 표면 위 요소에만 부드러운 드롭 섀도우 적용. 장식용 그라데이션·불필요한 테두리 없음

---

## 📝 라이선스

이 프로젝트는 MIT License 하에 배포됩니다.
