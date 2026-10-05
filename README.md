# 사랑니 YouTube 영상·댓글 수집 및 수기 코딩

## 새 GitHub 저장소에 올리기

1. ZIP을 압축 해제합니다.
2. GitHub에서 새 저장소를 만듭니다. 예: `Youtube_OMFS_recovery`.
3. `Upload files` 또는 `Add file → Upload files`를 선택합니다.
4. 압축 해제한 폴더 **안의 파일들과 pages 폴더**를 함께 드래그하여 업로드합니다. ZIP 자체를 올리지 마세요.
5. `Commit changes`로 저장합니다.

저장소 첫 화면에 `main.py`, `requirements.txt`, `README.md`, `secrets.example.toml`, `pages`가 보여야 합니다.
`pages/1_댓글_분석.py`의 폴더 구조를 유지하세요. 바깥의 `Youtube_OMFS_ready` 폴더를 통째로 중첩 업로드하지 마세요.
`.gitignore`는 숨김 파일일 수 있습니다. 업로드하지 못해도 앱 실행에는 영향이 없지만, 실제 비밀값 파일은 업로드하지 마세요.

## Streamlit 배포

- Repository: 방금 만든 저장소
- Branch: `main` (GitHub에 표시된 실제 기본 브랜치를 선택)
- Main file path: `main.py`
- Python: 3.12 권장 (이 패키지를 실제 Cloud 환경에서 실행 검증한 것은 아닙니다)
- App URL: 사용 가능한 새 주소

배포 화면의 Advanced settings 또는 앱 설정의 Secrets에 아래 이름으로 **기존 값을 그대로** 입력합니다.

```toml
YOUTUBE_API_KEY = "기존 앱의 YouTube API 키"
SHEET_URL = "기존 앱의 Google Apps Script 웹 앱 URL (/exec로 끝나는 주소)"
```

예시 문구 자체를 붙여 넣으면 연결되지 않습니다. 실제 값은 기존 앱의 Secrets에서 직접 복사하세요.
`secrets.example.toml`은 참고용이며 자동으로 읽히는 설정 파일이 아닙니다.

## 기존 Google Sheets에 계속 저장하기

이 앱은 `SHEET_URL`로 지정된 기존 Apps Script에 데이터를 전송합니다.
새 GitHub 저장소나 새 Streamlit 주소를 만들었다는 이유만으로 Google Sheet나 Apps Script를 새로 만들 필요는 없습니다.
기존 `SHEET_URL`과 Apps Script의 접근 권한/배포가 유효하면 같은 시트에 저장하도록 요청합니다.
실제 Apps Script 코드는 이 저장소에 없어서 접근 조건과 실행 상태는 검증하지 못했습니다.
Apps Script에 별도의 인증 또는 발신지 제한을 추가했다면 해당 설정도 확인해야 합니다.

- 기존 Apps Script와 Google Sheet는 그대로 사용하세요.
- 기존 앱은 새 앱 구동과 저장 확인이 끝날 때까지 유지하세요.
- 기존 Google Sheets 자료를 새 앱으로 자동 불러오는 기능은 없습니다. 저장 대상만 동일하게 유지됩니다.
- 기존 브라우저의 미저장 코딩 결과와 수집 목록은 새 앱으로 자동 이전되지 않습니다. 보유한 CSV를 댓글 분석 페이지에 업로드할 수 있습니다.
- 기존 앱에서 이미 저장한 코딩 페이지를 새 앱에서 다시 제출하지 않도록 유의하세요. 중복 판정은 기존 Apps Script 구현에 따릅니다.

## 포함된 기능

- 조회수 기준 영상 검색, 검색 후보 최대 500개
- 영상별 최상위 댓글 최대 100개 수집
- 키워드 자동 제안과 연구자 수기 코딩
- 20개 단위의 기존 Google Sheets 전송
- CSV 다운로드

## 이번 정리 범위와 검증

원본: `Nickname-kr/Youtube_OMFS`, 커밋 `cc71509e85b3af2478894de55713e58071613bba`.

- `main.py`와 댓글 분석 페이지는 원본 그대로 유지했습니다.
- 직접 사용하는 streamlit, pandas, requests를 requirements.txt에 명시했습니다.
- 업로드·배포 안내, 비밀값 예시와 .gitignore를 추가했습니다.
- Python 파일 문법과 ZIP 내부 폴더 구조를 확인했습니다.
- 버전 범위는 의존성 선언이며 고정된 실행 환경을 보장하지 않습니다.
- 실제 Streamlit 배포, YouTube API 호출, Google Sheets 저장은 검증하지 않았습니다.
- 이 패키지가 Streamlit 플랫폼의 서버 시작 장애 자체를 해결한다고 보장할 수는 없습니다.

## 로컬 실행 (선택)

```bash
python -m venv .venv
python -m pip install -r requirements.txt
python -m streamlit run main.py
```

설치 전에 생성한 가상환경을 활성화하세요. 로컬 실행 시 실제 비밀값은 `.streamlit/secrets.toml`에 넣고 GitHub에는 올리지 마세요.
