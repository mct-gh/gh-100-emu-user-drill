## Step 3: 토큰 하나로 SSO 를 이해한다

SAML SSO 를 켜면 로그인만 바뀌는 게 아닙니다. **토큰도 SSO 와 묶여야** 합니다. 여기서 많이 막힙니다.

### 📖 Theory: 인증과 인가는 다른 층이다

- **인증(authentication)** — 너는 누구인가. IdP 가 SAML 어설션으로 대답합니다.
- **인가(authorization)** — 이 토큰이 이 조직의 데이터를 만져도 되는가. 토큰마다 따로 정해집니다.

개인 계정으로 SAML 조직에 들어간 경우, 문서가 정한 규칙은 이렇습니다.
- **PAT (classic)** 는 만든 뒤 토큰 목록에서 `Configure SSO → Authorize` 를 눌러 조직별로 인가해야 합니다. 안 하면 그 조직에 대해 아무것도 못 합니다.
- **fine-grained PAT** 는 만들 때 이미 인가됩니다. 문서 원문은 "authorized during token creation" 입니다.

여러분은 지금 **관리형 사용자** 입니다. 계정 자체가 엔터프라이즈 소유라서 개인 계정과 화면이 다를 수 있습니다.
이 단계의 목적은 규칙을 외우는 것이 아니라, **자기 계정에서 실제로 어떤 화면이 나오는지 확인하고 기록하는 것**입니다.

> [!WARNING]
> 이 랩에서 만든 토큰은 끝나면 지우세요. 기록 파일에 **토큰 값을 절대 붙여 넣지 마세요.**
> 응답 메시지만 적습니다. 토큰 값이 들어 있으면 채점이 실패합니다.

### ⌨️ Activity: pat-sso.md 를 만든다

1. Settings → Developer settings → Personal access tokens → **Fine-grained tokens** 에서 토큰을 하나 만듭니다.
   - Resource owner 에서 어떤 선택지가 보이는지 봅니다. 개인 계정 대신 조직이나 엔터프라이즈가 뜰 수 있습니다.
   - Repository access 는 이 리포 하나만, Permissions 는 Metadata read-only 만.
2. 그 토큰으로 이 리포 정보를 불러 봅니다.
   ```bash
   curl -s -H "Authorization: Bearer <토큰>" https://api.github.com/repos/<조직>/<이 리포 이름>
   ```
3. 토큰 목록으로 돌아가서 **Configure SSO** 같은 인가 버튼이 있는지 봅니다. 있으면 눌러 보고, 없으면 없다고 적습니다.
4. 가능하면 **Tokens (classic)** 도 하나 만들어 같은 명령을 돌려 봅니다. 엔터프라이즈 정책이 classic 을 막아 두었으면 그 화면을 적습니다.
5. `records/pat-sso.md` 를 만들어 아래를 적습니다.
   - `fine-grained` 토큰으로 API 를 불렀을 때 응답 (성공이면 첫 줄, 실패면 오류 메시지 원문)
   - 인가 버튼이 있었는지, 있었다면 누르기 전과 후에 무엇이 달라졌는지
   - classic 토큰을 만들 수 있었는지. 막혔다면 어떤 정책 문구가 보였는지
   - 인증과 `인가` 의 차이를 한 줄로
   - 토큰을 지웠는지 여부
6. push 합니다.

<details><summary>채점 기준</summary>

- `records/pat-sso.md` 가 있다
- 그 안에 `fine-grained` 가 있다
- 그 안에 `인가` 가 있다
- 그 안에 토큰 값이 없다 (`ghp_`, `github_pat_` 로 시작하는 문자열이 있으면 실패합니다)
</details>
