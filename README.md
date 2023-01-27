# 프로젝트 매니저

## 📖 목차

1. [소개](#-소개)
2. [프로젝트 구조](#-프로젝트-구조)
3. [구현 내용](#-구현-내용)
4. [실행 화면](#-실행-화면)
5. [트러블 슈팅 & 어려웠던 점](#-트러블-슈팅--어려웠던-점)
6. [참고 링크](#-참고-링크)

## 😁 소개

|<img src= https://i.imgur.com/ryeIjHH.png width=150>|
|:---:|
|[토털이](https://github.com/tottalE)|

## 🛠 프로젝트 구조

### 📊 UML


### 🌲 Tree
```
├── ProjectManager
│   ├── ProjectManager
│   │   ├── Info.plist
│   │   ├── AppDelegate.swift
│   │   ├── SceneDelegate.swift
│   │   ├── Assets.xcassets
│   │   ├── Base.lproj
│   │   ├── Controller
│   │   │   ├── AddProjectViewController.swift
│   │   │   ├── EditProjectViewController.swift
│   │   │   ├── ProjectsViewController.swift
│   │   │   └── SubviewControllers
│   │   │       └── TaskListViewController.swift
│   │   ├── Extensions
│   │   │   └── Date+Extension.swift
│   │   ├── Model
│   │   │   └── Task.swift
│   │   └── View
│   │       ├── HeaderView.swift
│   │       ├── ProjectListView.swift
│   │       ├── TaskCell.swift
│   │       └── TaskSettingView.swift
│   ├── Podfile
│   ├── Pods
│   │   ├── SwiftLint
│   ├── ProjectManager.xcodeproj
│   └── ProjectManager.xcworkspace

```
## 📌 구현 내용

### 프로젝트 전체 구현 사항
- Container View를 통한 로직 분리
메인 Container View에 3개의 Child 뷰를 넣어주어 뷰컨트롤러를 분리해보는 시도를 해보았다. 그 과정에서 각각의 ChildView를 TaskListViewController를 subclassing한 각각의 뷰컨트롤러로 만들어주고 싶었는데 시간이 부족해 일단은 각각의 컨트롤러 객체가 분리는 되어있지만 모두 TaskListViewController 클래스가 객체인 상태이다.
- Cell의 높이가 dynamic하게 변하는 automaticDimension 구현
- 지난 날짜를 빨간색으로 표시하고, 커스텀 포맷으로 표현
- AddProjectViewController를 통해 할일 추가 기능을 구현
- 할일 터치시 상세내용 표시 및 Edit 버튼을 통한 수정화면, 수정 기능 구현
- 길게 셀을 터치할시, Popover을 띄우고 할일의 수행정도를 수정할 수 있도록 구현
- 기한 날짜를 사용자의 지역 포맷에 맞게 구현
- 셀을 스와이핑시 삭제 메뉴를 표시하고 끝까지 스와이핑 혹은 삭제 버튼을 클릭하면 삭제하도록 구현

### Model
#### 1. **Task**
할일을 저장하는 DTO 모델으로 할일의 수행정도를 수정시, Navigation Title 지정시에 필요한 TaskStatus를 함께 가지고 있음.

### Controller
#### 1. ProjectsViewController
- 프로젝트 앱화면을 켰을 때 가장 먼저 나오는 뷰 컨트롤러로, TaskListViewController의 Container View 역할을 한다. Container 내부의 child 뷰들의 데이터를 전달하고 수정하기 위한 Delegate 메서드가 함께 있다.

#### 2. TaskListViewController
- ProjectsViewController의 child view 역할을 하며, popover나 swipeAction들을 관리하는 역할을 한다. 또한, Container 뷰를 통해 데이터를 주고 받으며 교류한다. 
- filter된 Task를 가지고 있어 사용자가 할일의 수행정도를 수정하거나 새로운 할일을 추가했을 때 자동적으로 할일이 추가될 수 있도록 diffableDataSource와 snapShot으로 구현이 되어 있다.

#### 3. AddProjectViewController
- Task를 추가할 수 있는 화면을 위한 컨트롤러이다. 제목, 날짜, 상세 내용을 쓸 수 있으며 done 버튼을 누르면 ProjectsViewController로 데이터가 전달이 되어 TaskListViewController 내부의 filter된 task list로 전달이 된다. 그렇게 Task를 추가할 수 있다.
#### 4. EditProjectViewController
- AddProjectViewController를 부모 클래스로 두는 컨트롤러로, 저장이 아닌 수정을 위한 화면을 담당하고 있다. 수정시에 TableView에서 데이터를 가져와 TaskListViewController로 데이터가 넘어가며, 넘어간 데이터는 ProjectsViewController에 다시 전달되어 삭제 및 추가 기능을 수행한다.
### View

## 📱 실행 화면
|할일 추가 화면|
:--:
|![](https://i.imgur.com/ttE1aBl.gif)|
|할일 수정 화면|
|![](https://i.imgur.com/tvNCiz6.gif)|
|할일 척도 변경 기능|
|![](https://i.imgur.com/fqwF8rY.gif)|
|할일 삭제 기능|
|![](https://i.imgur.com/3oRUWuT.gif)|


## ❓ 트러블 슈팅 & 어려웠던 점
추후 추가 예정 - PR 리뷰 후 추가

---

## 📖 참고 링크

[UIPicker](https://developer.apple.com/documentation/uikit/uipickerview)

---

[🔝 맨 위로 이동하기](#일기장-)
