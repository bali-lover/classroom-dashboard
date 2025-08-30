# 학습 진도판 관리 시스템 - GitHub Pages 배포판

## 🌐 Live Demo
**GitHub Pages URL**: `https://[username].github.io/[repository-name]/`

## 📁 파일 구성
```
github_pages_deploy/
├── index.html        # 메인 랜딩 페이지
├── dashboard.html    # 선생님용 대시보드
├── student.html      # 학생용 진도판
├── check-setup.html  # Firebase 설정 확인 도구
└── README.md         # 이 파일
```

## 🚀 GitHub Pages 배포 방법

### 1단계: GitHub 저장소 생성
1. GitHub에서 새 저장소 생성 (예: `classroom-progress`)
2. `Public` 저장소로 설정 (GitHub Pages 무료 사용을 위해)

### 2단계: 파일 업로드
1. 이 폴더의 모든 파일을 GitHub 저장소에 업로드
2. 커밋 및 푸시 완료

### 3단계: GitHub Pages 활성화
1. 저장소 → **Settings** 탭
2. **Pages** 섹션으로 이동
3. **Source**를 `Deploy from a branch` 선택
4. **Branch**를 `main` (또는 `master`) 선택
5. **Save** 클릭

### 4단계: 접속 확인
- 약 5-10분 후 `https://[username].github.io/[repository-name]/`에서 접속 가능
- Green 체크가 표시되면 배포 완료

## 🔧 Firebase 설정 (필수!)

이제 **코드 수정 없이** 브라우저에서 Firebase 설정을 할 수 있습니다!

### Firebase 프로젝트 생성
1. [Firebase Console](https://console.firebase.google.com/) 접속
2. "프로젝트 추가" 클릭
3. 프로젝트 이름 입력 (원하는 이름 사용 가능)
4. **Firestore Database** 활성화 (테스트 모드)
5. **Realtime Database** 활성화 (테스트 모드)

### 🎯 새로운 설정 방법 (코드 수정 불필요!)
1. **대시보드 접속**: `dashboard.html`을 열기
2. **Firebase 설정 버튼**: "⚙️ Firebase 설정" 클릭
3. **정보 입력**: 
   - API Key (Firebase 콘솔에서 복사)
   - Project ID 
   - Database URL
4. **연결 테스트**: "🔍 연결 테스트" 버튼으로 확인
5. **저장**: "💾 저장" 버튼으로 완료

### 🔍 Firebase 설정 정보 찾는 방법
Firebase 콘솔 → 프로젝트 설정(⚙️) → 일반 탭 → 앱 섹션에서:
- **API Key**: 웹 API 키
- **Project ID**: 프로젝트 ID 
- **Database URL**: Realtime Database → 데이터 탭에서 URL 확인

## ✅ 설정 확인 방법

배포 후 `check-setup.html` 페이지로 접속하여:
1. Firebase 연결 상태 확인
2. 데이터베이스 읽기/쓰기 테스트
3. 문제가 있을 경우 해결 방법 안내

## 📱 사용 방법

### 🎯 기본 흐름
1. **선생님**: `index.html` → "선생님용 대시보드" → 새 수업 생성
2. **QR 코드 생성**: 대시보드에서 QR 코드 버튼 클릭
3. **학생 접속**: QR 코드 스캔 또는 직접 학생용 URL 접속
4. **실시간 모니터링**: 대시보드에서 학생들의 진도 실시간 확인

### 🔗 각 페이지 직접 접속
- **메인 페이지**: `https://[username].github.io/[repository-name]/`
- **선생님용**: `https://[username].github.io/[repository-name]/dashboard.html`
- **학생용**: QR 코드를 통해 접속 (Firebase 설정이 자동으로 전달됨)
- **설정 확인**: `https://[username].github.io/[repository-name]/check-setup.html`

### 📱 새로운 학생 접속 방식
**중요**: 이제 학생들은 반드시 **QR 코드를 통해 접속**해야 합니다!
- 대시보드에서 "📱 QR 코드" 버튼으로 QR 코드 생성
- QR 코드에 Firebase 설정과 클래스 정보가 자동으로 포함됨  
- 학생들이 직접 URL을 입력하면 Firebase 설정 오류 발생

## 🔒 보안 설정 (권장)

### Firestore 보안 규칙
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;  // 개발용 - 추후 제한 권장
    }
  }
}
```

### Realtime Database 규칙
```json
{
  "rules": {
    ".read": true,
    ".write": true  // 개발용 - 추후 제한 권장
  }
}
```

## ⚡ 빠른 시작 체크리스트

- [ ] GitHub 저장소 생성
- [ ] 파일들 업로드  
- [ ] GitHub Pages 활성화
- [ ] Firebase 프로젝트 생성 (Firestore + Realtime Database)
- [ ] 대시보드에서 "⚙️ Firebase 설정" 완료
- [ ] 설정 확인 페이지로 테스트
- [ ] 첫 수업 생성 및 QR 코드 테스트

## 🆘 문제 해결

### GitHub Pages가 안 보여요
- 저장소가 Public인지 확인
- Settings → Pages에서 올바른 branch 선택했는지 확인
- 5-10분 정도 기다려보기

### Firebase 연결 오류
- 대시보드에서 "🔍 연결 테스트" 먼저 실행
- `check-setup.html`에서 구체적인 오류 메시지 확인  
- Firebase 설정 정보가 올바른지 재확인
- Firebase 프로젝트에서 Firestore/Realtime Database 활성화했는지 확인

### 학생 페이지에서 "Firebase 설정이 필요합니다" 오류
- **원인**: 학생이 QR 코드 없이 직접 접속함
- **해결**: 대시보드에서 생성한 QR 코드를 통해서만 접속 가능
- QR 코드에 Firebase 설정과 클래스 정보가 자동으로 포함됨

### 실시간 업데이트가 안돼요
- Firebase Realtime Database 활성화 확인
- 보안 규칙이 너무 제한적이지 않은지 확인
- 브라우저 개발자 도구에서 콘솔 오류 확인

## 📞 지원

문제가 있으시면:
1. `check-setup.html`에서 진단 먼저 실행
2. 브라우저 개발자 도구(F12) 콘솔 확인
3. Firebase 콘솔에서 데이터 확인

---

**🎓 교육 현장에서 바로 사용할 수 있는 실시간 진도 관리 시스템입니다!**
