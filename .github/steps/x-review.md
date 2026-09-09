## 🎉 완주했습니다

여러분이 겪은 것:

- 내 계정이 IdP 에서 만들어졌다는 것. 이름조차 내가 못 정한다는 것
- public 리포와 엔터프라이즈 밖 활동이 막힌다는 것
- 로그인이 되어도 토큰은 따로 인가받아야 한다는 것
- 내 행동이 전부 감사 로그에 남는다는 것

### 시험에서 이렇게 물어봅니다

- managed user 와 personal account 중 무엇을 골라야 하는 상황인가
- SAML SSO 와 SCIM 은 각각 무엇을 담당하는가 (인증과 프로비저닝)
- SCIM 과 team synchronization 의 차이는 무엇인가
- 배포 시나리오 네 가지의 차이 (GHEC + personal, GHEC + EMU, GHEC + Data Residency + EMU, GHES)

### 여기서 다루지 못한 것 (강사 시연)

- IdP 쪽 SAML 과 SCIM 배선 화면. 엔터프라이즈 하나에 IdP 는 하나만 붙습니다
- team synchronization 으로 IdP 그룹이 GitHub 팀이 되는 과정
- 사용자 정지와 라이선스 회수
- GHES 의 support bundle 과 관리 콘솔

IdP 쪽을 직접 만들어 보는 실습은 **랩 F (gh-100-idp-wiring-drill)** 입니다.

### 다음에 볼 것

- [About Enterprise Managed Users](https://docs.github.com/en/enterprise-cloud@latest/admin/managing-iam/understanding-iam-for-enterprises/about-enterprise-managed-users)
- [Choosing an enterprise type](https://docs.github.com/en/enterprise-cloud@latest/enterprise-onboarding/getting-started-with-your-enterprise/choose-an-enterprise-type)
- [Authorizing a personal access token for use with SAML single sign-on](https://docs.github.com/en/enterprise-cloud@latest/authentication/authenticating-with-saml-single-sign-on/authorizing-a-personal-access-token-for-use-with-saml-single-sign-on)
