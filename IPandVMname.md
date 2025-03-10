## 虚拟机命名和IP地址分配

以下表格可以用来查询规划设计，在正式部署章节，会更详细的解释配置的作用。

按照以下规划来进行虚拟机的命名配置和地址配置。为了便于`理解和提交反馈`，在第一次POC阶段，请不要修改设计。

| 资源              | 需求量                                     |
| ----------------- | ------------------------------------------ |
| VHD模板操作系统   | 至少15G硬盘空间                            |
| 网络              | 1个`内部网络`类型的虚拟交换机，命名为`POC` |
| VLAN              | `不要设置`VLAN，且不支持。                 |
| 虚拟化            | 开启`嵌套虚拟化`，开启`MAC地址欺骗`        |
| 检查点/自动检查点 | 手动关闭                                   |
|                   |                                            |


| 事项     | 内容        |
| -------- | ----------- |
| 域名     | contoso.com |
| 默认密码 | `poc.123`   |
|          |             |

| 虚拟机     | 功能                                       | IP地址      |
| ---------- | ------------------------------------------ | ----------- |
| POC-DC01   | Active Directory域控制器                   | 192.148.0.2 |
| POC-DCGW   | 安装了RRAS角色的不加域虚拟机，用来做软路由 |             |
| POC-COMP1  | 承载计算节点的虚拟机，开启嵌套虚拟化       | 192.148.0.9 |
| POC-COMP2  | 承载SDN基础架构的虚拟机，开启嵌套虚拟化    |             |
| POC-SQL01  | 数据库节点，用来承载SCVMM和SCOM的数据库    | 192.148.0.4 |
| POC-VMM01  | VMM节点，用来承载虚拟机管理平台            | 192.148.0.5 |
| POC-OM01   | SCOM节点，用来承载监控平台                 |             |
| POC-MGMT01 | 远程管理用的主机                           |             |

| 网络            | 功能                       |
| --------------- | -------------------------- |
| 192.148.0.0/24  | 物理主机网络（真实网络）   |
| 192.148.11.0/24 | 管理网络，由POC-DCGW实现   |
| 192.148.12.0/24 | PA子网，由POC-DCGW实现     |
| 192.148.13.0/24 |                            |
| 192.148.14.0/24 | PrivateVIP，由POC-DCGW实现 |
| 192.148.15.0/24 | PublicVIP，由POC-DCGW实现  |