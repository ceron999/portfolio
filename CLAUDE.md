# CLAUDE.md — 정윤석 포트폴리오 웹사이트 프로젝트 컨텍스트

> 이 파일은 Claude Code가 포트폴리오 웹사이트를 구축할 때 참조하는 컨텍스트 문서입니다.
> 정윤석(Ceron)의 이력서, 자기소개서, 포트폴리오 PDF에서 추출한 정보와 추가 맥락을 정리했습니다.

---

## 1. 인적 사항

- 이름: 정윤석 (Jung Yunseok)
- 직무: Game Client Programmer (Unity 2D/3D)
- 생년월일: 1998.03.19
- 이메일: ceron999@naver.com
- 연락처: 010-9911-8362
- GitHub: https://github.com/ceron999
- 포트폴리오 (My Box): http://naver.me/5eUfiJ3V
- Project HD 프로토타입 플레이 영상: https://youtu.be/dKIKGcPVkH4

---

## 2. 학력 / 병역 / 자격증

- 홍익대학교 컴퓨터공학 전공 졸업 (2018.02 ~ 2025.02)
- 세일고등학교 졸업 (2014.02 ~ 2017.02)
- 육군 병장 만기전역, 보병 (2018.10 ~ 2020.06)
- 한국사능력검정고사 1급 (2020.08)

---

## 3. 기술 스택

| 분류 | 상세 |
|------|------|
| Engine/Language | Unity (5, 6), C# |
| Collaboration | GitHub, Notion |
| 데이터 처리 | JSON, Scriptable Object, Excel |
| 3rd Party | Odin Inspector, vFolder2 |
| 기타 | Visual Studio, Spine, Cinemachine, NavMesh, Input System, URP |

---

## 4. 자기소개서 요약

### 지원 동기
게임의 재미를 오래 붙잡는 핵심은 성장이라고 믿으며, 인게임 시스템 구현/AI 행동 구조 정리/최적화/데이터 구조화를 통해 플레이 흐름을 안정적으로 뒷받침하는 클라이언트 프로그래머를 지향함.

### 강점 1 — 책임감
Project HD 12월 빌드 마감 전 50여 개 잔여 과제를 4단계 우선순위로 세분화하여 체계적 작업 리스트 수립, 일정 내 안정적 프로토타입 완성 배포.

### 강점 2 — 협력적 태도
구현 기능을 짧은 영상으로 촬영해 Notion/Discord에 수시 공유. Odin Inspector로 타 부서도 직관적으로 데이터 제어할 수 있는 에디터 툴 제작.

### 강점 3 — 로직/데이터 분리 설계 + 최적화
SO 중심 데이터 구조로 기획자/아트가 필요한 SO만 찾아 정보를 변경 가능하게 설계. GC Alloc 80KB+ → 1KB 이하 최적화 달성. BT 노드 세분화로 유지보수 비용 절감.

### 성장 노력
Unity Seoul 행사 참여, 인프런 강의 수강, 학습 내용을 사이드 프로젝트에 직접 적용. Google Sheets-Unity 연동 파이프라인 구축, Cinemachine 심화 학습, Spine 4방향 상하체 분리 애니메이션 구현, ECS 적용 검토 중.

---

## 5. 프로젝트 (웹사이트 표시 순서)

### 5-1. Project HD — HD-2D 익스트랙션 어드벤처 게임 (대표 프로젝트)

- 기간: 2025.08 ~ 진행 중
- 규모: 6명 (기획 1, 프로그래밍 2, 아트 3)
- 장르/목표: 서바이벌 + 익스트랙션, 스쿼드 전술 기반 루프 구현
- 기술: Unity 2022.3, Input System, NavMesh, BT, SO, Odin, Spine
- 역할: 인게임 프로그래밍 파트 (AI, 전투, 인벤토리, 스킬, 데이터 관리, 최적화 등) + 프로젝트 관리(병합/충돌 해결)
- 플레이 영상: https://youtu.be/dKIKGcPVkH4

#### 핵심 기여

**1) Squad Command System**
- BT, Input System, Squad Controller를 활용해 아군 캐릭터 명령 통제
- 이동/공격/정지/집합/비살상 모드/스킬/아이템/상호작용 등 다양한 Command 대응
- 사수/탱커/힐러/채광 등 전문성에 따라 세부 로직 변경
- PlayerInput → Input System → BT & Command Routing 구조
- BlackBoard를 만들어 약 30개 데이터 Dictionary 저장/조회, 중복 연산 제거
- 입력을 행동에 직접 연결하지 않고 Command로 추상화 → BT가 실행/전환 담당

**2) Behavior Tree**
- FSM 대신 BT를 선택한 이유: 복잡한 행동 트리 구현의 유연성, 높은 AI 지능 구현 목적
- 4가지 특성(캡틴, 사수, 탱커, 힐러, 채광)에 맞는 BT를 캐릭터 생성 시 초기화
- 중복 사용 가능한 Node는 분리하여 재사용
- 기획 변경에 따른 기능 교체가 용이하도록 설계
- 적 AI: Idle(순찰) → Warning(감지범위 진입 시 이동) → Chase(타겟 지정 범위 진입 시 추격) → Attack(공격 범위 진입 시 공격) 단계

**3) Game System (개발한 시스템 목록)**
- Skill 시스템: SO 기반 데이터, Skill Factory/Base Skill/Skill Activator/Skill Context 구조, Odin ShowIf로 조건부 Inspector 노출
- Noise 시스템: 소음 발생 타입(스프레드 파동/에어리어) × 타이밍(싱글/멀티) × 잔재 여부(인스턴트/서스테인/에코), NoiseMaker → NoiseManager → NoiseListener 구조
- Item / Trap: SO 기반, 타 부서가 쉽게 이해하고 변경 가능하도록 설계
- Input System (Legacy + Input Action)
- Squad 관리 (부대 지정 등)
- 인벤토리 (아이템 루팅/탈장착)
- 미션 (인벤토리와 연동)
- 카메라 시스템
- VFX, Sound Manager, Buff 시스템

**4) 최적화**
- BT & NavMesh 최적화: tick 시간 0.1~0.2초 분산, SetDestination 호출 최소화, OverlapSphereNonAlloc, 원거리 적 BT 미진행, SqrMagnitude 사용
- 시야 시스템 최적화: Profiler BeginSample로 GC 위치 구체화, Dictionary/HashSet 캐싱, GetComponentInParent → Transform.root.GetComponent로 변경 → GC 할당 0B 근접 + 약 10ms 감소
- 미니맵 렌더링 최적화: 미니맵 전용 Renderer 생성(RenderFeature 최소화), Depth/Stencil=None, Orthographic Size 최소화 → Camera Render 50% 이상 절감

---

### 5-2. Libs Rarry (Project LR) — 3D 로그라이크 덱 빌딩 게임

- 기간: 2025.01 ~ 진행 중
- 규모: 6명 (기획 1, 프로그래밍 2, 아트 3)
- 시작: 2024 Nexon GameJam에서 2박 3일 만든 프로토타입을 발전
- 기술: Unity 6, Cinemachine, DOTween, Camera Stack, Google Sheets 연동
- 역할: 시스템 기획 반영 + SO 데이터 구조 구현, UI/Cinemachine 연출, 프로젝트 관리

#### 핵심 기여

**1) 변경된 기획 및 연출**
- Game Volume 증가: 5회 전투 → 50회 전투/이벤트/보스 (Slay the Spire 방식)
- 1~5개 Stage 랜덤 표시, 매 5라운드마다 Boss Stage
- 시작 연출 변경: DoTween → Cinemachine 여러 대 활용한 시작 연출
- UI 퀄리티 업그레이드: 호버링 시 카드 UI 표시, 버튼 클릭으로 적 캐릭 선택
- Skill System 변경, AP 소모 시스템 추가, 적마다 특수 Gimmick 추가, 다양한 카메라 연출 추가

**2) Camera Stack을 활용한 렌더링 순서 변화**
- UI Camera + OverUI Camera를 Main Camera stack에 배치
- 늑대 오브젝트를 OverUI Layer로 설정, 전용 카메라로만 렌더링
- 스킬 사용 시 Fade UI 이후 Wolf 렌더링 구현 (가장 난이도 높았던 구현)

**3) Google Sheets 데이터 파이프라인**
- Google Sheet API → GoogleSheetParser → ISheetData/IWrapper → JSON 저장
- 기획자가 익숙한 시스템(Google Sheets)에서 데이터 수정 → Unity에서 자동 갱신
- 제네릭 ConvertResponseToJson<T, TWrapper> 구조로 범용성 확보

**4) 시스템 구조도**
- UML 기반 오브젝트 관계도 작성 후 작업 시작 (Battle, Stage, Gimmick 등)
- StageManager 코드: Level/Stage/Encounter 함수 분류 그룹화, FuncSummary 활용

**5) 기타**
- Excel/JSON/SO 등 다양한 데이터 관리 구조
- Stage 진입/퇴장 연출, 보유 스킬 UI, Fade 등 다수 연출 구현
- Stack 기반 턴당 n개 스킬 실행 + 연쇄 발동 시스템
- Encounter 이벤트: 스킬 강화, 가챠 기반 스킬 변경, 스탯 변화

---

### 5-3. Side TPS Project — 3D TPS 자기계발 프로젝트

- 개인 프로젝트
- 장르: TPS (서든어택 A 보급과 유사한 룰)
- 기술: Unity, Rigging, Animation, Cinemachine, NavMesh, Post-Processing, UGUI
- 목표: TPS 핵심 기능을 대부분 구현한 자기계발 프로젝트

#### 핵심 기여
- Player 이동 기능: 걷기/달리기/앉기 (8방향)
- Player 무기 5가지: 라이플, 스나이퍼(Zoom), 권총, 수류탄, C4 (Object Pool 활용)
- Animation Rigging: Aim Rig로 에임 맞추기, Red Ray(총알 발포 ray)
- 전투 UI: MiniMap, Timer, Crosshair, Status, 상황판
- 적 AI: FSM 기반 (Search/Battle/Die/TakeWarning), 5개 순찰 지점, 자율 순찰
- Post-Processing: Bloom, Color Grading으로 사막 분위기 연출
- 연출: Dolly Track 활용 카메라 이동

---

### 5-4. ETC — 동아리 프로젝트 (2021~2023)

- 홍익대 게임 개발 동아리 EXP에서 진행
- 약 10개 프로젝트 (출시 5개, Google Play 배포)
- 장르: TPS/퍼즐/캐주얼/시뮬레이션/Visual Novel 등

#### 출시 게임 목록 (Project Timeline)
| 연도 | 게임명 |
|------|--------|
| 2021 | 우리집은 어디에? |
| 2022 | Ghost |
| 2022 | 어서오세요. 카페 24에 |
| 2023 | Neo Slasher (뱀서라이크 핵앤슬래시) |
| 2023 | Dumbest Letter |

#### Neo Slasher 상세
- 사이버펑크 배경 뱀서라이크 게임
- 15개 × 4개 등급 아이템 = 총 60개 구현
- 20레벨 특성 시스템 (레벨마다 2~4개 해금, 1개 선택)
- 4단계 난이도 시스템
- 전투에 관련된 모든 부분 구현 (아이템, 특성, 적 AI 등)

#### 구현 기능 키워드
Rigging/Animation, Cinemachine, NavMesh, JSON, AI(FSM), Dialogue System, 100개 이상의 스킬/아이템 데이터 관리

---

### (제외) Chess Program — 졸업 프로젝트
> 웹사이트에 포함하지 않음. 참고용으로만 기록.
- Algorithm 기반 체스 AI (MinMax + Q-learning 개념 혼합)
- 기물 이동, 특수 규칙(Castling/Promotion), 기보 저장/리뷰 기능

---

## 6. 웹사이트 하단 — 최근 노력하고 있는 것들

### 코딩 테스트 준비
- C++ 프로그래머스 알고리즘 문제 풀이 (Sort, Simulation, DP, Greedy 등)
- GitHub에 꾸준히 커밋 (Algorithm 레포)
- 인프런 온라인 코딩 테스트 강의 수강 중
- 노션에 한 줄 요약/핵심 아이디어/시간 복잡도/오답 노트 형식으로 정리

### 기술 학습
- Unity 6 Shader Graph 입문과 활용 (인프런)
- OpenGL/3D 그래픽스 강의 수강 예정
- Unity 6 멀티플레이 디펜스, TPS 마스터클래스 수강 예정
- More Effective C# 학습 (GitHub 커밋)
- 유니티 디자인 패턴 책 학습 (GitHub 커밋)
- ECS 구조 학습 및 NavMesh 최적화 적용 검토 중

### 행사 참여
- 2025 Unite Seoul 참가 (다양한 인사이트 획득)

### 자기계발 습관
- 학교 수업과 병행하며 꾸준히 Commit
- Branch 나누어 작업 후 Merge 방식으로 협업
- 2025 졸업 이후 개인 공부 + 출시 목적 프로젝트 병행

---

## 7. 웹사이트 구조 가이드

### 목적
정윤석의 게임 클라이언트 프로그래머 포트폴리오 웹사이트

### 프로젝트 표시 순서 (최신순)
1. Project HD (대표 프로젝트, 가장 상세하게)
2. Libs Rarry
3. Side TPS Project
4. ETC (동아리 프로젝트들)

### 페이지 구성 제안 (논의 필요)
- Hero / 소개 섹션
- 프로젝트 섹션 (각 프로젝트 카드 → 상세 페이지)
- 기술 스택 섹션
- 하단: 최근 노력 / 학습 기록 섹션
- Contact

### 호스팅
- 미정 (GitHub Pages / Vercel / Netlify 중 논의 예정)

### 참고 링크
- GitHub: https://github.com/ceron999
- 포트폴리오 원본 (My Box): http://naver.me/5eUfiJ3V
- Project HD 플레이 영상: https://youtu.be/dKIKGcPVkH4

---

## 8. 주의사항 (Claude Code용)

- Project HD와 Libs Rarry(Project LR)는 완전히 별개의 프로젝트로 항상 명확히 구분할 것
- 컨텐츠라는 단어를 사용할 것 (콘텐츠 X)
- 큰따옴표를 사용하지 않을 것
- 한국어 기반 웹사이트이나, 기술 용어는 영문 그대로 사용
