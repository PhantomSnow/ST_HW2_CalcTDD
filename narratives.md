# TDD Narratives

## Cycle 1: Subtract

- **Red**:
  - 新增測試案例 `test_subtract`，傳入 `5` 與 `3`，預期結果為 `2`。
  - 執行 `python -m unittest CalcTest.py` 得到 `AttributeError: 'Calculator' object has no attribute 'subtract'`。確認在未實作時測試如期失敗。
  - **Green**:
  - 在 `Calculator` 實作 `subtract(self, a, b)` 並回傳 `a - b`。
  - 執行 `python -m unittest CalcTest.py`，2 項測試全數通過（`OK`）。
- **Refactor**:
  - 代碼簡潔且符合單一職責原則，現階段無冗餘邏輯，維持原狀。

## Cycle 2: Multiply

- **Red**:
  - 新增測試案例 `test_multiply`，傳入運算元 `3` 與 `4`，預期回傳值為 `12`。
  - 執行 `python -m unittest CalcTest.py` 得到 `AttributeError: 'Calculator' object has no attribute 'multiply'`，確認在實作代碼存在前測試如期失敗。
  - **Green**:
  - 在 `Calculator` 實作 `multiply(self, a, b)` 並回傳 `a * b`。
  - 執行 `python -m unittest CalcTest.py`，3 項測試全數通過（`OK`）。
- **Refactor**:
  - 運算邏輯清晰，程式碼符合單一職責，無多餘代碼需要抽取。

## Cycle 3: Divide (Normal Cases & Return Type Decision)

- **Red**:
  - 新增測試案例 `test_divide`，輸入 `5` 與 `2`，預期回傳值為 `2.5`。
  - **設計決策 (Design Decision)**：依作業規範在測試中先敲定回傳型別，本實作選擇回傳浮點數（float），以保留除法的精確小數結果而非整數截斷。
  - 執行 `python -m unittest CalcTest.py` 得到 `AttributeError: 'Calculator' object has no attribute 'divide'`，確認測試在實作前如期失敗。
  - 新增測試案例 `test_divide_by_zero`，傳入運算元 `5` 與 `0`，預期捕捉到 `ValueError` 例外。
  - **設計決策 (Design Decision)**：依作業規範在實作前明確定義邊界條件。當除數為 0 時，決定拋出具語意化的 `ValueError("Cannot divide by zero")`，而非讓系統直接噴出 Python 預設的 `ZeroDivisionError`，以符合計算機領域對無效輸入的例外定義。
  - 執行結果：若 `divide` 僅有 `return a / b`，執行 `python -m unittest CalcTest.py` 會拋出 `ZeroDivisionError` 而非預期的 `ValueError`，導致 `assertRaises(ValueError)` 判定失敗（Red）。
