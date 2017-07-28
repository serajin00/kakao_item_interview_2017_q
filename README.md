# 로그 해석 문제 프로젝트

임의의 상품을 판매하는 어떤 스토어에 발생한 이벤트 로그 파일이 주어집니다.

로그의 기간은 '2017년 1월 1일 ~ 6월 30일' 입니다.

전체 로그 파일
> log.txt.gz

샘플 로그 파일
> log.sample.txt


로그 파일은 한 줄에 하나의 이벤트가 JSON 으로 기록되어 있습니다.

# 이벤트 설명
이벤트는 총 6종류가 있고 다음과 같습니다.

## 0. 이벤트 공통 속성

| 속성명 | 타입 | 설명 |
| ---  | --- | --- | 
| type | String | 이벤트의 종류를 구분합니다. <br><br> 예) "user_item_buy" |
| timestamp | String | 이벤트가 발생한 시간입니다. <br> ISO8601 포맷으로 기록됩니다. <br><br> 예) "2017-01-04T22:55:11+09:00" | 

## 1. 상품 등록 이벤트

type: "item_register"

아이템이 판매중인 상태로 스토어에 등록됩니다.

| 속성명 | 타입 | 설명 |
| ---  | --- | --- | 
| item_id | Number | 아이템 ID |
| price | Number | 아이템 가격 |


> ```json
> {"type":"item_register","item_id":10019,"price":3000,"timestamp":"2017-01-04T00:00:00+09:00"}
> ```

## 2. 상품 판매종료 이벤트

type: "item_unregister"

아이템이 판매종료 처리되어 스토어에서 내려갑니다.

| 속성명 | 타입 | 설명 |
| ---  | --- | --- | 
| item_id | Number | 아이템 ID |

> ```json
> {"type":"item_unregister","item_id":10026,"timestamp":"2017-02-09T00:00:00+09:00"}
> ```

## 3. 사용자 가입 이벤트

type: "user_register"

유저가 스토어에 가입해서 활동을 하는 상태가 됩니다.

| 속성명 | 타입 | 설명 |
| ---  | --- | --- | 
| user_id | Number | 사용자 ID |
| age | Number | 나이 (18..45) |
| gender | String | 성별, "M" 또는 "F" |

> ```json
> {"type":"user_register","user_id":3237,"age":30,"gender":"F","timestamp":"2017-01-04T19:57:09+09:00"}
> ```

## 4. 사용자 탈퇴 이벤트

type: "user_unregister"

유저가 스토어에서 탈퇴합니다. 더이상 활동하지 않습니다.

| 속성명 | 타입 | 설명 |
| ---  | --- | --- | 
| user_id | Number | 사용자 ID |

> ```json
> {"type":"user_unregister","user_id":3026,"timestamp":"2017-01-18T05:21:27+09:00"}
> ```

## 5. 아이템 클릭 이벤트

type: "user_item_click"

유저가 아이템을 클릭합니다. (view 또는 hit 로 생각할 수 있습니다.)

| 속성명 | 타입 | 설명 |
| ---  | --- | --- | 
| user_id | Number | 사용자 ID |
| item_id | Number | 아이템 ID |

> ```json
> {"type":"user_item_click","user_id":3131,"item_id":10006,"timestamp":"2017-01-04T20:42:53+09:00"}
> ```

## 6. 아이템 구매 이벤트

type: "user_item_buy"

유저가 아이템을 구매합니다. 

| 속성명 | 타입 | 설명 |
| ---  | --- | --- | 
| user_id | Number | 사용자 ID |
| item_id | Number | 아이템 ID |

> ```json
> {"type":"user_item_buy","user_id":3168,"item_id":10017,"timestamp":"2017-01-04T16:21:47+09:00"}
> ```

# Question

* 3월 31일 24시에 판매중인 상품은 몇개인가요?
> Answer 1 : 162

* 4월에 가장 많은 매출을 올린 상품과 그 매출을 출력하세요.
> Answer 2 : 10455 (770000)

* 5월에 판매된 상품중 CTR 이 가장 높은 상품과 그 CTR 을 출력하세요. (CTR = buy per click)
> Answer 3 : 10771 (0.24)

* 6월 1일 24시 남아있는 유저수는 몇 명인가요? 성별 비율은 어떻게 될까요? 평균 나이는?
> Answer 4 : 1331 (M 0.42 / F 0.58 / A 31.44)

* (America/New_York)에서 접속한 유저가 현지시간 4월 1일 24시에 살수 있는 상품은 몇개인가요?
> Answer 5 : 163
