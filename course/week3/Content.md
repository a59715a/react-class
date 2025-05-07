# 🧮 第三週：進階狀態管理與計算功能

Week 3: Advanced State Management and Calculation Functions

## 📚 課程概述 Course Overview

本週將深入探討 React 的進階狀態管理技巧，學習如何整合多個 useState，並實作複雜的計算功能。我們將從基礎的計算邏輯開始，逐步學習如何處理錯誤情況，並使用 PrimeReact 的進階元件來建立專業的計算機介面。

This week we will explore advanced state management techniques in React, learn how to integrate multiple useState, and implement complex calculation functions. We'll start with basic calculation logic, gradually learn how to handle error cases, and use PrimeReact's advanced components to create a professional calculator interface.

## 📑 章節 Chapters

1. 📝 複雜狀態管理（多個 useState 整合）
   Complex State Management (Multiple useState Integration)
2. ➕ 計算邏輯實作與錯誤處理
   Calculation Logic Implementation and Error Handling
3. 🔄 資料轉換與格式化
   Data Transformation and Formatting
4. 🎯 使用 PrimeReact 進階元件
   Using PrimeReact Advanced Components

## 📝 課程內容 Course Content

### 1. 📝 複雜狀態管理（多個 useState 整合）

Complex State Management (Multiple useState Integration)

#### **多個狀態的整合 Multiple State Integration**

在實際應用中，我們經常需要管理多個相關的狀態。讓我們看看如何有效地整合這些狀態。

In real applications, we often need to manage multiple related states. Let's see how to effectively integrate these states.

```tsx
"use client";
import { useState } from "react";

interface CalculatorState {
  firstNumber: number;
  secondNumber: number;
  operation: string;
  result: number;
  error: string;
}

export default function Calculator() {
  const [state, setState] = useState<CalculatorState>({
    firstNumber: 0,
    secondNumber: 0,
    operation: "+",
    result: 0,
    error: "",
  });

  const handleCalculate = () => {
    try {
      let result = 0;
      switch (state.operation) {
        case "+":
          result = state.firstNumber + state.secondNumber;
          break;
        case "-":
          result = state.firstNumber - state.secondNumber;
          break;
        case "*":
          result = state.firstNumber * state.secondNumber;
          break;
        case "/":
          if (state.secondNumber === 0) {
            throw new Error("除數不能為零");
          }
          result = state.firstNumber / state.secondNumber;
          break;
      }
      setState({ ...state, result, error: "" });
    } catch (error) {
      setState({ ...state, error: error.message });
    }
  };

  return (
    <div>
      <input
        type="number"
        value={state.firstNumber}
        onChange={(e) =>
          setState({ ...state, firstNumber: Number(e.target.value) })
        }
      />
      <select
        value={state.operation}
        onChange={(e) =>
          setState({ ...state, operation: e.target.value })
        }
      >
        <option value="+">+</option>
        <option value="-">-</option>
        <option value="*">*</option>
        <option value="/">/</option>
      </select>
      <input
        type="number"
        value={state.secondNumber}
        onChange={(e) =>
          setState({ ...state, secondNumber: Number(e.target.value) })
        }
      />
      <button onClick={handleCalculate}>計算</button>
      {state.error ? (
        <p style={{ color: "red" }}>{state.error}</p>
      ) : (
        <p>結果: {state.result}</p>
      )}
    </div>
  );
}
```

### 2. ➕ 計算邏輯實作與錯誤處理

Calculation Logic Implementation and Error Handling

#### **基本計算功能 Basic Calculation Functions**

讓我們實作一個具有基本計算功能的計算機。

Let's implement a calculator with basic calculation functions.

```tsx
"use client";
import { useState } from "react";
import { InputNumber } from "primereact/inputnumber";
import { Button } from "primereact/button";
import { Card } from "primereact/card";

export default function AdvancedCalculator() {
  const [display, setDisplay] = useState<string>("0");
  const [memory, setMemory] = useState<number>(0);
  const [operation, setOperation] = useState<string>("");
  const [waitingForOperand, setWaitingForOperand] = useState<boolean>(false);

  const handleDigit = (digit: string) => {
    if (waitingForOperand) {
      setDisplay(digit);
      setWaitingForOperand(false);
    } else {
      setDisplay(display === "0" ? digit : display + digit);
    }
  };

  const handleOperation = (op: string) => {
    const currentValue = parseFloat(display);

    if (operation && !waitingForOperand) {
      const result = calculate(memory, currentValue, operation);
      setDisplay(String(result));
      setMemory(result);
    } else {
      setMemory(currentValue);
    }

    setWaitingForOperand(true);
    setOperation(op);
  };

  const calculate = (a: number, b: number, op: string): number => {
    switch (op) {
      case "+":
        return a + b;
      case "-":
        return a - b;
      case "*":
        return a * b;
      case "/":
        if (b === 0) {
          throw new Error("除數不能為零");
        }
        return a / b;
      default:
        return b;
    }
  };

  return (
    <Card title="進階計算機" className="w-25rem">
      <div className="flex flex-column gap-2">
        <div className="text-2xl font-bold text-right p-2 border-1 border-round">
          {display}
        </div>
        <div className="grid">
          <Button label="7" onClick={() => handleDigit("7")} />
          <Button label="8" onClick={() => handleDigit("8")} />
          <Button label="9" onClick={() => handleDigit("9")} />
          <Button label="+" onClick={() => handleOperation("+")} />
          <Button label="4" onClick={() => handleDigit("4")} />
          <Button label="5" onClick={() => handleDigit("5")} />
          <Button label="6" onClick={() => handleDigit("6")} />
          <Button label="-" onClick={() => handleOperation("-")} />
          <Button label="1" onClick={() => handleDigit("1")} />
          <Button label="2" onClick={() => handleDigit("2")} />
          <Button label="3" onClick={() => handleDigit("3")} />
          <Button label="*" onClick={() => handleOperation("*")} />
          <Button label="0" onClick={() => handleDigit("0")} />
          <Button label="." onClick={() => handleDigit(".")} />
          <Button label="=" onClick={() => handleOperation("=")} />
          <Button label="/" onClick={() => handleOperation("/")} />
        </div>
      </div>
    </Card>
  );
}
```

### 3. 🔄 資料轉換與格式化

Data Transformation and Formatting

#### **數字格式化 Number Formatting**

使用 PrimeReact 的 InputNumber 元件來實現數字格式化。

Use PrimeReact's InputNumber component to implement number formatting.

```tsx
"use client";
import { InputNumber } from "primereact/inputnumber";
import { useState } from "react";

export default function NumberFormatting() {
  const [value, setValue] = useState<number>(0);

  return (
    <div className="flex flex-column gap-2">
      <label htmlFor="currency">貨幣格式</label>
      <InputNumber
        id="currency"
        value={value}
        onValueChange={(e) => setValue(e.value)}
        mode="currency"
        currency="TWD"
        locale="zh-TW"
      />

      <label htmlFor="percent">百分比格式</label>
      <InputNumber
        id="percent"
        value={value}
        onValueChange={(e) => setValue(e.value)}
        mode="decimal"
        minFractionDigits={2}
        maxFractionDigits={2}
        suffix="%"
      />
    </div>
  );
}
```

### 4. 🎯 使用 PrimeReact 進階元件

Using PrimeReact Advanced Components

#### **ButtonGroup 元件 ButtonGroup Component**

ButtonGroup 元件可以將多個按鈕組合在一起。

ButtonGroup component can group multiple buttons together.

```tsx
"use client";
import { Button } from "primereact/button";

export default function ButtonGroupDemo() {
  return (
    <div className="flex flex-column gap-2">
      <div className="flex">
        <Button label="儲存" icon="pi pi-save" />
        <Button label="取消" icon="pi pi-times" severity="secondary" />
        <Button label="刪除" icon="pi pi-trash" severity="danger" />
      </div>

      <div className="flex">
        <Button icon="pi pi-check" className="p-button-success" />
        <Button icon="pi pi-times" className="p-button-danger" />
        <Button icon="pi pi-search" className="p-button-info" />
      </div>
    </div>
  );
}
```

## 🎯 課程重點

Course Highlights

1. **複雜狀態管理** 📝
   - 多個 useState 的整合
   - 狀態之間的關聯性
   - 狀態更新的最佳實踐

2. **計算邏輯** ➕
   - 基本運算功能實作
   - 錯誤處理機制
   - 計算機功能擴展

3. **資料格式化** 🔄
   - 數字格式化
   - 貨幣顯示
   - 百分比轉換

4. **進階元件應用** 🎨
   - ButtonGroup 的使用
   - 元件樣式客製化
   - 事件處理整合

## 📝 課程總結

Course Summary

本週我們深入學習了 React 的進階狀態管理技巧，實作了複雜的計算功能，並學習了如何使用 PrimeReact 的進階元件。通過實作計算機應用，我們掌握了如何整合多個狀態、處理錯誤情況，以及格式化資料。這些技能將幫助我們在後續課程中建立更複雜的應用程式。

This week we delved into advanced state management techniques in React, implemented complex calculation functions, and learned how to use PrimeReact's advanced components. Through implementing a calculator application, we mastered how to integrate multiple states, handle error cases, and format data. These skills will help us build more complex applications in subsequent courses.

## 🔜 下週預告

Next Week Preview

下週我們將學習資料處理與動態渲染，包括資料結構設計、動態列表渲染，以及使用 PrimeReact 的資料展示元件。

Next week, we will learn about data processing and dynamic rendering, including data structure design, dynamic list rendering, and using PrimeReact's data display components.
