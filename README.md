GitHub README에 바로 올리실 수 있도록 요청하신 내용을 반영하여 수정했습니다. 인벤터 버전 제약 사항을 명시하고, 불필요한 FAQ 섹션은 제거했습니다.
🚀 PTC Creo 10.0 & MATLAB R2025b Simscape Multibody Link 연동 가이드

이 가이드는 PTC Creo 10.0 모델을 MATLAB R2025b의 Simscape 환경으로 내보내기 위한 Simscape Multibody Link 설정 방법을 다룹니다.
⚠️ 중요: 소프트웨어 버전 및 호환성 주의사항

    SolidWorks 구버전 이슈: SolidWorks 2004 이전 버전에서 생성된 모델은 최신 환경에서 지원되지 않습니다. 반드시 STEP(.step) 파일로 변환하여 임포트하십시오.

    Autodesk Inventor 호환성: * 본 플러그인은 Inventor 2021 버전이 설치되어 있어야 정상 작동합니다.

        현재 공식적으로는 2023 버전까지 다운로드 및 설치가 가능하지만, 플러그인과의 안정적인 연동을 위해서는 버전 확인이 필수적입니다.

        PC에 해당 CAD 소프트웨어가 설치되어 있지 않으면 연동 기능을 사용할 수 없습니다.

1. MATLAB 플러그인 설치

MATLAB을 관리자 권한으로 실행한 후 커맨드 창에 다음 명령어를 입력합니다.
Matlab

% 플러그인 압축 파일(smlink-r2025b-win64.zip)이 있는 폴더에서 실행
installaddon('smlink-r2025b-win64.zip')

% MATLAB 서버 등록
regmatlabserver

2. 핵심 DLL 파일 확인 및 이동

R2025b 버전부터는 연결할 CAD 프로그램 버전에 맞는 전용 DLL 파일을 사용해야 합니다.

    압축 파일 내부의 bin\win64 폴더에서 자신의 환경에 맞는 파일을 찾습니다.

        Creo 10 사용 시: cl_proe2sm10.dll

        Inventor 사용 시: cl_inventor2sm.dll

    해당 파일을 아래 경로에 복사합니다: C:\Program Files\MATLAB\R2025b\bin\win64\ (관리자 권한 필요 시 '계속' 클릭)

3. protk.dat 파일 생성 및 설정 (Creo 전용)

Creo가 MATLAB 라이브러리를 로드할 수 있도록 이정표 역할을 하는 protk.dat 파일을 작성합니다.

    파일 위치: C:\Program Files\PTC\Creo 10.0.9.0\Common Files\text\protk.dat

    파일 내용: (메모장으로 작성)

Plaintext

name            Simscape Multibody Link
startup         dll
exec_file       C:\Program Files\MATLAB\R2025b\bin\win64\cl_proe2sm10.dll
text_dir        C:\Program Files\MATLAB\R2025b\toolbox\physmod\smlink\cad_systems\proe
allow_stop      true
delay_start     false
end

4. 최종 연동 확인

    Creo 실행 → 파일 → 옵션 → 구성 편집기에서 toolkit_registry_file 값을 위 protk.dat 경로로 지정합니다.

    설정을 저장(config.pro)하고 Creo를 재시작합니다.

    상단 메뉴바 우측에 [Simscape Multibody Link] 탭이 나타나면 모든 설정이 완료된 것입니다.

이 가이드를 통해 성공적으로 연동하셨다면 ⭐ Star를 눌러주세요
