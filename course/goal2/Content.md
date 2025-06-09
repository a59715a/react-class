# 🛒 當我的畫面畫好 測試資料也玩膩了怎麼辦？

## 🌐 串接WebApi

### 🔍 熟悉api 內容

#### 📥 下載 Postman

下載 Postman [https://www.postman.com/](https://www.postman.com/)
![1749359472995](image/Content/1749359472995.png)
![1749359630831](image/Content/1749359630831.png)

#### 🔧 安裝Postman

若沒有要登入帳號 可以選擇最下面的 `Continue without an account`
![1749359860442](image/Content/1749359860442.png)
![1749360031126](image/Content/1749360031126.png)

#### 🧪 測試api

先測試一個簡單的api
 查詢所有使用者
 請先點 Import 並將以下cUrl 貼到輸入框

```bash
  curl --location 'https://ottfwogpkzhitdekrnkq.supabase.co/rest/v1/UsersTbl?select=*' \
--header 'apikey: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im90dGZ3b2dwa3poaXRkZWtybmtxIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NDkxMzQxMzMsImV4cCI6MjA2NDcxMDEzM30.56I4EssOz4RGnPcKeHl-vLI0D_QYEPbuKdzxWjMYmXU'
```

 ![1749360220038](image/Content/1749360220038.png)
  ![1749360366587](image/Content/1749360366587.png)
  按下 `Send` 按鈕  可以看到下方 Response 的內容
  ![1749361035477](image/Content/1749361035477.png)

這是一個簡單的api 測試，目的是測試我們的api 是否能夠正常運作、回傳我們預期的資料
此api 的內容是 查詢所有使用者 會以 json 格式回傳 一個物件陣列

#### 📊 測試api 回傳的資料

```
[
    {
        "id": 2,
        "created_at": "2025-06-05T15:24:08.837024+00:00",
        "name": "測試名字",
        "email": "test@test.com",
        "password": "QQ",
        "gender": "male"
    },
    {
        "id": 4,
        "created_at": "2025-06-08T05:36:24.399997+00:00",
        "name": "測試阿通",
        "email": "test2@test.com",
        "password": "QQ2",
        "gender": "female"
    }
]
```

#### ✅ 練習

1. 🔧 安裝 Postman
2. 🧪 測試 api
3. 🧠 理解 api 回傳的 json 資料

### 📝 串接註冊 API

#### 🔰 功能說明

將原本註冊功能的假資料回傳替換成真實的API串接。這個改動讓我們的應用程式能夠與後端服務進行互動，實現真正的資料存儲功能。
![1749366712446](image/Content/1749366712446.png)
![1749366731979](image/Content/1749366731979.png)

#### 📋 API curl

```
curl --location 'https://ottfwogpkzhitdekrnkq.supabase.co/rest/v1/UsersTbl' \
--header 'apikey: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im90dGZ3b2dwa3poaXRkZWtybmtxIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NDkxMzQxMzMsImV4cCI6MjA2NDcxMDEzM30.56I4EssOz4RGnPcKeHl-vLI0D_QYEPbuKdzxWjMYmXU' \
--header 'Content-Type: application/json' \
--header 'Prefer: return=minimal' \
--data-raw '{
    "name": "測試名字",
    "email": "test@test.com",
    "password": "QQ",
    "gender": "male"
}'

```

#### 🔑 技術重點

- **⏱️ 非同步處理**：使用 `async/await` 處理API請求
- **🛡️ 錯誤處理**：使用 `try/catch` 捕獲並處理可能的錯誤
- **🌐 HTTP請求**：使用 `fetch` API發送POST請求

> 💡 **提示**：如果您不熟悉 async/await，可以參考 [chatGPT - 什麼是 async](https://chatgpt.com/share/68452bee-5b88-8003-ae6d-2ca1dcc66125) 了解更多。

#### 📄 完整程式碼

```typescript
"use client";

import { useState } from "react";
import { Card } from "primereact/card";
import { InputText } from "primereact/inputtext";
import { RadioButton } from "primereact/radiobutton";
import { Button } from "primereact/button";

interface FormDataIF {
    name: string; // 姓名
    email: string; // 電子郵件
    password: string; // 密碼
    gender: string; // 性別
}

const authService = {
    register: async (formData: FormDataIF) => {
        try {
            // 串接後端API
            const response = await fetch("https://ottfwogpkzhitdekrnkq.supabase.co/rest/v1/UsersTbl", {
                // 使用 POST 方法
                method: "POST",
                // 設定 headers
                headers: {
                    // 設定 apikey
                    'apikey': 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im90dGZ3b2dwa3poaXRkZWtybmtxIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NDkxMzQxMzMsImV4cCI6MjA2NDcxMDEzM30.56I4EssOz4RGnPcKeHl-vLI0D_QYEPbuKdzxWjMYmXU',
                    // 設定 Content-Type
                    'Content-Type': 'application/json',
                    // 設定 Prefer (回傳的內容不要太多廢話)
                    'Prefer': 'return=minimal'
                },
                // 設定 body
                body: JSON.stringify(formData)
            });
            // 如果 API 請求失敗，則拋出錯誤
            if (!response.ok) {
                throw new Error(`API請求失敗: ${response.status}`);
            }
            // 如果 API 請求成功，則回傳 true
            return true;
        } catch (error) {
            // 如果 API 請求失敗，則拋出錯誤
            console.error('註冊錯誤:', error);
            return false;
        }
    }
}

export default function MemberForm() {
    // 表單狀態
    const [formData, setFormData] = useState<FormDataIF>({
        name: "",
        email: "",
        password: "",
        gender: "",
    });


    // 處理表單提交
    const handleSubmit = async (e: React.FormEvent<HTMLFormElement>) => {
        e.preventDefault();

        try {
            const success = await authService.register(formData);

            if (success) {
                const formDataString =
                    "姓名: " +
                    formData.name +
                    "\n" +
                    "電子郵件: " +
                    formData.email +
                    "\n" +
                    "密碼: " +
                    formData.password +
                    "\n" +
                    "性別: " +
                    formData.gender +
                    "\n";
                alert("註冊成功! \n表單資料: \n" + formDataString);
            } else {
                alert("註冊失敗，請稍後再試");
            }
        } catch (error) {
            console.error('提交表單錯誤:', error);
            alert("發生錯誤，請稍後再試");
        }
    };

    return (
        // css flex: 使用 flexbox 來排版
        // justify-center: 水平置中
        // items-center: 垂直置中
        <div className="flex justify-center items-center h-full">
            <Card title="會員註冊" className="w-full max-w-md">
                <form onSubmit={handleSubmit} className="flex flex-col gap-4">
                    <div className="flex flex-col gap-2">
                        <label htmlFor="name">
                            姓名
                        </label>
                        <InputText
                            id="name"
                            value={formData.name}
                            onChange={(e) =>
                                setFormData({ ...formData, name: e.target.value })
                            }
                        />
                    </div>

                    <div className="flex flex-col gap-2">
                        <label htmlFor="email">電子郵件</label>
                        <InputText
                            id="email"
                            type="email"
                            value={formData.email}
                            onChange={(e) =>
                                setFormData({ ...formData, email: e.target.value })
                            }
                        />
                    </div>

                    <div className="flex flex-col gap-2">
                        <label htmlFor="password">密碼</label>
                        <InputText
                            id="password"
                            type="password"
                            value={formData.password}
                            onChange={(e) =>
                                setFormData({ ...formData, password: e.target.value })
                            }
                        />
                    </div>

                    <div className="flex flex-col gap-2">
                        <label>性別</label>
                        <div className="flex gap-4">
                            <div className="flex items-center">
                                <RadioButton
                                    inputId="male"
                                    name="gender"
                                    value="male"
                                    checked={formData.gender === "male"}
                                    onChange={(e) =>
                                        setFormData({ ...formData, gender: e.value })
                                    }
                                />
                                <label htmlFor="male" className="ml-2">
                                    男性
                                </label>
                            </div>
                            <div className="flex items-center">
                                <RadioButton
                                    inputId="female"
                                    name="gender"
                                    value="female"
                                    checked={formData.gender === "female"}
                                    onChange={(e) =>
                                        setFormData({ ...formData, gender: e.value })
                                    }
                                />
                                <label htmlFor="female" className="ml-2">
                                    女性
                                </label>
                            </div>
                        </div>
                    </div>
                    <Button type="submit" label="註冊" className="mt-4" />
                </form>
            </Card>
        </div>
    );
}

```

#### 📝 實作步驟

1. 🏗️ 建立 `authService` 物件，包含 `register` 方法
2. 🌐 使用 `fetch` API 發送 POST 請求到 Supabase 後端
3. ⚙️ 設定適當的request header和request body
4. 🛡️ 處理回應和可能的錯誤
5. ⏱️ 在表單提交處理函數中使用 `async/await` 調用 API

#### ✅ 練習

1. 🧪 用Postman 測試註冊api
2. 📝 完成註冊功能的 API 串接

### 🔐 串接登入 API

#### 🔰 功能說明

將原本登入功能的假資料回傳替換成真實的API串接。這個改動讓我們的應用程式能夠與後端服務進行互動，實現真正的資料存儲功能。

#### 📋 API curl

```bash
curl --location --request GET 'https://ottfwogpkzhitdekrnkq.supabase.co/rest/v1/UsersTbl?select=*&email=eq.test%40test.com' \
--header 'apikey: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im90dGZ3b2dwa3poaXRkZWtybmtxIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NDkxMzQxMzMsImV4cCI6MjA2NDcxMDEzM30.56I4EssOz4RGnPcKeHl-vLI0D_QYEPbuKdzxWjMYmXU' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'select=*' \
--data-urlencode 'email=eq.test@test.com'
```

![1749372412895](image/Content/1749372412895.png)

#### 📄 完整程式碼

```ts

"use client";
import { useState } from "react";
import { Card } from "primereact/card";
import { InputText } from "primereact/inputtext";
import { Checkbox } from "primereact/checkbox";
import { Button } from "primereact/button";

// 宣告一個 FormDataIF 介面，裡面有 email, password, rememberMe 屬性 用於存放 表單資料
interface FormDataIF {
    email: string; // 帳號
    password: string; // 密碼
    rememberMe: boolean; // 記住我
}
// 宣告一個 UserInfoIF 介面，裡面有 name, email, password, gender 屬性 用於顯示 使用者資訊
interface UserInfoIF {
    name: string; // 姓名
    email: string; // 電子郵件
    password: string; // 密碼
    gender: string; // 性別
}

// 宣告一個 service 物件，裡面有 getUserInfo 方法  若是有串後端API 則在此處串接
const authService = {
    login: async (email: string, password: string) => {
        try {
            // 串接後端API
            const response = await fetch(
                // https://ottfwogpkzhitdekrnkq.supabase.co/rest/v1/UsersTbl 是後端API的URL
                // ?select=*&email=eq.${encodeURIComponent(email)} 是後端API的參數
                // encodeURIComponent(email) 是將 email 進行編碼
                `https://ottfwogpkzhitdekrnkq.supabase.co/rest/v1/UsersTbl?select=*&email=eq.${encodeURIComponent(email)}`,
                {
                    // 使用 GET 方法
                    method: 'GET',
                    // 設定 headers
                    headers: {
                        // 設定 apikey
                        'apikey': 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im90dGZ3b2dwa3poaXRkZWtybmtxIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NDkxMzQxMzMsImV4cCI6MjA2NDcxMDEzM30.56I4EssOz4RGnPcKeHl-vLI0D_QYEPbuKdzxWjMYmXU',
                    }
                }
            );

            if (!response.ok) {
                throw new Error('API請求失敗');
            }

            const data = await response.json();

            if (data && data.length > 0 && data[0].password === password) {
                return {
                    email: data[0].email,
                    password: data[0].password,
                    name: data[0].name || '未知',
                    gender: data[0].gender || '未知'
                };
            }

            return undefined;
        } catch (error) {
            console.error('登入錯誤:', error);
            return undefined;
        }
    },
};


export default function LoginForm() {

    // 宣告一個 formData 變數，用於存放 表單資料
    const [formData, setFormData] = useState<FormDataIF>({
        email: "",
        password: "",
        rememberMe: false,
    });

    // 宣告一個 userInfo 變數，用於存放 登入後使用者資訊
    const [userInfo, setUserInfo] = useState<UserInfoIF | undefined>(undefined);

    // 宣告一個 isInfoVisible 變數，用於控制 使用者資訊是否顯示
    const [isInfoVisible, setIsInfoVisible] = useState<boolean>(false);

    // 宣告一個 error 變數，用於存放 錯誤訊息
    const [error, setError] = useState<string | undefined>(undefined);

    // 宣告一個 handleLogin 方法，用於處理 登入
    const handleLogin = async () => {
        try {
            // 呼叫 service 物件的 login 方法，並將 formData 的 email 和 password 傳入
            const resultUserInfo = await authService.login(formData.email, formData.password);
            // 如果 resultUserInfo 有值
            if (resultUserInfo) {
                // 將 resultUserInfo 的值設定給 userInfo 變數
                setUserInfo(resultUserInfo);
                // 將 isInfoVisible 設為 true
                setIsInfoVisible(true);
                // 將 error 設為 undefined
                setError(undefined);
            }
            // 如果 resultUserInfo 沒有值
            else {
                // 將 isInfoVisible 設為 false
                setIsInfoVisible(false);
                // 將 error 設為 "帳號或密碼錯誤"
                setError("帳號或密碼錯誤");
            }
        } catch (err) {
            console.error('登入處理錯誤:', err);
            setIsInfoVisible(false);
            setError("登入失敗，請稍後再試");
        }
    };



    // 宣告一個css 變數 ： 垂直排列  水平(副軸)靠左 各元件間距 間距為 0.5rem
    const cssUserInfoItem = 'flex flex-col items-start gap-2 ';


    return (
        <div className="flex justify-center items-center h-full bg-gray-100 gap-4">
            <Card className="w-96" title="登入">
                <div className="space-y-4">
                    {/* tip */}
                    <p className="text-gray-500">
                        帳號: test@test.com
                        <br />
                        密碼: 123456
                    </p>
                    <div className="space-y-2">
                        <label
                            htmlFor="email"
                            className="block font-medium text-gray-700"
                        >
                            Email
                        </label>
                        <InputText
                            id="email"
                            value={formData.email}
                            onChange={(e) =>
                                setFormData({ ...formData, email: e.target.value })
                            }
                            className="w-full p-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
                        />
                    </div>
                    <div className="space-y-2">
                        <label
                            htmlFor="password"
                            className="block font-medium text-gray-700"
                        >
                            密碼
                        </label>
                        <InputText
                            id="password"
                            type="password"
                            value={formData.password}
                            onChange={(e) =>
                                setFormData({ ...formData, password: e.target.value })
                            }
                            className="w-full p-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
                        />
                    </div>
                    <div className="flex items-center gap-2">
                        <div>
                            <Checkbox
                                inputId="rememberMe"
                                checked={formData.rememberMe}
                                onChange={(e) =>
                                    setFormData({ ...formData, rememberMe: e.checked ?? false })
                                }
                            />
                            <label htmlFor="rememberMe" className="ml-2 text-gray-700">
                                記住我
                            </label>
                        </div>
                        {error &&
                            <p id='error' className="text-red-500">
                                {error}
                            </p>
                        }
                    </div>
                    <Button
                        label="登入"
                        type="submit"
                        className="w-full bg-blue-500 hover:bg-blue-600 text-white font-medium py-2 px-4 rounded-md transition-colors duration-200"
                        onClick={handleLogin}
                    />
                </div>
            </Card>

            <Card title="使用者資訊" className={`w-96 ${isInfoVisible ? '' : 'hidden'}`}>
                <div className="flex flex-col gap-4 ">
                    <div className={`${cssUserInfoItem}`}>
                        <label htmlFor="email" className="font-medium">Email:</label>
                        <div className="p-2 bg-gray-100 rounded">
                            {userInfo?.email}
                        </div>
                    </div>
                    <div className={`${cssUserInfoItem}`}>
                        <label htmlFor="password" className="font-medium">密碼:</label>
                        <div className="p-2 bg-gray-100 rounded">
                            {userInfo?.password}
                        </div>
                    </div>
                    <div className={`${cssUserInfoItem}`}>
                        <label htmlFor="name" className="font-medium">姓名:</label>
                        <div className="p-2 bg-gray-100 rounded">
                            {userInfo?.name}
                        </div>
                    </div>
                    <div className={`${cssUserInfoItem}`}>
                        <label htmlFor="gender" className="font-medium">性別:</label>
                        <div className="p-2 bg-gray-100 rounded">
                            {userInfo?.gender}
                        </div>
                    </div>
                </div>
            </Card>

        </div>
    );
}

```

#### 📝 實作步驟

1. 🏗️ 建立 `authService` 物件，包含 `login` 方法
2. 🌐 使用 `fetch` API 發送 GET 請求到 Supabase 後端
3. ⚙️ 設定適當的request header
4. 🛡️ 處理回應和可能的錯誤
5. ⏱️ 在表單提交處理函數中使用 `async/await` 調用 API

#### ✅ 練習

1. 🧪 用Postman 測試登入api
2. 📝 完成登入功能的 API 串接

### 📝 串接會員管理API

#### 🔰 功能說明

 將原本會員管理功能的假資料回傳替換成真實的API串接。這個改動讓我們的應用程式能夠與後端服務進行互動，實現真正的資料存儲功能。

#### 📋 API curl

```bash
curl --location 'https://ottfwogpkzhitdekrnkq.supabase.co/rest/v1/UsersTbl?select=*' \
--header 'apikey: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im90dGZ3b2dwa3poaXRkZWtybmtxIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NDkxMzQxMzMsImV4cCI6MjA2NDcxMDEzM30.56I4EssOz4RGnPcKeHl-vLI0D_QYEPbuKdzxWjMYmXU'
```

![1749373043836](image/Content/1749373043836.png)

#### 📄 完整程式碼

```ts
"use client";
import { useEffect, useState } from "react";
import { DataTable } from "primereact/datatable";
import { Column } from "primereact/column";
import { Button } from "primereact/button";
import { Tag } from "primereact/tag";

interface User {
    id: number;
    name: string;
    email: string;
    status: string;
    password: string;
    lastLogin: string;
    gender: string;
}

const userService = {
    getUsers: async () => {
        try {
            const response = await fetch('https://ottfwogpkzhitdekrnkq.supabase.co/rest/v1/UsersTbl?select=*', {
                headers: {
                    'apikey': 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im90dGZ3b2dwa3poaXRkZWtybmtxIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NDkxMzQxMzMsImV4cCI6MjA2NDcxMDEzM30.56I4EssOz4RGnPcKeHl-vLI0D_QYEPbuKdzxWjMYmXU'
                }
            });

            if (!response.ok) {
                throw new Error('API請求失敗');
            }

            const data = await response.json();

            // 添加缺少的字段
            return data.map((user: {
                id: number;
                name: string;
                email: string;
                password: string;
                gender: string;
                created_at: string;
            }) => ({
                ...user,
                status: "active",
                lastLogin: "2024-03-15 14:30"
            }));
        } catch (error) {
            console.error('獲取用戶數據時出錯:', error);
            return [];
        }
    }
}

export default function UserList() {
    // 使用者資料
    const [users, setUsers] = useState<User[]>([]);
    const [loading, setLoading] = useState<boolean>(true);

    // 使用 useEffect 來取得使用者資料
    useEffect(() => {
        const fetchUsers = async () => {
            setLoading(true);
            const data = await userService.getUsers();
            setUsers(data);
            setLoading(false);
        };

        fetchUsers();
    }, []);

    // 狀態標籤模板
    const statusTemplate = (rowData: User) => {
        return (
            <Tag
                value={rowData.status === "active" ? "啟用" : "停用"}
                severity={rowData.status === "active" ? "success" : "danger"}
            />
        );
    };

    // 性別模板
    const genderTemplate = (rowData: User) => {
        return rowData.gender === "male" ? "男" : "女";
    };

    // 操作按鈕模板
    const actionTemplate = (rowData: User) => {
        return (
            <div className="flex gap-2">
                <Button
                    icon="pi pi-pencil"
                    className="p-button-rounded p-button-text p-button-sm"
                    tooltip="編輯"
                    onClick={() => alert(`編輯 ${rowData.name}`)}
                />
                <Button
                    icon="pi pi-trash"
                    className="p-button-rounded p-button-text p-button-danger p-button-sm"
                    tooltip="刪除"
                    onClick={() => alert(`刪除 ${rowData.name}`)}
                />
            </div>
        );
    };

    return (
        <div className="card">
            <DataTable
                value={users}
                paginator
                rows={5}
                loading={loading}
                rowsPerPageOptions={[5, 10, 25, 50]}
                paginatorTemplate="FirstPageLink PrevPageLink PageLinks NextPageLink LastPageLink CurrentPageReport RowsPerPageDropdown"
                currentPageReportTemplate="顯示第 {first} 到 {last} 筆，共 {totalRecords} 筆"
                className="p-datatable-sm"
            >
                <Column
                    field="id"
                    header="ID"
                    sortable
                    className="w-[5%]"
                />
                <Column
                    field="name"
                    header="姓名"
                    sortable
                    className="w-[15%]"
                />
                <Column
                    field="email"
                    header="電子郵件"
                    sortable
                    className="w-[20%]"
                />
                <Column
                    field="password"
                    header="密碼"
                    sortable
                    className="w-[10%]"
                />
                <Column
                    field="gender"
                    header="性別"
                    body={genderTemplate}
                    sortable
                    className="w-[10%]"
                />
                <Column
                    field="status"
                    header="狀態"
                    body={statusTemplate}
                    sortable
                    className="w-[10%]"
                />
                <Column
                    field="lastLogin"
                    header="最後登入"
                    sortable
                    className="w-[15%]"
                />
                <Column
                    body={actionTemplate}
                    header="操作"
                    className="w-[10%]"
                />
            </DataTable>
        </div>
    );
}

```

#### 📝 實作步驟

1. 🏗️ 建立 `userService` 物件，包含 `getUsers` 方法
2. 🌐 使用 `fetch` API 發送 GET 請求到 Supabase 後端
3. ⚙️ 設定適當的request header
4. 🛡️ 處理回應和可能的錯誤
5. ⏱️ 在表單提交處理函數中使用 `async/await` 調用 API

## 🚀 部署網頁到github

因為github page 只接受靜態網頁，所以需要將專案以靜態方式打包。
📚 輸出 靜態、動態的差別
[輸出 靜態、動態的差別](https://chatgpt.com/share/68455876-5e9c-8003-8132-31960ac6d03e)

### 📝 實作步驟

#### 🔄 先將專案改成以靜態方式打包

   在專案根目錄下的 `next.config.ts` 或 `next.config.js` 中設定 `靜態輸出` 以及 `關閉圖片優化` 因為很多平台不支援圖片優化
   ![1749375743855](image/Content/1749375743855.png)
   修改指令如下:

```ts
    output: "export",
    images: {
        unoptimized: true,
    },
```

#### 📤 將專案推到github上

1. 📄 建立 `.gitignore` 檔案(若無則建立)
   請參考[gitignore](./.gitignore)
2. 🔍 進入原始檔控制頁面
   ![1749386012684](image/Content/1749386012684.png)
3. 🌍 選擇公開(若是私有要使用 Pages 每年要付 48 USD)
   ![1749386393330](image/Content/1749386393330.png)
4. ✅ 檢查是否建立及推送成功
   ![1749386202691](image/Content/1749386202691.png)
   ![1749386511728](image/Content/1749386511728.png)
5. ⚙️ 設定Github Pages

   * 點選Settings => Pages => Source
   * 把 `Deploy from a branch` 改成 `GitHub Actions`
   * 點選 Configure
     ![1749386721293](image/Content/1749386721293.png)
     ![1749386849212](image/Content/1749386849212.png)
6. 📋 新增 Actions 檔案
   ![1749387003662](image/Content/1749387003662.png)
   ![1749387062919](image/Content/1749387062919.png)
7. 🔄 確認 Actions 是否正常運作

   * ✓ 打勾就是好了
   * 🔍 可以點進去查看
     ![1749387126434](image/Content/1749387126434.png)
     ![1749387186237](image/Content/1749387186237.png)
8. 🌐 確認網頁

   * 🔗 這個網址就是你的網頁了
     ![1749387253300](image/Content/1749387253300.png)
     ![1749388833346](image/Content/1749388833346.png)

##### 📌 後續說明

此部分只是讓大家知道如何將網頁部署到github上
後續也許還有 `靜態資源路徑`的問題要解決
這就需要深入了解github路徑機制與next.js的basePath和assetPrefix配合，此處就不深入探討

## 🚀 部署網頁到 Vercel

### 📋 步驟說明

1. 🔑 登入
   ![1749389232988](image/Content/1749389232988.png)
2. 🔗 使用github帳號登入
   ![1749389263485](image/Content/1749389263485.png)
3. 📥 匯入
   ![1749389295016](image/Content/1749389295016.png)
4. 🔄 連結github帳號內的Repository
   ![1749389328636](image/Content/1749389328636.png)
5. 📂 選擇剛剛的專案，然後點擊Install
   ![1749389377991](image/Content/1749389377991.png)
6. 📤 Import
   ![1749389410142](image/Content/1749389410142.png)
7. 🚀 部署
   ![1749389472901](image/Content/1749389472901.png)
8. ✅ 完成後點選網址
   ![1749389747634](image/Content/1749389747634.png)
   ![1749389777661](image/Content/1749389777661.png)

## 🖥️ 部署到IIS

### 📋 步驟說明

1. 📦 打包成靜態網頁檔案

```bash
npm run build
```

2. 📂 把 out 資料夾複製到 `C:\inetpub\wwwroot`
   ![1749375849570](image/Content/1749375849570.png)
   ![1749390059131](image/Content/1749390059131.png)
3. ⚙️ 在IIS管理頁面中新增網站
   ![1749390106503](image/Content/1749390106503.png)
4. 🔧 設定名稱、路徑、port
   ![1749390167539](image/Content/1749390167539.png)
5. ✅ 驗證網頁是否能成功訪問
   ![1749390210382](image/Content/1749390210382.png)

## 📝 延伸閱讀

1. Supabase 的資料庫建立、Api 使用
2. Cloudflare 的域名申請、部署到Pages
3. Nginx 的安裝、設定、反向代理
4. 後端API服務架設(C# .NET 、 Java Spring Boot 、 Python Fastapi)
5. 使用者認證機制(JWT、OAuth、LDAP)
6. basePath 應用 ，同 port 架設多個 網頁應用(服務)，處理路徑問題
