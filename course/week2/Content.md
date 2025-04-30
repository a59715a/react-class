# 🎯 第二週：React 核心概念與 PrimeReact 元件應用

Week 2: React Core Concepts and PrimeReact Components

## 📚 課程概述 Course Overview

本週將深入探討 React 的核心概念，包括組件設計與 Props 傳遞，並學習使用 PrimeReact 的基礎元件來建立更豐富的用戶界面。我們將從基礎的組件概念開始，逐步學習如何建立可重用的組件，並使用 PrimeReact 的各種元件來增強應用程式的功能與外觀。

This week we will delve into React's core concepts, including component design and Props passing, and learn to use PrimeReact's basic components to create richer user interfaces. We'll start with basic component concepts and gradually learn how to create reusable components, using various PrimeReact components to enhance application functionality and appearance.

## 📑 章節 Chapters

1. 🧩 React 組件概念與 Props 傳遞
   React Component Concepts and Props Passing
2. 🔄 useState 基礎應用
   Basic useState Application
3. 🎨 PrimeReact 基礎元件教學
   PrimeReact Basic Components Tutorial
4. ✍️ 實作練習：會員註冊表單
   Practice: Member Registration Form

## 📝 課程內容 Course Content

### 1. 🧩 React 組件概念與 Props 傳遞

React Component Concepts and Props Passing

#### **組件基礎概念 Basic Component Concepts**

在 React 中，組件是構建用戶界面的基本單位。組件可以是函數或類，它們接收輸入（稱為 props）並返回描述應該在屏幕上顯示的內容的 React 元素。

In React, components are the basic building blocks of user interfaces. Components can be functions or classes, they receive inputs (called props) and return React elements that describe what should appear on the screen.

![1745977511558](image/Content/1745977511558.png)

```tsx
import React from "react";

// 函數組件 Function Component
function Welcome(props: { name: string; age: number }) {
  return (
    <h1>
      Hello, {props.name} {props.age} 歲
    </h1>
  );
}

// 使用組件 Using Component
export default function Home() {
  return (
    <div>
      <Welcome name="小明" age={16} />
      <Welcome name="小華" age={30} />
    </div>
  );
}

```

#### **Props 傳遞與使用 Props Passing and Usage**

Props 是組件之間傳遞數據的主要方式。它們是只讀的，這意味著組件不能修改其 props。

Props are the primary way to pass data between components. They are read-only, meaning a component cannot modify its props.

![1745977551410](image/Content/1745977551410.png)

```tsx
// 定義組件 Define Component
function UserCard({ name, age, isStudent }) {
  return (
    <div className="card">
      <h2>{name}</h2>
      <p>年齡: {age}</p>
      <p>身份: {isStudent ? "學生" : "非學生"}</p>
    </div>
  );
}

// 使用組件 Using Component
export default function Home() {
  return (
    <div>
      <UserCard name="小明" age={20} isStudent={true} />
      <UserCard name="小華" age={25} isStudent={false} />
    </div>
  );
}
```

### 2. 🔄 useState 基礎應用

Basic useState Application

#### **狀態管理基礎 Basic State Management**

useState 是 React 的一個 Hook，它允許我們在函數組件中添加狀態。
將需要即時顯示、重新渲染的狀態變數，放在 useState 中。

useState is a Hook in React that allows us to add state to function components.
Place state variables that need to be displayed and re-rendered in real-time in useState.

#### **useState 基本語法 Basic Syntax**

![1745978006634](image/Content/1745978006634.png)

```tsx
// useState 基本語法 Basic Syntax
"use client";
import { useState } from "react";
import { Button } from "primereact/button";

export default function Counter() {
    const [count, setCount] = useState(0);

    return (
        <div>
            <p>計數: {count}</p>
            <Button onClick={() => setCount(count + 1)}>增加</Button>
            <Button onClick={() => setCount(count - 1)}>減少</Button>
        </div>
    );
}

```

#### **多個狀態管理 Multiple State Management**

我們可以在一個組件中使用多個 useState。

We can use multiple useState in one component.

```tsx
"use client";
import { useState } from "react";

export default function UserForm() {
  const [name, setName] = useState("");
  const [age, setAge] = useState(0);
  const [isStudent, setIsStudent] = useState(false);

  return (
    <div>
      <input
        type="text"
        value={name}
        onChange={(e) => setName(e.target.value)}
        placeholder="姓名"
      />
      <input
        type="number"
        value={age}
        onChange={(e) => setAge(Number(e.target.value))}
        placeholder="年齡"
      />
      <input
        type="checkbox"
        checked={isStudent}
        onChange={(e) => setIsStudent(e.target.checked)}
      />
      <label>是否為學生</label>
    </div>
  );
}
```

### 3. 🎨 PrimeReact 基礎元件教學

PrimeReact Basic Components Tutorial

#### **Card 元件 Card Component**

Card 元件用於展示內容，通常包含標題、內容和頁尾。

Card component is used to display content, usually containing a title, content, and footer.

![1745994429931](image/Content/1745994429931.png)

```tsx
"use client";
import { Card } from "primereact/card";
import { Image } from 'primereact/image';
import { Button } from 'primereact/button';

export default function ProductCard() {
    return (
        <Card
            title="商品名稱"
            subTitle="商品描述"
            style={{ width: "25rem", marginBottom: "2em" }}
        >
            <p className="m-0">
                這是一個商品卡片，可以用來展示商品資訊。
            </p>
            <Image src="https://png.pngtree.com/element_our/20190530/ourlarge/pngtree-stacked-creative-book-illustration-image_1245638.jpg"
                alt="商品圖片" width="200" height="200" />
            <p className="text-2xl font-bold">100 元</p>
            <Button label="購買" />
        </Card>
    );
}

```

#### **Button 元件 Button Component**

Button 元件提供多種樣式和功能。

Button component provides various styles and functions.

![1745994713730](image/Content/1745994713730.png)

```tsx
"use client";
import { Button } from "primereact/button";

export default function ButtonDemo() {
  return (
    <div>
      <Button label="主要按鈕" />
      <Button label="次要按鈕" severity="secondary" />
      <Button label="成功按鈕" severity="success" />
      <Button label="警告按鈕" severity="warning" />
      <Button label="危險按鈕" severity="danger" />
    </div>
  );
}
```

#### **InputText 元件 InputText Component**

InputText 元件用於文字輸入。

InputText component is used for text input.

![1746022709273](image/Content/1746022709273.png)

```tsx
"use client";
import { InputText } from "primereact/inputtext";
import { useState } from "react";

export default function InputDemo() {
  const [value, setValue] = useState("");

  return (
    <div>
      <InputText
        value={value}
        onChange={(e) => setValue(e.target.value)}
        placeholder="請輸入文字"
      />
    </div>
  );
}
```

#### **RadioButton 元件 RadioButton Component**

RadioButton 元件用於單選功能。

RadioButton component is used for single selection.

![1746022998477](image/Content/1746022998477.png)

```tsx
"use client";
import { RadioButton } from "primereact/radiobutton";
import { useState } from "react";
export default function RadioButtonDemo() {
    const [value, setValue] = useState("");
    return (
        <>
            <div className="flex flex-row gap-0 items-center">
                <RadioButton name="gender" checked={value === "male"} value="male" onChange={(e) => setValue(e.value)} />
                <label htmlFor="male">男</label>
                <RadioButton name="gender" checked={value === "female"} value="female" onChange={(e) => setValue(e.value)} />
                <label htmlFor="female">女</label>
            </div>
            <p>選擇的值: {value}</p>
        </>
    );
}

```

#### **Checkbox 元件 Checkbox Component**

Checkbox 元件用於多選功能。

Checkbox component is used for multiple selection.


![1746024550318](image/Content/1746024550318.png)

```tsx
// Checkbox 元件 Checkbox Component
"use client";
import { Checkbox } from "primereact/checkbox";
import { useState } from "react";

export default function CheckboxDemo() {
    const [selections, setSelections] = useState<string[]>([]);
    return (
        <>
            <div className="flex flex-row gap-0 items-center">
                <Checkbox
                    value="reading"
                    checked={selections.includes("reading")}
                    onChange={(e) => {
                        if (e.checked) {
                            // 勾選的情況 將選項加入陣列 if e.checked is true , add the value to the array
                            setSelections([...selections, e.value]);
                        } else {
                            // 取消勾選的情況 將選項從陣列中移除 if e.checked is false , remove the value from the array
                            setSelections(selections.filter(item => item !== e.value));
                        }
                    }}
                />
                <label htmlFor="reading">閱讀</label>
                <Checkbox
                    value="writing"
                    checked={selections.includes("writing")}
                    onChange={(e) => {
                        if (e.checked) {
                            // 勾選的情況 將選項加入陣列 if e.checked is true , add the value to the array
                            setSelections([...selections, e.value]);
                        } else {
                            // 取消勾選的情況 將選項從陣列中移除 if e.checked is false , remove the value from the array
                            setSelections(selections.filter(item => item !== e.value));
                        }
                    }}
                />
                <label htmlFor="writing">寫作</label>
                <Checkbox
                    value="drawing"
                    checked={selections.includes("drawing")}
                    onChange={(e) => {
                        if (e.checked) {
                            // 勾選的情況 將選項加入陣列 if e.checked is true , add the value to the array
                            setSelections([...selections, e.value]);
                        } else {
                            // 取消勾選的情況 將選項從陣列中移除 if e.checked is false , remove the value from the array
                            setSelections(selections.filter(item => item !== e.value));
                        }
                    }}
                />
                <label htmlFor="drawing">繪畫</label>
            </div>
            <p>選擇的值: {selections.join(", ")}</p>
        </>
    );
}

```

### 4. ✍️ 實作練習：會員註冊表單

Practice: Member Registration Form

#### **練習題目 Practice Tasks**

1. 📦 使用 Card 元件建立會員註冊表單的容器
2. ✏️ 使用 InputText 元件建立姓名、電子郵件和密碼輸入欄位
3. 🔘 使用 RadioButton 元件建立性別選擇
4. ✅ 使用 Checkbox 元件建立興趣選擇
5. 🎯 使用 Button 元件建立提交按鈕
6. 🔄 使用 useState 管理表單狀態
   ![1746025554139](image/Content/1746025554139.png)

#### **提示 Hints**

```tsx
    // 表單狀態
    const [formData, setFormData] = useState<FormData>({
        name: '',
        email: '',
        password: '',
        gender: '',
        interests: []
    });


    // 處理表單提交
    const handleSubmit = (e: React.FormEvent<HTMLFormElement>) => {
        e.preventDefault();
        const formDataString =
            "姓名: " + formData.name + "\n" +
            "電子郵件: " + formData.email + "\n" +
            "密碼: " + formData.password + "\n" +
            "性別: " + formData.gender + "\n" +
            "興趣: " + formData.interests.join(", ");
        alert('表單資料: \n' + formDataString);
    };



                    <div className="flex flex-col gap-2">
                        <label htmlFor="name">姓名</label>
                        <InputText
                            id="name"
                            value={formData.name}
                            onChange={(e) => setFormData({ ...formData, name: e.target.value })}
                        />
                    </div>




                    <div className="flex flex-col gap-2">
                        <label htmlFor="password">密碼</label>
                        <InputText
                            id="password"
                            type="password"
                            value={formData.password}
                            onChange={(e) => setFormData({ ...formData, password: e.target.value })}
                        />
                    </div>

                            <div className="flex items-center">
                                <RadioButton
                                    inputId="female"
                                    name="gender"
                                    value="female"
                                    checked={formData.gender === 'female'}
                                    onChange={(e) => setFormData({ ...formData, gender: e.value })}
                                />
                                <label htmlFor="female" className="ml-2">女性</label>
                            </div>


                            {/* reading */}
                            <div className="flex items-center">
                                <Checkbox inputId="reading" name="interests" value="reading"
                                    checked={formData.interests.includes("reading")}
                                    onChange={(e) => {
                                        if (e.checked) {
                                            // 勾選的情況 將選項加入陣列 if e.checked is true , add the value to the array
                                            setFormData({ ...formData, interests: [...formData.interests, e.value] });
                                        } else {
                                            // 取消勾選的情況 將選項從陣列中移除 if e.checked is false , remove the value from the array
                                            setFormData({ ...formData, interests: formData.interests.filter(item => item !== e.value) });
                                        }
                                    }}
                                />
                                <label htmlFor="reading" className="ml-2">reading</label>
                            </div>

```

## 🎯 課程重點

Course Highlights

1. **React 組件概念** 🧩

   - 組件的定義與使用
   - Props 的傳遞與接收
   - 組件的可重用性
2. **狀態管理** 🔄

   - useState Hook 的使用
   - 多個狀態的管理
   - 狀態更新與渲染
3. **PrimeReact 元件** 🎨

   - Card 元件的應用
   - Button 元件的樣式與事件
   - InputText 元件的使用
   - 其他基礎元件的介紹
4. **實作練習** ✅

   - 會員註冊表單的建立
   - 表單狀態的管理
   - 元件的整合應用

## 📝 課程總結

Course Summary

本週我們學習了 React 的核心概念，包括組件設計和 Props 傳遞，並深入了解了 useState Hook 的使用。同時，我們也學習了 PrimeReact 的基礎元件，並通過實作會員註冊表單來整合這些知識。這些基礎知識將幫助我們在後續課程中建立更複雜的應用程式。

This week we learned React's core concepts, including component design and Props passing, and gained a deeper understanding of the useState Hook. We also learned about PrimeReact's basic components and integrated this knowledge by implementing a member registration form. These foundational concepts will help us build more complex applications in subsequent courses.

## 🔜 下週預告

Next Week Preview

下週我們將學習進階狀態管理與計算功能，包括多個 useState 的整合、計算邏輯的實作，以及使用 PrimeReact 的進階元件。

Next week, we will learn about advanced state management and calculation functions, including the integration of multiple useState, implementation of calculation logic, and the use of PrimeReact's advanced components.
