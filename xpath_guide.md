# XPath 실전 챌린지 정답 및 해설

- `xpath_workbook.html` 파일에 있는 미션들의 모범 답안입니다.
- XPath는 정답이 하나만 있는 것이 아닙니다. 상황에 따라 더 견고하고 효율적인 방법을 선택하는 것이 중요합니다!

## LEVEL 1. 쇼핑몰 상품 목록

### Mission 1-1: "게이밍 마우스"의 가격 선택

**목표:** 상품명 텍스트를 기준으로 그 상품의 가격 요소를 찾아야 합니다.

- **Best Answer:**
    
    ```
    //h4[text()='게이밍 마우스']/following-sibling::span[@class='price']
    ```
    
    *(설명: h4 태그 중 텍스트가 정확히 '게이밍 마우스'인 것을 찾고, 그 뒤에 나오는 형제 요소 중 class가 price인 span을 찾음)*
    
- **Alternative (contains 활용):**
    
    ```
    //h4[contains(text(), '마우스')]/following-sibling::span[contains(@class, 'price')]
    ```
    

### Mission 1-2: "품절" 상품의 "담기" 버튼 선택

**목표:** 상태(품절) 텍스트를 기준으로 버튼을 찾아야 합니다. DOM 구조상 버튼은 형제 요소일 수도 있고, 부모를 거쳐 내려와야 할 수도 있습니다.

- **Best Answer (형제 관계 이용):**
    
    ```
    //span[text()='품절']/following-sibling::button
    ```
    
- **Alternative (부모 경유):**
    
    ```
    //div[@class='item'][.//span[text()='품절']]//button
    ```
    
    *(설명: 내부에 '품절' span을 가지고 있는 item div를 먼저 찾고, 그 안의 버튼을 찾음. 이 방식이 더 안전할 때가 많습니다.)*
    

## LEVEL 2. 관리자 직원 목록 (테이블)

### Mission 2-1: "이영희"의 "삭제" 버튼

**목표:** 특정 텍스트가 있는 행(Row)을 찾고, 그 행 안의 특정 버튼을 클릭해야 합니다. 웹 자동화에서 가장 많이 쓰이는 패턴입니다.

- **Best Answer:**
    
    ```
    //td[text()='이영희']/parent::tr//button
    ```
    
    *(설명: '이영희' 텍스트가 있는 td를 찾고 -> 부모인 tr로 올라가서 -> 그 tr 안에 있는 button을 찾음)*
    
- **Alternative (한 줄로 쓰기):**
    
    ```
    //tr[td[text()='이영희']]//button
    ```
    
    *(설명: td 텍스트가 '이영희'인 tr을 조건(Predicate)으로 바로 찾음)*
    

## LEVEL 3. 동적 클래스 & 폼

### Mission 3-1: "동의함(Yes)" 라디오 버튼 (Label 텍스트 활용)

**목표:** Input 태그에 식별자가 없을 때, 사람이 읽는 Label 텍스트를 이용해 Input을 찾아야 합니다.

- **Best Answer (Label 안에 Input이 있는 경우):**
    
    ```
    //label[contains(., '동의함')]//input[@type='radio']
    ```
    
    *(설명: `.` 은 현재 노드의 모든 텍스트를 포함합니다. Label 안에 '동의함' 텍스트가 있고 Input이 자식으로 있으므로 이렇게 찾을 수 있습니다.)*
    
- **Alternative (Label 텍스트 형제 찾기):**
    
    ```
    //span[contains(text(), '동의함')]/preceding-sibling::input
    ```
    *(설명: '동의함' span을 찾고, 그 앞(preceding)에 있는 input 형제를 찾음)*
    

### Mission 3-2: 랜덤 클래스 무시하고 "저장" 버튼 찾기

**목표:** `jss-55102` 같은 랜덤 생성 클래스는 매번 바뀌므로 절대 사용하면 안 됩니다. 고정된 부분만 활용하세요.

- **Best Answer (클래스 일부 매칭):**
    
    ```
    //button[contains(@class, 'btn-save')]
    ```
    
    *(설명: 클래스 전체가 아닌 'btn-save'가 포함되어 있는지만 확인)*
    
- **Alternative (텍스트 내용 기반):**
    
    ```
    //button[contains(text(), '저장')]
    ```
    
    *(설명: 버튼에 쓰여진 텍스트를 기준으로 찾음. 가장 직관적임)*
    

## 💡 XPath 작성 꿀팁

1. **계층 구조 최소화:** `/html/body/div/div/table/tr[2]/td[1]` 처럼 긴 경로는 피하세요. 중간에 div 하나만 생겨도 깨집니다.
2. **고유한 텍스트 활용:** ID나 Class가 없다면 화면에 보이는 유니크한 텍스트(`text()`)가 가장 강력한 닻(Anchor)이 됩니다.
3. **인덱스 지양:** `tr[3]` 처럼 숫자를 쓰는 것보다, `tr[td[text()='과장']]` 처럼 내용 기반으로 찾는 것이 데이터 순서가 바뀌어도 안전합니다.
