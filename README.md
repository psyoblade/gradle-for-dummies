# Gradle 

## [작업: Task](https://docs.gradle.org/current/dsl/org.gradle.api.Task.html)
> 모든 작업은 이름을 가지고 있으며 전체 프로젝트에 걸처서 unique 한 값을 가집니다. 이 경로는 세미콜론(:)을 구분자로 접근이 가능합니다.

### Task Actions
> 작업은 Action 객체들의 시퀀스로 구성됩니다. 작업이 수행될 때에 매 작업들은 Action.execute(T) 호출에 의해 순서대로 수행됩니다.
* Task.doFirst(org.gradle.api.Action) 혹은 Task.doLast(org.gradle.api.Action) 호출에 의해 Action 들을 추가할 수 있습니다.

> 그루비 클로저 또한 작업 액션을 추가할 수 있습니다. 액션이 수행될 때에 파라메터로써 작업과 함께 클로저는 호출됩니다
* Task.doFirst(groovy.lang.Closure) 혹은 Task.doLast(groovy.lang.Closure) 호출에 의해 Action 들을 추가할 수 있습니다.

