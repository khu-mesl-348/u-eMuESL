# u-eMuESL
Unicorn engine 기반 ARM 가상화 도구

# Introduction 📖
- **현재 배포 버전**: `v1.1`
- **지원 프로세서**: ARMv7 이하 (ARM 버전 8부터는 Unicorn에서 지원하지 않음)
- **지원 파일 모드**: ARM mode, Thumb mode
- **버전 수정 사항**: Thumb mode 지원, stack 및 프로그램 사이즈 자동 할당
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
### 아키텍처 파일(.json)
clock count 계산을 위해 아키텍처 별 json 파일을 입력
```
ex_arch.json
```
* ins_set: {명령어 : (const int) | (equation) }
* value : equation 미지수에 입력할 설정값
  
### 실행 전 사용자 설정
```
input.json
```
* files
  * elf_file: 실행할 ELF 저장 경로 (ex: ./source/toy_ex_mod_add)
  * log_file_name: 로그 파일명 설정
* arch
  * <%architecture_name> : 실행할 아키텍처 json 파일


# How To Use 💻
## 1. ELF 펌웨어 실행
ELF(Executable and Linkable Format)을 인식하고 파일을 실행합니다.
(현재 배포 버전(`v1.0`): ARM mode로 컴파일한 파일만 지원)  
## 2. 에뮬레이션 실행 중 내부 상태 로깅
에뮬레이션 실행 과정을 로깅하여 /log 폴더에 저장합니다.  
아래 정보를 나타냅니다.  
* 실행 주소
* 실행 명령어
* 현재 레지스터 값 (r0값, r1값, ..., SP, LR, PC, CPSR)
* 값이 변경된 레지스터
* 소요된 clock count
* 특정 메모리 영역의 수정 전/후 데이터 값
## 3. 파일 내부 정보 출력
`reference.txt` 파일을 통해 ELF 파일의 전체의 내부 명령어 및 데이터, 섹션, 함수 등을 출력합니다.
아래 정보를 나타냅니다.
* 주소 (Flash address)
* 실행 주소 (Real address(including RAM address))
* 메모리 섹션
* 함수
* 전역변수
  
