# 本项目许可声明（GNU GPL 许可）

本项目基于 **GNU 通用公共许可证（GPL）** 进行开源，任何人均可自由使用、修改和分发代码，但需遵守 GPL 许可协议的相关规定。

## 重要声明

1. **许可协议**  
   本项目遵循 **GNU GPL 许可协议**，允许自由使用、修改和分发，但不得附加额外的限制。

2. **非商业声明**  
   本人 **从未使用以下接口盈利**，本项目 **完全免费**，仅用于技术研究和学习。

3. **禁止滥用**  
   本项目 **仅限学习和测试用途**，请勿滥用！请勿滥用！请勿滥用！

4. **责任声明**
    - 本项目仅提供 **技术研究用途**，对任何滥用行为概不负责。
    - 使用本项目提供的 **接口、文档等所造成的任何后果与本人无关**。

5. **项目发展**
    - 由于本项目的特殊性，**可能随时停止开发或删除相关内容**。

---

**继续阅读即表示同意以上声明**

## 快速获取积分可直接看1,2,3,12,13接口

> 原理:后端没有做任务完成校验,登陆-获取任务列表-调用`score-send`api即可完成任务-积分到账

### API

统一请求头信息:

- `User-Agent`: Mozilla/5.0 (iPhone; CPU iPhone OS 15_5 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko)
  Mobile/15E148 Html5Plus/1.0 (Immersed/20) uni-app

---

1. **验证码图片请求** (`GET /api/v1/captcha/`)

| 字段 | 位置    | 类型     | 必填 | 说明              |
|----|-------|--------|----|-----------------|
| s  | query | string | 是  | 请求标识随机数 (0-1之间) |
| r  | query | string | 是  | 请求时间戳           |

---

2. **请求短信验证码** (`POST /api/v1/acc/login/code`)

| 字段       | 位置   | 类型     | 必填 | 说明        |
|----------|------|--------|----|-----------|
| s        | body | string | 是  | 前一步生成的随机数 |
| authCode | body | string | 是  | 图片识别码     |
| un       | body | string | 是  | 手机号       |

---

3. **用户登录接口** (`POST /api/v1/acc/login`)

| 字段       | 位置   | 类型     | 必填 | 说明      |
|----------|------|--------|----|---------|
| openCode | body | string | 是  | 默认留空    |
| authCode | body | string | 是  | 手机短信验证码 |
| un       | body | string | 是  | 手机号     |
| cid      | body | string | 是  | 客户端标识码  |

---
> cid:"ce6a3dff5112b3e4f58738512afd1770"(任意MD5,其他值请自行测试)

4. **启动设备** (`GET /api/v1/dev/start`)

| 字段            | 位置     | 类型     | 必填 | 说明   |
|---------------|--------|--------|----|------|
| did           | query  | string | 是  | 设备标识 |
| Authorization | header | string | 是  | 用户令牌 |

---

5. **关闭设备** (`GET /api/v1/dev/end`)

| 字段            | 位置     | 类型     | 必填 | 说明   |
|---------------|--------|--------|----|------|
| did           | query  | string | 是  | 设备标识 |
| Authorization | header | string | 是  | 用户令牌 |

---

6. **设备基础信息获取** (`GET /api/v1/qr/use`)

| 字段            | 位置     | 类型     | 必填 | 说明   |
|---------------|--------|--------|----|------|
| id            | query  | string | 是  | 设备标识 |
| Authorization | header | string | 是  | 用户令牌 |

---

7. **用户常用设备列表** (`GET /api/v1/ui/app/master`)

| 字段            | 位置     | 类型     | 必填 | 说明   |
|---------------|--------|--------|----|------|
| Authorization | header | string | 是  | 用户令牌 |

---

8. **设备详细数据获取** (`GET /api/v1/ui/app/dev/home`)

| 字段            | 位置     | 类型     | 必填 | 说明   |
|---------------|--------|--------|----|------|
| apply         | query  | string | 否  | 扩展参数 |
| did           | query  | string | 否  | 设备标识 |
| Authorization | header | string | 否  | 用户令牌 |

---

9. **收藏设备管理** (`GET /api/v1/dev/favo`)

| 字段            | 位置     | 类型     | 必填 | 说明          |
|---------------|--------|--------|----|-------------|
| did           | query  | string | 否  | 设备标识        |
| remove        | query  | string | 否  | 删除标记（非空则删除） |
| Authorization | header | string | 否  | 用户令牌        |

---

10. **设备实时状态查询** (`GET /api/v1/ui/app/dev/status`)

| 字段            | 位置     | 类型     | 必填 | 说明   |
|---------------|--------|--------|----|------|
| did           | query  | string | 否  | 设备标识 |
| Authorization | header | string | 否  | 用户令牌 |

---

11. **余额查询接口** (`GET /api/v1/acc/wallet/owner`)

| 字段            | 位置     | 类型     | 必填 | 说明        |
|---------------|--------|--------|----|-----------|
| eid           | query  | string | 是  | 机构标识，空为全部 |
| all           | query  | string | 是  | 固定示例值     |
| Authorization | header | string | 是  | 用户令牌      |

---

12. **有效积分与任务列表查询** (`GET /api/v1/acc/score/mission-lst`)

| 字段            | 位置     | 类型     | 必填 | 说明   |
|---------------|--------|--------|----|------|
| Authorization | header | string | 是  | 用户令牌 |

---

13. **每日积分签到** (`POST /api/v1/acc/score/score-send`)

| 字段            | 位置     | 类型      | 必填 | 说明                     |
|---------------|--------|---------|----|------------------------|
| weekDay       | body   | integer | 是  | 签到第几天                  |
| adId          | body   | string  | 是  | 固定为默认值"DAILY_CHECK_IN" |
| Authorization | header | string  | 是  | 用户令牌                   |

> 将adId替换为任务列表中的任务ref,移除weekDay字段即可实现获取该任务积分

---
