# u-eMuESL
Unicorn engine 기반 ARM 가상화 도구

# Introduction 📖
- **현재 배포 버전**: `v2.0`
- **지원 프로세서**: ARMv7 이하 (ARM 버전 8부터는 Unicorn에서 지원하지 않음)
- **지원 파일 모드**: ARM mode, Thumb mode
- **버전 업데이트 추가 기능**: 이상행위 시나리오 주입, 데이터 프레임 생성
# Getting Started 💡
## 1. Download resource
```commandline
git clone https://github.com/khu-mesl-348/u-eMuESL.git
```

## 2. install packages
![Static Badge](https://img.shields.io/badge/python-3.10.2-blue)
![Static Badge](https://img.shields.io/badge/unicorn-2.0.1.post1-green)
![Static Badge](https://img.shields.io/badge/capstone-4.0.2-green)
### install unicorn (CPU Emulator)
```
pip install unicorn
```
### install capstone (Disassembler)
```
pip install capstone
```

## 3. Execution
### 실행 전 사용자 설정
```
config.py
```
* elf_file = "./source/<ELF 파일명>" : 실행할 ELF 저장 경로
* log_vir_in_file = "./ini_set/LogVirIN.csv" : 프로그램 input 설정 CSV 파일 경로
* fault_reg_file = "./ini_set/LogFI.csv" : 이상행위 시나리오 설정 CSV 파일 경로
* log_file_name = "<로그 파일명>" : 사용자 임의 설정 로그 파일명  

### 프로그램 입력 파일
* ./ini_set/LogVirIN.csv : 프로그램 input(전역변수명: vir_IN) 설정 CSV
    * (0,n) : ctr
    * (1 + n, n) : 전역변수 배열 index
* ./ini_set/LogFI.csv: 이상행위 시나리오 설정 CSV 파일 경로
    * 미 설정 시, 정상 시나리오 자동 실행

### 프로그램 출력 파일
* LogVirOUT.csv : 프로그램 output(전역변수명: vir_OUT)
* LogVirOUT_Faulty.csv : 이상행위 설정 시 생성되는 프로그램 output
* LogReg_Faulty.csv :  이상행위 설정 시 생성되는 로그 파일  


# How To Use 💻
## 1. ELF 펌웨어 실행
ELF(Executable and Linkable Format)을 인식하고 파일을 실행합니다.
## 2. 에뮬레이션 실행 중 내부 상태 로깅
에뮬레이션 실행 과정을 로깅하여 /log 폴더에 저장합니다. 
(저장 파일명: <날짜> LogReg.csv)
아래 정보를 나타냅니다.  
* 로그 라인 넘버(ctr)
* 실행 주소
* 실행 명령어
* 명령어 실행 전 레지스터 값
* 명령어 실행 후 레지스터 값
## 3. 런타임 중 프로그램 input 데이터 변경
프로그램 실행 중 프로그램 input 데이터를 지정 및 변경합니다.
(파일명: ./ini_set/LogVirIN.csv)
아래 정보를 나타냅니다.
* (0,n) : ctr
    * 로그 라인 넘버(ctr)를 통해 데이터 변경 지점을 설정합니다.
* (1 + n, n) : 전역변수 배열 index
## 4. 이상행위 시나리오 수행
프로그램 실행 중 이상행위(오류 주입) 시나리오를 실행합니다.
기능은 및 설정 방법은 아래와 같습니다.
* 레지스터별 데이터 변경
    * 미 변경 시, "NaN" 입력
* bit flip(Flip)
    * 설정 시, "Flip" 입력
* NOP
    * 설정 시, isNOP "TRUE" 또는 "FALSE" 입력

## 5. 파일 내부 정보 출력
`reference.txt` 파일을 통해 ELF 파일의 전체의 내부 명령어 및 데이터, 섹션, 함수 등을 출력합니다.
아래 정보를 나타냅니다.
* 주소 (Flash address)
* 실행 주소 (Real address(including RAM address))
* 메모리 섹션
* 함수