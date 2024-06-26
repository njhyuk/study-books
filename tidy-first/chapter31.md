# 챕터 31 : 결합도와 결합도 제거

왜 결합도를 완전히 제거하지 않을까? 결합도는 왜 있어야 할까?

* 결합도는 드러나지 않고 동작 변경을 하려다 알아차린다.
  * 이걸 바꾸면 저걸 바꿔야하고 또 저것도...
* 현금흐름 할인은 일부 결합도를 설명한다.
  * 결합도가 생겨도 빠르게 코드를 작성하는 길
  * 결합도 없이 더 긴 시간과 더 많은 노력을 들여서 코드를 작성하는 길
  * 구현할 당시에는 결합도가 있어도 구현하는 것이 경제적인 올바른 결정이었다.
    * 이제 그 나중이 온 것
* 시스템에 결합도가 있어야 하는 또 다른 정당한 이유
  * 방금 전 까지만 해도 문제가 되지 않았다.
  * 언어를 변경해야 될 줄 아무도 몰랐다.
  * 어떤 결합도는 피할 수 없기 떄문이다. (확신에 찬 단언)

## 예제로 살펴보기

보내는 함수와 받는 함수가 있다.

```
send()
    writeField1()
    writeField2()

receive()
    readField1()
    readField2()
```

두 함수 사이에는 결합도가 있다.

변경 사항을 완벽하게 동기화 하여 배포하는 것에 대해 걱정해야 한다.

### 결합도 제거

```
fields = [
    {name: 'field1', type: 'string'},
    {name: 'field2', type: 'string'}
]

send()
    writeFields(fields)
    
receive()
    readFields(fields)
```

결합도가 사라졌다. 한 곳에서 변경할 수 있다.

* 이렇게 하더라도 sender 내부 깊숙한 곳에선 여전히 신규 필드가 추가될때, 계산코드를 추가 해야 한다.
* receive 코드에서는 위 작업이 끝나야 읽을 수 있다. 여전히 결합되어 있다.


## 결론

* 한 종류의 코드 변경에 대한 결합도를 줄일수록 다른 종류의 코드 변경에 대한 결합도가 커진다.
  * 모든 결합을 없애려고 애쓰지 말아야 한다.
* 결합도와 결합도 제거의 정확한 비용은 미리 알 수 없다.
  * 모두 시간이 지남에 따라 발생하는 비용이다.
  * 이로 인해 할인된 현금 흐름이 발생한다.
  * 결합도 제거는 불확실하고 시간이 지남에 따라 가치가 변하는 옵션을 만들어난다.
* 결정 공간은 여전히 남아있다.
  * 결합도에 따른 비용을 지불할 수 있고, 제거 비용을 지불할 수 있다.
  * 소프트웨어 설계까 어려운 것은 당연하다.

