---
layout: post
title: "HiEngine_input"
date: 2021-01-27
excerpt: "HiEngine_input"
tag:
- cpp
- funtional
- HiEngine
category: [ Cpp ]
feature: ../assets/img/title/basic.jpg
comments: true
---

## C++ Funtional Library를 활용한 Input funtion 등록

[Github](https://github.com/BudlePlay/Hi-Engine2_forLEDMatrix_Linux)


다음과 같은 Function을 
```cpp
void Player::up()
{
	control(UP);
}
```



이런 식으로 등록시킬 수 있다.   
```cpp
input_->BindAction("Up", EInputEvent::IE_Pressed, this, [=]() {
		this->up();
});
```



BindAction의 내부
```cpp
void Input::BindAction(std::string name, EInputEvent KeyEvent, Object* object, const std::function<void()>& func)
{
	input_map_.insert(std::make_pair(name, func));
}
```



input_map은 name과 Function Template를 저장한다.  
그리고 프레임마다 name과 매치되는 function을 실행시킨다.

```cpp
const auto input_setting = InputSetting::Action_map.find(pressed_key);

if (input_setting != InputSetting::Action_map.end())
{
    const auto action_name_setting = input_setting->second;
    const auto input = input_map_.find(action_name_setting);

    if (input != input_map_.end())
        input->second();
}
```




여기서 InputSetting의 Action_map은 Input 장치로부터 받는 int와 지정시킬 name의 맵이다.

```cpp
struct InputSetting
{
public:
	static std::map<int,std::string> create_action_map()
	{
		std::map<int, std::string> m;

		m[0] = "Up";
		m[1] = "Down";
		m[2] = "Left";
		m[3] = "Right";
		m[10] = "Attack";
		return m;
	}

	const static std::map<int, std::string> Action_map;
};
```


