---
title: "云用户管理"
date: 2021-06-11T08:22:33+08:00
weight: 30
---

### 关联云用户

该功能用于将云用户与云用户组关联，关联云用户后，该云用户组将会将会同步到对应的公有云平台，且会创建一条缓存记录。


1. 在左侧导航栏，选择 **_"多云管理/云账号/云用户组"_** 菜单项，进入云用户组页面。
2. 单击云用户组右侧操作列 **_"更多"_** 按钮，选择下拉菜单 **_"关联云用户"_** 菜单项，弹出关联云用户对话框。
2. 选择云用户，单击 **_"确定"_** 按钮，完成操作。

```bash
# 云用户组关联云用户
climc cloud-group-add-user <云用户组名称或ID> <云用户的名称或ID>
```

### 移除云用户

该功能用于将云用户移出云用户组。

**单个移除**

1. 在左侧导航栏，选择 **_"多云管理/云账号/云用户组"_** 菜单项，进入云用户组页面。
2. 单击云用户组名称项，进入云用户组详情页面。
2. 单击“云用户”页签，进入云用户页面。
3. 单击云用户右侧操作列 **_"移除"_** 按钮，弹出操作确认对话框。
4. 单击 **_"确定"_** 按钮，完成操作。

**批量移除**

1. 在左侧导航栏，选择 **_"多云管理/云账号/云用户组"_** 菜单项，进入云用户组页面。
2. 单击云用户组名称项，进入云用户组详情页面。
2. 单击“云用户”页签，进入云用户页面。
3. 在云用户列表中选择一个或多个云用户，单击列表上方 **_"移除"_** 按钮，弹出操作确认对话框。
4. 单击 **_"确定"_** 按钮，完成操作。



```bash
# 云用户组移除云用户
climc cloud-group-remove-user <云用户组名称或ID> <云用户的名称或ID>
```