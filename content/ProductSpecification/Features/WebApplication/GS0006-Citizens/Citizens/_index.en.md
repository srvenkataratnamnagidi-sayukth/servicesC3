---
title: Citizens
tags : ["Composing"]
---

## Introduction
Citizens are one of the features of our software product. Details of every person in a panchayat is created and saved in citizens block. Users should have permission to access this feature.

## Business Assumptions
Creating, updating and removing the citizens can be done at the run time based on the requirement.

## Requirements
### Functional Requirements
Only panchayat level users should create, update, remove, or view the citizens.

### Non-functional Requirements
The system can support any number of citizens but this design will limit 3,00,00,000 citizens for this system. Beyond the 3,00,00,000 citizens may experience performance issues. 


### Problem Statement
Identity, education details, employment details of a citizen in a panchayat should be captured.

### Design 
1. We can Create, Update, View, and remove the citizens.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_citizen_create|To create the citizen|
|uc_citizen_update|To update the citizen|
|uc_citizen_remove|To remove the citizen|
|uc_citizen_view|To view the citizen|
|uc_citizen_search|To search the citizen|
|uc_citizen_export|To export the citizen in 2 formats Excel, PDF|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|Aadhaar Number|YES|NA|Allowed 0-9 and length should be 12|@Column(name = "aid", length = 12, nullable = false)|aid varchar(12) not null |YES|NO|YES|YES|YES|YES||
|Name|YES|NA|Allowed a-z = A-Z = 0-9 = _ = - and length 3 to 64|@Column(name = "name", length = 64, nullable = false)|name varchar(64) not null|YES|YES|YES|YES|YES|YES||
|Surname|YES|NA|Allowed a-z = A-Z = 0-9 = _ = - and length 3 to 32|@Column(name = "surname", length = 32, nullable = false)|surname varchar(32) not null|YES|YES|YES|YES|YES|YES||
|Father / Spouse Name|YES|NA|Allowed a-z , A-Z , 0-9 , _ , -, .,/,:, Space and length 3 to 64|@Column(name = "fsname", length = 64, nullable = false)|fsname varchar(64) not null|YES|YES|YES|YES|NO|NO||
|Mobile Number|YES|NA|Allowed 0-9 and length should be 10|@Column(name = "mobile", length = 13, nullable = false)|mobile varchar(13) not null |YES|YES|YES|YES|YES|YES||
|Gender|YES|NA|Drop Down List|@Column(name = "gender", length = 8, nullable = false)|gender varchar(8) not null |YES|YES|YES|YES|NO|NO||
|Date Of Birth|YES|NA|Date dd-MM-YYYY|@Column(name = "dob", nullable = false)|dob datetime not null|YES|YES|YES|YES|NO|NO||
|Marital Status|YES|NA|Drop Down List|@Column(name = "married", length = 16, nullable = false)|married varchar(16) not null |YES|YES|YES|YES|NO|NO||
|Email|YES|NA|Allowed a-z = A-Z = 0-9 = @ and length 3 to 64|@Column(name = "email", length = 64, nullable = true)|email varchar(64) default null|YES|YES|YES|YES|NO|NO||
|Religion|YES|NA|Drop Down List|@Column(name = "religion", length = 16, nullable = false)|religion varchar(16) not null |YES|YES|NO|YES|NO|NO||
|Caste Category|YES|NA|Drop Down List|@Column(name = "caste_cat", length = 8, nullable = false)|caste_cat varchar(8) not null |YES|YES|YES|YES|YES|YES||
|Sub Caste|YES|NA|Drop Down List|@Enumerated(EnumType.STRING) @Column(name = "caste_group_type", length = 6, nullable = true)|caste_group_type varchar(6) default null |YES|YES|YES|YES|NO|NO||
|Caste|YES|NA|Drop Down List|@Column(name = "caste", length = 64, nullable = true)|caste varchar(64) default null |YES|YES|YES|YES|NO|NO||
|Education Status|YES|NA|Drop Down List|@Column(name = "edu_status", length = 16, nullable = false)|edu_status varchar(16) not null |YES|YES|YES|YES|YES|YES||
|Education Qualification|YES|NA|Drop Down List|@Column(name = "edu_qual", length = 16, nullable = false)|edu_qual varchar(16) not null |YES|YES|YES|YES|YES|NO||
|Occupation|YES|NA|Drop Down List|@Column(name = "emp_occ", length = 16, nullable = false)|emp_occ varchar(16) not null |YES|YES|YES|YES|YES|YES||
|Relationship With Family Head|YES|NA|Drop Down List|@Column(name = "rel_head", length = 16, nullable = false)|rel_head varchar(16) not null |YES|YES|YES|YES|NO|NO||
|Disability Type|YES|NA|Drop Down List|@Column(name = "spl_status", length = 6, nullable = false)|spl_status varchar(6) not null |YES|YES|YES|YES|NO|NO||
|Long Disease Type|YES|NA|Drop Down List|@Column(name = "long_disease", length = 24, nullable = false)|long_disease varchar(24) not null |YES|YES|YES|YES|NO|NO||
|Long Disease Type|YES|NA|Drop Down List|@Column(name = "long_disease", length = 24, nullable = false)|long_disease varchar(24) not null |YES|YES|YES|YES|NO|NO||
|Health Card Used|YES|False|Boolean|@Column(name = "healthcard_used", nullable = false)|healthcard_used boolean default null |YES|YES|YES|YES|NO|NO||
|General Insurance|YES|False|Boolean|@Column(name = "gen_insurance", nullable = false)|gen_insurance boolean default null |YES|YES|YES|YES|NO|NO||
|Medical Insurance|YES|False|Boolean|@Column(name = "health_insurance", nullable = false)|health_insurance boolean default null |YES|YES|YES|YES|NO|NO||
|Updated Reason|YES|NA|Allowed a-z, A-Z, 0-9, space, _ , - , . and length 6 to 256|@Column(name = "update_comment", nullable = true)|update_comment varchar(255) DEFAULT NULL|NO|YES|NO|YES|NO|NO||
|Removed Reason|YES|NA|Allowed a-z, A-Z, 0-9, space, _ , - , . and length 6 to 256|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|NO|YES|YES|NO|NO||

#### ENUM CONSTANTS

##### Gender

{{<mermaid align="left">}}
classDiagram
    class Name{
      MALE
      FEMALE
      OTHER
    }
{{< /mermaid >}}

##### Marital Status

{{<mermaid align="left">}}
classDiagram
    class Name{
      SINGLE
      MARRIED 
      DIVORCED 
      WIDOWED
      SEPERATED
      SPOUSE_DEAD
      LIVING_RELATION
    }
{{< /mermaid >}}

##### Religion

{{<mermaid align="left">}}
classDiagram
    class Name{
      HINDU
      ISLAM 
      CHRISTIAN 
      BUDDHIST
      SIKH
      JAIN
      PARSI
      ATHEIST
      TRIBAL
      NOT_KNOWN
      CONFIDENTIAL
      NONE
      OTHERS
    }
{{< /mermaid >}}

##### Caste Category

{{<mermaid align="left">}}
classDiagram
    class Name{
      OC
      BC
      SC
      ST
      MINORITY
      OTHERS
      NONE
    }
{{< /mermaid >}}

##### Sub Caste

{{<mermaid align="left">}}
classDiagram
    class Name{
      BC_A
      BC_B
      BC_C
      BC_D
      BC_E
      NONE
    }
{{< /mermaid >}}

##### Caste
##### OC
{{<mermaid align="left">}}
classDiagram
    class Name{
      ADI_SAIVA
      ADI_VELAMA
      AHEER_GOULI
      AKUTHOTA_REDDY
      ARAVA_KOMATI
      ARCHAKA_BRAHMIN
      BALIJA
      BALIJA_KOMATI
      NATTI_KOTTAICHETTY
      BERI_KOMATI
	  BHOOMANCHI_REDDY
	  BOHARA
	  BOHRA
	  BRAHMAN
	  BURGAM_KALINGA
	  CHITTEPU_KAPU
	  KULLA_KADAGI
	  CUTCHI_MENON
	  DASARI_GOLLA
	  DESAI_REDDY
	  DESUR_REDDY
   	  DHEEMARI_KAPU
   	  DHOMMARI_REDDY
   	  DORA
   	  EZHAVA
   	  GAJULA_BALIJA
   	  GANJAM_REDDY
   	  GAVARA_KOMATI
   	  GODUGULANATI_KAPU
   	  GONA_VELAMA
   	  GONE_REDDY
   	  GOPATHI_BALIJA
	  GOPITA_BALIJA
	  GOSWAMY
	  GOUDA_SETTI
	  GOULI
	  GOWDAS
	  GUDATI_REDDY
	  GUDETI_GONEKAPU
	  GULA
	  ILLELA_REDDY
	  IRANI
	  ISSAI_VELLALAR
	  JAISWAL
	  JAMAYAT
	  JANNI
	  JAT
	  JETTY
	  KAMMA
	  KAPU
	  KAPU_VELAMA
	  KARUNEEGAR
	  KARANAM
	  KANNAKKAPILLAI
	  KHANDAYATA
	  KODITHI_KAPU
	  KODRAS
	  KONDA_VETAGANDLU
	  KONDETI_BALIJA
	  KSHATRIYA
	  THUGATAVEERA_KSHATRIYA
	  KUNBI
	  KUNITIMALLAREDDY
	  KURUVA_KAPU
	  LINGA_BALIJA
	  LONARI_SAMAJ
	  MAILARLA
	  MAJJULA
	  MALAYALA_KSHATRIYA
	  MALLIKARJUNA
	  MORUSU_KAPU
	  KAPU_GOUDA
	  MOTATI_REDDY
	  MUGHAL
	  MOGHAL
	  MULA_TELAGA
	  MUSTIGOLLA
	  MUSUGU_BALIJA
	  MUSUGU_KAPU
      NADAL_REDDY
      NADAR
      NADI_TARAM_REDDY
	  NAIKOTI
	  MANNEVARU
	  NALLELAMA
	  NALLEVELAMA_KAPU
	  NANI_KONDA_REDDY
	  NAVAYATH
	  NERAVATI_REDDI
	  NEYYALA
	  ONTARI
	  ORUGANTI_REDDY
	  PAALA_KAPU
	  PAKANATI_KAPU
	  PAKANATI_REDDY
	  PANASA
	  PANTAAKAPU
	  PANTA_REDDY
	  PEDAKANTI_KAPU
	  PEDAKANTI_REDDY
	  POKANATI_REDDY
	  POKANATI_KAPU
	  PONNETI_VELAMA
	  RAJAMAHENDRAM_BALIJA
	  RAJU_KSHATRIYA
	  RAMJOSHI
	  REDDY_GANDLA
	  RENATI_REDDY
	  ROWLAS
	  SAJJANA_KAPU
	  SAJJANA_REDDY
	  SAMJOGI
	  SANCHARA_BHAVAJI
	  SAROLLU
	  SETTY_BALIJA
	  SIKHS
	  SONNAILU
	  SOURASHTRA
	  SUGAMANCHI_REDDY
	  TELAGA
	  TELI
	  TELUGU
	  TENUGOLLU
	  THOLAGARI
	  THURUPU_CHALUKYA_KAPU
	  TIYORA
	  TEERA
	  TOLUBOMMALATAVALLU
	  TRIVARNIKA
 	  UPPU_BALIJA
 	  VADDI
 	  VAIKHANASA
 	  VALLUVA
 	  VALLUVAR
 	  VALLUVAN
 	  VALLUVA_NAYANAR
 	  VANNIA_OR_VANNIAR
 	  VARANASI_REDDY
 	  VEGINA_KOMATI
 	  BUKKA_KOMATI
 	  JANAPASETTY
	  VELAMA_KAPU
	  VELAMA_MUDALIAR
	  VELAMA
	  PEDDA
	  PADMA_NAYAKA_VELAMA
	  VELANATI_REDDY
	  VISAKHAPATNAM_REDDY
	  RAYALASEEMA_REDDY
	  VYSYA_VALLUVA_PANDARI
	  VALLUVA_SATANI
	  VALLUVA_DASARI
	  YANADI_VELAMA
	  YENATI_VELAMA
	  YENATI_POLINATI_VELAMA_DORA
	  YERLAM_KAPU
    }
{{< /mermaid >}}

##### BC_A

{{<mermaid align="left">}}
classDiagram
    class Name{
      AGNIKULA_KSHATRIYA
      PALLI 
      VADABALIJA 
      BESTHA 
      JALARI 
      GANGAVARU  
      GANGA_PUTRA
      GOONDLA 
      VANYA_KULA_KSHATRIYA 
      NEYYALA
      PATTAPU 
      BALA_SANTHU
      BAHURUPI 
      BANDARA 
      BUDA_BUKKALA 
      RAJAKA 
      DASARI 
      DOMMARA 
      GANGIREDDLAVARU
      JANGAM
      JOGI 
      KATIPAPALA 
      KORCHA 
      MEDARI_OR_MAHENDRA
      MONDI_VARU 
      MONDI_BANDA 
      BANDA 
      NAYI_BRAHMIN 
      NAYEEBRAHMIN  
      VAMSHA_RAJ 
      PICHIGUNTLA 
      PAMULA	 
      PARDHI 
      PAMBALA 
      PEDDAMMAVANDLU 
      YELLAMMAVANDLU 
      DEVARAVANDLU 
      MUTYALAMMAVANDLU
      DAMMALI  
      DAMMALA 
      DAMMULA 
      DAMALA 
      VEERA_MUSTHI
      VEERA_BHADREEYA 
      VALMIKI_BC_A 
      BOYA 
      TALAYARI
      CHUNDUVALLU  
      GUDALA 
      KANJARA_BHATTA 
      KALINGA 
      KEPMARE 
      REDDIKA 
      MONDI_PATTA 
      NOKKAR 
      PARIKI_MUGGULA 
      YATA 
      CHOPEMARI 
      KAIKADI 
      JOSHINANDIWALAS 
      ODDE 
      MANDULA
      MEHTAR 
      KUNAPULI 
      PATRA 
      KURAKULA 
      PONDARA 
      SAMANTHULA 
      SAMANTHA 
      SOUNTIA 
      SAUNTIA  
      PALA_EKARI 
      EKILA_VYAKULA 
      EKIRI 
      NAYANIVARU 
      PALEGARU 
      TOLAGARI
      KAVALI 
      RAJANNALA 
      RAJANNALU
      BUKKA_AYAVAR   
      GOTRALA 
      KASIKAPADI 
      KASIKAPUDI 
      SIDDULA 
      SIKLIGAR 
      SAIKALGAR 
      POOSALA
      AASADULA 
      ASADULA 
      KEUTA 
      KEVUTO
      KEVITI
      }
{{< /mermaid >}}

##### BC_B

{{<mermaid align="left">}}
classDiagram
    class Name{
      ACHUKATLAVANDLU
      ARYAKSHATRIYA
      CHITTARI
      GANIYAR
      CHITRAKARA
      NAKHAS
      DEVANGA
      GOUD
      SETTIBALIJA_BC_B
      SRISAYANA
      DUDEKULA
      LADDAF
      PINJARI
      NOORBASH
      GANDLA
      TELIKULA
      DEVATILAKULA
      SENGNATEN
      SENGUNTLA
      JANDRA
      KUMMARA
      KULALA
      SALIVAHANA
      KARIKALABHAKTHULU
      KAIKOLAN_OR_KAIKALA
      KARNABHAKTHULU
      KURUBA_OR_KURUMA
      NAGAVADDILU
      NEELAKANTHI
      PATKAR
      PERIKA
      NESSI_OR_KURNI
      PADMASALI
      SWAKULASALI
      THOGATA
      THOGATI_THOGATA_VEERAKSHATRIYA
      VISWABRAHMIN
      VISWAKARMA
      KUNCHITIVAKKLIGA
      VAKKALIGARA
      KUNCHITIGA
      LODH
      LODHI
      LODHA
      BONDILI
      AREMARATHI
      MARATHA
      ARAKALIES
      SURABI_NATAKALAVALLU
      NEELI
      BUDUBUNJALA
      BHUNJWA
      BHADUHUNJA
      GUDIA
      GUDIYA
    }
{{< /mermaid >}}

##### BC_C

{{<mermaid align="left">}}
classDiagram
    class Name{
      CHRISTIANS
    }
{{< /mermaid >}}

##### BC_D

{{<mermaid align="left">}}
classDiagram
    class Name{
      AGARU
      AREKATIKA
      KATIKA
      ARE_SURYAVAMSHI
      ATAGARA
      BHATRAJU
      CHIPPOLU
      GAVARA
      GODABA
      HATKAR
      JAKKALA
      JINGAR
      KANDRA
      KOSHTI
      KACHI
      SURYABALIJA 
	  KALAVANTHULA
	  GANIKA
	  KRISHNA_BALIJA
	  KOPPULA_VELAMA
	  KOPPALA_VELAMA
	  MATHURA
	  MALI
	  MUDIRAJ
	  MUTRASI
	  TENNGOLLU
	  MUNNURU_KAPU
	  NAGAVAMSAM
	  POLINATIVELAMA
	  PASSI
	  RANGAREZBHAVASARA_KSHATRIYA
	  RANGARIJU
	  SADHU_CHETTY
	  SATANI
	  TAMMALI
	  TAMBALI
	  ADISAIVA
	  TURUPUKAPUS_OR_GAJULAKAPUS_BC_D
	  UPPARA
	  SAGARA
	  VANJARA
	  YADAVA
	  ARE
	  AREVALLU_ARAOLLU
	  SADARA
	  SADARU
	  ARAVA
	  AYYARAKA
	  NAGARALU
	  AGHAMUDIAN
	  AGHAMUDIAR
	  BERIVYSYA
	  BERI_CHETTI
	  ATIRASA
	  SONDI
	  SUNDI
	  VARALA
	  SISTAKARNAM
	  LAKKAMARIKAPU
	  VEERA_SHAIVA_LINGAYAT
	  KURMI, KALINGA_KOMATI
	  KALINGA_VYSYA      
    }
{{< /mermaid >}}

##### BC_E

{{<mermaid align="left">}}
classDiagram
    class Name{
      ACHUKATTLAVANDLU 
      SINGALI 
      SINGAMVALLU 
      ACHUPANIVALLU 
      ACHUKOTTU_VARU 
      ACHUKATLAVANDLU 
      ATTAR_SAIBULU 
      ATTAROLLU 
      DHOBI_MUSLIM
      MUSLIM_DHOBI
      DHOBI_MUSALMAN 
      TURAKA_CHAKALA
      TURAKA_SAKALA
      TURAKA_CHAKALI
      TULUKKA_VANNAN
      TSAKALAS_OR_CHAKALAS
      MUSLIM_RAJAKAS
      FAQIR
      FHAKIR
      BUDBUDKI 
	  GHANTI_FHAKIR
	  GHANTA_FHAKIRLU
	  TURAKA_BUDBUDKI
	  DARVESH
	  FAKEER
	  GARADI_MUSLIM
	  GARADI_SAIBULU
	  PAMULAVALLU
	  KANIKATTU_VALLU
	  GARADOLLU
	  GARADIGA	
	  GOSANGI_MUSLIM
	  PAKEER_SAYEBULU
	  GADDI_ELUGUVALLU
	  ELUGU_BANTUVALLU
	  MUSALMAN_KEELU_GURRALAVALLU
	  HAJAM
	  NAI
	  NAI_MUSILIM_NAVID
	  LABBI
	  LABBAI
	  LABBA
	  LABBON
	  PAKEERLA
	  BOREWALE
	  DEERA_PHAKIRLU
	  BONTHALA
	  QURESHI
	  KURESHI
	  KHURESHI
	  KHASAB
	  MARATIKHASAB
	  MUSLIMKATIKA
	  KHATIK_MUSLIM
	  SHAIK
	  SHEIKH
	  SIDDI
	  YABA
	  HABSHI
	  JASI
	  TURAKA_KASHA
	  KAKKUKOTTEZINKA_SAIBULU
	  CHAKKITA_KANEVALE
	  TERUGADU_GONTALAVARU
	  THIRUGATI_GANTLA
	  ROLLUKU_KAKKU_KOTTEVARU
	  PATTAR_PHODULU
	  CHAKKAETAKARE
	  THURAKA_KASHA
    }
{{< /mermaid >}}

##### Scheduled Castes

{{<mermaid align="left">}}
classDiagram
    class Name{
      ADI_ANDHRA
      ADI_DRAVIDA
      ANAMUK
      ARAYMALA
      ARUNDHATIYA
      ARWA_MALA
      BARIKI
      BAVURI
      BEDA_SC
      BINDLA
      BAYAGARA
      BAYAGARI
      CHACHATI
      CHALAVADI
      CHAMAR
      MOCHI
      MUCHI
      CHAMBHAR
      CHANDALA
      DAKKAL
      DOKKALWAR
      DAMDASI
      DHOR
      DOM
      DOMBARA
      PAIDI
      PANO
      ELLAMMALAWAR
      ELLAMMALA_WANDLU
      GHASI
      HADDI
      RELLI
      CHAMCHANDI
      GODAGALI
      GODAGULA_SC
      GODARI
      GOSANGI
      HOLEYA
      HOLEYA_DASARI
      JAGGALI
      JAMBUVULU
      KOLUPUL_VANDLU
      PAMBADA 
	  PAMBANDA
	  PAMBALA
	  MADASI_KURUVA
	  MADARI_KURUVA
	  MADIGA
	  MADIGA_DASU
	  MASHTEEN
	  MAHAR
	  MALA
	  MALA_AYAWARU
	  MALA_DASARI
	  MALA_DASU
	  MALA_HANNAI
	  MALA_JANGAM
	  MALA_MASTI
	  MALA_SALE
	  NETHANI
	  MALA_SANYASI
	  MANG
	  MANG_GARODI
	  MANNE
	  MASHTI
	  MATANGI
	  MEHTAR
	  MITHA_AYYALVARU
	  MUNDALA
	  PAKY
	  MOTI
	  THOTI
	  PAMIDI
	  PANCHAMA
	  PARIAH
	  SAMAGARA
	  SAMBAN
	  SAPRU
	  SINDHOLLU
	  CHINDOLLU
	  YATALA
	  VALLUVAN
    }
{{< /mermaid >}}

##### Scheduled Tribes

{{<mermaid align="left">}}
classDiagram
    class Name{
      ANDH
      SADHU_ANDH
      BAGATA
      BHIL
      CHENCHU
      GADABAS
      BODO_GADABA
      GUTOB_GADABA
      KOLLAYI_GADABA
      PARANGI_GADABA
      KATHERA_GADABA
      KAPU_GADABA
      GONDA
      GOUDU_ST
	  HILL_REDDIS
	  JATAPUS
	  KAMMARA
	  KATTU_NAYAKAN
	  KOLAM
	  KOLAWAR
	  KONDA_DHORA
	  KUBIS
	  KONDA_KAPUS
	  KONDA_REDDIS
	  KONDHS
	  KODI
	  KODHU
	  DESAYA_KONDHS
	  DONGRIA_KONDHS
	  KUTTIYA_KONDHS
	  TIKIRIA_KONDHS
	  YENITY_KONDHS
	  KUVINGA
	  KOTIA
	  BENTHO_ORIYA
	  BARTIKA
	  DULIA
	  HOLVA
	  SANRONA
	  SIDHO_PAIKO
	  KOYA
	  DOLI_KOYA 
	  GUTTA_KOYA
	  KAMMARA_KOYA
	  MUSURA_KOYA
	  ODDI_KOYA
	  PATTIDI_KOYA
	  RAJAH
	  RASHAKOYA
	  LINGA_DHARI_KOYA
	  KOTTU_KOYA
	  BHINE_KOYA
	  RAJKOYA
	  KULIA
	  MALIS_ST
	  MANNA_DORA
	  MUKHADORA
	  NOOKA_DHORA
	  NAYAKS_ST
	  PARDHAN
	  PORJA
	  PARANGI_PERJA
	  REDDI_DHORAS
	  RONA_RENA
	  SAVARAS
	  SUGALIS
	  LAMBADIS
	  BANJARA
	  THOTI_ST   
	  VALMIKI_ST
	  YENADIS
	  CHELLA_YENADI
	  KAPPALA_YENADI
	  MANCHI_YENADI
	  REDDI_YENADI
	  YERUKULAS
	  KORACHA
	  DABBA_YERUKULA
	  KUNCHAPURI_YERUKULA
	  UPPU_YERUKALA
	  NAKKALA
	  KURVIKARAN
	  DHULIYA
	  PAIKO
	  PUTIYA_ST
    }
{{< /mermaid >}}

##### Education Status

{{<mermaid align="left">}}
classDiagram
    class Name{
      STUDYING 
      COMPLETED 
      DISCONTINUED 
      ILLITERATE 
      NONE
    }
{{< /mermaid >}}

##### Education Qualification 

{{<mermaid align="left">}}
classDiagram
    class Name{
      NURSERY 
      PRIMARY 
      SECONDARY 
      SSC 
      ITI 
      INTERMEDIATE 
      DIPLOMA 
      GRADUATE 
      POST_GRADUATE 
      DOCTORATE
      NONE 
      OTHER 
    }
{{< /mermaid >}} 
   
##### Occupation

{{<mermaid align="left">}}
classDiagram
    class Name{
      SMALL_FARMER 
      LEASE_FARMER 
      FARMER 
      FARMER_LABOUR 
      DAILY_LABOUR 
      FARMER_ANIMAL_HUSBANDRY 
      BUSINESS 
      EMPLOYEE_PVT
      EMPLOYEE_CONTRACT 
      EMPLOYEE_GOVT 
      EMPLOYEE_PART_TIME 
      NONE
    }
{{< /mermaid >}} 

##### Relationship With Family Head

{{<mermaid align="left">}}
classDiagram
    class Name{
      SELF 
      FATHER
      MOTHER
      SISTER
      BROTHER
      SON
      DAUGHTER
      GRAND_FATHER
      GRAND_MOTHER
      UNCLE
      AUNT
      HUSBAND
      WIFE
	  DAUGHTER_IN_LAW
	  SON_IN_LAW
	  FATHER_IN_LAW
	  MOTHER_IN_LAW
	  GRAND_SON
	  GRAND_DAUGHTER
	  BROTHER_IN_LAW
	  SISTER_IN_LAW
	  NIECE
	  NEPHEW
	  UNRELATED
	  NONE
	  OTHER
    }
{{< /mermaid >}} 

##### Disability Type

{{<mermaid align="left">}}
classDiagram
    class Name{
      BLIND
      DEAF
      DUMB
      LEGS
      HANDS
      MENTAL
      NONE 
      OTHER 
    }
{{< /mermaid >}} 

##### Long Disease Type

{{<mermaid align="left">}}
classDiagram
    class Name{
	  DIABETES
	  BP
	  CARDIAC
	  BP_DIABETES
	  CARDIAC_DIABETES
	  BP_CARDIAC
	  BP_CARDIAC_DIABETES
	  OTHER
	  NONE    
    }
{{< /mermaid >}} 

#### Feature Permission
|Permission code|Action|
|---------------|-------|
|CITIZEN_CREATE|Create|
|CITIZEN_UPDATE|Update|
|CITIZEN_REMOVE|Remove|
|CITIZEN_VIEW|View|
|CITIZEN_VIEW|List|
|CITIZEN_VIEW|Export|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Keys|uk__gs_citizen__aid (aid)|

## Acceptance Criteria
|Permission|Description|
|-------------|-----------|
|ac_citizen_create|Only user having the permission to create, should create this functionality|
|ac_citizen_update|Only user having the permission to update, should update this functionality|
|ac_citizen_remove|Only user having the permission to remove, should remove this functionality|
|ac_citizen_view|Only user having the permission to view, should view this functionality|
|ac_citizen_view|Only user having the permission to export, should export the user role in 2 formats Excel, PDF|

## User Experience
1. Create page based on the standard UX Listing Template
1. Update page based on the standard UX Listing Template
1. Remove page based on the standard UX Listing Template
1. Listing page based on the standard UX Listing Template
1. View page based on the standard UX Listing Template
1. Export functionality based on the standard UX Listing Template 

### List Page Buttons
{{<mermaid align="left">}}
graph LR 
    CreteBtn[Create]---UpdateBtn[Update]---RemoveBtn[Remove]---ViewBtn[View]---ExportBtn[Export]---SearchBtn[Search]
{{< /mermaid >}}


### State Machine
{{<mermaid align="left">}}
flowchart TD
	CitizensMenu((Citizens Menu))
	ListPage{Citizens List Page}
	CreatePage((Create Page))
	UpdatePage((Update Page))
    RemovePage((Remove Page))
    ViewPage((View Page))
    DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->CitizensMenu
    subgraph Menu
    CitizensMenu
	end
	subgraph List
	CitizensMenu-->ListPage
	ListPage--C-U-R-V-E-->ListPage
	end
	subgraph Error
	CitizensMenu-->ErrorPage
	ErrorPage-->Stop
	end
	subgraph Create
	ListPage--C-->CreatePage
	CreatePage--SB-->ListPage
	CreatePage--SB-->CreatePage
	end
	subgraph Update
	ListPage--U-->UpdatePage
	UpdatePage--SB-->ListPage
	UpdatePage--SB-->UpdatePage
	end
	subgraph View
	ListPage--V-->ViewPage
	ViewPage--SB-->ListPage
	ViewPage--SB-->ViewPage
	end
	subgraph Remove
	ListPage--R-->RemovePage
	RemovePage--SB-->ListPage
	RemovePage--SB-->RemovePage
	end
	subgraph Download
    ListPage--E-->DownloadFile
    end
    %%For success Representation
    linkStyle 1 stroke:green,stroke-width:2px;
    linkStyle 5 stroke:green,stroke-width:2px;
    linkStyle 6 stroke:green,stroke-width:2px;
    linkStyle 8 stroke:green,stroke-width:2px;
    linkStyle 9 stroke:green,stroke-width:2px;
    linkStyle 11 stroke:green,stroke-width:2px;
    linkStyle 12 stroke:green,stroke-width:2px;
    linkStyle 14 stroke:green,stroke-width:2px;
    linkStyle 15 stroke:green,stroke-width:2px;
    linkStyle 17 stroke:green,stroke-width:2px;    
    %%For failure representation
    linkStyle 2 stroke:red,stroke-width:2px;
    linkStyle 3 stroke:red,stroke-width:2px;
    linkStyle 7 stroke:red,stroke-width:2px;
    linkStyle 10 stroke:red,stroke-width:2px;
    linkStyle 13 stroke:red,stroke-width:2px;
    linkStyle 16 stroke:red,stroke-width:2px;
	
{{< /mermaid >}}

|Symbol|Action|
|:-----|:----|
|C|Create|
|U|Update|
|R|Remove|
|V|View|
|E|Export|
|S|Submit|
|B|Back|
|SB|Submit or Back|
|VE|View or Export|
|C-U-R-V-E|Create or Update or Remove or View or Export|
|Green Arrow|Success|
|Red Arrow|Failure|

### Sequence Diagram

{{<mermaid align="center">}}
sequenceDiagram
    participant CitizensListPage as Browser
    participant Net as Browser Net Tools
	participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        CitizensListPage->>+Net: Check Internet, GET /app/ctx/Citizen/list ListPage
        Net--x-CitizensListPage: F : Connection Error
        CitizensListPage->>+cloud: S:  GET /app/ctx/Citizen/list ListPage
        cloud-->>-CitizensListPage: RES:List Page
    end
    rect rgb(244,244,244)
        CitizensListPage->>+Net: Check Internet, GET /app/Citizen/create/form CreateFormPage
        Net--x-CitizensListPage: F : Connection Error
        CitizensListPage->>+cloud: S : GET /app/Citizen/create/form CreateFormPage
        cloud-->>-CitizensListPage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        CitizensListPage->>+Net: Check Internet: POST /app/Citizen/create Create
        Net--x-CitizensListPage: F : Connection Error
        CitizensListPage->>+cloud: S : POST /app/Citizen/create Create
        cloud-->>-CitizensListPage: RES: An Citizen Successfully Created
    end
    rect rgb(244,244,244)
        CitizensListPage->>+Net: Check Internet: GET /app/Citizen/update/form UpdateFormPage
        Net--x-CitizensListPage: F : Connection Error
        alt
        Note right of Net: Citizen Cache Object Found
        CitizensListPage->>+Cache: S : GET /app/Citizen/update/form UpdateFormPage
        Cache-->>-CitizensListPage: RES: Update Form Loaded
        else
        Note right of Net: Citizen Cache Object Not Found
        Cache->>+cloud: GET /app/Citizen/update/form UpdateFormPage
        cloud-->>-CitizensListPage: RES: Update Form Loaded
        end
    end
    rect rgb(244,244,244)
        CitizensListPage->>+Net: Check Internet: POST /app/Citizen/update update
        Net--x-CitizensListPage: F : Connection Error
        CitizensListPage->>+cloud: S : POST /app/Citizen/update Update
        cloud-->>-CitizensListPage: RES: An Citizen Successfully Updated
    end
    rect rgb(244,244,244)
        CitizensListPage->>+Net: Check Internet: GET /app/Citizen/remove/form RemoveFormPage
        Net--x-CitizensListPage: F : Connection Error
        CitizensListPage->>+cloud: S : GET /app/Citizen/remove/form RemoveFormPage
        cloud-->>-CitizensListPage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        CitizensListPage->>+Net: Check Internet: POST /app/Citizen/remove Remove
        Net--x-CitizensListPage: F : Connection Error
        CitizensListPage->>+cloud: S : POST /app/Citizen/remove Remove
        cloud-->>-CitizensListPage: RES: A Citizen Successfully Removed
    end
    rect rgb(244,244,244)
        CitizensListPage->>+Net: Check Internet: GET /app/Citizen/view ViewPage
        Net--x-CitizensListPage: F : Connection Error
        alt
        Note right of Net: Citizen Cache Object Found
        CitizensListPage->>+Cache: S : GET /app/Citizen/view ViewPage
        Cache-->>-CitizensListPage: RES: citizen View
        else
        Note right of Net: Citizen Cache Object Not Found
        Cache->>+cloud: GET /app/Citizen/view ViewPage
        cloud-->>-CitizensListPage: RES: citizen View
        end
    end
    rect rgb(244,244,244)
        CitizensListPage->>+Net: Check Internet: GET /app/Citizen/exportPdf ExportPdf
        Net--x-CitizensListPage: F : Connection Error
        alt
        Note right of Net: Citizen Cache Object Found
        CitizensListPage->>+Cache: S : GET /app/Citizen/exportPdf ExportPdf
        Cache-->>-CitizensListPage: RES: citizen Pdf
        else
        Note right of Net: Citizen Cache Object Not Found
        Cache->>+cloud: GET /app/Citizen/exportPdf ExportPdf
        cloud-->>-CitizensListPage: RES: citizen Pdf
        end
    end
    rect rgb(244,244,244)
        CitizensListPage->>+Net: Check Internet: GET /app/Citizen/exportListPdf ExportListPdf
        Net--x-CitizensListPage: F : Connection Error
        CitizensListPage->>+cloud: S : GET /app/Citizen/exportListPdf ExportListPdf
        cloud-->>-CitizensListPage: RES: citizen List Pdf
    end
    rect rgb(244,244,244)
        CitizensListPage->>+Net: Check Internet: GET /app/Citizen/exportXlx ExportXlx
        Net--x-CitizensListPage: F : Connection Error
        alt
        Note right of Net: Citizen Cache Object Found
        CitizensListPage->>+Cache: S : GET /app/Citizen/exportXlx ExportXlx
        Cache-->>-CitizensListPage: RES: citizen Xlx
        else
        Note right of Net: Citizen Cache Object Not Found
        Cache->>+cloud: GET /app/Citizen/exportXlx ExportXlx
        cloud-->>-CitizensListPage: RES: citizen Xlx
        end
    end
    rect rgb(244,244,244)
        CitizensListPage->>+Net: Check Internet: GET /app/Citizen/exportListXlx ExportListXlx
        Net--x-CitizensListPage: F : Connection Error
        CitizensListPage->>+cloud: S : GET /app/Citizen/exportListXlx ExportListXlx
        cloud-->>-CitizensListPage: RES: citizen List Xlx
    end
    
          
{{< /mermaid >}}

## Unit Test Cases
#### Authorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count| Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create | ut_p_c_GSTS_WEB_CITIZEN_103 ut_n_c_GSTS_WEB_CITIZEN_104 ut_n_c_GSTS_WEB_CITIZEN_106 ut_n_c_GSTS_WEB_CITIZEN_701 ut_n_c_GSTS_WEB_CITIZEN_702 ut_n_c_GSTS_WEB_CITIZEN_703|**Positive Test Cases:** Creating Citizen with Authorised User **Negative Test Cases:** 1.Creating Citizen with Invalid Inputs 2.Creating Citizen without DB Connection 3.Creating Citizen with Authorised User At District Level 4.Creating Citizen with Authorised User At Division Level 5.Creating Citizen with Authorised User At Mandal Level|**aid:** 1.Valid characters 2.length=12 3.null **name:** 1.Valid Characters 2.length>3 and length<64 3.null **surname:** 1.Valid Characters 2.length>1 and length<32 3.null **fsname:** 1.Valid Characters 2.length>3 and length<64 3.null **mobile:** 1.Valid Characters [starts with 6,7,8,9] 2.length=10 3.null **dob:** date **gender:** Enum values:3 **marriedStatus:** Enum values:7 **disabledStatus:** Enum values:8 **relationHead:** Enum values:26 **livingType:** Enum values:2 **religion:** Enum values:13 **castCat:** Enum values:7 **eduStatus:** Enum values:5 **eduQualification:** Enum values:12 **empOccupation:** Enum values:11 **longDiseaseType:** Enum values:9|26|9|35|testAuthorisedUserCreateCitizen, testAuthorisedUserCreateCitizenNegativeTestCase, testAuthorisedUserCreateCitizenWithoutDBConnection, testAuthorisedUserCreateCitizenAtDistrictLevel, testAuthorisedUserCreateCitizenAtDivLevel, testAuthorisedUserCreateCitizenAtMandalLevel|
|1.0|Create Form|ut_p_c_GSTS_WEB_CITIZEN_100 |**Positive Test Cases:** 1.Open Citizen Create form with Authorised User  **Negative Test Cases:** |N/A|1|0|1|testAuthorisedUserOpenCitizenCreateForm|
|1.0|Update| ut_p_u_GSTS_WEB_CITIZEN_203 ut_n_u_GSTS_WEB_CITIZEN_204 ut_n_u_GSTS_WEB_CITIZEN_206 ut_n_u_GSTS_WEB_CITIZEN_307 |**Positive Test Cases:** Updating Citizen with Authorised User **Negative Test Cases:** 1.Updating Citizen with Invalid Input 2.Updating Citizen without DB Conenction 3.Updating Already Removed Citizen with Authorised User| **updateComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |1|3|4|testAuthorisedUserUpdateCitizen, testAuthorisedUserUpdateCitizenNegativeTestCase, testAuthorisedUserUpdateCitizenWithoutDBconnection, testAuthorisedUserUpdateAlreadyRemovedCitizen|
|1.0|Update Form|ut_p_u_GSTS_WEB_CITIZEN_200 ut_n_u_GSTS_WEB_CITIZEN_202 |**Positive Test Cases:** 1.Open Citizen Update form with Authorised User  **Negative Test Cases:** 1.Open Citizen Update form with Invalid id |1.Valid Id 2.Invalid Id|1|1|2|testAuthorisedUserOpenCitizenUpdateForm, testAuthorisedUserOpenCitizenUpdateFormWithInvalidId|
|1.0|Remove| ut_p_r_GSTS_WEB_CITIZEN_304 ut_n_r_GSTS_WEB_CITIZEN_303 ut_n_r_GSTS_WEB_CITIZEN_305 ut_n_r_GSTS_WEB_CITIZEN_310 ut_n_r_GSTS_WEB_CITIZEN_311 |**Positive Test Cases:** Removing Citizen with Authorised User **Negative Test Cases:** 1.Removing Citizen without DB Connection 2.Removing Citizen with Invalid inputs with Authorised User 3.Removing already removed Citizen with Authorised User 4.Removing Citizen with Invalid id with Authorised User|**removeComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |1|4|5|testAuthorisedUserRemoveCitizenWithoutDBConenction, testAuthorisedUserRemoveCitizen, testAuthorisedUserRemoveCitizenNegativeTestCase, testAuthorisedUserRemoveAlreadyRemovedCitizen, testAuthorisedUserRemoveCitizenWithInvalidId|
|1.0|Remove Form|ut_p_r_GSTS_WEB_CITIZEN_300 ut_n_r_GSTS_WEB_CITIZEN_302 ut_n_r_GSTS_WEB_CITIZEN_308 ut_n_r_GSTS_WEB_CITIZEN_309 |**Positive Test Cases:** 1.Open Citizen Remove form with Authorised User **Negative Test Cases:** 1.Open Citizen Remove form without DB Connection 2.Open Citizen Remove form for Already Removed Citizen 3.Open Citizen Remove form with Invalid id|1.Valid Id 2.Invalid Id|1|3|4|testAuthorisedUserOpenCitizenRemoveForm, testAuthorisedUserOpenCitizenRemoveFormWithoutDBConnection, testAuthorisedUserOpenCitizenRemoveFormForRemovedCitizen, testAuthorisedUserOpenCitizenRemoveFormWithInvalidId|
|1.0| View |ut_p_v_GSTS_WEB_CITIZEN_400 ut_n_v_GSTS_WEB_CITIZEN_401 ut_n_v_GSTS_WEB_CITIZEN_403 |**Positive Test Cases:** View Citizen with Valid Id  with Authorised User **Negative Test Cases:** 1.View Citizen with Invalid ID with Authorised User 2.View Citizen without DB Connection|1.Valid Id 2.Invalid Id|1|2|3|testAuthorisedUserViewCitizenWithValidId, testAuthorisedUserViewCitizenWithInValidId, testAuthorisedUserViewCitizenWithoutDBConnection|
|1.0| Search |ut_p_s_GSTS_WEB_CITIZEN_500 ut_n_s_GSTS_WEB_CITIZEN_501 ut_n_s_GSTS_WEB_CITIZEN_503 ut_n_s_GSTS_WEB_CITIZEN_504|**Positive Test Cases:** Search Citizen with Authorised User **Negative Test Cases:** 1.Search Citizen with Invalid Inputs 2.Search Citizen without DB Connection 3.Search Citizen with Invalid dates with Authorised User|**name:** 1.valid characters 2.length>3 and length<64 **aid:** 1.valid characters 2.length=4 or length=12 **surname:** 1.Valid Characters 2.length>1 and length<32 **mobile:** 1.Valid Characters [starts with 6,7,8,9] 2.length=10 **castCat:** Enum values **eduStatus:** Enum values **empOccupation:** Enum values|7|6|13|testAuthorisedUserSearchCitizen, testAuthorisedUserSearchCitizenNegativeTestCase, testAuthorisedUserSearchCitizenWithoutDBConnection, testAuthorisedUserSearchCitizenNegativeCase|
|1.0| List |ut_p_l_GSTS_WEB_CITIZEN_600 ut_n_l_GSTS_WEB_CITIZEN_601 |**Positive Test Cases:** Check the object list with valid data with Authorised User **Negative Test Cases:** 1.Check the object list with Invalid data with Authorised User|Validating with unique field|1|1|2|testAuthorisedUserListCitizen, testAuthorisedUserListCitizenNegativeTestCase|
|1.0| PDF |ut_p_ep_GSTS_WEB_CITIZEN_800 ut_n_ep_GSTS_WEB_CITIZEN_804 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:** 1.Export Pdf with Invalid Id 2.Export Pdf Without DB Connection|Id |1|1|2|testAuthorisedUserExportPdfWithValidId, testAuthorisedUserExportPdfWithInvalidId|
|1.0| List PDF |ut_p_elp_GSTS_WEB_CITIZEN_801 ut_n_elp_GSTS_WEB_CITIZEN_805 ut_n_elp_GSTS_WEB_CITIZEN_813 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** Export List Pdf with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListPdfWithValidId, testAuthorisedUserExportListPdfWithInvalidId, testAuthorisedUserExportListPdfWithoutDBConnection|
|1.0| XLX |ut_p_ex_GSTS_WEB_CITIZEN_802 ut_n_ex_GSTS_WEB_CITIZEN_806 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** Export Xlx with Invalid Id and Without DB Connection|Id |1|1|2|testAuthorisedUserExportXlxWithValidId, testAuthorisedUserExportXlxWithInvalidId|
|1.0| List XLX |ut_p_elx_GSTS_WEB_CITIZEN_803 ut_n_elx_GSTS_WEB_CITIZEN_807 ut_n_elx_GSTS_WEB_CITIZEN_815 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** Export List Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListXlxWithValidId, testAuthorisedUserExportListXlxWithInvalidId, testAuthorisedUserExportListXlxWithoutDBConnection|

#### UnAuthorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Name| 
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create | ut_n_c_GSTS_WEB_CITIZEN_105|Unauthorised User does not have permission to create| **aid:** 1.Valid characters 2.length=12 3.null **name:** 1.Valid Characters 2.length>3 and length<64 3.null **surname:** 1.Valid Characters 2.length>1 and length<32 3.null **fsname:** 1.Valid Characters 2.length>3 and length<64 3.null **mobile:** 1.Valid Characters [starts with 6,7,8,9] 2.length=10 3.null **dob:** date **gender:** Enum values:3 **marriedStatus:** Enum values:7 **disabledStatus:** Enum values:8 **relationHead:** Enum values:26 **livingType:** Enum values:2 **religion:** Enum values:13 **castCat:** Enum values:7 **eduStatus:** Enum values:5 **eduQualification:** Enum values:12 **empOccupation:** Enum values:11 **longDiseaseType:** Enum values:9|0|1|1|testUnAuthorisedUserCreateCitizen|
|1.0|Update|ut_p_u_GSTS_WEB_CITIZEN_205 |Unauthorised User does not have permission to update| **updateComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |0|1|1|testUnAuthorisedUserUpdateCitizen|
|1.0|Update Form|ut_n_u_GSTS_WEB_CITIZEN_201|Open Citizen Update form with UnAuthorised User|1.Valid Id 2.Invalid Id|0|1|1|testUnAuthorisedUserOpenCitizenUpdateForm |
|1.0|Remove| ut_n_r_GSTS_WEB_CITIZEN_306|Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |0|1|1|testUnAuthorisedUserRemoveCitizen|
|1.0|Remove Form|ut_n_r_GSTS_WEB_CITIZEN_301|Open Citizen Remove form with UnAuthorised User|1.Valid Id 2.Invalid Id|0|1|1|testUnAuthorisedUserOpenCitizenRemoveForm |
|1.0| View |ut_n_v_GSTS_WEB_CITIZEN_402|Unauthorised User does not have permission to view|1.Valid Id|0|1|1|testUnAuthorisedUserViewCitizenWithValidId|
|1.0| Search |ut_n_s_GSTS_WEB_CITIZEN_502|Unauthorised User does not have permission to search|  **name:** 1.valid characters 2.length>3 and length<64 **aid:** 1.valid characters 2.length=4 or length=12 **surname:** 1.Valid Characters 2.length>1 and length<32 **mobile:** 1.Valid Characters [starts with 6,7,8,9] 2.length=10 **castCat:** Enum values **eduStatus:** Enum values **empOccupation:** Enum values|0|1|1|testUnAuthorisedUserSearchCitizen|
|1.0| List |ut_n_l_GSTS_WEB_CITIZEN_602 |Unauthorised User does not have permission to list|Validating with unique field|0|1|1|testUnAuthorisedUserListCitizen|
|1.0| PDF |ut_n_ep_GSTS_WEB_CITIZEN_808 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportPdf|
|1.0| List PDF |ut_n_elp_GSTS_WEB_CITIZEN_809 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportListPdf|
|1.0| XLX |ut_n_ex_GSTS_WEB_CITIZEN_810 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportXlx|
|1.0| List XLX |ut_n_elx_GSTS_WEB_CITIZEN_811 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportListXlx|

#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Name|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|-----------|
|1.0|Create|ut_n_c_GSTS_WEB_CITIZEN_700| Creating Citizen at state level with authorised User| N/A |Will not be created|1|testAuthorisedUserCreateCitizenAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_CITIZEN_704| View Citizen at state level with authorised user| N/A |User not able to view the Citizen at state level|1|testAuthorisedUserViewCitizenAtStateLevel|
|1.0|Update|ut_n_u_GSTS_WEB_CITIZEN_705|Update Citizen at state level with authorised user| N/A |User not able to update the Citizen at state level|1|testAuthorisedUserUpdateCitizenAtStateLevel|
|1.0|Update|ut_n_u_GSTS_WEB_CITIZEN_706|Update Citizen at District level with authorised user| N/A |User not able to update the Citizen at district level|1|testAuthorisedUserUpdateCitizenAtDistrictLevel|
|1.0|Update|ut_n_u_GSTS_WEB_CITIZEN_707|Update Citizen at Division level with authorised user| N/A |User not able to update the Citizen at division level|1|testAuthorisedUserUpdateCitizenAtDivLevel|
|1.0|Update|ut_n_u_GSTS_WEB_CITIZEN_708|Update Citizen at Mandal level with authorised user| N/A |User not able to update the Citizen at mandal level|1|testAuthorisedUserUpdateCitizenAtMandalLevel|
|1.0|Update|ut_n_r_GSTS_WEB_CITIZEN_709|Remove Citizen at State level with authorised user| N/A |User not able to remove the Citizen at state level|1|testAuthorisedUserRemoveCitizenAtStateLevel|
|1.0|Update|ut_n_r_GSTS_WEB_CITIZEN_710|Remove Citizen at District level with authorised user| N/A |User not able to remove the Citizen at district level|1|testAuthorisedUserRemoveCitizenAtDistrictLevel|
|1.0|Update|ut_n_r_GSTS_WEB_CITIZEN_711|Remove Citizen at Division level with authorised user| N/A |User not able to remove the Citizen at division level|1|testAuthorisedUserRemoveCitizenAtDivLevel|
|1.0|Update|ut_n_r_GSTS_WEB_CITIZEN_712|Remove Citizen at Mandal level with authorised user| N/A |User not able to remove the Citizen at mandal level|1|testAuthorisedUserRemoveCitizenAtMandalLevel|

## Security compliance check
1. Only user having the user role with permission **ROLE_CITIZEN_CREATE** should create this functionality 
1. Only user having the user role with permission **ROLE_CITIZEN_UPDATE** should update this functionality 
1. Only user having the user role with permission **ROLE_CITIZEN_REMOVE** should remove this functionality 
1. Only user having the user role with permission **ROLE_CITIZEN_VIEW** should view this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the CITIZENS in the User Manual. It's scope is limited to Developer Technical Documentation

## Feature/Defect list
|Feature/Defect ID|Link|Status|
|----|----|---|
|GS-0003|[GS-0003](https://shadkona.atlassian.net/browse/GS-0003)|Closed|


## References
1. [Spring Security](https://spring.io/projects/spring-security)
1. [Intro to Spring Security Expressions](https://www.baeldung.com/spring-security-expressions)
1. [Spring Security Role Based Access Authorization Example](https://www.journaldev.com/8748/spring-security-role-based-access-authorization-example)

## Development Estimations
|Release Tag|Feature/Defect ID|Scrum Deatils|Start date|End date|
|-----------|-----------------|-------------|----------|--------|
|2020OCT|GS-0002|Scrum 2020OCTs2|14 OCT 2020|28 OCT 2020|

## Feature Doneness Criteria
Check list for the Doneness criteria

|Metric|Unit Measure|Expected Result|Actual Result|Accepted?|Remarks|Approver|
|------|------------|---------------|-------------|---------|-------|----------|
|Acceptance Criteria Defined?|YES or NO|YES|YES|Accepted|All test cases passed|PM|
|Architecture Approved?|YES or NO|YES|YES|Accepted|Design is accepted|Architect|
|Coding Completed?|YES or NO|YES|YES|Completed|Completed|EM|
|Product Defects|Number|0|0|Accepted||EM|
|Unit Test Case Count?|Number|>5|8|Accepted|Tested|EM|
|Integration Test Cases Count|Number|>5|9|Accepted|Tested|EM|
|Sonar Vulnerabilities Count|Number|0|0|Accepted|validated|EM|
|Code Coverage|Number|>98%|99%|Accepted|Validated|EM|
|User Manual Verified?|YES or NO|YES|YES|Accepted|Validated|DocM|
|PenTest Defect Count?|Number|<2|0|Accepted|Validated|EM|
|PM Accepted?|YES or NO|YES|YES|Accepted|Good to go|PM|
|OM Accepted?|YES or NO|YES|YES|Accepted|Good to go|OM|
|Deployed to Staging?|YES or NO|YES|YES|Accepted|Good to go|EM|
|Deployed to Production?|YES or NO|YES|YES|Accepted|Good to go|OM|




 
