# GH-100 Lab E — EMU 사용자로 살아 보기

_Enterprise Managed User 계정으로 로그인해서, 관리자가 건 통제를 몸으로 겪는 실습입니다._

## Welcome

- **과정**: GH-100 GitHub fundamentals - Administration basics and product features
- **모듈**: M2 Introduction to GitHub administration, M6 Authenticate and authorize user identities, M7 GitHub administration for enterprise support and adoption
- **시험 도메인**: 1 Manage GitHub identities and access (배점 15~20%)
- **소요 시간**: 약 40분
- **선행**: 강사가 준비한 EMU 엔터프라이즈에 여러분 계정이 프로비저닝되어 있어야 합니다

세 모듈 모두 공식 실습이 없습니다. SAML SSO, SCIM, EMU 는 읽기만 하고 넘어가기 쉬운 주제입니다.
이 랩은 그것을 **사용자 입장에서 직접 겪게** 만듭니다.

이 랩에서 여러분은:

1. IdP 로 로그인해서 자기 계정이 **관리형 사용자(managed user)** 임을 확인합니다.
2. public 리포를 만들려고 시도해서 **막히는 것**을 겪고 그 이유를 적습니다.
3. PAT 를 만들고, **SSO 인가(authorization)** 를 거치기 전과 후의 API 응답 차이를 기록합니다.
4. 감사 로그에서 자기 행동을 찾아 이벤트 이름을 적습니다.

## 시작하는 법

> [!IMPORTANT]
> 이 랩은 **개인 GitHub 계정이 아니라, 강사가 준 EMU 계정으로** 진행합니다.
> 로그인한 계정 이름에 `_` 가 들어 있는지 먼저 확인하세요. 예: `contoso_dlee`

1. 강사가 안내한 **학습 전용 조직** 안에 이 템플릿을 복사합니다. (**Use this template**)
   - 리포 이름 끝에 자기 이름을 붙이세요. 예: `gh-100-emu-user-drill-dlee`
   - **visibility 는 Private 로 둡니다.** EMU 계정은 public 리포를 만들 수 없습니다.
2. 약 20초 후 새로고침하면 첫 단계가 이슈로 열립니다.
3. 이슈에 적힌 대로 `records/` 안에 기록 파일을 만들고 push 하면 채점됩니다.

## 이 랩의 제약 — 먼저 읽어 주세요

### 1. 강사 준비가 필요합니다

이 랩은 혼자서는 돌릴 수 없습니다. EMU 엔터프라이즈와 IdP 가 있어야 합니다.

| 필요한 것 | 어떻게 | 비고 |
|---|---|---|
| EMU 엔터프라이즈 | GitHub Enterprise Cloud 30일 트라이얼에서 `enterprise with managed users` 선택 | 라이선스 50개까지 |
| 호스트 선택 | 반드시 **github.com** | `ghe.com` (데이터 레지던시) 는 Skills 랩이 지원되지 않음 |
| IdP | Entra ID 또는 Okta 등 파트너 IdP 하나 | SAML 인증 + SCIM 프로비저닝 |
| 학습 전용 조직 | 엔터프라이즈 안에 따로 만듦 | 설정은 [skills-for-emu](https://github.com/skills/skills-for-emu) 를 따름 |

준비 절차는 `lab\100\강사준비_EMU테넌트.txt` 에 있습니다.

### 2. 채점이 다른 랩보다 가볍습니다. 이유가 있습니다

워크플로의 `GITHUB_TOKEN` 은 조직과 엔터프라이즈 설정을 읽을 권한이 없습니다.
그래서 팀 멤버십, IdP 그룹, 엔터프라이즈 정책은 **워크플로가 확인할 수 없습니다.**

| 항목 | 채점 방식 |
|---|---|
| 로그인 계정이 managed user 인지 | 자동 (`github.actor` 와 기록 파일 대조) |
| 리포가 private 인지 | 자동 (API) |
| 나머지 관찰 기록 | 기록 파일 안의 문구 검사 |
| 팀 멤버십이 IdP 에서 왔는지 | 강사가 엔터프라이즈 화면에서 확인 |

> [!NOTE]
> 이 랩은 "설정을 했느냐" 를 채점하지 않습니다. **"무엇을 관찰했느냐"** 를 채점합니다.
> 체험이 목적이기 때문입니다. 관리자 설정을 직접 만드는 실습은 랩 F(IdP 배선)와 랩 A(Actions 거버넌스)에 있습니다.

### 3. 트라이얼에서 못 하는 것

- **Codespaces 가 포함되지 않습니다.** 이 랩은 Codespaces 를 쓰지 않습니다. 다른 공식 Skills 랩을 섞을 때는 확인하세요.
- Actions 분수가 3,000분입니다. 이 랩은 실행당 1분 이내입니다.
- 트라이얼은 30일입니다. 강의 직전에 만드세요.

### 4. 강사 시연으로 돌리는 것

- SAML SSO 와 SCIM 배선 화면 (엔터프라이즈 하나에 IdP 하나만 붙습니다)
- 팀 동기화(team synchronization) 설정
- EMU 사용자 정지와 해제, 라이선스 회수
- support bundle 생성 (GHES 전용)

<!-- 이 랩은 GH-100 커스텀 랩입니다. 공식 GitHub Skills 랩이 아닙니다. -->
