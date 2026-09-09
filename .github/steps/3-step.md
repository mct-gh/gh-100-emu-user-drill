## Step 3: 토큰 하나로 SSO 를 이해한다

SAML SSO 를 켜면 로그인만 바뀌는 게 아닙니다. **토큰도 따로 인가를 받아야** 합니다. 여기서 많이 막힙니다.

### 📖 Theory: 인증과 인가는 다른 층이다

- **인증(authentication)** — 너는 누구인가. IdP 가 SAML 어설션으로 대답합니다.
- **인가(authorization)** — 이 토큰이 이 조직의 데이터를 만져도 되는가. 토큰마다 따로 승인합니다.

SSO 를 강제한 조직에서는 새로 만든 PAT 가 그 조직에 대해 **아무것도 못 합니다.**
토큰 목록에서 `Configure SSO` 를 눌러 조직을 인가해야 그때부터 통합니다.

> [!WARNING]
> 이 랩에서 만든 토큰은 끝나면 지우세요. 기록 파일에 **토큰 값을 절대 붙여 넣지 마세요.**
> 응답 메시지만 적습니다.

### ⌨️ Activity: pat-sso.md 를 만든다

1. Settings → Developer settings 에서 **PAT (classic)** 를 하나 만듭니다. 스코프는 `repo` 만.
2. 인가하기 **전에** 그 토큰으로 조직 정보를 한 번 불러 봅니다.
   ```bash
   curl -s -H "Authorization: Bearer <토큰>" https://api.github.com/orgs/<조직이름>/repos
   ```
3. 돌아온 오류 메시지를 그대로 복사합니다. `SAML` 이라는 단어가 들어 있을 것입니다.
4. 토큰 목록에서 **Configure SSO → Authorize** 를 누릅니다.
5. 같은 명령을 다시 실행하고 결과가 어떻게 달라졌는지 봅니다.
6. `records/pat-sso.md` 를 만들어 아래를 적습니다.
   - 인가 전 응답 (오류 메시지 원문. `SAML` 이 들어간 줄을 반드시 포함)
   - 인가 후 응답이 어떻게 달라졌는지
   - 인증과 인가의 차이를 한 줄로
   - 토큰을 지웠는지 여부
7. push 합니다.

<details><summary>채점 기준</summary>

- `records/pat-sso.md` 가 있다
- 그 안에 `SAML` 이 있다
- 그 안에 `인가` 가 있다
- 그 안에 토큰 값이 없다 (`ghp_` 로 시작하는 문자열이 있으면 실패합니다)
</details>
