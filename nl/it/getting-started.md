---

copyright:
  years: 2017, 2019
lastupdated: "2019-02-05"

---
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:DomainName: data-hd-keyref="DomainName"}

# Introduzione a {{site.data.keyword.cloud_notm}} Mass Data Migration
{: # GettingStarted}

**Prerequisiti**

Recupera queste informazioni prima di inoltrare una richiesta di Mass Data Migration e completare la migrazione.

1. Impostazioni di rete per il dispositivo di archiviazione
   - Indirizzo IP statico
   - Maschera di rete per abilitare il trasferimento dati
2. Impostazioni di rete per il computer remoto
   - Indirizzo IP statico
   - Maschera di rete
   - Gateway predefinito per accedere all'interfaccia utente
3. Destinazione di download di Cloud Object Storage <br/>

   Per completare il modulo di richiesta, devi disporre di almeno un account {{site.data.keyword.cos_full}} e di un bucket in più regioni dell'UE o degli Stati Uniti standard. Se non hai ancora un account {{site.data.keyword.cos_full_notm}}}, creane uno prima di richiedere il dispositivo Mass Data Migration. Fai riferimento a [Informazioni su {{site.data.keyword.cos_full}}](/docs/services/cloud-object-storage?topic=cloud-object-storage-about-ibm-cloud-object-storage){:new_window}.
   {:important}

## Creazione di una richiesta

1. Esegui l'accesso alla [console IBM Cloud](https://{DomainName}/){:new_window} e fai clic sull'icona di menu nell'angolo superiore sinistro. Seleziona **Infrastructure**.

   In alternativa, puoi eseguire l'accesso alla [console {{site.data.keyword.cloud_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/catalog/){:new_window}.
2. Seleziona **Storage** > **Data Migration** > **Mass Data Migration** dalla barra di navigazione per accedere alla pagina di destinazione di Mass Data Migration.
3. Fai clic su **Request Device** per aprire il modulo d'ordine.
4. Completa ogni campo nel modulo d'ordine di **Mass Data Migration**.
   - **Shipping address** - questo modulo non è precompilato e ogni campo è modificabile. Fornisci il nome della persona che accetterà la consegna del dispositivo nel campo Attention. Quando scegli il luogo di consegna, considera il peso del dispositivo (66 libbre con la sua custodia) e l'accessibilità.

   Il dispositivo è dotato di ruote e maniglia a scomparsa per la manovra.
   {:note}

   - **Key migration contacts** - questo modulo non è precompilato. Ogni campo è modificabile. È possibile aggiungere più di una persona.
   - **Data center network configuration** - Fornisci i dettagli di configurazione di rete per il pre-provisioning della porta Eth3 sul dispositivo Mass Data Migration prima della spedizione.
   - **Data offload destination** - seleziona il tuo account di destinazione esistente dall'elenco.
   - **Request name** - immetti un nome per aiutarti a tracciare il tuo ordine.
5. Seleziona la casella di spunta **I have read and agree to the full terms of the Mass Data Migration Agreement** dopo aver letto ciascun accordo di servizio.
6. Fai clic su **Place Request** per inviare la richiesta. Fai clic su **Cancel** per abbandonare completamente il modulo e tornare alla pagina di destinazione di Mass Data Migration.


## Preparazione e spedizione

Dopo aver inviato la richiesta, lo stato per il ticket di richiesta viene visualizzato come `Processing Request`. Quando la tua richiesta viene accettata, {{site.data.keyword.IBM}} inizia la pre-configurazione del successivo dispositivo disponibile.

Quando il dispositivo è in fase di preparazione, lo stato nella pagina [Requests ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://control.softlayer.com/storage/mdms){:new_window} mostra `Prepping Device` seguito da `Awaiting Shipment`. Dopo che la tua richiesta entra nello stato `Awaiting Shipment`, non può più essere annullata.

Quando il dispositivo viene prelevato dal corriere per essere inviato alla tua posizione, lo stato della richiesta viene aggiornato a `Device Shipped`. Il numero di tracciabilità viene condiviso con te nella sezione **Order Details** della pagina [Requests ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://control.softlayer.com/storage/mdms){:new_window}.


## Ricezione e collegamento

1. Il dispositivo arriva preconfigurato per te. Vengono incluse [istruzioni di alimentazione e connettività](user-instructions.html) di base. <br/>

   Il nome utente e la password del pool di archiviazione vengono forniti separatamente. Controlla i dettagli della richiesta (**Request Details**) nella tua pagina [Requests ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://control.softlayer.com/storage/mdms){:new_window} per le credenziali.
   {:note}
2. Punta il browser all'indirizzo IP statico che hai fornito nel modulo d'ordine.
3. Accedi e immetti la password per sbloccare il pool di archiviazione vuoto. <br/>

   Vedi i dettagli della richiesta (Request Details) della tua pagina [Requests ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://control.softlayer.com/storage/mdms){:new_window} per la password.
   {:tip}
4. Monta la condivisione file NFS sul tuo server.
5. Esegui di nuovo l'inventario di DataShuttle per assicurarti che gli eventuali nuovi file vengano catturati.

## Spostamento dei dati
1. Esegui la copia di DataShuttle per spostare i dati.
2. Blocca il pool di archiviazione.
3. Spegni normalmente il dispositivo Mass Data Migration.
4. Rispedisci la scatola al data center {{site.data.keyword.BluSoftlayer_full}} utilizzando l'etichetta di spedizione fornita.

Quando il dispositivo viene restituito a {{site.data.keyword.BluSoftlayer}}, lo stato della richiesta cambia in `Device Received`.

## Scaricamento e accesso

Durante il processo di trasferimento, lo stato della richiesta viene visualizzato come `Offloading Data`. Lo stato cambia di nuovo quando la migrazione al bucket di {{site.data.keyword.objectstorageshort}} viene completata (`Offload Complete`). I tuoi dati sono immediatamente accessibili una volta completato lo scaricamento ad alta velocità nel tuo bucket di Cloud Object Storage.

## Cancellazione del dispositivo

{{site.data.keyword.IBM}} implementa requisiti di cancellazione dei dati a livello DOD per cancellare in modo permanente i tuoi dati dal dispositivo. Al termine, lo stato della tua richiesta visualizza `Erase Complete`.