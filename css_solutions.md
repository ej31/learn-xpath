# CSS Selector 실전 챌린지 정답 및 해설

- css_workbook.html 파일의 미션에 대한 모범 답안입니다.

- CSS 선택자는 HTML 구조에 따라 다양한 방식으로 작성할 수 있으며 아래 답안은 가장 효율적이고 일반적인 방법들입니다.

## LEVEL 1. 메뉴 네비게이션

### Mission 1-1: 'Active' 상태인 메뉴 아이템

**목표:** 클래스 이름이 공백으로 구분된 경우(`menu-item active`)를 선택하는 방법입니다.

- **Best Answer:**
    
    ```
    .menu-item.active
    ```
    
    *(설명: 두 클래스를 공백 없이 붙여 쓰면 AND 조건이 됩니다. `menu-item`이면서 동시에 `active` 클래스를 가진 요소를 찾습니다.)*
    
- **Alternative:**
    
    ```
    li.active
    ```
    

### Mission 1-2: 드롭다운 내부의 모든 링크

**목표:** 특정 부모 요소 아래에 있는 모든 자손 요소를 선택합니다.

- **Best Answer:**
    
    ```
    #dropdown a
    
    ```
    
    *(설명: 공백(Space)은 '자손 결합자'입니다. ID가 dropdown인 요소 하위의 모든 `a` 태그를 선택합니다.)*
    
- **Alternative (직계 자식이 아닌 경우도 포함):**
    
    ```
    .menu-item div a
    
    ```
    

## LEVEL 2. 회원가입 폼

### Mission 2-1: 필수 입력 이메일창

**목표:** HTML 속성(Attribute)을 기반으로 요소를 선택합니다.

- **Best Answer:**
    
    ```
    input[type="email"][required]
    ```
    
    *(설명: 속성 선택자 `[]`를 연달아 사용하여 조건을 추가할 수 있습니다. 타입이 email이고 required 속성이 있는 input을 찾습니다.)*
    
- **Alternative:**
    
    ```
    #u-email
    ```
    
    *(설명: ID가 있다면 ID를 쓰는 것이 가장 빠르고 정확하지만, 문제의 의도인 속성 선택자 연습을 위해 위 방법을 추천합니다.)*
    

### Mission 2-2: 라벨 바로 다음 입력창

**목표:** 형제 관계, 특히 바로 뒤에 오는 요소를 선택합니다.

- **Best Answer:**
    
    ```
    label[for="u-pw"] + input
    ```
    
    *(설명: `+`는 '인접 형제 결합자'입니다. 라벨 바로 다음에 나오는 input 태그 하나만 선택합니다.)*
    

## LEVEL 3. 상품 목록 관리

### Mission 3-1: 세 번째 상품 (Item 3)

**목표:** 요소의 순서를 기반으로 선택합니다.

- **Best Answer:**
    
    ```
    #product-list li:nth-child(3)
    
    ```
    
    *(설명: `:nth-child(n)`은 부모의 n번째 자식을 선택합니다. 1부터 시작합니다.)*
    

### Mission 3-2: 품절이 아닌(구매 가능한) 버튼

**목표:** 부정 가상 클래스(`:not`)를 사용하여 특정 요소를 제외합니다.

- **Best Answer:**
    
    ```
    button:not(:disabled)
    ```
    
    *(설명: `:disabled` 상태가 아닌 버튼만 선택합니다. 가장 깔끔한 방법입니다.)*
    
- **Alternative (클래스 기반):**
    
    ```
    button:not(.sold-out)
    ```
    
    *(설명: `sold-out` 클래스가 없는 버튼을 선택합니다.)*
    

## LEVEL 4. 파일 탐색기 (계층 구조 심화)

### Mission 4-1: 직계 자식 파일 선택

**목표:** 중첩된 구조에서 '직계 자식'만 선택하고 '자손(손자)'은 제외합니다.

- **Best Answer:**
    
    ```
    #explorer > .folder > .file
    ```
    
    *(설명: `>`는 직계 자식 결합자입니다. `#explorer` 바로 아래 `.folder`, 그 바로 아래 `.file`만 선택하며, 더 깊이 있는 `.file`은 선택하지 않습니다.)*
    
    *주의: `#explorer .file` 처럼 공백을 쓰면 모든 파일이 선택되므로 오답입니다.*
    

### Mission 4-2: 기준 파일 이후의 모든 형제

**목표:** 특정 요소 뒤에 나오는 같은 레벨의 형제들을 선택합니다.

- **Best Answer:**
    
    ```
    .file.active ~ .file
    ```
    
    *(설명: `~`는 일반 형제 결합자입니다. `.active` 클래스를 가진 파일 **뒤에 나오는** 모든 `.file` 형제들을 선택합니다.)*
    

## LEVEL 5. 고급 설정 패널

### Mission 5-1: 선택된 라디오 버튼의 라벨

**목표:** 사용자의 인터랙션(체크 상태)에 따라 스타일을 다르게 줄 때 자주 쓰이는 패턴입니다.

- **Best Answer:**
    
    ```
    input:checked + label
    ```
    
    *(설명: `:checked` 가상 클래스로 체크된 input을 찾고, `+` 결합자로 바로 뒤에 있는 label을 선택합니다.)*
    

### Mission 5-2: 태그 타입 기반 순서 (nth-of-type)

**목표:** 중간에 다른 태그가 섞여 있을 때 순서를 정확히 세는 방법입니다.

- **Best Answer:**
    
    ```
    article p:nth-of-type(2)
    ```
    
    *(설명: `:nth-child(2)`를 쓰면 두 번째 자식 요소(여기서는 `span.published`)가 선택되거나, `p`가 아니어서 선택되지 않을 수 있습니다. `:nth-of-type`은 형제 요소들 중 `p` 태그만 따로 세어서 두 번째를 찾습니다.)*