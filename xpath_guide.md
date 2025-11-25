
# XPath 실전 챌린지 정답 및 해설

- `xpath_workbook.html` 파일에 있는 미션들의 모범 답안입니다.
- XPath는 정답이 하나만 있는 것이 아닙니다. 상황에 따라 더 견고하고 효율적인 방법을 선택하는 것이 중요합니다!

## LEVEL 0. 로그인 페이지 (입문)

### Mission 0-1: ID로 제목 찾기

- **정답:** `//*[@id='login-title']`
- **해설:** ID는 유일하므로 가장 빠릅니다.

### Mission 0-2: "로그인" 버튼 찾기

- **정답:** `//button[text()='로그인']`
- **해설:** `text()` 함수로 정확한 텍스트 매칭을 합니다.

### Mission 0-3: placeholder 속성으로 찾기

- **정답:** `//input[@placeholder='비밀번호 입력']`

## LEVEL 1. 블로그 포스트 (계층 구조)

### Mission 1-1: ID 내부의 작성자 span 찾기

- **정답:** `//div[@id='content']//span`
- **해설:** `//`는 하위의 모든 자손을 의미합니다. ID가 'content'인 div 아래의 모든 span을 찾습니다.

### Mission 1-2: class가 'date'인 요소 찾기

- **정답:** `//*[@class='date']` 또는 `//span[@class='date']`
- **해설:** 클래스 속성을 직접 타겟팅합니다.

## LEVEL 2. 소셜 링크 (문자열 매칭)

### Mission 2-1: href가 'https://twitter'로 시작

- **정답:** `//a[starts-with(@href, 'https://twitter')]`
- **해설:** `starts-with(@속성, '시작문자열')` 함수는 URL 필터링에 매우 유용합니다.

### Mission 2-2: class에 'instagram' 포함

- **정답:** `//a[contains(@class, 'instagram')]`
- **해설:** 클래스가 여러 개일 때(예: `social-link instagram`) 유용합니다.

## LEVEL 3. 페이지네이션 (순서와 인덱스)

### Mission 3-1: 첫 번째 페이지 번호

- **정답:** `//ul[@id='pagination']/li[1]`
- **해설:** XPath 인덱스는 **1부터 시작**합니다.

### Mission 3-2: 마지막 페이지 번호

- **정답:** `//ul[@id='pagination']/li[last()]`
- **해설:** `last()` 함수는 요소의 개수가 변해도 항상 마지막 요소를 찾아줍니다.

## LEVEL 4. 쇼핑몰 상품 목록 (형제 관계)

### Mission 4-1: "게이밍 마우스"의 가격 선택

- **정답:** `//h4[text()='게이밍 마우스']/following-sibling::span[contains(@class, 'price')]`
- **해설:** 텍스트로 기준 요소를 찾고 `following-sibling`으로 가격을 찾습니다.

### Mission 4-2: "품절" 상품의 "담기" 버튼 선택

- **정답:** `//span[text()='품절']/following-sibling::button`

## LEVEL 5. 관리자 직원 목록 (부모/조상)

### Mission 5-1: "이영희"의 "삭제" 버튼

- **정답:** `//td[text()='이영희']/parent::tr//button`
- **해설:** 이름을 찾고 -> 부모 행(tr)으로 이동 -> 다시 자식 버튼으로 이동하는 패턴입니다.

### Mission 5-2: "과장" 직급의 이메일

- **정답:** `//tr[td[2][text()='과장']]/td[3]`
- **해설:** `tr` 중에서 '2번째 td가 과장인 것'을 필터링하고, 그 `tr`의 3번째 td를 가져옵니다.

## LEVEL 6. 동적 클래스 & 폼 (고급)

### Mission 6-1: "동의함(Yes)" 라디오 버튼

- **정답:** `//label[contains(., '동의함')]//input`
- **해설:** `contains(., text)`는 현재 노드 및 자손 텍스트를 모두 검사합니다.

### Mission 6-2: 랜덤 클래스 무시하고 버튼 찾기

- **정답:** `//button[contains(@class, 'btn-save')]`

## 💡 XPath 작성 꿀팁

1. **계층 구조 최소화:** `/html/body/div/div/table/tr[2]/td[1]` 처럼 긴 경로는 피하세요. 중간에 div 하나만 생겨도 깨집니다.
2. **고유한 텍스트 활용:** ID나 Class가 없다면 화면에 보이는 유니크한 텍스트(`text()`)가 가장 강력한 닻(Anchor)이 됩니다.
3. **인덱스 지양:** `tr[3]` 처럼 숫자를 쓰는 것보다, `tr[td[text()='과장']]` 처럼 내용 기반으로 찾는 것이 데이터 순서가 바뀌어도 안전합니다.
