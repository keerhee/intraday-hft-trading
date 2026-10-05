# 인트라데이 전략 32 — 장중·고빈도 거래 전략의 비교와 검증

장중(인트라데이)·고빈도(HFT) 거래 전략 후보 **32개**를 여덟 유형(A–H)으로 나누고,
유형마다 **가설 → 측정 → 판정**의 같은 잣대로 검증 방법을 정리한 강의 덱 모음이다.
유형별 본편과 손계산 워크북, 후보마다 한눈에 보는 8장짜리 카드뉴스, 그리고 32개 후보를 한자리에 놓고 개발 순서를 정하는 비교 덱으로 이루어진다.

목록 사이트: https://keerhee.github.io/intraday-hft-trading/

> **모든 후보는 연구 가설이며, 수치 예제는 교육용 가정이다.** 검증을 마친 전략이나 매매 권고가 아니다.
> 개발 순서는 설계 판단이며 수익률 순위가 아니다.

## 구성

| 폴더 | 유형 | 핵심 질문 | 목표 보유 | 본편 | 워크북 |
|---|---|---|---|---:|---:|
| [`00_Comparison_Priority`](00_Comparison_Priority) | 비교와 개발 우선순위 | 32개 후보를 같은 잣대로 놓고 무엇을 먼저 만들까 | — | 33 | 8 |
| [`A_OrderFlow`](A_OrderFlow) | A · 주문 흐름과 호가 | 수급 압력이 수 초간 지속되는가 | 1–60초 | 44 | 14 |
| [`B_LiquidityShock`](B_LiquidityShock) | B · 유동성 충격과 회복 | 이 급락은 수급 충격인가, 정보 재평가인가 | 2초–10분 | 42 | 13 |
| [`C_TrendBreakout`](C_TrendBreakout) | C · 추세와 변동성 돌파 | 장중 수급의 방향이 수 분–수십 분 이어지는가 | 1–30분 | 40 | 14 |
| [`D_MeanReversion`](D_MeanReversion) | D · 평균회귀와 상대가치 | 어떤 기준에 대해 무엇이 30분 안에 돌아오는가 | 1–30분 | 41 | 13 |
| [`E_LeadLag`](E_LeadLag) | E · 선도·후행과 정보 전파 | 내 주문이 도착한 뒤에도 후행 움직임이 남는가 | 1초–10분 | 36 | 11 |
| [`F_PriceDiff_Hedge`](F_PriceDiff_Hedge) | F · 가격차와 헤지 거래 | 양쪽 비용과 위험을 다 빼도 가격차 수익이 남는가 | 1초–30분 | 47 | 18 |
| [`G_TimeEvents`](G_TimeEvents) | G · 시간대와 시장 사건 | 사건 전후의 변화가 비용을 넘는 수익을 남기는가 | 5초–30분 | 41 | 16 |
| [`H_MarketMaking`](H_MarketMaking) | H · 시장조성과 재고 관리 | 체결의 가격 우위가 역선택과 재고 비용을 넘는가 | 재고 1초–5분 | 41 | 16 |

덱 PDF 18개 · 488장 + 카드뉴스 PDF 32개 · 256장. 유형마다 네 연구 후보(예: A1–A4)를 다룬다.

## 유형별 덱의 짜임

각 본편은 같은 네 구획을 따른다.

1. **기본 개념** — 그 유형의 언어(호가창·충격 분해·장중 모멘텀·OU 반감기·Epps 효과·베이시스·사건 상대시간·스프레드의 세 원천 등)
2. **네 연구 후보** — 후보별 신호 정의와 진입·청산 조건
3. **실행과 비용** — 지연·틱 크기·세금·증거금·대기열 등, 국내 현물과 크립토 시장의 비용 관문
4. **사례와 검증** — 실패 사례(Flash Crash, Quant Quake, Knight, FTX 등)와 채택 기준

워크북은 본편의 수식과 손익 계산을 계산기 없이 따라가는 단계별 풀이다.

## 후보별 카드뉴스

각 유형 폴더의 `Cards/`에 후보 하나당 8장(세로 4:5) 카드뉴스 PDF가 있다. 표지는 호가창 같은 예시 하나로 후보를 소개하고, 마지막 장 「한눈에 보기」에 가설·데이터·신호·진입·청산·보유·핵심 실패·우선순위를 모은다.

| 후보 | 카드뉴스 |
|---|---|
| A1 | [주문 흐름 확인 모멘텀](A_OrderFlow/Cards/A1_OrderFlow_Momentum.pdf) |
| A2 | [다층 호가 불균형 방향성](A_OrderFlow/Cards/A2_Multilevel_Book_Imbalance.pdf) |
| A3 | [호가 소진과 재공급 부족](A_OrderFlow/Cards/A3_Depletion_Replenishment.pdf) |
| A4 | [체결 강도 가속 추종](A_OrderFlow/Cards/A4_Execution_Intensity_Acceleration.pdf) |
| B1 | [대량 매도 충격 후 반전](B_LiquidityShock/Cards/B1_Sell_Shock_Reversal.pdf) |
| B2 | [스프레드 급확대 후 정상화](B_LiquidityShock/Cards/B2_Spread_Normalization.pdf) |
| B3 | [강제청산 연쇄 후 회복](B_LiquidityShock/Cards/B3_Liquidation_Cascade_Recovery.pdf) |
| B4 | [반복 대량 매도 흡수 후 반등](B_LiquidityShock/Cards/B4_Absorption_Rebound.pdf) |
| C1 | [장 초반 범위 돌파](C_TrendBreakout/Cards/C1_Opening_Range_Breakout.pdf) |
| C2 | [변동성 압축 후 돌파](C_TrendBreakout/Cards/C2_Volatility_Squeeze_Breakout.pdf) |
| C3 | [상승 추세 중 VWAP 눌림목](C_TrendBreakout/Cards/C3_VWAP_Pullback.pdf) |
| C4 | [돌파 후 재시험 추종](C_TrendBreakout/Cards/C4_Breakout_Retest.pdf) |
| D1 | [시장·업종 조정 잔차 반전](D_MeanReversion/Cards/D1_Residual_Reversal.pdf) |
| D2 | [횡보 국면 VWAP 편차 회귀](D_MeanReversion/Cards/D2_Range_VWAP_Reversion.pdf) |
| D3 | [동종 자산 페어 스프레드 회귀](D_MeanReversion/Cards/D3_Pair_Spread_Reversion.pdf) |
| D4 | [유동성 높은 바스켓 대비 이탈 회귀](D_MeanReversion/Cards/D4_Basket_Deviation_Reversion.pdf) |
| E1 | [BTC 선도 알트코인 후행 추종](E_LeadLag/Cards/E1_BTC_Lead_Alt_Lag.pdf) |
| E2 | [거래소 간 선도 가격 추종](E_LeadLag/Cards/E2_Cross_Exchange_Lead.pdf) |
| E3 | [지수선물 선도 지수 ETF 추종](E_LeadLag/Cards/E3_Futures_Lead_ETF.pdf) |
| E4 | [업종 대표주 선도 동종주 추종](E_LeadLag/Cards/E4_Sector_Leader_Peer.pdf) |
| F1 | [현물·무기한선물 베이시스 회귀](F_PriceDiff_Hedge/Cards/F1_Perp_Basis_Reversion.pdf) |
| F2 | [사전 재고 기반 거래소 가격차](F_PriceDiff_Hedge/Cards/F2_Inventory_Cross_Exchange.pdf) |
| F3 | [ETF와 복제 바스켓 가격차](F_PriceDiff_Hedge/Cards/F3_ETF_Basket_Gap.pdf) |
| F4 | [현물과 만기선물 단기 베이시스](F_PriceDiff_Hedge/Cards/F4_Dated_Futures_Basis.pdf) |
| G1 | [시초가 갭 반응](G_TimeEvents/Cards/G1_Opening_Gap.pdf) |
| G2 | [VI 이후 가격 발견](G_TimeEvents/Cards/G2_Post_VI_Discovery.pdf) |
| G3 | [공시·뉴스의 지연 반응](G_TimeEvents/Cards/G3_News_Delayed_Reaction.pdf) |
| G4 | [펀딩 시점의 베이시스 거래](G_TimeEvents/Cards/G4_Funding_Basis_Trade.pdf) |
| H1 | [재고 한도 기반 양방향 호가](H_MarketMaking/Cards/H1_Inventory_Limit_Quoting.pdf) |
| H2 | [예측 신호 기반 비대칭 호가](H_MarketMaking/Cards/H2_Signal_Skewed_Quoting.pdf) |
| H3 | [변동성·역선택 대응 호가](H_MarketMaking/Cards/H3_Volatility_Adverse_Selection_Quoting.pdf) |
| H4 | [관련 상품으로 헤지하는 시장조성](H_MarketMaking/Cards/H4_Cross_Hedged_Market_Making.pdf) |

## 파일 이름

`A_OrderFlow/A_OrderFlow_Main.pdf` · `A_OrderFlow/A_OrderFlow_Workbook.pdf` — 유형 문자 + 슬러그 + 본편/워크북.
카드뉴스는 `A_OrderFlow/Cards/A1_OrderFlow_Momentum.pdf`처럼 후보 번호 + 슬러그. 낱장 PNG는 로컬에만 둔다(`Cards/PNG/`, 저장소 제외).
원본 PPTX는 저장소에 올리지 않는다.

## 라이선스

[CC BY-NC-SA 4.0](LICENSE) — 출처를 밝히면 비상업적 목적으로 자유롭게 쓰고 고칠 수 있다. 고친 자료도 같은 조건으로 공유한다.
