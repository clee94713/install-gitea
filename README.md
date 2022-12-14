# Gitea 설치 가이드

## 개요

## 구성 요소 및 버전

## 폐쇄망 구축 가이드

3. Keycloak 연동 시
	1. Keycloak에서 클라이언트 생성
	- Name: gitea
	- Client-Protocol: openid-connect
	- AccessType: confidential
	- Valid Redirect URIs: *

	2. 클라이언트 시크릿 복사
	- Client > gitea> Credentials > Secret

	3. gitea/values.yaml 설정
	```
	gitea:
	  oauth:
	    - name: 'giteaOAuth' # oauth 이름
	      provider: 'openidConnect' # 클라이언트 프로토콜
	      key: 'gitea' # Keycloak 클라이언트 이름
	      secret: '******' # Keycloak 클라이언트 시크릿
	      autoDiscoverUrl: 'https://{keycloakhost}:{keycloakport}/auth/realms/{realm}/.well-known/openid-configuration' # Keycloak의 autoDiscoverUrl
	                            ex) 'https://hyperauth.tmaxcloud.org/auth/realms/tmax/.well-known/openid-configuration' # hyperauth의 경우 사용 예시
	```

4. 추가 gitea/values.yaml 설정
```
gitea:
  config:
    server:
      PROTOCOL: http
      DOMAIN: gitea.testdomain.com # 도메인 설정
      ROOT_URL: http://gitea.testdomain.com # root url 설정
      SSH_DOMAIN: gitea.testdomain.com # ssh 도메인 설정
```