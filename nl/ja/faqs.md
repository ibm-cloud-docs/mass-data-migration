---

copyright:
  years: 2017, 2018
lastupdated: "2018-09-19"

---
{:new_window: target="_blank"}

# FAQ

## **{{site.data.keyword.cloud_notm}} 大量データ・マイグレーションとは何ですか?**

{{site.data.keyword.cloud}} 大量データ・マイグレーションは、120 TB の使用可能容量がある堅牢なポータブル・ストレージ・デバイスを使用して、テラバイト単位からペタバイト単位までのデータを {{site.data.keyword.cloud_notm}} に安全に移動する処理を高速で実行する物理データ転送サービスです。

<hr/>

## **大量データ・マイグレーションはどのように開始されますか?**

[{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window} を使用して要求を送信してください。 要求が承認され、処理が行われると、ネットワーク情報と配送先情報に基づいて次の利用可能なデバイスの構成が行われて、デバイスが配送されます。 このリンク (https://control.softlayer.com/storage/mdms) からすぐに開始できます。

<hr/>

## **なぜ大量データ・マイグレーションを使用するのですか?**

大量データ・マイグレーション・デバイスは、データ・センターやオフィスを始め、リモート・ロケーション、ウェアハウス、船舶など、ほぼすべての環境で実行できます。 コストや処理速度の点でネットワーク経由のデータ転送オプションが望ましくない場合や、そのようなオプションが利用できない場合にも、大量データ・マイグレーションを代替手段として活用できます。

<hr/>

## **大量データ・マイグレーションを使用してどれほどの量のデータを転送できますか?**

数テラバイトからペタバイト単位まで、転送可能なデータ量は実質的に無制限です。 1 台のデバイスの使用可能な容量は最大 120 TB ですが (RAID-6)、それを超えたワークロードにも複数のデバイスを使用して対応できます。 単一オブジェクトの最大サイズは 10 TB に制限されています。

<hr/>

## **120 TB を超えたワークロードを移動するために複数のデバイスを使用できますか? その場合は、どのような方法で使用できますか?**

複数のデバイスを並列または直列で使用して、すべてのデータを 1 回のマイグレーションで移動することも、1 台のデバイスでマイグレーションを反復的に実行することもできます。 例えば、1 PB のデータ転送に 9 台のデバイスを並列で使用することも、1 台のデバイスを使用してマイグレーションを 9 回実行することもできます。

<hr/>

## **データの転送にどれほどの時間がかかりますか?**

お客様が大量データ・マイグレーション要求を送信してから {{site.data.keyword.cos_full}} バケットでお客様のデータを利用できるようになるまでのターンアラウンド・タイムは、最短で 7 日程度です。 転送効率は、転送するファイルの数によって影響されます。 数百万個の小さなファイルを転送するときは、比較的少数のファイルに同じ量のデータを入れて転送するときより長い時間がかかります。

<hr/>

## **大量データ・マイグレーション・デバイスをどれほどの期間置いておくことができますか?**

最初の 10 営業日の間は、無料でデバイスをサイトに置いておくことができます。この時間フレームに、デバイスの配送日や受け取り日は含まれません。この期間内にデータの取り込みが完了しない場合は、1 日あたり 30 USD で使用期間を延長できます (米国と EU の地域が対象です)。

<hr/>

## **大量データ・マイグレーションはどんなネットワーク・インターフェースに対応していますか?**

大量データ・マイグレーション・デバイスには、10 Gbps のネットワーク・インターフェースと、RJ45 (CAT6a) と SFP+ 銅線に対応したネットワーク・ポートがあります。 RJ45 から SFP+ へのコンバーターが同梱されています。10 Gbps インターフェースではジャンボ・フレームが有効になっています。

<hr/>

## **大量データ・マイグレーションのデフォルトの配送オプションはどういうものですか?**

すべての大量データ・マイグレーション・デバイスで、UPS Next Day Air の往復配送を利用します。配送料は、デバイス 1 台あたり 395 USD という均一の低料金の中に含まれています。 現在は、お客様が別の配送方法を選択することはできません。

<hr/>

## **大量データ・マイグレーションを利用できるのは、どの地域ですか?**

大量データ・マイグレーションを利用できる地域は、米国と EU だけです。 すべてのデータがサービスの US Standard Cross Region か EU Cross Region の層にある {{site.data.keyword.cos_full}} にマイグレーションされます。 配送元とは別の地域にデバイスを返却することはできません。

<hr/>

## **データを {{site.data.keyword.cloud_notm}} にインポートするためにどの程度の費用がかかりますか?**

{{site.data.keyword.cloud_notm}} へのデータ転送は無料です。

<hr/>

## **大量データ・マイグレーションを使用してデータを {{site.data.keyword.cloud_notm}} からエクスポートできますか?**

現在は、大量データ・マイグレーションでは {{site.data.keyword.cloud_notm}} からのデータのエクスポートはサポートされていません。

<hr/>

## **大量データ・マイグレーションではデータが暗号化されますか?**

大量データ・マイグレーションでは、すべてのデータが AES 256 ビットで暗号化されます。強力なパスワードでストレージ・プールのロックを解除する機能もあります。 {{site.data.keyword.IBM}} では、すべてのデータ転送が SSL で行われます。

<hr/>

## **大量データ・マイグレーションの物理的な面でのデータ保護はどうなっていますか?**

すべての大量データ・マイグレーション・デバイスは、耐久性のある堅牢な筐体に入っています。 この収納ケースは、耐水設計、耐衝撃設計、改ざんの証拠を残す設計になっていて、配送の往復時にもデバイスとデータのセキュリティーが確保されています。

<hr/>

## **マイグレーション・プロセス全体で要求をどのように追跡管理できますか?**

要求の状況を追跡管理する場合は、[{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window} の大量データ・マイグレーションのページにあるアクティブ要求のセクションを参照してください。 このリンク (https://control.softlayer.com/storage/mdms) を使用して、ポータルにサインインできます。

<hr/>

## **データは {{site.data.keyword.cos_full_notm}} にオフロードされた後、どのように消去されますか?**

{{site.data.keyword.cos_full}} へのデータ・オフロードが完了すると、{{site.data.keyword.IBM}} はすぐに 4 パスの DOD レベルのデータ・ワイプを開始して、デバイスからデータを永久的に消去します。

<hr/>

## **ファイル・インターフェースとは何ですか?**

大量データ・マイグレーション・デバイスでは、デフォルトで、ネットワーク・ファイル・システム (NFS) と Server Message Block (SMB) が有効になった状態のファイル共有が含まれています。

<hr/>

## **ファイル・インターフェースはどのように使用されますか?**

最初に、暗号化プールのロックを解除します。 その後、マイグレーションするデータが入っているサーバーに共有をマウントします。その共有にデータ・ファイルをコピーする操作を開始します。

<hr/>

## **大量データ・マイグレーションのファイル・インターフェースにはどんなメリットがありますか?**

このファイル・インターフェースは、安定したファイル/ネットワーク・ソフトウェアに基づいているので、多数の巨大なファイルをコピーして {{site.data.keyword.cloud_notm}} に転送できます。

<hr/>

## **大量データ・マイグレーション・デバイスではファイルがどのように保管されますか?**

大量データ・マイグレーション・デバイスでは、ZFS ファイル・システムを使用しています。LZ4 の圧縮機能と AES 256 ビットの暗号化機能が付いています。

<hr/>

## **米国の場合、大量データ・マイグレーションの使用料はいくらですか?**

米国では、デバイス 1 台あたり 395 USD という均一料金になっています。 この費用の内訳は、デバイスの料金が 295 USD、UPS Next Day Air の往復配送料金が 100 USD です。この料金で、10 営業日の間、お客様のサイトでご利用いただけます。

<hr/>

## **{{site.data.keyword.cos_full_notm}} を使用するための費用はいくらかかりますか?**

{{site.data.keyword.cloud_notm}} へのデータ転送は無料です。 ただし、{{site.data.keyword.cos_full}} や他の {{site.data.keyword.cloud_notm}} サービスでデータを保管するための標準料金が発生します。 Standard Cross Region での {{site.data.keyword.cos_full}} の価格設定については、このリンク (https://www.ibm.com/cloud-computing/bluemix/pricing-object-storage#s3api) を参照してください。

<hr/>

## **{{site.data.keyword.cloud_notm}} 大量データ・マイグレーション・デバイスの購入は可能ですか?**

{{site.data.keyword.cloud_notm}} 大量データ・マイグレーションは販売していません。