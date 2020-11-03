# Visual Studio Code를 사용한 HTML/CSS 개발

## 목차

1. Visual Studio Code 설치 및 환경 세팅
   - Visual Studio Code 설치
   - Live Server 플러그인 설치
   - FTP 업데이트 환경 설정
   - Git 연동
2. 코드표준화
   - prettier now (코드포맷)
   - MDN 레퍼런스 보기
3. 편리한 기능
   - Emmet(코드 자동 완성)
   - Intellisense for CSS name(코드 자동완성)
   - auto rename(코드 자동 완성)
   - CSS Peek(코드 네비게이션)

## 1\. Visual Studio Code 설치 및 환경 세팅

### **Visual Studio Code 설치**

![Visual Studio Code Install](./img/img1.png)

https://code.visualstudio.com 에서 사용자 OS에 맞는 버전 다운로드하여 설치

### **Live Server 플러그인 설치**

- Live Server 는 서버 연동없이 작업중인 HTML/CSS 화면을 실시간으로 브라우저에 반영하여 보여주는 플러그인
- 화면 레이아웃을 확인하며 작업하기에 편리함  


![Live Server Plug-in install](./img/img3.png)

1. Vscode 실행하여 extension메뉴에서 live server 검색

2. Install 버튼 클릭하여 플러그인 설치 > 재시작


```
jdk 11 이하인 경우 지원하지 않는 문제가 있음
→anguage support for Java(TM) by Red Hat에서  최소 지원 버전이 JDK 11
→java.confirugation.runtimes 추가 설정이 필요함
```

![java home runtime.jpg](./img/java_home_runtime.jpg)  
<br>

## 2\. Java 실행환경 연동

```
참고
Java Project 생성(https://miaow-miaow.tistory.com/25)
```

### **SVN 소스 다운로드**

형상관리를 위해 사용하는 시스템과의 연동을 위해 플러그인을 추가로 설치해야 함.

![SVN_Extension.jpg](./img/SVN_Extension.jpg)

1. `SVN` 플러그인을 설치  
   설치 후 다음과 같은 에러메시지가 발생하는 경우, 로컬 PC에 SVN 설치 진행(svn이 설치되어있는 경우 4 단계로 이동)  
   ![svn_fail.jpg](./img/svn_fail.jpg)
2. 로컬 PC의 운영체제에 알맞는 파일 다운로드  
   (TortoiseSVN 설치: http://subversion.apache.org/packages.html)
   ![svn_download.jpg](./img/svn_download.jpg)
3. 설치 시 command line client tools를 포함하도록 옵션 변경  
   ![svn_install.jpg](./img/svn_install.jpg)
4. 설치가 끝난 후 Visual Studio Code를 재실행 해 안내 메시지 출력 확인
   ![svn_suc.jpg](./img/svn_suc.jpg)

5. Ctrl+Shift+p 사용 후 '>svn:checkout' 명령어를 사용
   ![svn_checkout.jpg](./img/svn_cko.jpg)

6. 체크아웃 받을 폴더를 선택
   ![svn_checkout_2.jpg](./img/svn_cko_2.JPG)

7. 소스파일이 저장될 폴더 입력(생성용)
   ![svn_checkout_3.jpg](./img/svn_cko_3.JPG)

### **JAR 파일 관리**

- Jar 추가  
  프로젝트 뷰의 'Referenced Livraries' 우측 '+' 기호를 클릭해 JAR 파일을 추가함  
  ![add_jar.jpg](./img/add_jar.jpg)
- 라이브러리 구성  
  setting.json 파일에 java.project.referencedLibaries 패턴을 추가해 라이브러리를 구성함  
  예)

```json
"java.project.referencedLibraries": {
    "include" :[
        "lib/**/*.jar",
        "/home/lib/test.jar"
    ],
    "exclude" :[
        "lib/sample/*.jar"
    ]
}
```

- source 경로 설정
  vscode 에서 Java 프로젝트를 생성하는 경우 /src, /lib 의 경로에서 source 파일과 dependencies 파일을 관리함  
  기존 프로젝트의 구조가 다른 경우 .classpath 파일을 수정해 경로를 설정해야 함.

  ##### **.classpath 경로 : C:\Users\사용자명\AppData\Roaming\Code\User\workspaceStorage\ (프로젝트경로)\redhat.java\jdt_ws\java_xxxxxxx\ .classpath**

  ##### └ java_xxxxxxx : launch.json 파일에 설정한 projectName

      ![classpath.jpg](./img/classpath.jpg)

      ① 프로젝트의 source 파일 경로 입력
      ② Referenced Livraries에 추가된 jar 파일

참조하는 classpath 경로가 모두 등록되면 JAVA PROJECTS 영역에 모든 source 경로가 조회되고, 각각의 패키지, 소스파일에서 문제가 없음을 확인할 수 있음  
 ![classpath_2.jpg](./img/classpath_2.jpg)

### **Run/Debug**

자바 소스에서 main 메소드가 있는 경우 다음의 방법을 통해 run/debug 모드를 실행할 수 있음

1. main 메소드 상단에 생성된 버튼 사용  
   ![run debug](./img/run_debug.jpg)
2. 소스파일 우클릭하고 run/debug 선택  
   ![run debug 2.jpg](./img/run_debug_2.jpg)
3. 단축키 사용해 run/debug

```
Run : F5 / Ctrl+F5
Debug : Ctrl+F11
```

운영중인 시스템은 개별 build 환경에 따라 세팅에 차이가 있으며, 일반적으로 war 파일을 생성한 후 해당 파일 사용해 서버를 구동 함.

#### WAR 파일 생성 (vscode TERMINAL 창에서 다음 구문 실행)

![create_war.jpg](./img/create_war.jpg)

```
(생성하고자 하는 폴더에서 실행)
~~~> jar cvf (파일명).war (압축 대상)
```

<br>
  
## 3\. 소스 편집  
### **Code Assist**   
메소드, 코드 템플릿 등을 표시해 내용 완성을 지원, Ctrl+space 사용 또는 타이핑시 표시됨  
![itl_1.jpg](./img/itl_1.jpg)  
![itl_2.jpg](./img/itl_2.jpg)

### **Code Navigation**

F12 또는 우클릭하여 다른 메소드나 클래스 소스 확인  
![itl_3.jpg](./img/itl_3.jpg)

### **snippets**

반복되는 코드 패턴을 snippets로 작성  
Ctrl+p 사용 후 '>Configure User Snippets' 입력>'Java' 입력 하면 java.json 파일이 생성됨  
![add_sni.jpg](./img/add_sni.jpg)

아래의 규칙을 사용해 코드 패턴을 작성

```json
"이름":{
    "prefix": "명령어",
    "body": "소스 코드",
    "description":"코드 설명"
}
```

예)  
![java_json_1.jpg](./img/java_json_1.jpg)  
▲ 실제 작성한 java.json 구문  
　\*\* $1, $2 : 구문 사용시 tab기능을 사용해 코드 입력하는 영역

![java_json_2.jpg](./img/java_json_2.jpg)  
▲ java.json에 설정된 snippets 사용

![java_json_3.jpg](./img/java_json_3.jpg)  
▲ java method 를 위한 주석 서식

### **파일명으로 파일 찾기**

Ctrl+p 사용 후 찾고자 하는 파일명 입력.  
eclipse의 Ctrl+shift+r 단축키 동작으로 eclipse에서는 입력한 단어의 위치에 따라 '\*' 기호를 조합해 입력하지만, VSC에서는 위치에 상관없이 단어가 일치하는 파일이 모두 조회됨  
![srch_file.jpg](./img/srch_file.jpg)

### **getter/setter, toString() 등 자주 사용하는 구문 자동 생성**

변수 선언 후 마우스 우클릭>Source Action>...  
![source_action_1.jpg](./img/source_action_1.jpg)

- organize import : 클래스에 불필요한 import구문을 제거해주고, 필요한 구문은 자동으로 추가
- Override/Implement Methods : 클래스를 상속 받았을때 자동으로 override 메소드 생성
- generate getters and setters : 변수의 getter, setter 메소드 자동으로 생성

<br>

## 4\. 코드 스타일 표준화

settings.json 파일을 수정해 에디터의 전반적인 설정값을 세팅하거나, beautify 같은 익스텐션을 설치해 코드 스타일을 표준화할수 있음

<!--  -->

### **settings.json > Word Wrap**

자동 줄바꿈 옵션. 모니터 크기에 맞춰 화면에 표시되는 소스의 길이를 조절  
![setting_wordwrap.jpg](./img/setting_wordwrap.jpg)

### **setting.json > editor.formar...**

- editor.formatOnType : 세미콜론 사용 시 해당 라인 표준화 적용 여부
- editor.formatOnSave : 파일 저장 시 표준화 적용 여부
- editor.formatOnPaste : 소스코드 붙여넣기 시 표준화 적용 여부
- files.trimFinalNewlines : 파일 저장 시 파일 끝의 비어있는 줄 제거 여부  
  ![setting_editorformat.jpg](./img/setting_editorformat.jpg)

### **자동정렬**

- shift+alt+f 단축키 동작으로 소스코드의 들여쓰기 등 포맷을 자동 정렬함  
   ![formatting_1.jpg](./img/formatting_1.jpg)
- 정렬하고자 하는 코드 영역을 선택하고 Ctrl+K+F 단축키 동작 시 선택한 영역의 코드 포맷을 자동 정렬함  
   ![formatting_2.jpg](./img/formatting_2.jpg)

## 5\. SpringBoot 개발환경

### **필수 플러그인 설치**

- Java Extension Pack(설치 완료)
- Spring Boot Extension Pack  
  ![Spring Boot Extension Pack](./img/spring_extension.JPG)

1. [View] - Command Palette 선택 또는 Ctrl+Shift+P 입력\*\*

- Spring Maven을 입력하여 Create a Maven Project 선택
  ![Spring Project Create](./img/spring_create.JPG)

2. 필요 버전 선택  
   ![Spring Project Create-2](./img/spring_create_2.JPG)

3. 언어 선택(Java)  
   ![Spring Project Create-3](./img/spring_create_3.JPG)

4. Gruop ID 선택  
   ![Spring Project Create-4](./img/spring_create_4.JPG)

5. Artifact ID 선택  
   ![Spring Project Create-5](./img/spring_create_5.JPG)

6. Package Type 선택  
   ![Spring Project Create-6](./img/spring_create_6.JPG)

7. JDK Version 선택  
   ![Spring Project Create-7](./img/spring_create_7.JPG)

8. 추가 의존성 도구 선택  
   ![Spring Project Create-8](./img/spring_create_8.JPG)

9. 저장될 디렉터리 선택  
   ![Spring Project Create-9](./img/spring_create_9.JPG)

- 생성된 Spring Project 기본적인 구조  
  ![Spring Example](./img/spring_example.JPG)

### **개발환경 테스트**

- 해당 디렉터리로 이동하여 Terminal 에서 .\mvnw spring-boot:run 실행
- 정상적으로 환경이 세팅되었다면 아래와 같은 화면 출력  
  ![Spring Test](./img/spring_test.JPG)
