# 이 프로젝트의 목표
## 테스트 코드 작성
- 각 API 엔드포인트에 대한 단위 테스트 및 통합 테스트를 작성한다.

## N+1 문제 경험
- N+1 문제를 의도적으로 발생시키고 해결 방법을 학습
- 리뷰 조회 시, 영화 정보와 함께 N+1 문제를 경험하고, 이를 해결하기 위한 방법을 적용한다.
- 이 문제를 경험하기 전에 가짜 데이터를 대량으로 추가하여 시간 비교

## 디버깅
- 디버깅 도구 사용법 익히기

---
# 요구사항 정의서

## 1. 개요
이 API는 영화와 해당 영화에 대한 리뷰를 관리하는 기능을 제공하며, 기본적인 인증 시스템과 관리자 권한이 필요한 엔드포인트를 포함합니다.

## 2. 사용자 역할
- **일반 사용자**: 영화와 리뷰를 조회하고, 리뷰를 작성할 수 있다.
- **관리자**: 영화 추가 및 삭제와 같은 관리 기능을 수행할 수 있다.

## 3. 관리자 권한이 필요한 엔드포인트
- **POST** `/movies`: 영화 추가 (관리자 전용)
- **DELETE** `/movies/{id}`: 영화 삭제 (관리자 전용)

## 4. API 엔드포인트

| **메서드** | **엔드포인트**                | **설명**                               | **권한**  |
|------------|-------------------------------|----------------------------------------|-----------|
| POST       | `/login`                      | 사용자 인증 및 JWT 토큰 발급        | 없음      |
| POST       | `/movies`                    | 영화 추가 (관리자 전용)              | 관리자    |
| DELETE     | `/movies/{id}`               | 영화 삭제 (관리자 전용)              | 관리자    |
| GET        | `/movies`                     | 모든 영화 목록 조회                  | 없음      |
| GET        | `/movies/{id}`                | 특정 영화 조회 및 리뷰 조회         | 없음      |
| POST       | `/movies/{id}/reviews`       | 특정 영화에 리뷰 추가                | 일반 사용자 |
| GET        | `/movies/{id}/reviews`       | 특정 영화의 모든 리뷰 조회           | 없음      |

## 5. 인증 및 권한 처리
- 각 요청 시 JWT 토큰을 검증하여 사용자의 인증 상태를 확인합니다.
- 관리자 전용 엔드포인트에 대해서는 사용자 역할이 "관리자"인지 확인하여 접근을 허용합니다.

## 6. 에러 처리
- **401 Unauthorized**: 인증 실패 시.
- **403 Forbidden**: 접근 권한이 없을 경우 (예: 관리자가 아닌 사용자가 관리자 전용 엔드포인트에 접근 시).
- **404 Not Found**: 요청한 영화가 존재하지 않을 경우.
