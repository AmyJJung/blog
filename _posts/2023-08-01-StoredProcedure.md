---
layout: post
title: 회사에서 프로시저를 사용하면서 느낀점
tags:
  - 회사생활
---

<br>

> 오늘은 내가 프로시저를 사용해서 개발하면서 느낀점에 대해 정리해보려고 한다. 현재 나는 회사에서 닷넷, C#, MSSQL을 사용해서 서비스를 개발하고 있다. 입사후 처음 서비스를 파악하려고 SQL Server Management Studio에 들어가서 프로시저 하나를 열었는데, 엄청나게 길고 복잡한 쿼리문을 보고 당황했던 기억이 있다. 우리 회사에서는 프로시저 안에 비즈니스 로직을 넣어서 개발하는 경우가 허다하다. 돌이켜보면 나 역시도 입사 후에 당연하게 이 방식대로 개발을 해왔던것 같다. 그런데 1년 동안 이렇게 개발을 하면서 이게 과연 최선일까? 라는 의문이 들때가 많았다. 그래서 오늘은 내가 <b>프로시저를 사용하면서, 특히 프로시저 안에 비즈니스 로직을 넣어서 개발할 때 느꼈던 단점들에 대해 정리해보았다.</b> 

<br>

### 1. 버전관리가 어렵다

프로시저는 버튼 한번으로 너무나 쉽게 반영이 가능하기 때문에, 누군가 실수로 운영 프로시저의 내용을 수정할 수도 있다. 그리고 여러 개발자가 함께 수정 작업을 진행할 경우 다른 사람이 수정한 내용을 실수로 날리는 경우도 허다하다. 실제로 이런 문제점은 1년동안 정말 많이 경험했다. 그래서 우리팀의 경우 프로시저 내용 자체를 깃에 푸쉬해서 버전관리를 하게 되었는데. 이게 생각보다 더 귀찮고, 이마저도 누군가 수정사항을 푸쉬하지 않을 경우 제대로 버전관리가 되지 않는다. 실제로 나의 경우 입사 초기에는 버전관리가 어려운 프로시저의 특징 때문에 프로시저를 사용해서 개발하는 방식을 사랑했던(?) 적도 있다. 그 이유는 프로시저 배포는 소스 배포 과정에 비해 훨씬 부담이 적고, 티도 잘 안나고, 간편하기 때문이었다. 이 말은 곧 누구나 쉽게 운영중인 프로시저를 조작할 수 있다는 뜻이기 때문에, 제대로 관리되지 않을 경우 서비스 장애로 이어질 수도 있음을 의미한다. 

<br>

### 2. 가독성이 떨어지고 디버깅하기 어렵다

프로시저에 여러 복잡한 로직이 들어있을 경우 가독성이 떨어져서 내용을 파악하는데 꽤 오랜 시간이 걸린다. 그리고 중간에 오타가 있거나 로직의 오류로 인해 디버깅을 할때도 한줄 한줄 읽어내려가면서 오류를 찾아내야 하는데 많은 시간과 집중력이 필요한 것 같다. 특히 동적 쿼리로 개발된 프로시저의 경우는 모든 코드가 빨간색으로 되어있어서 진짜 헬이다.

<br>

### 3. 객체지향적으로 개발할 수 없다

SQL은 객체지향 언어가 아니기 때문에 객체지향적으로 로직을 개발할 수 없다. 그렇기 때문에 객체지향적으로 개발했을 때 얻을 수 있는 여러 장점들을 당연히 기대할 수 없다. 

<br>

### 4. 비즈니스 로직이 분산되어 있어 유지보수가 어렵다

우리 회사의 경우 어떤 개발자분들은 모든 로직을 프로시저 내부에서 처리하고, 또 어떤 개발자분들은 소스코드에서 처리하는 경우도 있었다. 이런 부분들이 통일되지 않다보니 비즈니스 로직이 여러곳에 분산되어 있다. 그렇기 때문에 운영할 때 오류 수정건이 들어오면 비주얼 스튜디오와 SSMS을 왔다갔다 하면서 흐름을 파악하는데 많은 시간이 소요된다. 

<br>

### 5. DB 전문가가 없을 경우 쿼리 퀄리티를 보장할 수 없다

DB는 비싼 자원이기 때문에 효율적인 쿼리를 작성하는게 중요한 것 같다. 또 실행 결과는 같더라도 개발자 역량에 따라 수행시간이 천차만별일 수 있는것 같다. 우리 회사처럼 대부분의 중요한 비즈니스 로직이 프로시저 안에서 실행될 경우, 쿼리 퀄리티가 정말정말 중요하다. 내가 처음 입사했을 시절에는 디비팀DBA 분들이 개발자들이 작성한 쿼리를 다 검수해주는 프로세스가 있었다. 그래서 개발자가 디비에 관한 지식이 좀 부족해도 한번 필터링이 되기 때문에 성능관련 큰 이슈가 없었던 것 같다. 그런데 개발자 수에 비해 DB 인력은 턱없이 부족하고 쌓여가는 프로시저를 모두 디비팀에서 검수하는건 쉽지 않았다. (옆에서 지켜봤는데 DBA 두분이 맨날 야근하면서 갈아넣어서 운영되는 프로세스였다) 결국 그때 DBA분들은 모두 퇴사하시고,,, 그렇게 우리 회사는 DB 암흑기가 시작되었다.. 더이상 디비팀에서 개발자가 작성한 모든 프로시저를 검수해줄 수 없게 되었고, 개발자 각자의 역량에 맡기는 수밖에 없었다. 이때부터 진짜 성능 관련해서 많은 이슈가 발생했던것 같다 (여전히 ing..) 결론은 이런 방식으로 운영하려면 DB전문 인력이 꼭 필요한 것 같다. 

 <br>

<br>

내가 아는 선에서 느낀점들을 정리해보았는데 이거 말고 다른 장점이다 단점도 있을 수 있을 것 같다. 요즘 회사에서 개발을 하다보면 알고보면 간단한 오류인데도 기존 코드를 파악하는데 불필요하게 시간을 잡아먹은 경우가 종종 있었다. 그 원인으로는 아키텍쳐의 문제, 코드 퀄리티의 문제 등을 뽑을 수 있을 것 같다. 이래서 다들 클린 아키텍쳐.. 클린 코드.. 하는가보다. 입사 후 1년 정도는 회사 업무를 파악하고 조금은 수동적으로 다른 분들이 개발하는 방식을 참고해서 개발을 해왔던것 같다. 이제는 그런 방법들을 당연하게 생각하고 모방하는 것을 넘어서 더 좋은 방법은 없을까? 정말 이게 최선일까? 라는 고민을 해야하는 시기가 된것 같다. 그러기 위해서는 회사에서 배우는 내용 외에도 다양한 input(책, 오픈소스, 교육, 커뮤니티 등등) 이 필요할 것 같다. 결론은.. 공부하자!







