git revert란 일부 기존의 커밋들을 되돌리는 작업이다. git reset과는 다른 것이, git reset은 기존의 커밋을 아예 삭제해버린다. 하지만 git revert는 변경 사항을 되돌린 커밋을 하나 새로 생성한다. 예를 들어 아래와 같은 커밋 A, B, C가 있다고 가정해보자. (알파벳은 커밋을 구분하기 위해 임의로 붙인 이름이다.)

![image](https://github.com/yeon-06/memo/assets/53105735/9411cf95-b1b5-4d1c-875b-cce915b60a0e)

이 때 커밋 C의 변경 내역을 reset, revert를 통해 되돌린다면 어떻게 될까? 커밋 내역을 살펴보면 git reset은 커밋 C에 대한 기록이 아예 없어진다. git revert는 새로운 커밋 X가 생긴다. 커밋 X의 변경 내역을 살펴보면, 커밋 C에서 변경했던 코드들이 그 이전 상태로 돌아가있다.

![image](https://github.com/yeon-06/memo/assets/53105735/6539cea3-6b68-4a87-a262-8bbfcd52f51e)
