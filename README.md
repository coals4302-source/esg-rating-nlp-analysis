# ESG 등급 NLP 분석 (ESG Rating NLP Analysis)

비정형 데이터 처리 수업 텀프로젝트 — DART 사업보고서 텍스트를 기반으로 ESG 등급을 분석합니다.

---

## 프로젝트 개요

한국 상장기업의 DART(전자공시시스템) 사업보고서에서 ESG 관련 텍스트를 추출하고, NLP 기법을 적용하여 ESG 등급(D ~ A+)과의 관계를 분석합니다.

**핵심 질문**: 기업의 공시 문서에 담긴 ESG 서술이 실제 ESG 등급과 유의미한 관계를 가지는가?

---

## 분석 흐름

```
DART XML 수집 → 코퍼스 구축 → EDA → 형태소 분석(Kiwi)
→ ESG 사전 구축(FastText + 임베딩 확장) → 상관분석 / 증분설명력 분석
→ ESG 감성분석 (등급 수준 / 변화량) → 생존분석(Cox PH)
```

---

## 주요 분석

| 분석 | 방법 | 내용 |
|------|------|------|
| 코퍼스 구축 | XML 파싱, Kiwi 형태소 분석 | DART 사업보고서 ESG 문장 추출 |
| EDA | 기술통계, 시각화 | ESG 등급(D/C/B/B+/A/A+) 분포 분석 |
| 증분설명력 분석 | TF-IDF | ESG 텍스트의 등급 설명력 측정 |
| 상관분석 | Spearman, Kruskal-Wallis, Mann-Whitney U | ESG 지수와 등급 간 상관 검정 |
| 감성분석 | ESG 도메인 사전 기반 | 문장 수준 긍/부정 감성 지수 산출 |
| 생존분석 (부록) | Cox PH 모형 | ESG 지수 변화가 등급 하락 위험에 미치는 영향 |

---

## 주요 결과

- ESG 감성 지수가 1단위 증가할수록 차년도 등급 하락 위험이 **4.1% 증가** (위험비 1.041)하는 역설적 결과 관찰
- 생존분석 p값 0.095 — 표본 수 제한(70행, 이벤트 11건)으로 통계적 유의성 확보 불가
- FastText + Kiwi 임베딩(threshold 0.80) 기반 ESG 도메인 사전 확장 수행

---

## 파일 구조

```
.
├── 비정형_최종.ipynb                          # 전체 분석 코드 (Google Colab)
│   └── 기말_보고서/기말텀프로젝트/
├── Short Research Paper.docx                  # 학술 소논문
└── 비정형.pdf                                 # 최종 발표 자료
```

---

## 사용 기술

- **형태소 분석**: [kiwipiepy](https://github.com/bab2min/Kiwi)
- **임베딩 / 사전 확장**: FastText, Word Embedding
- **ML / 통계**: scikit-learn (TF-IDF), scipy (Spearman, Kruskal-Wallis), lifelines (Cox PH)
- **딥러닝**: HuggingFace Transformers
- **환경**: Google Colab, Python 3

---

## 데이터

- **출처**: DART 전자공시시스템 (사업보고서 XML)
- **대상**: KOSPI / KOSDAQ 상장 기업
- **ESG 등급 기준**: D / C / B / B+ / A / A+ (6단계)
