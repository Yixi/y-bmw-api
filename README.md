# y-bmw-api 镜像仓库

这是一个用于存放 y-bmw-api 服务镜像的仓库。

## 镜像说明

该服务容器导出端口为 **8080**。

### 获取镜像

```bash
docker pull ghcr.io/yixi/y-bmw-api:sha-b7d8b70
```

### 启动示例

```bash
docker run -d -p 8080:8080 ghcr.io/yixi/y-bmw-api:sha-b7d8b70
```

## API 接口文档

以下是服务提供的三个主要接口。

### 1. 获取 Nonce (`/api/nonce`)

用于获取登录所需的 Nonce。

*   **URL**: `/api/nonce`
*   **Method**: `POST`
*   **Content-Type**: `application/json`

#### 请求参数

| 参数名 | 类型 | 必选 | 描述 | 校验规则 |
| :--- | :--- | :--- | :--- | :--- |
| `mobile` | string | 是 | 手机号码 | 长度13位，纯数字，以86开头 |

**请求示例:**

```json
{
  "mobile": "8613800138000"
}
```

#### 响应参数

| 参数名 | 类型 | 描述 |
| :--- | :--- | :--- |
| `nonce` | string | 返回的 Nonce 值 |

**响应示例:**

```json
{
  "nonce": "random-nonce-string"
}
```

---

### 2. 用户登录 (`/api/login`)

用户登录接口。

*   **URL**: `/api/login`
*   **Method**: `POST`
*   **Content-Type**: `application/json`

#### 请求参数

| 参数名 | 类型 | 必选 | 描述 | 校验规则 |
| :--- | :--- | :--- | :--- | :--- |
| `mobile` | string | 是 | 手机号码 | 长度13位，纯数字，以86开头 |
| `password` | string | 是 | 密码 | 必填 |

**请求示例:**

```json
{
  "mobile": "8613800138000",
  "password": "your-password"
}
```

#### 响应参数

*   返回类型: `Any` (具体结构视业务实现而定)

---

### 3. 刷新 Token (`/api/refresh-token`)

用于刷新用户的访问令牌。

*   **URL**: `/api/refresh-token`
*   **Method**: `POST`
*   **Content-Type**: `application/json`

#### 请求参数

| 参数名 | 类型 | 必选 | 描述 |
| :--- | :--- | :--- | :--- |
| `refresh_token` | string | 是 | 刷新令牌 |
| `gcid` | string | 是 | GCID 标识 |

**请求示例:**

```json
{
  "refresh_token": "your-refresh-token-value",
  "gcid": "your-gcid-value"
}
```

#### 响应参数

*   返回类型: `Any` (具体结构视业务实现而定)
