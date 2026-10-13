# TDD Narratives

## Cycle 1: Subtract

- **Red**:
  - 新增測試案例 `test_subtract`，傳入 `5` 與 `3`，預期結果為 `2`。
  - 執行 `python -m unittest CalcTest.py` 得到 `AttributeError: 'Calculator' object has no attribute 'subtract'`。確認在未實作時測試如期失敗。