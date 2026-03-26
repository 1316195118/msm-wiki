# UniFi 配置指南

适用于 UniFi Network 控制器（UDM/USG/UXG 等）。不同版本界面略有差异。

## 示例环境

- UniFi 网关：`192.168.1.1`
- MSM 主机：`192.168.1.2`

## 步骤一：配置 DHCP DNS

在 **Settings > Networks** 中编辑 LAN 网络，设置 DNS：

- **DNS Server**：选择 **v6-Manual**
- **DNS Server 1**：`192.168.1.2`
- **DNS Server 2**：可选填运营商 DNS

可选 **有v6环境并已打开** 中编辑 LAN 网络，设置 DNS：

- **DNS Server**：选择 **v6-Manual**
- **DNS Server 1**：`fe80::1`
- **DNS Server 2**：可选填运营商 v6DNS

## 步骤二：添加静态路由（FakeIP）

在 **Routes / Static Routes** 页面依次新增路由：

**FakeIP1** 

- **Destination Network**：`28.0.0.0/8`
- **Next Hop**：`192.168.1.2`
- **Type**：Next Hop（或网关）

**FakeIP2** 
 
- **Destination Network**：`8.8.8.8/32`
- **Next Hop**：`192.168.1.2`
- **Type**：Next Hop（或网关）
  
 **FakeIP3**  

- **Destination Network**：`1.1.1.1/32`
- **Next Hop**：`192.168.1.2`
- **Type**：Next Hop（或网关）

可选 **有v6环境并已打开** 需新增路由：

**FakeIP v6**
- **Destination Network**：`fe80::1`
- **接口**：`Internet 出口`
- **Next Hop**：`f2b0::/18`
- **Type**：Next Hop（或网关）

## 步骤三： 可选：Telegram 路由

分别按#步骤二#的方法添加以下路由

| 目标地址 | 网关 |
| --- | --- |
| `149.154.160.0/22` | `{MSM主机IP}` |
| `149.154.164.0/22` | `{MSM主机IP}` |
| `149.154.172.0/22` | `{MSM主机IP}` |
| `91.108.4.0/22` | `{MSM主机IP}` |
| `91.108.20.0/22` | `{MSM主机IP}` |
| `91.108.56.0/22` | `{MSM主机IP}` |
| `91.108.8.0/22` | `{MSM主机IP}` |
| `95.161.64.0/22` | `{MSM主机IP}` |
| `91.108.12.0/22` | `{MSM主机IP}` |
| `91.108.16.0/22` | `{MSM主机IP}` |
| `67.198.55.0/24` | `{MSM主机IP}` |
| `109.239.140.0/24` | `{MSM主机IP}` |

### 步骤四. 可选：Netflix 路由

分别按#步骤二#的方法添加以下路由

| 目标地址 | 网关 |
| --- | --- |
| `207.45.72.0/22` | `{MSM主机IP}` |
| `208.75.76.0/22` | `{MSM主机IP}` |
| `210.0.153.0/24` | `{MSM主机IP}` |
| `185.76.151.0/24` | `{MSM主机IP}` |

> 路由菜单名称因控制器版本而异，请在设置中查找 “Routes / Static Routes”。

## 验证

客户端执行：

```bash
nslookup google.com
```

应返回 `28.0.0.0/8` 段地址。

白名单设备能访问国外站点，非白名单设备无法访问


## 下一步

- [设备管理](/zh/guide/device-management)
- [DNS 服务管理](/zh/guide/mosdns)
