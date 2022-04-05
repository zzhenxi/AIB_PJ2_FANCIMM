# 팬심M 감성분석 팀프로젝트
✏️ 코드스테이츠에서 진행한 기업협업 프로젝트입니다. (with 일리오)

프로젝트 개요
---------------
- 프로젝트 기간 : 2021/12/27 ~ 2022/01/18

**팬과 셀럽을 연결하는 채팅 어플 ‘셀럽M’의 채팅 데이터를 바탕으로 팬들의 심리를 파악합니다.**
팬들이 표현해준 소중한 **팬심**, 파악해야 하는 이유는 무엇일까요? 소통 어플 **팬심M**은 팬들의 참여가 아주 중요해요! 셀럽 역시 팬들의 심리를 알아야 더 전략적으로 팬 관리를 할 수 있죠. 저희 팀은 셀럽이 어떻게 팬 관리를 하면 좋을지 딥러닝 모델을 이용하여 팬 채팅 **감정을 분류**한 후, 상위 셀럽에 대한 **데이터 분석과 가설 검정**을 바탕으로 로드맵을 제시하고자 했어요.

프로젝트 목표와 구성
---------------

  1) 팬심M 서비스의 장점을 셀럽에게 어필
  
      - 팬심M 서비스를 이용하는것이 셀럽에게 어떤 장점이 있는가 ?

        1. 트게더, 유튜브, 팬카페 등 다양한 플랫폼의 팬들과 팬심M을 통해 소통 가능
        2. 타 커뮤니티와 팬심M의 감성분석을 통해 긍정적인 소통의 비율 비교
        
  2) 팬의 참여가 높은 셀럽의 특징 조사
  
      - 시간대별 대화 분석 : 일별 대화량과 시간대별 대화량의 변화를 통해 참여도가 높은 셀럽과 낮은 셀럽의 차이를 확인
      - 긍정/부정 비율 비교 : 참여도가 높은 셀럽과 낮은 셀럽의 대화 중 긍정/부정의 비율 차이를 확인
      - 파일 전송 수 비교 : 대화 이외에 이미지파일 첨부 등의 파일을 전송한 수와 팬들의 대화 참여가 상관이 있는지 확인
      
프로젝트 과정
-------------------
- 데이터 전처리
- EDA
- 라벨링 과정 (KoBERT 모델 fine-tuning)
- 인스타그램 크롤링
- 가설검정 (회귀분석, 상관분석, 비율검정)


결론
--------------------
**3(팬) : 1(셀럽)의 대화 비율을 유지하고, 주 평균 4개의 파일을 전송한 상위 3개의 셀럽에 대해 팬의 긍정률이 34.7 높았어요!**

- **감정 분류**

협업 기업인 ‘일리오’ 측에서 제공해준 만개의 데이터에 대해 긍정, 부정, 일상 3개 label로 나누어 분류해주었습니다. 분류에는 KoBERT 모델을 fine-tuning하여 사용하였고, test dataset에서 88.7의 accuracy가 나왔습니다. 

- **데이터 분석**

대화 비율 분석, 시간 흐름에 따른 대화량 변화, 시간대별 분석, 가설 검정 등을 통해 상위 셀럽들의 속성을 파악하고 시각화 하였습니다.


회고
--------------------
[아쉬운 점]

- 기업으로부터 데이터를 조달 받는데 문제가 생겨 임시로 받은 **10,000개의 라벨이 없는 샘플**로만 프로젝트를 진행. 원래는 10,000개의 샘플을 fine-tuning에 사용하려고 하였으나, 모두 test에 사용하였습니다.
    
    → 한국어로 pre-train된 KoBERT를 사용하고, fine-tuning에는 AI 허브에서 **일상 생활, sns와 관련된 데이터셋**을 가져와 사용하였습니다. 
    
    → 받은 데이터에 대한 라벨링은 팀원 한분과 반절씩 나눠 직접 해주었습니다. 주관적 판단에 맡긴 라벨링이었기 때문에, 라벨을 나누기 애매한 데이터에 대해서는 회의를 통해 맥락을 고려하며 라벨링을 해주었습니다.
    

[개선 방향]

- pre-trained 모델을 선정할때는 학습 시 데이터를 고려할 것
    
    모델을 채택할때, 채팅 데이터의 특성상 은어와 줄임말, 비표준어들이 많이 섞여있다는 것을 고려해야 합니다.
    
    → 위키백과에 나오는 말뭉치로 pre-train된 KoBERT보다 [LMKor](https://github.com/kiyoungkim1/LMkor)같이 다채로운 데이터로 학습한 모델이 더 좋을 수 있습니다.
    

[소감]

- 처음으로 매우 **raw한 채팅 데이터**를 다룰 수 있었던 프로젝트였어요.
    
    아무렇게나 나열된 데이터에서 규칙을 찾아 train을 위한 정갈한 (table 형태의) dataset으로 변환하는 것부터, 문자열 전처리까지 직접 해볼 수 있었습니다.
    
- 첫번째 **팀**프로젝트였어요. 팀원이 있다는 것은 든든한 거야!
    
    저를 포함하여 두명의 팀원밖에 없었지만, 일을 분배하고, 소통하는 것은 쉬운일이 아니였습니다. **노션**을 사용하여 현재 진행중인 업무를 공유하고, 의논할 일이 생기면 줌을 이용하여 회의를 진행하였습니다. **회의는 주에 최소 2번씩** 진행하였어요. 항상 혼자 프로젝트를 해오다가..**의논할 팀원이 있다는건, 정말 든든한 일이군요!😌**
    
- 시각화, 하고보니 조금 뿌듯
    
    BI툴을 사용하는 것을 생각해보았지만, matplotlib로도 예쁘고, 보기 편하게 만들려고 노력했습니다.

팀원
--------------
| <img src="https://avatars.githubusercontent.com/u/86307300?v=4" width="150"> | <img src="https://avatars.githubusercontent.com/u/78654687?v=4" width="150"> |
|:--------:|:---------:|
| [안동기](https://github.com/ADGGi) | [장진희](https://github.com/zzhenxi) |
