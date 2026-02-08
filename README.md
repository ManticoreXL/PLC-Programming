# PLC-Programming
대한상공회의소 서울기술교육센터  
AI융합 로봇 SW개발자 2기생 최민석  
PLC 프로그래밍 수업 미니 프로젝트

## 프로젝트 목표
PLC와 MPS 훈련 장비를 사용한 지능형 소재 가공/분류/적재/하역 시스템 구축

## 핵심 기능
- 기본 동작 구현
  - 소재 가공 및 분별 적재
  - 순차적 장비 점검
- 응용 동작 구현
  - 소재 선입선출(FIFO) 적재
  - 소재 개별 하역 및 일괄 하역

## FIFO 알고리즘
### 구현 개요
창고가 가득 찬 상태에서 새로운 소재가 투입되면, 가장 먼저 들어온 소재를 자동으로 하역하고 새로운 소재를 적재하는 선입선출(FIFO) 시스템이다.

### 알고리즘 동작 순서
1. 재질 판별 후, 해당 재질의 창고가 모두 차있는지 확인
2. 창고가 가득 찬 경우, 가장 작은 적재 순서 번호를 가진 소재를 탐색
3. 해당 소재를 창고에서 꺼내 컨베이어 벨트 위에 적재
4. 컨베이어 벨트를 가동해 하역한 소재를 버리고 새로운 소재 적재 준비
5. 비워진 공간에 새로운 소재 적재 후 우선순위 갱신 (작업 완료 총계 + 1)

### 우선순위 관리
- 각 창고 칸마다 데이터 레지스터로 우선순위 관리
- 적재시 현재 총계값을 기반으로 고유한 우선순위 부여
- 하역 완료시 해당 창고의 우선순위를 0으로 초기화

## HMI 작화
### 화면 구성
1. 주 화면 (Main Panel)
   - 전원 인가시 초기 화면
   - 각 제어 화면으로 이동하는 스크린 스위칭 버튼 배치

2. 서보 제어 패널 (Servo Panel)
   - 서보 모터 제어 기능: JOG 운전, 원점 복귀, 고속 원점 복귀
   - 서보의 현재 위치와 속도를 0.01mm 단위로 실시간 모니터링 가능
   - 에러/경고 코드 표시 및 에러 발생시 리셋 가능

3. 시퀀스 제어 패널 (Sequence Panel)
   - MPS 제어 기능: RUN (공정 가동), TEST(순차적 장비 점검), UNLOAD ALL (일괄 하역)
   - Storage Indicator: 6개 창고의 적재 상태 시각화 및 개별 하역 기능 제공
   - 7개의 물리 램프와 부저를 HMI에서 시각적 피드백 제공
   - 재질별 작업 계수 및 총계 표시

4. 통계 패널 (Statistics Panel)
   - Cycle Time 그래프: 최근 7건의 층별 적재 시간 시각화 
     - 1층은 붉은색으로, 2층은 초록색으로, 3층은 하늘색으로 표시
   - 통계량 표시: 각 층별 평균 적재 수행 시간 표시

5. 설정 패널 (Setting Panel)
   - 가공 설정: 드릴 동작 횟수 및 시간을 조정 가능
   - 다국어 지원: 영어, 한국어, 일본어 전환 가능 

## 서보 모터 설정
### Parameters
- Pr.8: Speed limit value = 4000.00 mm/min
- Pr.31: JOG speed limit value = 1000.00 mm/min
- Pr.44: HPR direction = 1:Reverse Direction (Address Decrease Direction)
- Pr.46: HPR speed = 900.00 mm/min
- Pr.47: Creep speed = 90.00 mm/min

### ServoParameters
- **PA04**: *AOP1: Function selection A-1 = 2100

### Positioning Data
1. dd
2. dd
3. dd
4. dd
5. dd
6. dd
7. dd
8. ㅇㅇ


# Lab Environment
- MITSUBISHI ELECTRIC MELSEC-Q Series
  - PLC: **Q03UDVCPU**
  - Input module: **QX40** * 2 EA
  - Output module: **QY10** * 2 EA
  - Analog I/O module: Q64AD2DA
  - Network module: QJ61BT11N
  - Positioning module: **QD77MS2**
  - Servo Driver: **MR-J4-10B**
  - Servo Motor: **HG-KR13J**
  - HMI Device: **GOT2000**

- MITSUBISHI ELECTRIC MELSOFT Series
  - PLC Programming: **GX Works2** (1.631H)
  - HMI Design: **GT Designer3** (1.256S)
  - HMI Simulator: **GT Simulator3** (1.256S)

# MPS Training System Composition
- Pneumatics
  - Double solenoid pneumatic cylinder * 5 EA
  - Single solenoid pneumatic cylinder * 2 EA
  - Pressure regulator: AW20-01BG-A (for penumatic control)
  - Vacuum suction cup
- Motors
  - Training Drill Unit
  - Conveyor belt

### Memory Map
ㅇㅇ



 
