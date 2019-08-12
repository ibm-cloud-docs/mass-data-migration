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

# Migrando bancos de dados PureData System for Analytics para o {{site.data.keyword.dashdbshort_notm}}
{: #migrate-netezza-databases}

O {{site.data.keyword.mdms_full}} pode ser usado para migrar grandes bancos de dados IBM PureData System for Analytics (desenvolvidos com tecnologia Netezza) para o {{site.data.keyword.dashdbshort}}. É possível usar esse documento como uma referência para as ferramentas que determinam a quantia de dados a serem transferidos e os métodos de exportação.
{: shortdesc}

## Determinando o tamanho do objeto de banco de dados
{: #determine-db-object-size}

1. No [Suporte IBM > Fix Central > Netezza Tools ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www-945.ibm.com/support/fixcentral/options?selectionBean.selectedTab=find&selection=ibm%2fInformation+Management%3bPureData+System+for+Analytics%3bibm%2fInformation+Management%2fNetezza+Tools){:new_window}, faça download da versão apropriada do Netezza Tools que corresponde à sua instância do Netezza.

   Por padrão, as ferramentas de suporte são instaladas no servidor Netezza no diretório `/nz/support-IBM_Netezza<version>/bin`
   {:note}

2. Execute os dois comandos a seguir.
   - `nz_db_size` para determinar o tamanho do banco de dados

     ```
     nz_db_size
     Object | Name | Bytes | KB | MB | GB | TB
     -----------------------------------------------------------------------------------------------------------
     Appliance | cdcntze1 | 23,388,712,337,408 | 22,840,539,392 | 22,305,214 | 21,782.4 | 21.3
     Database | DHDB | 183,537,500,160 | 179,235,840 | 175,035 | 170.9 | .2
     Table | DH71964I1 | 880,803,840 | 860,160 | 840 | .8 | .0
     Table | DH71964T1 | 96,120,078,336 | 93,867,264 | 91,667 | 89.5 | .1
     Table | DH71964T10 | 9,615,179,776 | 9,389,824 | 9,170 | 9.0 | .0
     Table | DH71964T2 | 9,615,179,776 | 9,389,824 | 9,170 | 9.0 | .0
     Table | DH71964T3 | 9,615,179,776 | 9,389,824 | 9,170 | 9.0 | .0
     Table | DH71964T4 | 9,615,179,776 | 9,389,824 | 9,170 | 9.0 | .0
     Table | DH71964T5 | 9,615,179,776 | 9,389,824 | 9,170 | 9.0 | .0
     Table | DH71964T6 | 9,615,179,776 | 9,389,824 | 9,170 | 9.0 | .0
     Table | DH71964T7 | 9,615,179,776 | 9,389,824 | 9,170 | 9.0 | .0
     Table | DH71964T8 | 9,615,179,776 | 9,389,824 | 9,170 | 9.0 | .0
     Table | DH71964T9 | 9,615,179,776 | 9,389,824 | 9,170 | 9.0 | .0
     ```
     {: codeblock}

   - `nz_compressedTableRatio` para estimar o tamanho dos dados quando eles são descompactados.

      ```
      nz_compressedTableRatio
  ....................................................................................
      . The values below show the estimated size ratio of a compressed table to its .
      . uncompressed form. An uncompressed table is approximately <ratio> times larger .
      . than its compressed version. .
      . .
      . The 'Compressed Size' is the actual amount of storage being used by the table. .
      . The 'Uncompressed Size' is an estimate based on mathematical calculations. .
      ....................................................................................
      Database: DHDB
Table/MView Name Ratio Compressed Size Uncompressed Size Size Difference
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
Total For This Database 1.50 183,537,500,160 275,251,242,240 91,713,742,080
      ```
      {: codeblock}

## Extraindo dados e migrando
{: #extract-data}

É possível usar duas opções para extrair os dados do Netezza.
- Use o utilitário  ` nz_backup ` .
   ```
   /nz/support/contrib/bin/nz_backup –db   {db_name} –d  {target_directory}  ascii threads 4
   ```

   O `{target_directory}` é o compartilhamento NFS fornecido pelo dispositivo MDMS e montado nesse servidor.
   {:tip}

- Use a instrução  ` CREATE EXTERNAL TABLE ` .
   - Selecione  ` FORMAT `  = "Texto"
   - Forneça à equipe do {{site.data.keyword.dashdbshort_notm}} a cláusula `USING` que foi usada na exportação para a reutilização durante o processo `LOAD`.


## Validando Dados
{: #validate-data}

Os dados podem ser lidos novamente no Netezza usando a instrução `SELECT FROM` com a tabela externa `myfile` e uma cláusula `USING(....)` para assegurar que os dados estejam corretos.

** Informações adicionais **

Para obter mais informações sobre o PureData System for Analytics, consulte [Documentação do usuário do banco de dados IBM Netezza ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/en/SSULQD_7.2.1/com.ibm.nz.dbu.doc/c_dbuser_plg_overview.html){:new_window}.