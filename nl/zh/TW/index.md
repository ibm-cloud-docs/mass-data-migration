---

copyright:
  years: 2017-2018
lastupdated: "2018-04-26"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 開始使用 {{site.data.keyword.cloud_notm}} Mass Data Migration

## 要求裝置時需要的資訊

1. 儲存裝置的網路設定
   - 靜態 IP 位址
   - 啟用資料傳送的網路遮罩
2. 遠端電腦的網路設定
   - 靜態 IP 位址
   - 網路遮罩 
   - 用來存取使用者介面的預設閘道
3. Cloud Object Storage 下載目的地 <br/>
   **重要事項**：您在美國跨區域或美國南部位置必須至少具有一個 {{site.data.keyword.cos_full}} 帳戶及一個儲存區，才能完成要求表單。如果您尚未具有 {{site.data.keyword.cos_full_notm}}} 帳戶，請在要求 Mass Data Migration 裝置之前先建立一個帳戶。請參閱[關於 {{site.data.keyword.cos_full}}](https://console.bluemix.net/docs/services/cloud-object-storage/about-cos.html){:new_window}。

## 步驟 1：建立要求

1. 使用唯一的認證存取 [{{site.data.keyword.slportal}}](https://control.softlayer.com/){:new_window}。
2. 從「導覽列」中，選取**儲存空間** > **資料移轉** > **Mass Data Migration**，以存取 Mass Data Migration 登入頁面。
3. 按一下**要求裝置**鏈結，以開啟訂單表單。
4. 完成 **Mass Data Migration** 訂單表單中的每一個欄位。
   - **出貨地址**：此表單並未預先填入，而且每一個欄位都可編輯。請在「注意」欄位中提供接受裝置交付的人員的名稱。挑選交付地點時，請考量裝置的重量（加上外殼有 66 磅）及可存取性。<br/> （**附註**：此裝置配備輪子及用於操作的彈出式把手。）
   - **主要移轉聯絡人**：此表單並未預先填入。每一個欄位都可編輯。可以加入多個人。 
   - **資料中心網路配置**：提供網路配置詳細資料，以在出貨前於 Mass Data Migration 裝置上預先佈建 Eth3 埠。
   - **資料卸載目的地**：從下拉清單中選取現有目標帳戶。
   - **要求名稱**：輸入名稱，以協助您追蹤訂單。
5. 在讀取提供的每一份服務合約之後，請選取**我已閱讀並同意 Mass Data Migration 合約的完整條款**勾選框。
6. 按一下**工作區要求**，以提交「要求」。按一下**取消**，完全放棄表單並回到 Mass Data Migration 登入頁面。


## 步驟 2：備貨並出貨

提交要求之後，要求問題單的狀態會呈現為*正在處理要求*。「要求」處理完成後，{{site.data.keyword.IBM}} 就會開始預先配置下一個可用的裝置，而[要求](https://control.softlayer.com/storage/mdms){:new_window}網格上的狀態會顯示*正在準備裝置*，後面接著顯示*正在等待出貨*。

當訂單被接受且裝置正在準備中，[要求](https://control.softlayer.com/storage/mdms){:new_window}網格上的狀態就會顯示*正在準備裝置*，後面接著顯示*正在等待出貨*。「要求」進入*正在等待出貨* 狀態之後，就無法被取消。 

當裝置由快遞接收並運送到您的地點時，「要求」狀態就會更新為*裝置已出貨*。即會在[要求](https://control.softlayer.com/storage/mdms){:new_window}網格的**訂單詳細資料**區段中與您分享追蹤號碼。


## 步驟 3：接收並連接

1. 會為您預先配置裝置。包括基本的[電源/連線指示](user-instructions.html)。<br/>
  **附註**：個別提供使用者名稱及儲存區密碼。請檢查[要求](https://control.softlayer.com/storage/mdms){:new_window}網格中的**要求詳細資料**，以取得認證資訊。
2. 將瀏覽器指向您在訂單表單中提供的靜態 IP 位址。
3. 登入，提供密碼以解除鎖定空的儲存區。<br/>
   **附註**：請參閱[要求](https://control.softlayer.com/storage/mdms){:new_window}網格中的「要求詳細資料」，以取得密碼資訊。
4. 在伺服器上裝載 NFS 共用。
5. 重新執行 DataShuttle 庫存，以確定自應用程式擷取後所建立的全部新檔案。

## 步驟 4：汲取並退還
1. 執行 DataShuttle 複製，以移動資料。
2. 鎖定儲存區。
3. 溫和地關閉 Mass Data Migration 裝置。
4. 使用提供的運送標籤，裝箱運回 {{site.data.keyword.BluSoftlayer_full}} 資料中心。

當裝置回到 {{site.data.keyword.BluSoftlayer}} 時，要求狀態會變更為*已收到裝置*。 

## 步驟 5：卸載並存取

在傳送過程期間，要求狀態顯示會顯示為*正在卸載資料*。移轉至 {{site.data.keyword.objectstorageshort}}「儲存區」完成時（*卸載完成*），狀態會再次變更。在高速卸載至 Cloud Object Storage 儲存區已完成之後，您的資料就立即可供存取。

## 步驟 6：清除裝置

{{site.data.keyword.IBM}} 將實作 DOD 層級資料抹除需求，以永久清除裝置中的資料。已完成時，「要求」狀態將顯示*清除完成*。

## 其他附註

### 在儲存區中是唯一的

若要在物件名稱複製到儲存區時確保它們是唯一的，請在物件名稱字首中包括檔案路徑；複製到儲存區時，`/root/user/config.ini` 會變成 "root/user/config.ini"。

### 儲存區

如果目標儲存區不存在，則予以建立。如果它確實存在，則必須是空的，否則複製無法繼續進行。  

### 檔案系統

在掃描過程期間，會跳過「符號鏈結」及「硬鏈結」。