# ing_Indicator _만드는 중.. 일단 display되는 signal 정리 

BOS ↑/↓: 현재 구조 방향과 같은 쪽의 확정 스윙을 종가로 돌파한 추세 지속 구조.
CHOCH ↑/↓: 저장된 구조 방향과 반대로 처음 발생한 구조 돌파입니다. 추세 변화 “경고” 단계.
MSS ↑/↓: CHOCH 중에서도 직전에 반대편 유동성 스윕이 있었던 경우. 현재 기본 스윕 유효기간은 12봉(TEST 中, 이 기간도 알고리즘으로 넘길 예정).
MSWP: Major Sweep. 고점 위를 쓸고 내려오면 매도 방향, 저점 아래를 쓸고 올라오면 매수 방향 유동성 제거.
SWP: 조건을 통과한 Minor Sweep, m은 아직 조건을 통과하지 못한 Raw Minor Sweep.
EQH/EQL: 확정 피벗 두 개 이상이 ATR 허용폭 안에 모인 동일 고점/저점 유동성. 돌파되면 해당 선은 계산상 소진.
C: 확률 조건까지 통과한 Candidate. 아직 최종 L/S 신호는 아님...
L/S: RR·EV·목표 확률·Posterior·Coherence 등 최종 게이트까지 통과한 신호.
주황 실선은 EMA Fast, 파란 실선은 EMA Slow, 노란 굴곡선은 60봉 Dealing Range의 중간값 EQ.
긴 보라색 점선은 PWH/PWL(전주 고가/저가), 노란 점선은 PDH/PDL(전일 고가/저가). * 이미 소진된 선은 투명해져 회색에 가깝게 보일 수 있음.!
주황/청록 점선은 활성 EQH/EQL, 짧은 형광 초록/분홍 점선은 Bull/Bear FVG·IFVG의 CE.!



R5에서 추가: 
Show Native TF Zones
- 현재 보고 있는 차트 시간대의 FVG/IFVG를 표시.
- 4시간 차트 → 4시간 FVG
- 일봉 차트 → 일봉 FVG
- 주봉 차트 → 주봉 FVG

Show HTF1 Zones
- 현재 차트보다 한 단계 높은 핵심 시간대의 FVG/IFVG를 표시.
- 4시간 차트 → 일봉
- 일봉 차트 → 주봉
- 주봉 차트 → 월봉

Show HTF2 Zones
- 현재 차트보다 두 단계 높은 시간대의 FVG/IFVG를 표시.
- 4시간 차트 → 주봉
- 일봉 차트 → 월봉
- 주봉 이상 → 비활성화

- 적용 예시

- 4시간 단기매매: Native + HTF1 + HTF2 (복잡하면 HTF1, HTF2는 끄기)
- 일봉 스윙: Native + HTF1, HTF2는 선택
- 주봉 장기분석: Native + HTF1
