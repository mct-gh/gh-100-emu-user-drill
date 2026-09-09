## Step 1: 내 계정은 누가 만들었나

지금 로그인한 계정은 여러분이 만든 계정이 아닙니다. IdP 에서 SCIM 으로 **프로비저닝된** 계정입니다.

### 📖 Theory: managed user 와 personal account 의 차이

| | personal account | managed user |
|---|---|---|
| 계정 생성 | 본인이 직접 | IdP 에서 SCIM 으로 |
| 사용자 이름 | 본인이 정함 | `<shortcode>_<idp사용자>` 형태로 고정 |
| 비밀번호 | GitHub 에 있음 | 없음. IdP 로만 로그인 |
| 엔터프라이즈 밖 활동 | 자유 | 불가 |
| public 리포 | 만들 수 있음 | 만들 수 없음 |
| 계정 삭제 | 본인이 | IdP 에서 사용자를 지우면 따라 지워짐 |

> [!NOTE]
> `_` 앞부분이 엔터프라이즈의 **shortcode** 입니다. 엔터프라이즈를 만들 때 정하고, 그 뒤로 모든 계정 이름에 붙습니다.
> 첫 관리자 계정만 예외로 `<shortcode>_admin` 이고, 이 계정만 SCIM 으로 만들어지지 않습니다.

### ⌨️ Activity: identity.md 를 만든다

1. `records/identity.md` 파일을 만듭니다.
2. 아래를 적습니다.
   - 내 로그인 이름 전체 (`_` 포함해서 그대로)
   - 그중 shortcode 부분과 IdP 사용자 부분
   - `managed user` 라는 말을 넣어, 이 계정이 어떤 종류인지 한 줄로 설명
   - 이 리포의 visibility 와 그렇게 된 이유
3. `main` 에 커밋하고 push 합니다.

<details><summary>이렇게 확인하면 편합니다</summary>

프로필 아이콘을 눌러 이름을 보거나, 리포에서 Actions 로그의 `github.actor` 값을 봐도 됩니다.
</details>

<details><summary>채점 기준</summary>

- `records/identity.md` 가 있다
- 그 안에 내 로그인 이름이 그대로 적혀 있다
- 그 안에 `managed user` 가 있다
- 이 리포가 private 이다 (API 로 확인)
</details>
