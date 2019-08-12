---

copyright:
  years: 2017, 2019
lastupdated: "2019-06-19"

keywords: migrate Netezza databases, PureData System for Analytics databases, 

subcollection: mass-data-migration

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}

# 将 PureData System for Analytics 数据库迁移到 {{site.data.keyword.dashdbshort_notm}}
{: #migrate-netezza-databases}

{{site.data.keyword.mdms_full}} 可用于将大型 IBM PureData™ System for Analytics（基于 Netezza® 技术）数据库迁移到 {{site.data.keyword.dashdbshort}}。使用用于确定传输的数据量和导出方法的工具时，可以将此文档作为参考。
{: shortdesc}

## 确定数据库对象大小
{: #determine-db-object-size}

1. 从 [IBM 支持 > Fix Central > Netezza Tools ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www-945.ibm.com/support/fixcentral/options?selectionBean.selectedTab=find&selection=ibm%2fInformation+Management%3bPureData+System+for+Analytics%3bibm%2fInformation+Management%2fNetezza+Tools){:new_window}，下载与 Netezza 实例相对应的相应 Netezza Tools 版本。

   缺省情况下，支持工具会安装在 Netezza 服务器的 `/nz/support-IBM_Netezza<version>/bin` 目录下。
   {:note}

2. 运行以下两个命令。
   - `nz_db_size`，用于确定数据库大小

     ```
     nz_db_size
     对象 | 名称 | 字节 | KB | MB | GB | TB
     -----------------------------------------------------------------------------------------------------------
     设备  | cdcntze1 | 23,388,712,337,408 | 22,840,539,392 | 22,305,214 | 21,782.4 | 21.3
     数据库| DHDB | 183,537,500,160 | 179,235,840 | 175,035 | 170.9 | .2
     表    | DH71964I1 | 880,803,840 | 860,160 | 840 | .8 | .0
     表    | DH71964T1 | 96,120,078,336 | 93,867,264 | 91,667 | 89.5 | .1
     表    | DH71964T10 | 9,615,179,776 | 9,389,824 | 9,170 | 9.0 | .0
     表    | DH71964T2 | 9,615,179,776 | 9,389,824 | 9,170 | 9.0 | .0
     表    | DH71964T3 | 9,615,179,776 | 9,389,824 | 9,170 | 9.0 | .0
     表    | DH71964T4 | 9,615,179,776 | 9,389,824 | 9,170 | 9.0 | .0
     表    | DH71964T5 | 9,615,179,776 | 9,389,824 | 9,170 | 9.0 | .0
     表    | DH71964T6 | 9,615,179,776 | 9,389,824 | 9,170 | 9.0 | .0
     表    | DH71964T7 | 9,615,179,776 | 9,389,824 | 9,170 | 9.0 | .0
     表    | DH71964T8 | 9,615,179,776 | 9,389,824 | 9,170 | 9.0 | .0
     表    | DH71964T9 | 9,615,179,776 | 9,389,824 | 9,170 | 9.0 | .0
     ```
     {: codeblock}

   - `nz_compressedTableRatio`，用于估算解压缩后的数据大小。

      ```
  nz_compressedTableRatio
  ....................................................................................
      . 下面的值显示了压缩表与其未压缩格式的估计大小 .
. 比率。未压缩表大约是其压缩版本的 <ratio> .
. 倍。.
      . .
      . “压缩大小”是表实际使用的存储量。.
      . “未压缩大小”是根据数学计算估计的值。.
      ....................................................................................
      数据库：DHDB
表/MView 名称 比率 压缩大小 未压缩大小 大小差异
================== ===== ================ =============== ===========
DH71964I1 1.49 880,803,840 1,310,723,840 429,920,000
DH71964T1 1.50 96,120,078,336 144,179,203,840 48,059,125,504
DH71964T10 1.50 9,615,179,776 14,417,923,840 4,802,744,064
DH71964T2 1.50 9,615,179,776 14,417,923,840 4,802,744,064
DH71964T3 1.50 9,615,179,776 14,417,923,840 4,802,744,064
DH71964T4 1.50 9,615,179,776 14,417,923,840 4,802,744,064
DH71964T5 1.50 9,615,179,776 14,417,923,840 4,802,744,064
DH71964T6 1.50 9,615,179,776 14,417,923,840 4,802,744,064
DH71964T7 1.50 9,615,179,776 14,417,923,840 4,802,744,064
DH71964T8 1.50 9,615,179,776 14,417,923,840 4,802,744,064
DH71964T9 1.50 9,615,179,776 14,417,923,840 4,802,744,064
================================ ===== =================== ===================
此数据库的总计 1.50 183,537,500,160 275,251,242,240 91,713,742,080
```
      {: codeblock}

## 抽取数据并上线
{: #extract-data}

可以使用两个选项从 Netezza 中抽取数据。
- 使用 `nz_backup` 实用程序。
   ```
  /nz/support/contrib/bin/nz_backup –db   {db_name} –d  {target_directory}  ascii threads 4
  ```

   `{target_directory}` 是安装到此服务器且由 MDMS 设备提供的 NFS 共享。
{:tip}

- 使用 `CREATE EXTERNAL TABLE` 语句。
   - 选择 `FORMAT` = ”Text”
   - 为 {{site.data.keyword.dashdbshort_notm}} 团队提供用于导出的 `USING` 子句，以在 `LOAD` 过程中复用。


## 验证数据
{: #validate-data}

可以使用 `SELECT FROM` 语句以及外部表 `myfile` 和 `USING(....)` 子句在 Netezza 上重新读回数据，以确保数据正确。

**其他信息**

有关 PureData System for Analytics 的更多信息，请参阅 [IBM Netezza database user documentation ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/support/knowledgecenter/en/SSULQD_7.2.1/com.ibm.nz.dbu.doc/c_dbuser_plg_overview.html){:new_window}。