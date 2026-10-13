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