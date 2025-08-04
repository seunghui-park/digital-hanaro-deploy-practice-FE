# 하나로 풀스택 배포 프로젝트 - Frontend

## 기술 스택

- React + Vite
- TypeScript
- Axios
- AWS S3 (정적 웹 호스팅)
- GitHub Actions (CI/CD)

---

## 배포 인프라 개요

### 1. AWS S3란?

Amazon S3(Simple Storage Service)는 AWS에서 제공하는 **클라우드 객체 스토리지 서비스**
정적 파일(html, js, css 등)을 업로드하면 **웹 호스팅처럼 사용할 수 있고**,  
**EC2 없이도 React/Vite 앱을 배포**할 수 있음

### 2. 왜 S3를 사용했나?

- Vite로 빌드된 React 앱은 정적 파일로 구성됨 (`index.html`, js, css, etc)
- S3는 이런 정적 리소스를 호스팅하기에 최적화됨
- 서버가 따로 필요 없고, 유지비가 적으며, CloudFront와 연동하면 CDN 배포도 가능
- GitHub Actions를 통해 자동 배포도 쉽게 설정 가능

---

## 🚀 배포 흐름 요약

1. Vite 앱을 빌드 → `dist/` 폴더 생성
2. `main` 브랜치에 push 시 GitHub Actions가 동작
3. `.env` 파일에서 API 주소를 주입
4. 빌드된 정적 파일을 **S3 버킷**에 업로드
5. 사용자는 S3 URL로 배포된 웹앱에 접속 가능

### .env 예시
```env
VITE_API_BASE_URL=http://<백엔드 EC2 Elastic IP>:8080/api
```

---

## 배포 결과
![Image](https://github.com/user-attachments/assets/5deea251-95cc-4f30-9473-a67dc2d511a6)
