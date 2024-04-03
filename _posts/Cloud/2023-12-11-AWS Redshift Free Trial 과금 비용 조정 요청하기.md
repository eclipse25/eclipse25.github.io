---
layout: post
title: "AWS 과금 비용 조정 요청하기"
categories: [Cloud]
tags: [Cloud, AWS]
---

대충 배경은 이렇다.

데브코스에서 팀프로젝트를 하던 중 어쩌다가 Redshift에 스키마와 테이블을 만들고 여기에 S3 버킷에 있는 csv파일들을   카피해서 데이터베이스를 만드는 역할을 맡게 되었다.

<img width="640" alt="aws1" src="https://github.com/eclipse25/eclipse25.github.io/assets/109349939/391b9b70-4d39-47c8-b87b-dedb419c992e">

AWS에는 서비스들을 일정량 무료로 사용하게 해주는 것들이 있는데 나도 Redshfit를 사용해보는데 있어 데이터 교육과정 중에 안내받았던 대로 주황색의 free trial로 프로젝트를 진행하고 있었다.

그런데 마지막 날 갑자기 무료로 받은 크레딧이 끝나있었고... 바로 만들어두었던 인스턴스를 모두 삭제했지만 결국 이렇게 됐다ㅜㅜ

![aws2](https://github.com/eclipse25/eclipse25.github.io/assets/109349939/41bfa5d4-b0d2-4971-aad5-249c98602e12)

공부용으로도 웬만하면 그 1년치 프리티어가 아니면 개인계정으로 AWS를 사용하지 않는 편이 나을것 같다. Redshift가 비싸다고 했을 때 그 말을 들었어야 했는데 무료 구간에서도 생각보다 크레딧이 빠르게 줄어든다..! 나는 거의 하루만에 거의 250달러가 넘게 청구된 것 같다.(크레딧 줄어든 것 포함)

(이틀정도 Redshift에 조금씩 스키마랑 테이블 몇개 만들었고 카피해서 Superset에서 연결해서 하루정도 밖에 안썼다..)

테이블에 복사했던 파일 크기들도 다 그냥 바이트에서 11KB 수준이라 크게 걱정을 안했는데 정말 단 몇시간 안보는 사이에 무료 크레딧이 다 끝나 있었고 거의 바로 삭제했는데 123달러가 청구되어 있었다.

생각보다 이런 일이 빈번하게 있고 학생이면 한번은 봐준다는 것 같길래 메일을 보내보기로 했다.

근데 메일이 아니라 Support Center에서 Case를 작성해야 한다.(결국 GPT 동원해서 Case 씀)

한국어로 써도 된다고는 했는데 빠른 처리 기원 + 하기 싫은 애매한말할때는 영어가 최고라서 그냥 영어로 보냈다.

![aws3](https://github.com/eclipse25/eclipse25.github.io/assets/109349939/c0aeaf1c-2338-4143-9bad-64a9f9f009d8)

똑같이는 아니지만 대충 이렇게 썼는데 한국어를 선호한다고 체크했더니 한국어로 답변을 주셨다. 영어로도 주신다...

> 안녕하세요, AWS 고객지원팀입니다. 고객님의 문의를 한국어 지원팀에서 접수했습니다.  
> 현재 많은 고객님들의 계정 및 요금 관련 문의가 접수되고 있습니다.  
> 문의에 대한 상세 확인을 마치는 대로 케이스를 통해 순차적으로 답변드리겠습니다.  
> 감사합니다.
>
> We value your feedback. Please share your experience by rating this and other correspondences in the AWS Support Center. You can rate a correspondence by selecting the stars in the top right corner of the correspondence.
>
> Best regards,   
> Amazon Web Services

이렇게 왔고 하루 더 있다가 아래처럼 왔다.

> 안녕하세요, 아마존 웹 서비스입니다. AWS 프리 티어(Free Tier) 사용 중 예상치 못한 비용이 발생하여 문의하신 것으로 이해하였습니다. 비용이 발생한 배경과 예외적으로 비용 조정 검토를 접수하는 절차에 대해 안내드리겠습니다. \[비용이 발생한 배경\] 고객님의 청구 내역을 확인한 결과, 계정 내 Asia Pacific (Seoul) 리전에서 운영 중이던 Redshift의 Serverless로 인해 비용이 발생한 것으로 확인하였습니다. AWS 프리 티어는 고객에게 서비스별로 지정된 한도 내에서 무료로 AWS 서비스를 살펴보고 사용해 볼 수 있는 기능을 제공합니다. 다만, 프리 티어가 범주에 포함되지 않거나 프리 티어 범위를 초과할 경우에는 사용량에 따라 표준 서비스 요금을 지불하시게 됩니다. Redshift 프리티어 범주는 2개월간 매월 DC2.Large 노드 750시간을 제공하는 것으로 확인되며, Serverless는 프리 티어 범주에 포함되지 않는 것으로 확인됩니다. 고객님의 비용에 대한 세부 내역은 아래 빌링 콘솔에서 확인할 수 있습니다. - 빌링 콘솔:  
> https://console.aws.amazon.com/billing/home#/bill  
> 비용이 발생한 리소스별 표준 요율은 다음 링크를 통해 확인하실 수 있습니다. - Amazon Redshift 요금:  
> https://aws.amazon.com/ko/redshift/pricing/  
> 보다 자세한 내용이 궁금하실 경우, 아래의 링크 참고 부탁드리겠습니다. - AWS 프리 티어 사용:  
> https://docs.aws.amazon.com/ko\_kr/awsaccountbilling/latest/aboutv2/billing-free-tier.html  
> \- AWS 프리 티어 FAQ:  
> https://aws.amazon.com/ko/free/free-tier-faqs/  
> \[과금 리소스 삭제\] 현재 비용이 발생한던 Redshift 리소스는 모두 삭제된 것으로 확인됩니다. 본 계정을 추가로 확인한 결과 Redshift 외에도 다양한 리소스가 운영되고 있는 것으로 확인됩니다. 추후 과금에 대한 모든 가능성을 배제하기 위해 사용을 원하지 않는 모든 리소스에 대한 삭제를 부탁드립니다. 콘솔 접속 시, 우측 상단 지역을 'Asia Pacific (Seoul)' 으로 설정하여 삭제 진행 부탁드립니다. ● Glue Database 삭제 방법  
> https://docs.aws.amazon.com/glue/latest/dg/console-databases.html  
> ● Secrets Manager 삭제 방법  
> https://docs.aws.amazon.com/secretsmanager/latest/userguide/manage\_delete-secret.htmlt  
> ● S3 버킷 삭제 방법 - 리전 선택이 불필요합니다.  
> https://docs.aws.amazon.com/ko\_kr/AmazonS3/latest/userguide/delete-bucket.html  
> 현재 운영 중인 리소스를 삭제 후 회신해 주시면, 본 계정 내 추가 비용이 발생하는 지 확인을 위해 본 계정의 세부 모니터링을 진행할 예정입니다. 본 계정의 세부 모니터링이 진행되는 동안, 유관 부서에 예외적으로 비용 조정 검토 요청을 접수하기 위한 문항을 안내해 드리겠습니다. 비용 조정 요청은 유관 부서에서 검토 후 승인 여부가 결정되기 때문에, 현시점에서 비용 조정 가능 여부 및 금액에 대하여 확답을 드릴 수 없으며, 해당 요청을 검토하는데 시일이 소요될 수 있는 점 미리 양해 부탁드립니다. 관련하여 추가 문의 사항 혹은 요청 사항이 있으시면 언제든지 본 케이스를 통해 회신 주시기 바라며, 본 케이스의 회신은 하기의 서포트 센터 링크에 접속하시면 등록하실 수 있습니다. · 서포트 센터 링크: https://console.aws.amazon.com/support/home?#/case/?caseId=  
> 감사합니다.  
> We value your feedback. Please share your experience by rating this and other correspondences in the AWS Support Center. You can rate a correspondence by selecting the stars in the top right corner of the correspondence.  
> Best regards, Amazon Web Services

프리 티어와 레드시프트 프리 트라이얼이 다른 것이라는 사실을 알게 되었다... 아무튼 Redshift 말고도 활성화 해 놓은 인스턴스들 중에 삭제가 가능한 것은 다 삭제하고 회신했다.

그랬더니 이렇게 답장을 받았다. (답장은 보통 하루 이내에서 주시는 것 같다.)

> 안녕하세요, 아마존 웹 서비스입니다. 신속한 삭제 조치와 회신에 감사드립니다. 고객님의 계정을 확인한 결과 안내드린 리소스에 대한 삭제가 완료된 것으로 확인됩니다. 비용 조정 담당팀으로 비용 조정 검토 요청을 접수하기 위해 하기 필수 문항에 회신해 주시기 바랍니다. 담당팀은 하기에 작성된 정보를 토대로 요청을 검토할 예정이므로, 상세한 답변 부탁드립니다.
>
> \[1\] 비용 조정을 요청하는 서비스 / 기간 / 금액 아래 AWS 결제 및 비용 관리 콘솔 청구서 페이지를 확인하여 지난 청구 세부 정보를 확인하신 후, 원하지 않는 비용이 발생한 서비스명, 기간, 그리고 금액을 회신해 주시기를 바랍니다:  
> https://console.aws.amazon.com/billing/home#/bills  
> \* 서비스명:  
> \* 기간:  
> \* 금액 (월별로 기재 부탁드립니다): (서비스세부 항목 우측에 위치한 '세전 금액'으로 기재 부탁드립니다.)  
> \[2\] 아래의 (3) 가지 방법 중 (1) 개 이상 설정 후 설정한 방법 회신 \* AWS Budget:  
> http://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/budgets-managing-costs.html  
> \* Cloudtrail: https://aws.amazon.com/cloudtrail/getting-started/  
> \* Cloudwatch: http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-cloudwatch.html  
> \[3\] 리소스 삭제, 계정 해지 이외 예상치 못한 비용 발생 방지를 위해 노력하고 계신 대책 (예: AWS 요금 체계에 대한 연구 및 건전한 리소스 사용법에 대한 숙지 등)
>
> 비용 조정은 전담팀에서 검토 후 승인 여부가 결정되기 때문에 현시점에서 비용 조정 가능 여부 및 금액에 대하여 확답을 드릴 수 없으며, 해당 요청을 검토하는데 시일이 소요될 수 있는 점 미리 양해 부탁드립니다. 마지막으로 AWS 계정 내 모든 활동과 그에 따라 발생하는 서비스 요금에 대한 책임은 사용자의 의도 및 해당 활동에 대한 승인 여부와 관계없이 사용자에게 있음을 안내해 드립니다. AWS 이용 계약 및 공동 책임 모델을 통해 AWS는 AWS 클라우드에서 제공되는 모든 서비스를 실행하는 네트워크 및 인프라를 보호할 책임을 지며, 개인 계정 관련 활동 및 이에 따른 보안 책임 및 수행 범위는 사용자에게 있음을 명시하고 있습니다. 자세한 내용은 아래 링크를 통해 확인하실 수 있습니다.  
> \* AWS 이용 계약 |  
> https://d1.awsstatic.com/legal/aws-customer-agreement/AWS\_Customer\_Agreement-Korean\_2020-11-30.pdf  
> \* AWS 와 사용자간의 공동 책임 모델 |  
> https://aws.amazon.com/ko/compliance/shared-responsibility-model/  
> 그럼 고객님의 회신을 기다리겠습니다. 추가 문의사항이 있으시면 언제든지 본 케이스를 통해 회신주시기 바랍니다. 감사합니다.  
> We value your feedback. Please share your experience by rating this and other correspondences in the AWS Support Center. You can rate a correspondence by selecting the stars in the top right corner of the correspondence.  
> Best regards, Amazon Web Services

이전에 학생이고 공부하는데만 썼으니까 한번만 봐주시면 좋겠다고 살짝 빌었는데 사유가 뭐든 어쨌든 비용이 발생한 것은 니 책임이라는 말을 살짝 붙이길래 걱정했는데 그래도 잘 해결되었다.

해당 내용을 받고 AWS Budget에서 예산을 생성했는데 생각보다 매우 간단했다. 다른 내용들은 아주 길게 쓸 필요 없고 그냥 두세줄 정도 공손하게 쓰면 그래도 한번은 봐주시는 것 같다.

![aws4](https://github.com/eclipse25/eclipse25.github.io/assets/109349939/dad71be6-a4cd-4d1d-b585-2e8d4b5604cb)

하루 - 이틀 사이에 다음과 같은 답변을 받았고 다행히도 잘 마무리 되었다.

<img width="527" alt="aws5" src="https://github.com/eclipse25/eclipse25.github.io/assets/109349939/2bb1c7e3-64ed-450a-ac1e-19dccc522cdb">
<img width="521" alt="aws6" src="https://github.com/eclipse25/eclipse25.github.io/assets/109349939/b95b9b74-443c-4499-8822-faa489c85157">

혹시 비슷한 일을 겪었다면 너무 당황하지 말고 한번만 봐달라고 서포트 센터에 요청해보자... 그렇지만 두번은 안봐주실 것 같기 때문에 개인적인 용도로 비용을 발생시킬 일이 없도록 하는게 좋을 것 같다.
