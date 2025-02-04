## 기능 분석

### 입력

- 공통 예외 처리

  - 숫자가 아닐 경우 예외 처리한다.
  - 공백일 경우 예외 처리한다.

- 로또 구입 금액을 입력받는다.

  - 1000원 단위로 입력받는다.
  - 1000원으로 나누어 떨어지지 않을 경우 예외 처리한다.

- 당첨 번호를 입력 받는다.

  - 쉼표(,)로 구분한다.
  - 입력된 번호가 6개가 아닐 경우 예외 처리한다.
  - 중복된 번호가 입력되지 않도록 예외 처리한다.
  - 1~45 사이의 숫자가 아닐 경우 예외 처리한다.

- 보너스 번호를 입력 받는다.

  - 1~45 사이의 숫자가 아닐 경우 예외 처리한다.
  - 당첨 번호와 중복되지 않도록 예외 처리한다.

### 로또 계산

- 구입 금액에 따른 로또 번호 목록을 생성한다.

  - 중복되지 않은 6개의 번호를 생성한다.
  - 1~45 사이의 숫자를 생성한다.
  - 생성된 번호를 오름차순으로 정렬한다.

- 로또 번호와 당첨 번호를 비교하여 등수를 구한다.

  - 보너스 번호를 제외한 6개의 번호가 일치할 경우 1등이다.
  - 보너스 번호를 포함하여 6개의 번호가 일치할 경우 2등이다.
  - 5개, 4개, 3개의 번호가 일치할 경우 3등, 4등, 5등이다.

- 수익률을 계산한다.

  - 구입 금액을 100%로 두고 당첨 금액을 구한다.
  - 당첨 금액을 구입 금액으로 나누어 수익률을 구한다.
  - 수익률은 소수점 첫째 자리까지 표현한다. (ex. 62.5%), 계산식: `parseFloat((당첨금액 / 구입금액) \* 100).toFixed(1)`

### 출력

- 구입 금액에 따른 로또 번호 목록을 출력한다.

  - `[1, 2, 3, 4, 5, 6]\n` 형식으로 출력한다.

- 당첨 통계를 출력한다.

  - 다음과 같은 형식으로 출력한다.

  ```text
  당첨 통계
  ---
  3개 일치 (5,000원)- 1개
  4개 일치 (50,000원)- 0개
  5개 일치 (1,500,000원)- 0개
  5개 일치, 보너스 볼 일치(30,000,000원)- 0개
  6개 일치 (2,000,000,000원)- 0개
  ```

- 수익률을 출력한다.
  - `총 수익률은 62.5%입니다.` 형식으로 출력한다.

## 세부 구현

### Lotto class

- 로또 번호를 관리하는 클래스
- 로또 번호를 입력받아 번호에 대한 유효성 검사를 수행한다.
  - 1~45 사이의 숫자인지 검사한다.
  - 중복된 번호가 입력되지 않도록 검사한다.
  - 입력된 숫자의 개수가 6개인지 검사한다.

### Model - UserLottoModel class

- 로또 구입 금액, 구매한 로또 번호, 당첨 결과를 관리하는 클래스
- 구입 금액을 입력받아 구입 금액에 따른 로또 번호 목록을 생성한다.
  - 구입 금액에 대한 유효성 검사를 수행한다.
    - 1000원 단위로 나누어 떨어지는지 검사한다.
  - 로또 번호 생성시 `Lotto` 생성자 함수를 통해 로또 번호를 생성한다.
- 로또 번호 목록에 대한 당첨 결과를 계산한다.
  - 입력 받은 일치 번호 개수에 따른 당첨 결과를 계산한다.

### Model - LottoManageModel class

- 당첨 번호, 보너스 번호를 관리하는 클래스
- 당첨 번호를 입력받아 관리한다.

  - `Lotto` 생성자 함수를 통해 로또 번호를 생성한다.

- 보너스 번호를 입력받아 관리한다.
  - 보너스 번호에 대한 유효성 검사를 수행한다.
    - 당첨 번호와 중복되지 않는지 검사한다.
    - 1~45 사이의 숫자인지 검사한다.
- 로또 번호를 입력받아 당첨 번호, 보너스 번호와 비교하여 일치하는 번호의 개수를 반환한다.

### View - InputView class

- 사용자 입력을 관리하는 클래스
- 입력에 대한 유효성 검사를 수행한다.

  - 숫자가 아닌지 검사한다.
  - 공백인지 검사한다.

- 구입 금액을 입력받는다.

  <details>
    <summary>입력</summary>

  ```text
  구입금액을 입력해 주세요.
  3000
  ```

  </details>

- 당첨 번호를 입력받는다.

  <details>
    <summary>입력</summary>

  ```text
  당첨 번호를 입력해 주세요.
  1,2,3,4,5,6
  ```

    </details>

- 보너스 번호를 입력받는다.
  <details>
    <summary>입력</summary>

  ```text
  보너스 번호를 입력해 주세요.
  7
  ```

    </details>

### View - OutputView class

- 출력을 관리하는 클래스
- 로또 번호 목록을 출력한다.
  <details>
    <summary>출력</summary>

  ```text
  3개를 구매했습니다.
  [1, 2, 14, 15, 20, 44]
  [5, 9, 11, 26, 33, 42]
  [4, 23, 24, 29, 33, 38]
  ```

  </details>

- 당첨 통계를 출력한다.
  <details>
    <summary>출력</summary>

  ```text
  당첨 통계
  ---
  3개 일치 (5,000원) - 0개
  4개 일치 (50,000원) - 0개
  5개 일치 (1,500,000원) - 0개
  5개 일치, 보너스 볼 일치 (30,000,000원) - 0개
  6개 일치 (2,000,000,000원) - 0개
  ```

  </details>

- 수익률을 출력한다.
  <details>
    <summary>출력</summary>

  ```text
  총 수익률은 62.5%입니다.
  ```

  </details>
