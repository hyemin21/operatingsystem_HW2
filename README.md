# OS_HW2 cimin project

##Project Name
Cimin project

##Description
이 프로젝트는 입력 시퀀스를 생성하여 대상 프로그램에 제공하고, 대상 프로그램이 충돌하는 입력 시퀀스를 찾아내는 프로젝트이다. 

1. Crash.json 파일을 열고, 전체 파일을 메모리에 로드
2. 입력 시쿼스의 길이를 조정하여 모든 가능한 입력 시퀀스를 생성
3. 각 입력 시퀀스를 대상 프로그램에 제공하여 실행
4. 대상 프로그램이 종료될 때까지 대기하고, 종료 상태를 확인
5. 프로그램이 충돌하며 입력 시퀀스를 출력

이 코드는 파이프를 사용하여 대상 프로그램에 입력 시퀀스를 전달하고, 대상 프로그램의 출력을 읽어서 충돌을 확인한다.

또한 fork를 사용하여 대상 프로그램을 실행하고, 부모 프로세스가 자식 프로세스의 종료 상태를 확인한다. 

Makefile 실행 설명 —> 필요



##Prerequisite

https://github.com/hongshin/OperatingSystem/tree/hw2/jsmn
https://github.com/hongshin/OperatingSystem/tree/hw2/balance
https://github.com/hongshin/OperatingSystem/tree/hw2/libxml2

위 주소를 통해 json, balance, libxml2의 예제 코드를 다운 받을 수 있다. 
1. Jsmn
: open source JSON library
이 프로그램에는 heap-buffer overflow errors를 발생하는 버그가 있다. 
1. jsmn/build.sh -> 프로그램 빌드 (LLVM AddressSanitizer를 사용하여 heap-buffer overflow errors 발생 감지) -> jsondump 생성
2. jsondump이 jsmn/testcases/crash.json을 받으면 충돌 (에러)

라이브러리 파일 -> jsmn.c , jsmn.h 
Test -> jsmn_test.c
라이브러리 빌드 -> makefile 실행
빌드 성공 -> libjsmn.a 라이브러리 얻게 됨 ("jsmn.h" 포함)

Libxml2 : XML 및 HTML과 같은 다양한 마크업 언어로 서식이 지정된 데이터를 구문 분석하고 조작
1. libxml2/build.sh 실행 -> 모든 라이브러리 및 유틸리티 프로그램(xmllint -> null 포인터 참조 오류가 발생하는 버그) 빌드 
2.  “—recover —postvalid -" 옵션과 함께 xmllint를 실행하고 표준 입력으로 libxml2/testcases/crash.xml을 전달하여 이 버그를 트리거함.
==> libxml2 라이브러리 빌드하고, 테스트 케이스인 crash.xml파일은 xmlint를 사용하여 검증
이때, "AddressSanitizer: SEGV on unknown address" 오류 메시지가 표준 오류 출력으로 출력됨
-> 해당 오류는 NULL포인터 역참조로 인해 발생한 충돌이다. 

Balance : 주어진 문자열에서 괄호가 올바르게 매치되는지 확인하는 프로그램 
Ex) “((()))”와 같이 모든 괄호가 올바르게 매치되면 -> suceess, “(())(” -> fail
1. balance/build.sh -> 프로그램 빌드
2. balance/testcases/fail -> 무한 루프 —> 시간 제한을 초과하면 테스트 실행 종료


##Environment


