---
title: Citizen
tags : ["Composing"]
---

## Introduction
Citizens are one of the features of our software product. Using this feature, Survey User can create citizen with organization required data.
Citizen details mean person identity( Aadhaar Details ), employment details, and health details.

## Business Assumptions
1. Citizen feature should be planned at the design phase.
1. Creating and updating the citizens can be done at the run time based on the requirement.

## Requirements
### Functional Requirements
1. After completing the house creation only, the Survey User is allowed to create a citizen.
1. Only one citizen is allowed with the same Aadhaar number. This means a citizen's Aadhaar number has to be unique.

### Non-functional Requirements
1. Multiple users can create citizens in the same panchayat.
1. Multiple users can create same citizen in the same panchayat or different panchayat. But only one house property will sync among all users based on who sync first.

### Problem Statement
Identity, education details, employment details of a citizen in a panchayat should be captured.

### Design 
1. Each Citizen has an Aadhaar Input Type, owner’s Aadhaar number, Name, Surname, Father/Spouse Name, Mobile Number, Gender, Date Of Birth, Age, Marital Status, Religion, Caste Category, Sub Caste Category, Caste Name, Disability Type, Education Status, Education Qualification, Occupation, Long Disease Type, General Insurance, Health Insurance, Health Card Used and Living Place Type filed.
2. Survey User can Create, Update, and View the citizens.

#### Checks in the Citizen module
1. Marital Status Field is based on the Date of Birth Field
2. Relationship with Head field is depends on Age and Gender fields
3. Sub Caste Category is based on the Caste Category field
4. Caste Name is based on the Caste Category and Sub Caste Category
5. If the age>3 then we will show Education Status Field else we hide the field

#### Dependant Features
| Feature name | Reference Link           | Remarks     |
|--------------|--------------------------|-------------|
| Family       | [Family]({{< ref "" >}}) | Parent Page |

#### Use cases
| Use case Code     | Description           |
|-------------------|-----------------------|
| uc_citizen_create | To create the citizen |
| uc_citizen_edit   | To update the citizen |
| uc_citizen_view   | To view the citizen   |


#### Model Attributes
| Attribute name          | Mandatory | Default value | Input Allowed Char set Layout/API       | KV Database Key        | SQLite Column Definition        | Create | Update | Remove | View | List | Search | Remarks |
|-------------------------|-----------|---------------|-----------------------------------------|------------------------|---------------------------------|--------|--------|--------|------|------|--------|---------|
| id                      | YES       | NA            | a-zA-Z0-9, maxlen=128                   | NA                     | id String                       | YES    | NO     | YES    | NO   | NO   | NO     ||
| aadhaar_input_type      | YES       | OCR           | NA                                      | AADHAR_INPUT_TYPE_KEY  | aadhaar_input_type String       | YES    | YES    | YES    | YES  | NO   | NO     ||
| aid                     | YES       | NA            | 0-9, maxlen=12                          | AADHAR_KEY             | aid String                      | YES    | YES    | YES    | YES  | NO   | NO     ||
| headAadhaarId           | YES       | NA            | 0-9, maxlen=12                          | HEAD_AADHAAR_ID        | headAadhaarId String            | YES    | YES    | YES    | YES  | NO   | NO     ||
| name                    | YES       | NA            | a-z A-Z, maxlen=64                      | NAME_KEY               | name String                     | YES    | YES    | YES    | YES  | NO   | NO     ||
| surname                 | YES       | NA            | a-z A-Z, maxlen=32                      | SURNAME_KEY            | surname String                  | YES    | YES    | YES    | YES  | NO   | NO     ||
| fsname                  | YES       | NA            | a-zA-Z /, maxlen=64                     | FATHER_SPOUSE_NAME_KEY | fsname String                   | YES    | YES    | YES    | YES  | NO   | NO     ||
| mobile                  | YES       | NA            | 0-9, maxlen=10                          | MOBILE_KEY             | mobile String                   | YES    | YES    | YES    | YES  | NO   | NO     ||
| gender                  | YES       | Male          | Radio Button Value                      | GENDER_KEY             | gender String                   | YES    | YES    | YES    | YES  | NO   | NO     ||
| dob                     | YES       | NA            | 0-9/-, maxlen=10                        | DATE_OF_BIRTH_KEY      | dob String                      | YES    | YES    | YES    | YES  | NO   | NO     ||
| age                     | YES       | NA            | 0-9, maxlen=3                           | AGE_KEY                | age String                      | YES    | YES    | YES    | YES  | NO   | NO     ||
| email                   | NO        | NA            | a-zA-Z0-9. /-@&amp;_#,:;()/\, maxlen=64 | EMAIL_KEY              | email String                    | YES    | YES    | YES    | YES  | NO   | NO     ||
| married                 | YES       | Choose        | Spinner Value                           | MARTIAL_STATUS_KEY     | married String                  | YES    | YES    | YES    | YES  | NO   | NO     ||
| relation_with_head      | YES       | Choose        | Spinner Value                           | RELATION_HEAD_KEY      | relation_with_head String       | YES    | YES    | YES    | YES  | NO   | NO     ||
| religion_type           | YES       | Choose        | Spinner Value                           | RELIGION_TYPE_KEY      | religion_type String            | YES    | YES    | YES    | YES  | NO   | NO     ||
| caste_type              | YES       | Choose        | Spinner Value                           | CASTE_KEY              | caste_type String               | YES    | YES    | YES    | YES  | NO   | NO     ||
| sub_caste_type          | YES       | Choose        | Spinner Value                           | SUB_CASTE_TYPE         | sub_caste_type String           | YES    | YES    | YES    | YES  | NO   | NO     ||
| caste_name              | YES       | Choose        | Spinner Value                           | CASTE_NAME_KEY         | caste_name String               | YES    | YES    | YES    | YES  | NO   | NO     ||
| disability_type         | YES       | Choose        | Spinner Value                           | DISABLE_STATUS_KEY     | spl_status String               | YES    | YES    | YES    | YES  | NO   | NO     ||
| education_status        | YES       | Choose        | Spinner Value                           | EDU_STATUS_TYPE_KEY    | education_status String         | YES    | YES    | YES    | YES  | NO   | NO     ||
| education_qualification | YES       | Choose        | Spinner Value                           | EDU_QUALIFICATION_KEY  | education_qualification String  | YES    | YES    | YES    | YES  | NO   | NO     ||
| occupation_type         | YES       | Choose        | Spinner Value                           | OCCUPATION_KEY         | occupation_type String          | YES    | YES    | YES    | YES  | NO   | NO     ||
| long_disease_type       | YES       | Choose        | Spinner Value                           | LONG_DISEASE_TYPE_KEY  | long_disease_type String        | YES    | YES    | YES    | YES  | NO   | NO     ||
| general_insurance       | YES       | False         | 0(No), 1(Yes)                           | GENERAL_INSURANCE_KEY  | general_insurance Boolean       | YES    | YES    | YES    | YES  | NO   | NO     ||
| health_insurance        | YES       | False         | 0(No), 1(Yes)                           | HEALTH_INSURANCE_KEY   | health_insurance Boolean        | YES    | YES    | YES    | YES  | NO   | NO     ||
| healthCard_used         | YES       | False         | 0(No), 1(Yes)                           | HEALTH_CARD_USED_KEY   | healthCard_used Boolean         | YES    | YES    | YES    | YES  | NO   | NO     ||
| living_place_type       | YES       | False         | 0(No), 1(Yes)                           | LIVING_PLACE_TYPE_KEY  | liviPlace_type Boolean          | YES    | YES    | YES    | YES  | NO   | NO     ||
| dataSync                | YES       | NA            | 0(No), 1(Yes)                           | NA                     | dataSync Boolean                | NA     | NA     | NA     | NO   | NO   | NO     ||
| imageSync               | YES       | NA            | 0(No), 1(Yes)                           | NA                     | imageSync Boolean               | NA     | NA     | NA     | NO   | NO   | NO     ||
| survey_start_time       | YES       | NA            | a-zA-Z0-9, maxlen=128                   | SURVEY_START_TIME      | survey_start_time String        | YES    | NA     | NA     | YES  | NO   | NO     ||
| survey_end_time         | YES       | NA            | a-zA-Z0-9, maxlen=128                   | SURVEY_END_TIME        | survey_end_time String          | YES    | NA     | NA     | YES  | NO   | NO     ||
| isHouseOwner            | YES       | NA            | 0(No), 1(Yes)                           | NA                     | isHouseOwner Boolean            | NA     | NA     | NA     | NO   | NO   | NO     ||
| isOwnerExistInAnyFamily | YES       | NA            | 0(No), 1(Yes)                           | NA                     | isOwnerExistInAnyFamily Boolean | NA     | NA     | NA     | NO   | NO   | NO     ||

#### ENUM CONSTANTS

##### Aadhaar Input Type

{{<mermaid align="left">}}
classDiagram
    class AadhaarInputType{
      OCR
      QRCODE
      MANUAL
    }
{{< /mermaid >}}

##### Gender

{{<mermaid align="left">}}
classDiagram
    class GenderType{
      MALE
      FEMALE
      OTHER
    }
{{< /mermaid >}}

##### Marital Status

{{<mermaid align="left">}}
classDiagram
    class MartialStatusType{
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
    class ReligionType{
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
    class CasteType{
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
    class SubCasteType{
      BC_A
      BC_B
      BC_C
      BC_D
      BC_E
      NONE
    }
{{< /mermaid >}}

##### Caste Names

##### OC Caste Names

{{<mermaid align="left">}}
classDiagram
    class OCCasteNames{
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

##### ST Caste Names

{{<mermaid align="left">}}
classDiagram
    class STCasteNames{
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
    
        KOTTU_KOYA5
    
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

##### SC Caste Names

{{<mermaid align="left">}}
classDiagram
    class SCCasteNames{
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

##### BC_A

{{<mermaid align="left">}}
classDiagram
    class BCGroupACasteNames{
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
    class BCGroupBCasteNames{
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
    class BCGroupCCasteNames{
      CHRISTIANS
    }
{{< /mermaid >}}

##### BC_D

{{<mermaid align="left">}}
classDiagram
    class BCGroupDCasteNames{
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
    class BCGroupECasteNames{
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
##### Education Status

{{<mermaid align="left">}}
classDiagram
    class EduStatusType{
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
    class EduQualificationType{
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
    class EmpOccupationType{
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
    class RelationWithHeadType{
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
    class DisabledStatusType{
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
    class LongDiseaseType{
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
| Permission code | Action |
|-----------------|--------|
| -               | -      |


#### Constraints
| Constraint  | Key |
|-------------|-----|
| Primary Key | id  |
| Unique Keys | aid |

## Acceptance Criteria
| Description                                                      |
|------------------------------------------------------------------|
| Version : 1.0                                                    |
| 1. Survey User can able to Create, View, and Update the citizens |


## User Experience

### citizen form Page
{{<mermaid align="left">}}
graph LR 
    BackBtn[<- Back Button]-->NextBtn[Next Button]
{{< /mermaid >}}

### citizen Details Confirmation Page
{{<mermaid align="left">}}
graph LR 
    BackBtn[<- Back Button]-->FinishBtn[Finish Button]
{{< /mermaid >}}

### citizen View Page
{{<mermaid align="left">}}
graph LR 
    BackBtn[<- Back Button]-->EditBtn[Edit Button]
{{< /mermaid >}}

### State Machine
{{<mermaid align="left">}}
flowchart TD
	ListPage((Citizen List))
	FromPage[Citizen Form Page]
	ConfirmationPage[Citizen Details Confirmation Page]
    ViewPage[Citizen View Page]
	Start((Start))
    AddBtn[Add Button]
    NextBtn1[Next Button]
    FinishBtn1[Finish Button]
    EditBtn[Edit Button]
    BackBtn1[Back Button]
    CitizenItem[Citizen Item]
    End((end))
    %% link 0
    Start-->ListPage
	subgraph Family Page
        %% link 1
        ListPage--C-->AddBtn
        %% link 2
        ListPage-->End
        %% link 3
        ListPage--C-->CitizenItem
	end
    subgraph Form Page
        %% link 4
        AddBtn--S-->FromPage
        %% link 5
        AddBtn--F-->ListPage
        %% link 6
        FromPage--C-->NextBtn1
	end
	subgraph Details View Page
	    %% link 7
        NextBtn1--F-->FromPage
        %% link 8
        NextBtn1--S-->ConfirmationPage
        %% link 9
        ConfirmationPage--C-->FinishBtn1
        %% link 10
        FinishBtn1--F-->ConfirmationPage
        %% link 11
        FinishBtn1--S-->ListPage
        %% link 12
        ConfirmationPage--C-->BackBtn1
        %% link 13
        BackBtn1--F-->ConfirmationPage
        %% link 14
        BackBtn1--S-->FromPage
	end
	subgraph View Page
	    %% link 16
        CitizenItem--F-->ListPage
	    %% link 15
        CitizenItem--S-->ViewPage
        %% link 17
        ViewPage--C-->EditBtn
        %% link 18
        EditBtn--F-->ViewPage
        %% link 19
        EditBtn--S-->FromPage
	end
	%% For click Repressentation,  links : 1,3,6,9,12,17
    linkStyle 1 stroke:blue,stroke-width:2px;
    linkStyle 3 stroke:blue,stroke-width:2px;
    linkStyle 6 stroke:blue,stroke-width:2px;
    linkStyle 9 stroke:blue,stroke-width:2px;
    linkStyle 12 stroke:blue,stroke-width:2px;
    linkStyle 17 stroke:blue,stroke-width:2px;
    %% For success Representation, links :4,8,11,14,16,19
    linkStyle 4 stroke:green,stroke-width:2px;
    linkStyle 8 stroke:green,stroke-width:2px;
    linkStyle 11 stroke:green,stroke-width:2px;
    linkStyle 14 stroke:green,stroke-width:2px;
    linkStyle 16 stroke:green,stroke-width:2px;
    linkStyle 19 stroke:green,stroke-width:2px;
    %% For failure Representation, links : 5,7,10,13,15,18
    linkStyle 5 stroke:red,stroke-width:2px;
    linkStyle 7 stroke:red,stroke-width:2px;
    linkStyle 10 stroke:red,stroke-width:2px;
    linkStyle 13 stroke:red,stroke-width:2px;
    linkStyle 15 stroke:red,stroke-width:2px;
    linkStyle 18 stroke:red,stroke-width:2px;    
		
	
{{< /mermaid >}}

| Symbol     | Action                          |
|:-----------|:--------------------------------|
| C          | ClickOn                         |
| S          | OnSuccess                       |
| F          | OnFailure                       |
| Blue Link  | Click                           |
| Green Link | Success                         |
| Red Link   | Failure or Exception occurrence |

### Sequence Diagram

{{<mermaid align="center">}}
sequenceDiagram
    participant SQLite as SQLite Database
    participant ListPage as Family page: citizen List
    participant FormPage as Citizen Form Page
    participant KVDB as KV Database
    participant ViewPage as Citizen View Page
    autonumber 
    
    rect rgb(244,244,244)
        Note right of FormPage: If (Adding new Citizen or update citizen) (1) else { (5) }
        FormPage->>+KVDB: save Citizen KV Data in KVDatabase
    end
    rect rgb(244,244,244)
        ViewPage->>+KVDB: get Citizen KV Data 
        KVDB-->>-ViewPage: KV Citizen Data    
    end  
    rect rgb(244,244,244)
        Note Left of ViewPage: if (Edit == true) {update Citizen} else {insert Citizzen}
        ViewPage->>+SQLite: updateCitizen(Citizen) (or) insertCitizen(Citizen) 
    end  
    rect rgb(244,244,244)
        ListPage->>+SQLite: load All citizens based on family head id
        SQLite-->>-ListPage: List Of citizens
    end    
    rect rgb(244,244,244)
        Note left of ViewPage: View Citizen Data
        ViewPage->>+SQLite: fetchCitizenById(id) 
        SQLite-->>-ViewPage: Citizen Object
    end   
    rect rgb(244,244,244)
        Note left of ViewPage: Edit Citizen Data
        FormPage->>+SQLite: fetchCitizenById(id) 
        SQLite-->>-FormPage: Citizen Object
    end    
    rect rgb(244,244,244)
        Note right of FormPage: Repeat (1) to (4)
    end
    rect rgb(244,244,244)
        Note right of SQLite: Repeat (5) and (6)
    end    
    
{{< /mermaid >}}

## Unit Test Cases
| Product Version | UnitTest Id | Description |
|-----------------|-------------|-------------|
| -               | -           | -           |

## Security compliance check
1. Only Survey User should Create, View, and Update citizen Data.

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the CITIZENS in the User Manual. It's scope is limited to Developer Technical Documentation

## Feature/Defect list
| Feature/Defect ID | Link                                                     | Status |
|-------------------|----------------------------------------------------------|--------|
| GS-0003           | [GS-0003](https://shadkona.atlassian.net/browse/GS-0003) | Closed |


## References
1. [Spring Security](https://spring.io/projects/spring-security)
1. [Intro to Spring Security Expressions](https://www.baeldung.com/spring-security-expressions)
1. [Spring Security Role Based Access Authorization Example](https://www.journaldev.com/8748/spring-security-role-based-access-authorization-example)

## Development Estimations
| Release Tag | Feature/Defect ID | Scrum Deatils   | Start date  | End date    |
|-------------|-------------------|-----------------|-------------|-------------|
| 2020OCT     | GS-0002           | Scrum 2020OCTs2 | 14 OCT 2020 | 28 OCT 2020 |

## Feature Doneness Criteria
Check list for the Doneness criteria

| Metric                       | Unit Measure | Expected Result | Actual Result | Accepted? | Remarks               | Approver  |
|------------------------------|--------------|-----------------|---------------|-----------|-----------------------|-----------|
| Acceptance Criteria Defined? | YES or NO    | YES             | YES           | Accepted  | All test cases passed | PM        |
| Architecture Approved?       | YES or NO    | YES             | YES           | Accepted  | Design is accepted    | Architect |
| Coding Completed?            | YES or NO    | YES             | YES           | Completed | Completed             | EM        |
| Product Defects              | Number       | 0               | 0             | Accepted  || EM                    |
| Unit Test Case Count?        | Number       | >5              | 8             | Accepted  | Tested                | EM        |
| Integration Test Cases Count | Number       | >5              | 9             | Accepted  | Tested                | EM        |
| Sonar Vulnerabilities Count  | Number       | 0               | 0             | Accepted  | validated             | EM        |
| Code Coverage                | Number       | >98%            | 99%           | Accepted  | Validated             | EM        |
| User Manual Verified?        | YES or NO    | YES             | YES           | Accepted  | Validated             | DocM      |
| PenTest Defect Count?        | Number       | <2              | 0             | Accepted  | Validated             | EM        |
| PM Accepted?                 | YES or NO    | YES             | YES           | Accepted  | Good to go            | PM        |
| OM Accepted?                 | YES or NO    | YES             | YES           | Accepted  | Good to go            | OM        |
| Deployed to Staging?         | YES or NO    | YES             | YES           | Accepted  | Good to go            | EM        |
| Deployed to Production?      | YES or NO    | YES             | YES           | Accepted  | Good to go            | OM        |




 
