# AI Usage Log (Question 6)

- Tool Name: Gemini
- Model & Version: Gemini 2.5 Pro

---

## Modulo Implementation

### Cycle 1: Basic Modulo

1. Prompt (verbatim):
> Please write a single failing test for a new method `modulo(self, a, b)` in `Calculator` that tests basic positive integer modulo (e.g., 10 % 3 = 1). Do not write any implementation code yet.

2. Agent Response:
> Here is the failing test case for `modulo`:
> ```python
> def test_modulo(self):
>     calc = Calculator()
>     result = calc.modulo(10, 3)
>     self.assertEqual(result, 1)
> ```

3. Failing Test Output:
`AttributeError: 'Calculator' object has no attribute 'modulo'`（已留存終端機截圖 `screenshot_modulo_red.png`）。

4. Your Review Comments:
測試案例精確測試了正整數取模的基本語意（`10 % 3 = 1`），斷言合理，符合最簡原則。審查通過並先行 Commit。

5. The Change the Agent Made:
在 `Calculator` 類別中新增最簡實作：
```python
def modulo(self, a, b):
    return a % b
```

6. Any Refactoring:
單行運算子回傳，邏輯精練，目前無需重構。

7. Rule Violations & Autonomous Decisions:
無直接違反 TDD 規則；但在引導初期，Agent 傾向直接假定採用 Python 內建取模行為，未主動發問確認運算規格。

### Cycle 2: Modulo by Zero (Edge Case Decision)

1. Prompt (verbatim):
> Please write a single failing test for `modulo` with a divisor of zero (e.g., `calc.modulo(10, 0)`). According to our design decision, it must expect a `ValueError` with "Cannot divide by zero" to remain consistent with `divide`. Do not write any implementation yet.

2. Agent Response:
> Here is the failing test case for modulo by zero:
> ```python
> def test_modulo_by_zero(self):
>     calc = Calculator()
>     with self.assertRaises(ValueError):
>         calc.modulo(10, 0)
> ```

3. Failing Test Output:
`ZeroDivisionError: integer division or modulo by zero`（因為實作尚未加入條件防護，系統丟出原生 ZeroDivisionError 而非預期的 ValueError，測試如期判定失敗；已留存終端機截圖 `screenshot_modulo_zero_red.png`）。

4. Your Review Comments:
測試案例明確驗證了除數為 0 時的例外處理，斷言型別符合先前統一的系統規範。審查通過並先行 Commit。

5. The Change the Agent Made:
在 `Calculator.modulo` 加入防禦性檢查：
```python
def modulo(self, a, b):
    if b == 0:
        raise ValueError("Cannot divide by zero")
    return a % b
```

6. Any Refactoring:
邏輯清晰，維持最精簡條件判斷。

7. Rule Violations & Autonomous Decisions:
None.

---

## Power Implementation

### Cycle 3: Basic Power

1. Prompt (verbatim):
> Please write a single failing test for a new method `power(self, a, b)` in `Calculator` that tests basic positive exponentiation (e.g., 2 ** 3 = 8). Do not write any implementation yet.

2. Agent Response:
> Here is the failing test case for `power`:
> ```python
> def test_power(self):
>     calc = Calculator()
>     result = calc.power(2, 3)
>     self.assertEqual(result, 8)
> ```

3. Failing Test Output:
`AttributeError: 'Calculator' object has no attribute 'power'`（實作尚未提供 `power` 方法，測試如期失敗；已留存終端機截圖 `screenshot_power_red.png`）。

4. Your Review Comments:
測試案例測試了正整數次方運算（2 的 3 次方為 8），斷言明確。審查通過並先行 Commit。

5. The Change the Agent Made:
在 `Calculator` 類別新增最簡實作：
```python
def power(self, a, b):
    return a ** b
```

6. Any Refactoring:
使用 Python 原生次方運算子 `**`，程式碼簡潔，無需重構。

7. Rule Violations & Autonomous Decisions:
None.

### Cycle 4: Power Edge Cases (Zero Base with Negative Exponent)

1. Prompt (verbatim):
> Please write a single failing test for `power` handling zero base with a negative exponent (e.g., `calc.power(0, -2)`). According to our design decision, zero raised to a negative exponent represents division by zero and must raise a `ValueError`. Do not write any implementation yet.

2. Agent Response:
> Here is the failing test case for zero base with a negative exponent:
> ```python
> def test_power_zero_base_negative_exponent(self):
>     calc = Calculator()
>     with self.assertRaises(ValueError):
>         calc.power(0, -2)
> ```

3. Failing Test Output:
`ZeroDivisionError: 0.0 cannot be raised to a negative power`（原生 Python 次方運算拋出 ZeroDivisionError，而非預期的 ValueError；已留存終端機截圖 `screenshot_power_zero_red.png`）。

4. Your Review Comments:
測試案例確認了 0 的負次方屬於無效除以零運算，斷言拋出 ValueError 符合全專案例外處理的一致性。審查通過並先行 Commit。

5. The Change the Agent Made:
在 `Calculator.power` 加入底數為 0 且指數小於 0 的條件防禦：
```python
def power(self, a, b):
    if a == 0 and b < 0:
        raise ValueError("Cannot raise zero to a negative power")
    return a ** b
```

6. Any Refactoring:
邏輯明確，條件覆蓋精確，維持最簡實作。

7. Rule Violations & Autonomous Decisions:
None.