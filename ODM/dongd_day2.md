# day2
++ 이모지 추가 해야함.


## 🤦‍♂️StudyEventDef 

![화면 캡처 2022-06-28 164439](https://user-images.githubusercontent.com/25499386/176123580-d7ba92f2-1e5c-40a1-b3f0-2f7820aa4de0.png)

- Body : Description?, FormRef*, Alias* 을 포함 할 수 있다.

- event관련해서 openEDC의 내용을 보면 대표적으로 작성되어 있는게 Baseline , follow-up 두 부분을 봤을때, 이는 방문순서의 일부분을 말하는 것으로 보임.
- 이하 다시 기술하겠지만 방문 타입이 3가지가 존재함. Scheduled 의 경우 예약된 것으로 각 주제에 대해 수집될 것으로 예상하는 일련의 양식.
- unscheduled 의 경우 심각한 부작용으로 인한 조기종료를 위해 일련의 양식처럼 발생되거나 발생되지 않을 수 있는 데이터를 수집한다.
- 마지막으로 common의 경우, 유해사례나 병용약물 로그와 같은 여러 다른 데이터 수집 이벤트에서 사용되는 양식이다.

- 해당 태그는 다음과 같은 속성을 포함한다.
  
  ### OID
  - oid 형식으로 작성. 명명 규칙은 RDF 관련하여 존재하는 것으로 파악.
  
  ### Name
  - name 형식으로 작성
  
  ### Repeating
  - Yes or No 형식으로 작성.
  - 이러한 연구 이벤트가 주어진 주제 내에서 반복적으로 발생하고 있는지 여부
  
  ### Type
  - Scheduled or Unscheduled or Common 세가지 중 하나를 선택	
  - 해당 타입에 따라서 양식이 달라질 수 있음. 각각의 목적이 다름.
  
  ### Category
  - text 형식으로 작성. 작성 여부는 선택적임.
  - 연구 이벤트에 적합한 연구단계를 나타내는데 사용됨. ex) 선별, 사전 치료, 치료 및 후속조치
  
  ## Description (문서에는 없으나, StudyEventDef 의 Body에 있는 태그)
  - 연구 메타데이터 구성요소에 대한 설명. 여기에서는 StudyEventDef 에 대한 설명.
  ![화면 캡처 2022-06-29 092226](https://user-images.githubusercontent.com/25499386/176325633-02eaed32-efe1-4f55-9de5-1e20992c7a25.png)

  
  ## FormRef
  ![image](https://user-images.githubusercontent.com/25499386/176326698-63246664-cd9a-47e4-a728-52d219065048.png)

  - 특정 StudyEventDef 내에서 발생하는 FormDef에 대한 참조.
  - FormRef 목록은 이러한 유형의 연구 이벤트 내에서 발생하도록 허용된 양식 유형을 식별한다.
  - 단일 StudyEventDef 내의 FormRef에는 중복 FormOID 또는 OrderNumber가 없어야 한다.

      ### FormOID
      - oidref 형식으로 참조는 FormDef의 oid 를 참조한다.

      ### OrderNumber (optional)
      - integer 형식으로 작성.
      - OrderNumbers는 양식 목록이 사용자에게 표시될 때마다 사용할 양식(포함하는 연구 이벤트 내)에 대한 순서를 제공한다.
      - 다만, 이 순서는 이벤트 일정, 시간 순서 또는 데이터 정확성에 대해서는 아무 것도 암시하지 않음.
      
      ### Mandatory
      - yes or no 형식으로 답변.
      - 필수 플래그는 포함하는 연구 이벤트의 인스턴스에 대한 임상 데이터가 이러한 유형의 인스턴스 없이는 불완전할 것임을 나타낸다.
      - 불완전한 ODM 임상 데이터 파일은 연구 검토 및 분석 목적을 위해 불완전한 것으로 간주될 수 있음.
      
      ### CollectionExceptionConditionOID (optional)
      - oidref 형식으로, 참조는 ConditionDef 의 oid 를 참조한다.
      - CollectionExceptionConditionOID 속성이 제공되면 이 Form에 대한 데이터가 수집되지 않아야 하는 상황을 설명하는 ConditionDef를 참조한다.
      - form 데이터가 수집되지 않아야 될 상황에 대한 레퍼런스.

      