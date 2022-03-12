# UIPath
UIPath Error Handling And Skill 공유

👉🏻회사에서 나를 굉장히 힘들게했던 TimeoutError를 정리해보자.

    Why? 🤷🏻‍♂️
    - 일반적으로 Timeout은 UI 정보값인 Selector를 일시적을 못불러올때 발생한다. 

    현상?
    - 위에서 언급한 TimeoutError가 일반적이 생각했지만, 내가 겪은 Timeout은 특이했다. 
    - 원격 접속하 모니터링 중임에도 실행 후 가장 첫번째로 클릭하게되는 Selector 값으 클릭하지 못하고 TimeoutError가 발생하였으며
    - 작업표시줄에 해당 윈도우창이 클릭을 기다리듯이 주황색으로 깜빡깜빡 하는 상태.
    - 그 상태에서 바탕화면 아무곳이나 클리 한번 해주면 그 이후로 프로세스는 잘 가동된다.
    
    해결
    - UIPath Technical Support도 진행 해봤지만, 회사 보안규정상 원격을 해결은 못하고, 알려주는 방법대로 다 해봤지만 효과 0%
    - 진짜 할 수 있는 방법으 다 해봤다. 클릭 전 대기하기, 클릭 두번하기 등등 
    - 그나마 효과있던 방법은 Selector가 Simulate 옵션으로 되어있으면 정상적으로 클릭을 하는데, 이미 개발이 다 된 상태에서 바꾸기가 엄두가 안났다
    - 구글링으로 뜻밖의 수확을 얻을 수 있었는데, Window10과 RDP세션 연결시 버그의 일종이였다.
    - 따라서 충돌이 발생하는 reg를 수정하였고, 그 뒤로 에러가 발생하지 않았다. 👍🏻


👉🏻클릭은 하는데... 조금 느리게 하네.. 에러는 안나는데...? 
    
    Why? 🤷🏻‍♂️
    - 바꾼거라곤 내 바람과는 다르게 속절없이 흘러가는 시간만 바꼈다..
    
    현상
    - UI Selector 정보를 가져오는 Activity들이 전부 엄처 느리게 작동한다. 
    - 작동으 안하는것은 아니고.. 하기 하는데 약 20배정도 느리게?
    
    해결
    - 생각보다 간단했다. 
    - 모든 Selector를 사용하는 Activity는 WaitForReady 라는 Property를 사용 할 수 있다.
    - 각 옵션을 설명하자면
    - None (UI info 가 전부 load 되지 않아도 클릭하겠다.)
    - Interactive (UI info가 어느정도 load되면 클릭하겠다. [default 값])
    - Complete (UI info가 전부 load되어야 클릭하겠다.)
    - 기본값ㅇ interactive로 되어있는데 이를 무자비해보이는 none으로 바꿨더니 됐다. 
    - 문제 해결! 👍🏻
