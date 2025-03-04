---
title: "SSH代理节点"
weight: 1
description: SSH代理节点用于建立平台与VPC网络之间的通信隧道，实现平台对VPC中资源的管理，安装监控Agent，收集监控数据等。
---

SSH代理节点用于建立平台与VPC网络之间的通信隧道，实现平台对VPC中资源的管理，安装监控Agent，收集监控数据等。

通过在VPC中选择一台能与外网联通的虚拟机作为SSH代理节点，后续平台可以通过该SSH代理节点的local forward为VPC内网络互通的虚拟机安装Agent，监控Agent收集到监控信息也将通过SSH代理节点的remote forward上报到平台。

**入口**：在云管平台单击左上角![](../../../images/intro/nav.png)导航菜单，在弹出的左侧菜单栏中单击 **_"网络/SSH代理/SSH代理节点"_** 菜单项，进入SS代理节点页面。

![](../../../images/network/sshproxy.png)

## 新建SSH代理节点

该功能用于新建代理节点。

1. 在SSH代理节点页面，单击列表上方 **_"新建"_** 按钮，进入新建SSH代理节点页面。
2. 在选择虚拟机页面设置以下参数：
    - 域：设置SSH代理节点所属域，并通过域过滤可选的虚拟机。
    - 名称：设置SSH代理节点的名称。
    - 区域：通过平台、区域过滤VPC。
    - 网络：通过VPC、网络过滤虚拟机。
    - 虚拟机：通过上面的筛选条件过滤出符合条件的虚拟机，并支持在搜索框中通过名称和IP搜索虚拟机，请确保所选的虚拟机符合[虚拟机配置要求](#虚拟机配置要求)，如没有合适的虚拟机，可以单击“新建”超链接，跳转到虚拟机列表页面创建符合需求的虚拟机。
3. 选择好虚拟机后，单击 **_"下一步"_** 按钮，开始探测虚拟机的免密登录状态。
    - 如虚拟机可免密登录，可直接单击 **_"确定"_** 按钮，开始创建虚拟机。
    - 如虚拟机不可免密登录，请先点击列表操作列 **_"查看"_** 按钮，查看探测免密登录失败的具体原因。
        - 如报错原因中提示“none publickey”或因为ssh端口不是默认端口而导致无法免密登录时，可通过设置免密登录功能，将虚拟机设置为免密登录状态。设置免密登录方式配置参数如下：
            - SSH端口：修改虚拟机的SSH端口，将通过该端口免密登录到虚拟机。
            - 设置方式：支持密钥、密码、脚本等方式将平台的公钥上传到虚拟机上。
            - 当设置方式为“密钥”时，请使用root用户或具有使用sudo免密权限的用户以其私钥，请确保可以通过用户名和私钥通过ssh连接到对应虚拟机，单击 **_"确定"_** 按钮，开始设置并探测虚拟机的免密登录状态是否变为免密登录。
            - 当设置方式为“密码”时，请使用root用户或具有使用sudo免密权限的用户以其密码，请确保可以通过用户名和密码通过ssh连接到对应虚拟机。单击 **_"确定"_** 按钮，开始设置并探测虚拟机的免密登录状态是否变为免密登录。
            - 当设置方式为“脚本”时，请请使用root或具有sudo权限的用户在虚拟机中执行以下脚本，执行完成后，单击 **_"确定"_** 按钮，开始设置并探测虚拟机的免密登录状态是否变为免密登录。
        - 如报错原因中提示“network error”，则需要返回上一步选择其他虚拟机，或为该虚拟机通过绑定EIP或NAT网关等方式，使其与平台网络可通。
4. 只有当虚拟机免密登录状态为“可免密登录”时，才支持单击 **_"确定"_** 按钮，开始创建SSH代理节点。
5. 在创建SSH代理节点时将会检查虚拟机的sshd配置是否符合虚拟机配置要求，若不符合将会尝试变更虚拟机的sshd配置，因此可能会造成创建ssh代理节点时间过长，若提示超时，请重新单击 **_"确定"_** 按钮，创建SSH代理节点。

### 虚拟机配置要求

- 目前只支持Linux操作系统的虚拟机作为SSH代理节点。
- 请确保虚拟机处于运行中状态；
- 请确保虚拟机支持通过平台免密登录；虚拟机能被平台免密登录，则要求虚拟机与平台网络通（即通过EIP、NAT网关或SSH代理等方式使虚拟机与平台网络通）以及虚拟机中存在平台的公钥文件。
- 请检查虚拟机的sshd配置，GatewayPorts是clientspecified，若该项值为no，则只允许绑定127.0.0.1的地址，使remote forward无法正常使用，造成安装监控Agent的虚拟机无法向平台上报监控数据等。

## 修改端口

该功能用于修改SSH代理节点的SSH端口。

**修改端口**

1. 在SSH代理节点页面，单击SSH代理节点右侧操作列 **_"修改端口"_** 按钮，弹出修改端口对话框。
2. 修改SSH端口，单击 **_"确定"_** 按钮，完成操作。

**批量修改端口**

1. 在SSH代理节点列表中选择一个或多个SSH代理节点，单击列表上方 **_"批量操作"_** 按钮，选择下拉菜单 **_"修改端口"_** 菜单项，弹出修改端口对话框。
2. 修改SSH端口，单击 **_"确定"_** 按钮，完成操作。

## 删除SSH代理节点

该功能用于删除SSH代理节点，当SSH代理节点下有转发规则时，不允许删除。目前转发规则列表暂未放开。

**单个删除**

1. 在SSH代理节点页面，单击SSH代理节点右侧操作列 **_"删除"_** 按钮，弹出操作确认对话框。
2. 单击 **_"确定"_** 按钮，完成操作。

**批量删除**

1. 在SSH代理节点列表中选择一个或多个SSH代理节点，单击列表上方 **_"批量操作"_** 按钮，选择下拉菜单 **_"删除"_** 菜单项，弹出操作确认对话框。
2. 单击 **_"确定"_** 按钮，完成操作。



## 查看SSH代理节点详情

该功能用于查看SSH代理节点的详细信息。

1. 在SSH代理节点列表，单击SSH代理节点名称项，进入SSH代理节点详情页面。
2. 查看以下信息，包括云上ID、ID、名称、状态、域、项目、内网地址、SSH地址、SSH端口、创建时间、更新时间、备注等。

## 适用范围管理

适用范围即表示SSH代理节点的生效范围，SSH代理节点创建成功后，默认在创建SSH代理节点的虚拟机所在的VPC和IP子网下生效，当VPC下存在网络隔离的情况下，仅在IP子网下生效。当VPC之间打通时，可通过关联网络的功能，在其他VPC下使用该SSH代理节点。
当VPC下IP子网互通时，VPC下只需要存在一个SSH代理节点即可，若VPC下存在不同子网网络隔离的情况时，需要分别针对于不同的子网设置一个SSH代理节点，用户提交转发请求时，优先匹配IP子网下的SSH代理节点，当IP子网中不存在时，才会匹配VPC下的SSH代理节点。

### 关联网络

该功能用于通过关联网络添加SSH代理节点的适用范围，添加之前，请确保要添加网络与代理节点所在的网络互通，否则即使添加了网络，恶意无法生效。

1. 在SSH代理节点列表，单击SSH代理节点名称项，进入SSH代理节点详情页面。
2. 单击“适用范围”页签，进入适用范围页面。
3. 单击列表上方 **_"关联"_** 按钮，弹出关联对话框。
4. 配置以下参数：
    - 名称：设置网络的名称。
    - 区域：选择网络所在区域。
    - 类型：支持选择VPC和IP子网。
    - VPC：选择网络所在VPC。
    - IP子网：当类型选择“IP子网”时，需要选择网络所在的IP子网。
5. 单击 **_"确定"_** 按钮，完成操作。

### 取消关联

该功能用于取消关联网络，即减少SSH代理节点的适用范围。

**取消关联**

1. 在SSH代理节点列表，单击SSH代理节点名称项，进入SSH代理节点详情页面。
2. 单击“适用范围”页签，进入适用范围页面。
3. 单击网络右侧操作列 **_"取消关联"_** 按钮，弹出操作确认对话框。
4. 单击 **_"确定"_** 按钮，完成操作。

**批量取消关联**

1. 在SSH代理节点列表，单击SSH代理节点名称项，进入SSH代理节点详情页面。
2. 单击“适用范围”页签，进入适用范围页面。
3. 在列表中选择一个或多个网络，单击列表上方 **_"取消关联"_** 按钮，弹出操作确认对话框。
4. 单击 **_"确定"_** 按钮，完成操作。

## 查看操作日志

该功能用于查看SSH代理节点相关操作的日志信息

1. 在SSH代理节点列表，单击SSH代理节点名称项，进入SSH代理节点详情页面。
2. 单击“操作日志”页签，进入操作日志页面。
    - 加载更多日志：列表默认显示20条操作日志信息，如需查看更多操作日志，请单击 **_"加载更多"_** 按钮，获取更多日志信息。
    - 查看日志详情：单击操作日志右侧操作列 **_"查看"_** 按钮，查看日志的详情信息。支持复制详情内容。
    - 查看时间段的日志：如需查看某个时间段的操作日志，在列表右上方的开始日期和结束日期中设置具体的日期，查询时间段的日志信息。
    - 导出日志：目前仅支持导出本页显示的日志。单击右上角![](../../../images/system/download.png)图标，在弹出的导出数据对话框中，设置导出数据列，单击 **_"确定"_** 按钮，导出日志。
