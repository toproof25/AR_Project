# AR-Core-Project
### Unity 2022.3.8f1
### AR 프로그래밍 기말 프로젝트
----

## 게임 진행 방법
1. AR Plane을 벽을 인식   
![1 AR 인식](https://github.com/toproof25/AR_Project/assets/41888060/49a882af-f24f-4052-997f-e80292c82b1a)

  
2. 터치를 통해 포탈을 생성(포탈을 통해서만 맵을 볼 수 있다)
3. 조이스틱으로 플레이어를 이동   
![2 포탈 생성 후 조이스틱 이동](https://github.com/toproof25/AR_Project/assets/41888060/f3784539-fcb1-4222-8321-b8b2062ee76d)

  
4. 열쇠를 획득   
![3  아이템 획득](https://github.com/toproof25/AR_Project/assets/41888060/203cb4d2-41ae-407f-bcc5-29e587334624)


5. 몬스터를 피해서 이동(공격 받으면 목숨이 깎인다)   
![4  공격 피격](https://github.com/toproof25/AR_Project/assets/41888060/550f63a7-6e1a-4b15-a772-ef9eed111e80)


6. 탈출 지점까지 이동   
![5  탈출](https://github.com/toproof25/AR_Project/assets/41888060/2135e596-c5f8-4847-9ef0-868ecf6d6d15)



### 환경 설정
- AR Core 템플릿으로 프로젝트 생성
- 3D Beginner: Tutorial Resources 에샛을 추가할 때 그냥 import하면 프로젝트 설정도 모두 오버라이드가 된다.
- 문제는 오버라이드를 하면 AR Core 설정도 변경되어 AR이 제대로 작동하지 않음.
- 고로 Project Setting은 체크 해제 후 모두 import


### 사용 애셋
[Unity Learn | 3D Beginner: Tutorial Resources | URP](https://assetstore.unity.com/packages/essentials/tutorial-projects/unity-learn-3d-beginner-complete-project-urp-143846)

----

### 현재 진행 상황
- 창문을 통해 맵을 보도록 설정(렌더러 마스크 지정)
- 실행 후 터치를 통해 창문을 스폰(해당 창문으로 맵을 확인)

### 남은 과제
- 플레이어 조작
- 1. 창문을 이동하면서 플레이어 컨트롤 UI를 통해 조작
  2. 바닥을 터치하면 플레이어가 해당 위치로 이동

- 게임 진행
- 1. 증강을 이용한 퍼즐 혹은 창문을 증강하면서 맵의 트리거나 열쇠같은 오브젝트를 찾아서 캐릭터와 상호작용
  2. 단순 캐릭터 조작으로 탈출만 하기

----
### 렌더러 마스크 지정(포탈 제작)
- 창문 레이어 PortalWIndow - Transparent  
- 맵 레이어 PortalCOntents - Opaque  
- Project Settings - Quality - Rendering - Render Pipeline Asset -> 렌더러 설정 
- Opaque Layer Mask - PortalContents만 해제
- Transparent ![1 AR 인식](https://github.com/toproof25/AR_Project/assets/41888060/39c2da13-2b1f-4270-919d-08a801a2b34e)
Layer Mask - PortalContents 해제

### 렌더링 포탈-맵 마스크 문제
- Portal 렌더러 설정값은 의도한대로 문제는 없었으나 게임을 실행하면 메인카메라, 프로젝트 렌더러가 기존 URP-Perfomant로 설정이됨
- 그래서 편집씬에서는 정상적으로 창문을 통해서만 맵을 볼 수 있었으나, 게임을 시작하면 렌더러가 바뀌면서 초기화가 되는 현상
- 이를 해결하기 위해 URP-Perfomant의 Renderer List를 마스크 설정이 된 URP-Portal Asset_Renderer로 설정하여, 렌더러가 URP-Perfomant으로 바뀌어도 문제가 없는 것을 확인. 즉 정상적으로 작동함
- 의문인 점은 URP-Performant-Renderer에서도 Portal Renderer와 같이 설정하였는데 다른 결과를 보인다는 점(이 부분은 따로 확인하지는 않았지만 실행하면 URP-Performant-Renderer여기의 설정들도 바뀔 수 있는 가능성이 높다고 생각)
