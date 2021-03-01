- 안드로이드 Release시 필요한 정보
1. VersionCode
- App이 가지고 있는 Version을 말하는 정수
- 1부터 시작하여 최대 2147483647까지 표시 가능
- PlayStore에 Release를 VersionCode 1로 했다면 다음 update시에는 최소 버전보다 높은 정수여야한다
- ex) Relase VersionCode가 10으로 store에 올라갔다면 다음 버전은 11부터 가능
- App을 사용하는 유저는 해당 VersionCode가 몇인지 알 수도 알 필요도 없다.

2. VersionName
- 사용자에게 보여지는 Version
- 일반적으로 3.2.1 <major>.<minor>.<patch> 식으로 표시
- major, minor 는 개발자가 직접 컨트롤
- patch 정보 및 VersionCode 는 Release 할 때마다 자동으로 update
