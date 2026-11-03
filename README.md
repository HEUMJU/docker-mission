# 🔧 트러블슈팅 기록

## 문제 1: VSCode에서 `ls -la` 명령어 동작 안 함

### 📌 발생 상황
- **도구**: VSCode (터미널)
- **명령어**: `ls -la`
- **에러 메시지**: 
Get-ChildItem : 매개 변수 이름 'la'과(와) 일치하는 매개 변수를 찾을 수 없습니다.
위치 줄:1 문자:4
+ ls -la
+    ~~~
    + CategoryInfo          : InvalidArgument: (:) [Get-ChildItem], ParameterBind 
   ingException
    + FullyQualifiedErrorId : NamedParameterNotFound,Microsoft.PowerShell.Command 
   s.GetChildItemCommand

   ### 🔍 원인 분석
- **근본 원인**: VSCode의 기본 터미널이 **PowerShell**로 설정되어 있음
- **PowerShell의 특징**: Windows 전용 쉘로 Unix 명령어(`ls`, `pwd` 등)를 지원하지 않음
- **필요한 것**: Unix 명령어를 지원하는 터미널 환경

### ✅ 해결 방법

#### 방법 1: Git Bash로 기본 터미널 변경 (✓ 적용함)

**단계:**
1. VSCode 하단 터미널 창 → 오른쪽 끝 드롭다운 버튼(`▼`) 클릭
2. "Select Default Profile" 메뉴에서 **"Git Bash"** 선택
3. Terminal → New Terminal 클릭 (또는 `Ctrl + Shift + `` )
4. 새 터미널이 Git Bash(`$` 기호)로 열림

**결과:**
```bash
$ ls -la
✅ 명령어 정상 동작!

장점:

Unix 명령어 완벽 지원
Git 작업할 때도 편함
Docker 명령어도 잘 작동
방법 2: PowerShell 네이티브 명령 사용 (대안)
PowerShell을 계속 쓰고 싶으면 PowerShell 고유 명령어 사용:

Unix 명령	PowerShell 명령
ls -la	Get-ChildItem -Force
pwd	Get-Location
mkdir 폴더명	New-Item -Path "폴더명" -ItemType Directory
단점:

명령어가 길고 복잡함
나중에 Docker/Git 작업할 때 호환성 문제 가능

📚 학습 포인트
개념	설명
쉘(Shell)	운영체제와 사용자 사이의 인터페이스
PowerShell	Windows 전용 쉘 (Unix 명령어 미지원)
Git Bash	Git 설치 시 함께 제공되는 Unix 호환 쉘
Unix 명령어	Linux/Mac/Git Bash에서 사용 가능한 표준 명령어

🎯 결론
VSCode에서 터미널 작업할 때는 Git Bash 사용 권장!

