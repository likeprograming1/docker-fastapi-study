# fastapi에서 docker image 생성

## 1. fastapi로 실행하기

### 1) 가상 환경 생성

Python의 `venv` 모듈을 사용하여 가상 환경을 만듭니다.

```bash
python -m venv venv
```

위 명령어는 `fastapi_project` 폴더 내에 `venv`라는 가상 환경을 생성합니다.

### 2) 가상 환경 활성화

운영체제에 따라 아래 명령어를 사용하세요.

#### Windows (CMD)

```cmd
venv\Scripts\activate
```

#### Windows (PowerShell)

```powershell
venv\Scripts\Activate.ps1
```

#### macOS/Linux (bash/zsh)

```bash
source venv/bin/activate
```

가상 환경이 활성화되면 터미널 프롬프트 앞에 `(venv)`가 표시됩니다.

---

### 3) requirements.txt 파일의 라이브러리를 설치합니다.

```bash
pip install -r requirements.txt
```

### 4) fastapi 실행

```bash
uvicorn main:app --reload
```

## 2. docker에서 실행하기

docker가 설치가 안되어 있으면 [https://www.docker.com/](https://www.docker.com/) 여기로 가셔서 설치

```bash
docker-compose up
```

### dockerfile의 설정 설명

```
FROM python:latest : 베이스가 되는 Docker Image로 python 이미지를 사용합니다.
WORKDIR /app/ : 처음 실행 시 사용 되는 경로 정보 입니다.
COPY ./main.py /app/ : 현재 경로의 main.py를 /app 경로로 복사합니다.
COPY ./requirements.txt /app/ : 현재 경로의 requirements.txt를 /app 경로로 복사합니다.
RUN pip install -r requirements.txt: 복사 된 requirements.txt를 사용하여 pip로 패키지를 추가합니다.
CMD uvicorn --host=0.0.0.0 --port 8000 main:app : uvicorn을 사용하여 main.py의 app을 실행시킵니다.
```

### 정상적으로 실행 확인

```bash
  docker-compose logs fastapi
```

### 재실행

```bash
docker-compose up --build
```
