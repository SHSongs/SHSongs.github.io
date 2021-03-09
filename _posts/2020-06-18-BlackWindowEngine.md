---
layout: post
title: "Black Window Engine 사용법 및 개요"
date: 2020-06-16
excerpt: "Black Window Engine"
tag:
- cpp
- engine
- manual
category: [ Cpp ]
feature: ../assets/img/BlackWindowEngine/DemoGame.png
comments: true
---

# Black Window Engine

- [Github](https://github.com/SHSongs/BlackWindowEngine)

콘솔창에서 게임을 만드려면 게임적인 요소 외에 화면을 지우는 등 여러 작업들을 해 주어야 한다. 그러면 게임 로직과 게임 외적인 부분이 섞이기 쉽다.  
이 소스를 이용하면 게임 로직에만 집중할 수 있게 한다.  

#### Engine LifeCycle
EngineManager  
SceneManager

#### SceneManager LifeCycle
Create  
Render


### 엔진 코드 
EngineManager :
```

```
SceneManager :
```
SceneManager::Create()      // Scene 생성될때 실행
SceneManager::Render(float dt)  // 반복적으로 실행 
SceneManager::SceneChange(SceneManager* scene)  // Scene 교체
```
WorldOutliner : Object를 관리해 줍니다   
```
// 오브젝트를 추가합니다.
WorldOutliner::AddObject(Object* object)

// 오브젝트를 이름으로 찾습니다
WorldOutliner::FindObject(string name) 

// 오브젝트를 제거합니다.
WorldOutliner::Destroy(Object* object)
```

Map : SceneManager에 장착된 객체   
String Vector이다   
단순히 맵의 모양을 기억하는 객체

Object : 맵에 있는 유닛
```
constructor
Object::Object(FPosition p, std::string name, std::string shape, Area Area, std::string direction, std::string Type)       
//Type 제거 예정
FPosition 위치 , name 이름, shape 맵에 나타날 모양, Area 크기

// 오브젝트가 한 프레임에 일할 내용 자동실행
Work()

//오브젝트를 이동시킴
Translate(FPosition p)
실수이기 떄문에 느린 움직임 표현 가능 ex) {0.5,0.5}

OnCollision(Object* object) // 매개변수는 충돌한 Object  
```

Tool : 커서이동 도구  
Unit : 
```
struct Position 
struct FPosition
struct Area     //width, height

class PositionTools
{
    // 실수 Position -> 정수 Position
    static Position FPtoIP(FPosition fp);
    // 실수 Position 매개변수를 정수로 비교해줌
    static bool IsEqual(FPosition m, FPosition o);
}
```

### 유저 코드 
? extend SceneManager  
? extend Object 






<script src="https://utteranc.es/client.js"
        repo="SHSongs/Blog-comments"
        issue-term="pathname"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>