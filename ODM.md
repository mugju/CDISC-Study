# ODM
- 본 자료에 사용된 ODM은 open EDC 사용 ODM이다.
- 본 문서에서는 ODM의 상위 태그부터 하위태그까지의 속성들을 순차적으로 설명한다.

- 각 태그의 바디내용은 명시되어 있지 않을 경우, 들여쓰기의 내용이 body 내용임을 나타낸다.
- 명시되어 있는 경우, 바디에 작성될 수 있는 타입이 명시된다.

본 문서에서 다룰 태그 영역은 다음과 같다.


```
- ODM 프리뷰 -

  Study
    📁  Globalvariables
        StudyName
        StudyDescription
        ProtocolName
    📁  BasicDefinitions
        MeasurementUnit
          Symbol
    📁  MetaDataVersion
        📌Protocol
            StudyEventRef
        📌StudyEventDef
            ✅ Description
            ✅ FormRef
        📌FormDef
            ✅ Description
		ItemGroupRef
        📌ItemGroupDef
            ✅ Description
               ItemRef
        📌ItemDef
            Question
            CodeListRef
            MeasurementUnitRef
            RangeCheck
        📌CodeList
            CodeListItem

```


## 🐱‍👤ODM 
- ODM의 이하 attribute들로는 다음과 같이 존재하는데,

  ### Description (text 형식)
  ODM의 설명으로써, 해당 문서의 이해를 정확하게 할수 있도록하는 역할을 한다.


  ### FileType ( Snapshot | Transactional )
  Snapshot or Transactional 으로 표현된다.
  snapshot 은 단순하게 현재상황의 데이터/ 메타데이터를 나타낸다면, Transactional의 경우 현재 이 데이터뿐만 아니라 이 데이터가 어떻게 존재하게 되었는지까지 나타내게 된다.


  ### Granularity ( All | Metadata | AdminData | ReferenceData | AllClinicalData | SingleSite | SingleSubject )
  해당 속성은 해당 문서의 정보의 폭을 나타낸다. 일반적으로 위의 범주에서 더 상세한 설명이 필요할 경우에는 Desc 속성에 추가하여 설명한다.


  ### Archival (Yes | No)
  해당 속성은 문서타입이 Transactional 일 경우에만 사용해야 하며, 21 CFR 11을 충족하는 경우에 Yes를 그렇지 않은 경우에는 No를 작성한다.
  * 21 CFR 11은 미국 의약품 의료기기 관리법률 중 전자 문서와 전자 서명에 관련한 규정이다. 


  ### FileOID (OID)
  유일한 이 파일의 인식자이다.
  OID 의 경우, 최소길이가 1인 문자열의 순서인데 조사한 바로는 특별한 명명규칙은 없는 것으로 보여진다.
  첨언하자면, openEDC에서 생성된 fileOID는 해당 study의 이름을 그대로 가져와 사용한다.


  ### CreationDateTime
  해당 파일의 생성 일시를 나타낸다. datetime 형식이며, 초까지 표현한다.


  ### PriorFileOID (oidref)
  이전파일이 있는 경우 해당 파일에 대한 참조이다.
  표현형식은 oidref이며, 표현형식은 oid와 동일하다.

  ### AsOfDateTime (datetime)
  문서를 만들기 위해 원본데이터베이스를 쿼리한 시간이다. 표현형식은 datetime 이다.


  ### ODMVersion ( 1.2 | 1.2.1 | 1.3 | 1.3.1 | 1.3.2 )
  사용한 ODM 표준 버전을 명시한다.
  ODM 버전은 최신버전이 2013년도 기준 릴리즈된 1.3.2 버전이며, 그 이후 업데이트는 홈페이지에 릴리즈 되어있지 않다.


  ### Originator
  해당 ODM 파일을 생성한 단체를 말한다.


  ### SourceSystem (text)
  컴퓨터 시스템이나 데이터베이스 관리시스템을 명시한다.


  ### SourceSystemVersion (text)
  SourceSystem의 버전을 명시한다.


  ### ID (ID)
  ds:Signature 에서 다시 사용할 요소. 현재로써 서명을 위한 요소로 이해된다.
  
      이하 코드는 ODM 속성 예시코드.
      <ODM xmlns="http://www.cdisc.org/ns/odm/v1.3" xmlns:ns2="http://www.w3.org/2000/09/xmldsig#" FileType="Snapshot" FileOID="CNR_ODM study" CreationDateTime="2022-06-27T08:39:40.595Z" ODMVersion="1.3.2" SourceSystem="OpenEDC">    
  
## Study
- ODM의 이하 먼저 나타나는 하위태그는 Study이다.
- Study의 속성으로는 OID 하나만 존재한다.
  
  ### OID
  예시는 다음과 같다.
  < Study OID="S.1">
  
  ## 🤷‍♂️GlobalVariables
  - 포함하는 속성은 없으며, 연구에 대한 일반적인 요약정보를 포함한다.
  
    ## 🤦‍♂️StudyName
    - body에 작성될수 있는 것은 text가 아닌 name 이다. name과 text의 차이는 최소길이가 지정되었는가, 지정되지 않았는가 이다.
    - text는 최소 작성길이가 없으나, name은 최소 작성길이가 1로 지정되어있다.
    - 포함하는 속성은 없으며, 이 문서의 Study 이름이다.
    
    ## 🤦‍♂️StudyDescription
    - body에 작성될수 있는 것은 text이다.
    - 포함하는 속성은 없으며, 해당 study에 대한 설명이다.
    
    ## 🤦‍♂️ProtocolName
    - body에 작성될수 있는 것은 name 이다.
    - 포함하는 속성은 없으며, 계획서의 스폰서 내부 이름을 나타낸다.
    
  ## BasicDefinitions
  - 포함되는 속성은 없다.

    
    ## 🤦‍♂️MeasurementUnit
    - 해당 태그의 속성은 다음과 같다.
    - 데이터 항목 또는 값에 대한 물리적 측정 단위. 해당 의미는 name 속성에 의해 지정된다.


      ### OID
      - 해당 부분 OID의 명명 예시의 경우 MU.1 ... 넘버링 사용하는 것으로 보임.
          
      
      ### Name
      - 속성은 Name 이나, 작성 유형은 text로 되어 있음. 
      - OID 와 동일하게 작성되는 경우도 존재.

            예시:
            <MeasurementUnit OID="MU.1" Name="kg">
      
      ## 🤦‍♀️symbol
      - 포함되는 속성은 없다.
      - 인간이 읽을 수 있는 측정단위 이름을 작성한다.
        
        ## TranslatedText
        - 포함되는 속성은 다음과 같다
          
          ### xml:lang
          - language tag로 작성된다.
          - 설명은 다음과 같이 되어 있으나, 	LL (-CC)* (see below)
          - 실제 사용되는 양식은 다음과 같았다. -> xml:lang="en" , xml:lang="ko" ...etc
      
      ## 🤦‍♀️Alias
      - 사실 MeasurementUnit 이하에 붙는다고 되어있지만, 공식 문서상에는 해당 내용이 존재하지 않는다.
      - 문서상에서 alias 가 붙는건 Contained in:Protocol, StudyEventDef, FormDef, ItemGroupDef, ItemDef, CodeList, CodeListItem, EnumeratedItem, MethodDef, ConditionDef
      - 이곳에 우리가 옵션으로 주는 annotated CRF 변수명같은 내용들이 포함 되어야 한다.

&nbsp;


  ## 🤷‍♂️MetaDataVersion 관련 내용 기술 예정
  - meta 내용 어쩌구 저쩌구
    ## 🤦‍♂️include
    - sdsd
    
    ## 🤦‍♂️protocol
    - 프로토콜 설명 어쩌구
      ## 🤦‍♀️description
      - 설명
      ## 🤦‍♀️studyeventref
      - 연구의 특정 버전 내에서 발생하는 StudyEventRef에 대한 참조
      - StudyEventRefs list : 연구 내에서 발생할 수 있는 연구 StudyEvent유형을 식별. 프로토콜 내의 StudyEventRefs에는 중복된 OrderNumbers나 StudyEventOIDs가 없어야 합니다.
    
        Contained in : Protocol
        
        ## Attributes
        
        | Attributes | type | description |
        | ----- | --- | -------- |
        | StudyEventOID | oidref | StudyEventDef의 OID를 참조한다. |
        | OrderNumber | integer | StudyEventDefs의 목록이 사용자에게 표시될 때마다 사용할 수 있도록 StudyEventDefs에 대한 순서를 제공합니다. event 일정, 작업시간, 데이터 정확성을 의미하는 것은 아니다. |
        | Mandatory | Yes \ No |  Yes일때, MetaDataVersion을 포함하는 임상 데이터가 Study event 인스턴스가 없으면 불완전하다는 것을 나타낸다. 불완전한 ODM 임상 데이터 파일은 연구 검토 및 분석하기에 불완전한 것으로 볼 수 있다.  |
        | CollectionExceptionConditionOID | oidref | Study event에 대한 데이터를 수집하면 안되는 상황을 설명한다. ConditionDef를 참조한다. |
        
        ### 예제
        
        ```xml
        <Protocol>
        	<StudyEventRef StudyEventOID="SE.1" Mandatory="No"/>
        	<StudyEventRef StudyEventOID="SE.2" Mandatory="No"/>
        	<StudyEventRef StudyEventOID="SE.3" Mandatory="No"/>
        </Protocol>
        <StudyEventDef OID="SE.1" Name="Baseline (T0)" Repeating="No" Type="Common">
        	<Description>
        		<TranslatedText xml:lang="en">Baseline (T0)</TranslatedText>
                    <TranslatedText xml:lang="de">Vorbefragung (T0)</TranslatedText>
           </Description>
           		<FormRef FormOID="F.1" Mandatory="No"/>
                    <FormRef FormOID="F.2" Mandatory="No"/>
        </StudyEventDef>
        ```
    
    ## 🤦‍♂️StudyEventDef 

    ![화면 캡처 2022-06-28 164439](https://user-images.githubusercontent.com/25499386/176123580-d7ba92f2-1e5c-40a1-b3f0-2f7820aa4de0.png)

    - Body : Description?, FormRef*, Alias* 을 포함 할 수 있다.

    - event관련해서 openEDC의 내용을 보면 대표적으로 작성되어 있는게 Baseline , follow-up 두 부분을 봤을때, 이는 방문순서의 일부분을 말하는 것으로 보임.
    - 이하 다시 기술하겠지만 방문 타입이 3가지가 존재함. Scheduled 의 경우 예약된 것으로 각 주제에 대해 수집될 것으로 예상하는 일련의 양식.
    - unscheduled 의 경우 심각한 부작용으로 인한 조기종료를 위해 일련의 양식처럼 발생되거나 발생되지 않을 수 있는 데이터를 수집한다.
    - 마지막으로 common의 경우, 유해사례나 병용약물 로그와 같은 여러 다른 데이터 수집 이벤트에서 사용되는 양식이다.

    - 해당 태그는 다음과 같은 속성을 포함한다.
  
      ### ✔OID
      - oid 형식으로 작성. 명명 규칙은 RDF 관련하여 존재하는 것으로 파악.
      
      ### ✔Name
      - name 형식으로 작성
      
      ### ✔Repeating
      - Yes or No 형식으로 작성.
      - 이러한 연구 이벤트가 주어진 주제 내에서 반복적으로 발생하고 있는지 여부
      
      ### ✔Type
      - Scheduled or Unscheduled or Common 세가지 중 하나를 선택	
      - 해당 타입에 따라서 양식이 달라질 수 있음. 각각의 목적이 다름.
      - Scheduled 의 경우, 예약된 것으로 각 주제에 대해 수집될 것으로 예상하는 일련의 양식.
      - unscheduled 의 경우, 심각한 부작용으로 인한 조기종료를 위해 일련의 양식처럼 발생되거나 발생되지 않을 수 있는 데이터를 수집한다.
      - common의 경우, 유해사례나 병용약물 로그와 같은 여러 다른 데이터 수집 이벤트에서 사용되는 양식이다. 
      - 해당 경우  V1 , V2 , V3의 병용약물 정보를 조사하는 경우, 각 Visit 별로 확인 하는 것이 아닌 한번에 보는 형태 (common)
      
      ### ✔Category
      - text 형식으로 작성. 작성 여부는 선택적임.
      - 연구 이벤트에 적합한 연구단계를 나타내는데 사용됨. ex) 선별, 사전 치료, 치료 및 후속조치
  

      ## 🤦‍♀️Description (문서에는 없으나, StudyEventDef 의 Body에 있는 태그)
      - Body : TranslatedText+
      - 연구 메타데이터 구성요소에 대한 설명. 여기에서는 StudyEventDef 에 대한 설명.
      ![화면 캡처 2022-06-29 092226](https://user-images.githubusercontent.com/25499386/176325633-02eaed32-efe1-4f55-9de5-1e20992c7a25.png)
      
      - 해당하는 속성은 없다.
      
        ## 🤷‍♀️TranslatedText
        - 특정 언어에 적합한 사람이 읽을 수 있는 텍스트. 
        - TranslatedText 요소는 일반적으로 시리즈로 나타나며 다양한 언어에 대한 대체 텍스트 변환 세트를 제공한다.
        - 해당 태그는 다음과 같은 속성을 사용한다.
          
          ### xml:lang (optional)
          - 작성 형식은 LanguageTag 이며, LL (-CC)* 형태를 가진다. (language code)-(contury code) ko-kr
            -  *ref https://www.loc.gov/standards/iso639-2/php/code_list.php , https://www.nationsonline.org/oneworld/country_code_list.htm
          - 사용방식은 다음과 같다.
          - ☝️ LT 태그가 있는 대상 언어에 적합한 텍스트를 찾으려면 xml:lang 특성이 LT와 정확히 일치(대소문자 무시)하는 번역 텍스트를 검색한다. e.g. "fr-FR"
          - ✌️ 실패한 경우, LT에서 종료 하위 태그를 제거하고 반복한다. e.g. "fr"
          - 👉 또 실패한 경우, xml:lang 속성이 없는 번역 텍스트를 검색해 사용한다. 만약 찾을 수 없는 경우, 사용 가능한 적절한 텍스트가 없는 것이다.
          

      
      ## 🤦‍♀️FormRef
      ![image](https://user-images.githubusercontent.com/25499386/176326698-63246664-cd9a-47e4-a728-52d219065048.png)
      ![image](https://user-images.githubusercontent.com/25499386/176327262-3fe7db2b-11a5-46cb-8148-c62cf81fba37.png)


      - 특정 StudyEventDef 내에서 발생하는 FormDef에 대한 참조.
      - FormRef 목록은 이러한 유형의 연구 이벤트 내에서 발생하도록 허용된 양식 유형을 식별한다.
      - 단일 StudyEventDef 내의 FormRef에는 중복 FormOID 또는 OrderNumber가 없어야 한다.

          ### ✔FormOID
          - oidref 형식으로 참조는 FormDef의 oid 를 참조한다.

          ### ✔OrderNumber (optional)
          - integer 형식으로 작성.
          - OrderNumbers는 양식 목록이 사용자에게 표시될 때마다 사용할 양식(포함하는 연구 이벤트 내)에 대한 순서를 제공한다.
          - 다만, 이 순서는 이벤트 일정, 시간 순서 또는 데이터 정확성에 대해서는 아무 것도 암시하지 않음.
          
          ### ✔Mandatory
          - yes or no 형식으로 답변.
          - 필수 플래그는 포함하는 연구 이벤트의 인스턴스에 대한 임상 데이터가 이러한 유형의 인스턴스 없이는 불완전할 것임을 나타낸다.
          - 불완전한 ODM 임상 데이터 파일은 연구 검토 및 분석 목적을 위해 불완전한 것으로 간주될 수 있음.
          - 분석적인 측면에서 필요한 것과 필요없는 것을 판단함.
          
          ### ✔CollectionExceptionConditionOID (optional)
          - oidref 형식으로, 참조는 ConditionDef 의 oid 를 참조한다.
          - CollectionExceptionConditionOID 속성이 제공되면 이 Form에 대한 데이터가 수집되지 않아야 하는 상황을 설명하는 ConditionDef를 참조한다.
          - form 데이터가 수집되지 않아야 될 상황에 대한 레퍼런스.
          - 참조를 conditionDef에 대해서 진행함을 기억하자
          ![image](https://user-images.githubusercontent.com/25499386/176353717-0a3c9c12-6550-4450-838e-12a3ce5cbf8b.png)
          - conditionDef 의 body에 조건에 해당하는 내용이 적혀있고, 이하 formal 태그내용에 이에대한 조건식이 작성되어 있음.
          
          - 이 값이 참인 경우에 해당값을 수집하지 않는 방식.
          ![image](https://user-images.githubusercontent.com/25499386/176354276-31564961-abd2-4503-9f9b-765fcbee7e19.png)
          - c.2는 여자가 아닌 경우 
          ![image](https://user-images.githubusercontent.com/25499386/176354353-07442040-491d-4c82-bec9-f900ad1770c5.png)
          - 임신 관련질문에 대한 exception으로 c.2를 걸었음.  


    ## 🤦‍♂️ FormDef
    
    ### 예제
    
    ```xml
    <FormDef OID="F.1" Name="Basis data" Repeating="No">
    	<Description>
    		<TranslatedText xml:lang="en">Basis data</TranslatedText>
    		<TranslatedText xml:lang="de">Basisdaten</TranslatedText>
    	</Description>
    	<ItemGroupRef ItemGroupOID="IG.1" Mandatory="No"/>
    	<ItemGroupRef ItemGroupOID="IG.2" Mandatory="No"/>
    </FormDef>
    <FormDef OID="F.2" Name="Medical history" Repeating="No">
    	<Description>
    		<TranslatedText xml:lang="en">Medical history</TranslatedText>
    		<TranslatedText xml:lang="de">Vorerkrankungen</TranslatedText>
    	</Description>
    	<ItemGroupRef ItemGroupOID="IG.3" Mandatory="No"/>
    	<ItemGroupRef ItemGroupOID="IG.4" Mandatory="No"/>
    </FormDef>
    ```
    연구에서 발생 될 수 있는 양식 유형.

    - Body : Description, ItemGroupRef, ArchiveLayout, Alias
  
    - 해당 태그는 다음과 같은 속성을 포함한다
      ### OID

      ### Name

      ### Repeating

      ## 🤦‍♀️ItemGroupRef
      - 특정 FormDef 내에서 발생하는 ItemGroupDef에 대해 참조한다.
      - ItemGroupRef의 목록은 Form의 유형 내에서 발생할 수 있는 ItemGroup의 유형을 식별한다.
      - 하나의 FormDef 내의 ItemGroupRefs는 중복 ItemGroupOID나 OrderNumber가 없어야한다.
      - 해당 태그는 다음과 같은 속성을 포함한다.
        ### ItemGroupOID

        ### OrderNumber

        ### Mandatory

        ### CollectionExceptionConditionOID

    ## 🤦‍♂️ ItemGroupDef
    
    ### 예제
    
    ```xml
    <ItemGroupDef OID="IG.1" Name="PersonalItems" Repeating="No">
                <Description>
                    <TranslatedText xml:lang="en">Personal questions</TranslatedText>
                    <TranslatedText xml:lang="de">Persönliche Fragen</TranslatedText>
                </Description>
                <ItemRef ItemOID="Age" Mandatory="No"/>
                <ItemRef ItemOID="Gender" Mandatory="No"/>
                <ItemRef ItemOID="Weight" Mandatory="No"/>
                <ItemRef ItemOID="Height" Mandatory="No"/>
                <ItemRef ItemOID="BMI" Mandatory="No" MethodOID="M.1"/>
                <ItemRef ItemOID="Pregnant" Mandatory="No" CollectionExceptionConditionOID="C.2"/>
                <ItemRef ItemOID="WeeksPregnant" Mandatory="No" CollectionExceptionConditionOID="C.5"/>
            </ItemGroupDef>
    
    ```
    - Body : Description?, ItemRef*, Alias* 를 포함할 수 있다.
    - 해당 태그는 다음과 같은 속성을 포함한다.
      ### OID
      - OID 형식으로 작성
      ### Name
      - name 형식으로 작성
      ### Repeating
      - Yes or No 형식으로 작성
      - 반복 플래그는 이러한 유형의 항목 그룹이 포함하는 양식(또는 참조 데이터) 내에서 반복적으로 발생할 수 있음을 나타냅니다.
      ### IsReferenceData
      - Yes or No 형식으로 작성
      - IsReferenceData가 Yes인 경우 이 유형의 항목 그룹은 ReferenceData 요소 내에서만 발생할 수 있습니다. Q. Refdata는 정확이 뭐를 의미하는가
      - IsReferenceData가 No이면 이러한 유형의 항목 그룹은 ClinicalData 요소 내에서만 발생할 수 있습니다
      - 속성의 기본 값은 No 이다.
      ### SASDatasetName
      - sasName 형식으로 작성 
      - 작성 형태는 다음과 같음. ( letter | _ )( letter | digit | _ )* (maxLength="8")
      ### Domain
      - text 형식으로 작성
      - Domain 이하,  Origin, Purpose 및 Comment 속성은 SDTM 메타데이터 제출 지침에 있는 CDISC 제출 메타데이터 모델에 설명된 대로 제출 정보를 전달합니다.
      ### Origin 
      - text 형식으로 작성
      ### Role (Deprecated)
      - name 형식으로 작성
      - But, 더이상 사용되지 않음. (새로운 application은 Role 대신 Purpose를 사용)
      - 역할 속성은 목적의 동의어로 간주될 수 있습니다.
      ### Purpose
      - text 형식으로 작성
      ### Comment
      - text 형식으로 작성

      ## 🤦‍♀️ItemRef
      - Body : none
      - 특정 ItemGroupDef 내에서 발생하는 ItemDef에 대한 참조입니다.
      - ItemRefs 목록은 이 유형의 항목 그룹 내에서 발생하도록 허용된 항목 유형을 식별합니다. 
      - 단일 ItemGroupDef 내의 ItemRef에는 중복된 ItemOID 또는 OrderNumber가 없어야 합니다.
      
      - 해당 태그는 다음과 같은속성을 포함한다.
        ### ItemOID
        - oidref 형식으로 작성 (참조는 ItemDef로 부터)

        ### OrderNumber
        - integer 형식으로 작성
        - OrderNumbers는 항목 목록이 사용자에게 표시될 때마다 사용할 항목(포함하는 항목 그룹 내)에 대한 순서를 제공합니다. 
        - 이벤트 일정, 시간 순서 또는 데이터 정확성에 대해서는 아무 것도 암시하지 않습니다.

        ### Mandatory
        - Yes or No 형식으로 작성
        - 필수 플래그는 포함하는 항목 그룹의 인스턴스에 대한 임상 데이터가 이러한 유형의 항목 인스턴스 없이는 불완전할 것임을 나타냅니다. 
        - 이러한 의미에서 불완전한 ODM 임상 데이터 파일은 연구 검토 및 분석 목적을 위해 불완전한 것으로 간주될 수 있습니다.

        ### KeySequence
        - integer 형식으로 작성
        - KeySequence(있는 경우)는 이 항목이 포함하는 항목 그룹의 키임을 나타냅니다.
        - 또한 키에 대한 순서를 제공합니다.

        ### MethodOID
        - oidref 형식으로 작성
        - MethodOID는 이 항목의 값을 파생하는 데 사용되는 MethodDef를 참조합니다.

        ### ImputationMethodOID
        - 현재는 사용되지 않음.

        ### Role
        - text 형식으로 사용. 
        - 역할 속성은 이 데이터 항목의 사용을 설명하는 단일 역할 이름을 제공합니다.
        - Role이 표준 용어로 정의되면 RoleCodeListOID를 사용하여 Role 속성 값을 가져오는 전체 역할 집합을 정의하는 CodeList를 참조할 수 있습니다.

        ### RoleCodeListOID
        - oidref 형식으로 작성
        - 이 속성은 Role 속성이 정의되어 있지 않으면 존재하지 않아야 합니다.
        - Role이 정의된 경우 RoleCodeListOID는 여전히 선택 사항입니다

        ### CollectionExceptionConditionOID
        - oidref 형식으로 작성 (conditionDef 참조)
        - 수집되지 않아도 되는 경우에 대한 것. 해당 부분은 이미 설명 된 바 있음.

    ## ItemDef
    ### 예제
    
    ```xml
    <!-- Item Definition: Variable Level (BRTHDTC) -->
    <ItemDef OID="IT.DM.BRTHDTC" Name="BRTHDTC" DataType="date"SASFieldName="BRTHDTC">
      <Description>
        <TranslatedText xml:lang="en">Date/Time of Birth</TranslatedText>
      </Description>
        <def:Origin Type="Collected" Source="Investigator">
        <def:DocumentRef leafID="LF.acrf">
        <def:PDFPageRef PageRefs="6" Type="PhysicalRef"/>
        </def:DocumentRef>
        </def:Origin>
    </ItemDef>
    
    ```
    
    - Body : (Description?, Question?, ExternalQuestion?, MeasurementUnitRef*, RangeCheck*, CodeListRef?, Role* Deprecated, Alias*)
    - ItemDef는 연구 내에서 발생할 수 있는 항목 유형을 설명합니다. 항목 속성에는 이름, 데이터 유형, 측정 단위, 범위 또는 코드 목록 제한 사항 및 기타 여러 속성이 포함됩니다.
    
    - 해당 태그의 속성은 다음과 같다.
      ### OID
      - oid 형식으로 작성
      ### Name
      - Name 형식으로 작성
      ### DataType
      - (text | integer | float | date | time | datetime | string | boolean | double | hexBinary | base64Binary | hexFloat | base64Float | partialDate | partialTime | partialDatetime | durationDatetime | intervalDatetime | incompleteDatetime | incompleteDate | incompleteTime | URI ) 형식으로 작성.
      - DataType 속성은 비교 및 ​​저장을 위해 해당 값 요소를 해석하는 방법을 지정한다.
      - DataType이 float인 경우 Length와 SignificantDigits가 모두 제공되거나 둘 다 없어야 한다.
      - DataType=integer인 경우 Length=N은 수신 시스템이 10의 N승 보다 작은 크기의 모든 정수 값을 처리하고 저장할 수 있어야 하는 요구 사항입니다. 더 큰 값은 거부될 수 있습니다.
      - DataType=float인 경우 Length=N 및 SignificantDigits=S는 수신 시스템이 10-S의 배수인 10N-S보다 작은 모든 숫자 값을 처리하고 저장할 수 있어야 하는 요구 사항입니다. 더 큰 값은 거부될 수 있습니다. 중간 값은 10의 -S승 의 가장 가까운 배수로 반올림될 수 있습니다. 
      
      - DataType=text인 경우 Length=N은 수신 시스템이 N보다 작거나 같은 길이의 모든 텍스트 문자열 값을 처리하고 저장할 수 있어야 한다는 요구 사항입니다.
      - Text 유형의 데이터는 ItemDataString 요소에서 전송되어야 합니다.
      ### Length
      - positiveInteger 형식으로 작성
      - +?digit+ (and representing an integer number > 0)
      - Length 속성은 DataType이 텍스트 또는 문자열일 때 필수.
      - DataType이 정수 또는 부동 소수점일 때 선택 사항이며, 다른 데이터 유형에는 제공해서는 안 됩니다.
      ### SignificantDigits
      - nonNegativeInteger 형식으로 작성
      - +?digit+ (and representing an integer number >= 0)
      - SignificantDigits 속성은 DataType이 부동일 때 선택 사항이며 다른 데이터 유형에 대해서는 제공해서는 안 됩니다.
      - Length 및 SignificantDigits는 값 요소에서 이러한 값을 나타내는 데 사용되는 문자 수가 아니라 항목의 데이터 값에 대한 설명입니다.
      ### SASFieldName
      - sasName 형식으로 작성 
      - 작성 형태는 다음과 같음. ( letter | _ )( letter | digit | _ )* (maxLength="8")
      - SAS 소프트웨어에서 식별할 수 있는 변수로 연결?
      ### SDSVarName
      - sasName 형식으로 작성 
      - 작성 형태는 다음과 같음. ( letter | _ )( letter | digit | _ )* (maxLength="8")
      - SDSVarName, Origin 및 Comment 속성은 최신 버전의 CDISC SDTM에 설명된 대로 제출 정보를 전달합니다.
      - 제출 표준에 대해 외부 소프트웨어가 환자 정보를 SDTM 변수에 맞춰 환자정보를 일치시키기 위한 변수. (환자정보를 일치시키다.)matching up patients 
      ### Origin
      ### Comment

      참고: ODM 모델에서 모든 내부 키는 변경할 수 없는 것으로 간주된다. 
      이는 감사 추적 문제가 작동하도록 하기 위해 수행되었습니다. audit trail

      모델의 SubjectKey가 환자의 실제 외부 주제 식별자(또는 무작위 ID)이고 해당 값이 하나의 ODM 파일에서 잘못 전송된 경우 수정할 방법이 없습니다. (???) Q. 잘못 전송된 경우란 어떤 경우를 시사하는가?

      후속 파일의 실수. 이를 수행할 때 외부 주제 키(및 기타 외부에서 볼 수 있는 키 변수)가 메타데이터의 항목으로 정의되어야 합니다.따라서 정상적인 수정/감사 메커니즘을 통해 수정할 수 있습니다. 이것은 연구 키의 수정을 지원하는 문제를 해결하지만 사용자는 어떤 ItemDefs가 특별한 의미를 가지고 있는지 또는 그 의미가 무엇인지 식별할 수 있는 방법이 없습니다. 이것이 문제가 되는 가장 명백한 위치는 외부 소스에서 데이터를 로드할 때 환자를 일치시키는 것입니다. 환자 ID를 찾을 수 없으면 어떻게 일치합니까?

      정답은 ItemDef의 SDSVarName 속성을 사용하는 것입니다. SDSVarName은 비즈니스 의미로 항목에 태그를 지정하는 데 사용할 수 있는 선택적 속성입니다. ODM 모델에서 가능한 모든 의미를 열거하려고 하기보다 ODM 작업 그룹은 CDISC SDTM에 정의된 변수 이름 집합에 의존하는 것이 가장 좋다고 생각했습니다. 이 목록은 임상 데이터 관리에 사용되는 핵심 변수를 포함하기 때문입니다. 따라서 ODM 호환 XML 인스턴스를 처리하는 소프트웨어는 SDSVarName 속성의 특정 값을 사용하여 자주 사용되는 표준 변수를 식별할 수 있습니다. 이 속성의 사용은 SDTM 모델에 정의된 변수로 제한됩니다. 변수에 태그를 지정할 때 해당 변수에 대한 SDTM 정의와 일치하는 것으로 식별합니다. 일반적으로 사용되는 값의 일부 목록은 다음과 같습니다.
      *SDS 는 제출 표준?

      STUDYID (Study Identifier Unique within a Submission)
      USUBJID (Study Identifier Unique within a Submission),
      SUBJID (Subject Identifier Unique within a Study),
      SITEID (Unique Identifier for a study Site)
      SEX (Sex or Gender, coded value),
      VISITNUM (Clinical encounter Number)
      VISIT (Protocol-defined description of clinical encounter),
      VISITDY (Planned study day of VISIT)

      이런 변수들을 쓴다더라~

      - 이하 Body에 대한 설명.
      Question 요소에는 이 항목에 대한 데이터를 제공하라는 메시지가 표시될 때 사용자에게 표시되는 텍스트가 포함됩니다. ExternalQuestion 요소는 동일한 작업을 수행하지만 외부에서 정의된 질문을 참조합니다. 둘 다 있는 경우 일관성이 있어야 합니다.

      MeasurementUnitRefs는 이 유형의 항목에 대해 허용되는 측정 단위를 나열합니다. 숫자 항목만 측정 단위를 가질 수 있습니다. MeasurementUnitRef가 하나만 있는 경우 이 유형의 모든 항목은 기본적으로 이 측정 단위를 사용합니다. ItemDef-MeasurementUnitRef.
      수치 항목의 정의에 MeasurementUnitRef가 없는 경우 항목의 값은 스칼라(즉, 순수)입니다.

      RangeChecks는 이 유형의 항목에 대해 허용되는 값을 제한합니다.

      CodeListRef(있는 경우)는 이 유형의 항목에 대해 허용되는 값을 참조된 코드 목록의 구성원으로 제한합니다.

      참고: 항목은 항목 그룹 내에서 반복되지 않습니다.
    
  

