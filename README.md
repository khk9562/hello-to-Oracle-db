# hello-to-Oracle-db

프로젝트 루트에 Dockerfile 생성

```
# Start your image with a node base image
FROM node:18-alpine

# The /app directory should act as the main application directory
WORKDIR /app

# Copy the app package and package-lock.json file
COPY package*.json ./

# Copy local directories to the current local directory of our docker image (/app)
COPY ./src ./src
COPY ./public ./public

# Install node packages, install serve, build the app, and remove dependencies at the end
RUN npm install \
    && npm install -g serve \
    && npm run build \
    && rm -fr node_modules

EXPOSE 3000

# Start the app using serve command
CMD [ "serve", "-s", "build" ]

```

### 도커 실행 명령어

`docker build -t welcome-to-docker .`



### 이렇게 하는게 맞는걸까요?

1. SQL Developer 설치:
   - 이미 다운로드 받으신 'sqldeveloper-23.1.1.345.2114-macos-x64.app.zip' 파일을 더블클릭하여 압축을 풉니다.
   - 압축 해제된 'SQL Developer.app' 파일을 Applications 폴더로 드래그하여 이동시킵니다.
   - Applications 폴더에서 SQL Developer를 실행해보세요.

2. Docker 설치:
   - Docker 웹사이트(https://www.docker.com/products/docker-desktop/)에서 macOS용 Docker Desktop을 다운로드합니다.
   - 다운로드 받은 .dmg 파일을 더블클릭하여 설치 프로그램을 실행합니다.
   - 화면의 지시에 따라 설치를 완료합니다.
   - 설치가 완료되면 Docker Desktop을 실행합니다.

3. Docker를 이용한 데이터베이스 설치 (예: Oracle Database):
   - 터미널을 엽니다.
   - 다음 명령어를 입력하여 Oracle Database 이미지를 다운로드하고 컨테이너를 실행합니다:
     ```
     docker run -d -p 1521:1521 -e ORACLE_PASSWORD=your_password container-registry.oracle.com/database/free:latest
     ```
   - 'your_password' 부분을 원하는 비밀번호로 변경하세요.

4. SQL Developer에서 데이터베이스 연결:
   - SQL Developer를 실행합니다.
   - '새 데이터베이스 연결' 버튼을 클릭합니다.
   - 연결 정보를 입력합니다:
     - 호스트 이름: localhost
     - 포트: 1521
     - SID: FREEPDB1
     - 사용자 이름: system
     - 비밀번호: Docker 실행 시 설정한 비밀번호

