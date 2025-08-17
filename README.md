# engking-voice-processor

## 소개
이 저장소는 **AI 기반 영어 학습 웹 애플리케이션** 팀 프로젝트 **Engking**의 음성 처리 모듈 중 제가 설계하고 구현한 부분만을 분리한 저장소입니다.  
AWS S3, Polly, Transcribe를 활용한 음성 업로드, 전사, 음성 합성 기능을 포함하고 있으며 Kubernetes(EKS)에 배포한 프로젝트이기 때문에 Docker Container 기반의 Application으로 개발되었습니다.

## 주요 기여
- **음성 업로드**: AWS S3 Presigned URL을 사용하여 음성 파일 업로드 기능 구현
- **음성 전사**: AWS Transcribe를 활용한 음성 파일의 텍스트 변환 기능 구현
- **음성 합성**: AWS Polly를 활용한 텍스트 기반 음성 합성 기능 구현
- **API 설계**: 음성 업로드 및 처리 결과를 반환하는 API 설계 및 구현
- **오류 및 예외 처리**: AWS 서비스와의 통신 오류 및 파일 검증 로직 추가, 헬스체크 엔드포인트 및 EFK 로깅용 예외 로그 출력

## 주요 파일 및 설명
- `app/modules/s3.py`: S3 Presigned URL 생성 및 파일 업로드/다운로드 로직
- `app/modules/transcribe.py`: AWS Transcribe를 활용한 음성 전사 로직
- `app/modules/polly.py`: AWS Polly를 활용한 음성 합성 로직
- `sh/upload_audio.sh`: S3에 음성 파일을 업로드하는 Bash 스크립트
- `sh/index.html`: Presigned URL을 사용한 클라이언트 측 파일 업로드 테스트 페이지
- `Dockerfile`: 음성 처리 애플리케이션의 Docker 이미지 생성 파일

## 실행 방법
1. **저장소 클론 및 의존성 설치**
   ```bash
   git clone https://github.com/ffwe/engking-voice-processor.git
   cd engking-voice-processor
   pip install -r requirements.txt
   ```

2. **환경 변수 설정**
   `.env` 파일을 생성하고 아래와 같이 설정합니다:
   ```
   AWS_ACCESS_KEY_ID=<your-access-key>
   AWS_SECRET_ACCESS_KEY=<your-secret-key>
   REGION_NAME=<your-region-name>
   BUCKET_NAME=<your-s3-bucket-name>
   ```

3. **로컬 서버 실행**
   ```bash
   uvicorn app.app:app --host 0.0.0.0 --port 8000 --reload
   ```

4. **테스트**
   - **음성 업로드**: `sh/upload_audio.sh` 실행
   - **Presigned URL 테스트**: `sh/index.html` 열기
   - **API 요청**: 아래와 같은 cURL 명령어 사용
     ```bash
     curl -X POST -F "file=@sample.mp3" http://127.0.0.1:8000/api/upload/
     ```

## 기술 스택
- **언어 및 라이브러리**: Python, Bash, FastAPI, Boto3
- **AWS 서비스**: S3, Transcribe, Polly
- **도구**: Docker, Uvicorn

## 참고
- 이 저장소는 제가 담당한 부분만 포함하고 있습니다. 전체 프로젝트 구조 및 다른 모듈은 아래 팀 프로젝트 레포지토리를 참고하세요.
- **팀 프로젝트 전체 레포지토리**: [Engking](https://github.com/acs5-4/engking)
