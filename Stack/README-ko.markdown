# Stack
# 스택

A stack is like an array but with limited functionality. You can only *push* to add a new element to the top of the stack, *pop* to remove the element from the top, and *peek* at the top element without popping it off.

스택은 배열과 유사하긴 하지만 기능이 제한되어 있다. 스택 맨 위에 새로운 원소를 추가하는 것은 *push* 만 가능하고, 맨 위 원소를 제거하는 것은 *pop* 만이 할 수 있으며 *peek* 을 사용하여 맨 위의 원소를 제거하지 않고 꺼낼 수 있다.

Why would you want to do this? Well, in many algorithms you want to add objects to a temporary list at some point and then pull them off this list again at a later time. Often the order in which you add and remove these objects matters.

//

A stack gives you a LIFO or last-in first-out order. The element you pushed last is the first one to come off with the next pop. (A very similar data structure, the [queue](../Queue/), is FIFO or first-in first-out.)

스택은 LIFO 또는 후입 선출 기능을 제공한다. 마지막에 추가한 원소는 다음번에 꺼내는 첫 번째 원소가 된다. (이와 매우 유사한 자료구조로 FIFO 또는 선입 선출을 제공하는 [큐](../Queue/) 가 있다.)

For example, let's push a number on the stack:

한 예로, 스택에 숫자를 추가해 보도록 하자.

```swift
stack.push(10)
```

The stack is now `[ 10 ]`. Push the next number:

이제 스택은 `[ 10 ]` 이 되었다. 다음 숫자를 추가해 보자.

```swift
stack.push(3)
```

The stack is now `[ 10, 3 ]`. Push one more number:

이제 스택은 `[ 10, 3 ]` 이 되었다. 숫자를 한번 더 추가해 보자.

```swift
stack.push(57)
```

The stack is now `[ 10, 3, 57 ]`. Let's pop the top number off the stack:

이제 스택은 `[ 10, 3, 57 ]` 이 되었다. 이번에는 스택의 맨 위의 숫자를 꺼내보도록 하자.

```swift
stack.pop()
```

This returns `57`, because that was the most recent number we pushed. The stack is `[ 10, 3 ]` again.

위 코드는 `57` 을 반환하는데, 이는 57이 가장 최근에 추가한 숫자이기 때문이다. 스택은 다시 `[ 10, 3 ]` 이 되었다.

```swift
stack.pop()
```

This returns `3`, and so on. If the stack is empty, popping returns `nil` or in some implementations it gives an error message ("stack underflow").

위 코드는 `3` 을 반환한다. 스택이 비어있는 경우라면 이 경우 `nil` 을 반환하거나 몇몇 구현체에서는 에러 메세지를 주기도 한다.(스택 언어플로우 같은).

A stack is easy to create in Swift. It's just a wrapper around an array that just lets you push, pop, and peek:

스위프트에서는 스택을 만들기가 쉽다. 이는 단지 푸시, 팝 그리고 픽을 허용하도록 배열을 감싼 래퍼에 지나지 않는다.

```swift
public struct Stack<T> {
  fileprivate var array = [T]()

  public var isEmpty: Bool {
    return array.isEmpty
  }

  public var count: Int {
    return array.count
  }

  public mutating func push(_ element: T) {
    array.append(element)
  }

  public mutating func pop() -> T? {
    return array.popLast()
  }

  public func peek() -> T? {
    return array.last
  }
}
```

Notice that a push puts the new element at the end of the array, not the beginning. 
Inserting at the beginning of an array is expensive, an **O(n)** operation, 
because it requires all existing array elements to be shifted in memory. 
Adding at the end is **O(1)**; it always takes the same amount of time, 
regardless of the size of the array.

푸시는 새로운 요소를 배열의 맨 처음이 아닌 맨 마지막에 넣는다는 것을 명심하도록 하자. 배열의 맨 처음에 추가하는 것은 **O(n)** 연산으로 메모리에 있는 모든 기존 배열 요소를 이동시켜야 하기 때문에 비용이 많이든다.
맨 끝에 추가하는 것은 **O(1)** 으로 배열의 크기에 관계없이 항상 같은 시간이 소요된다.

Fun fact about stacks: 
Each time you call a function or a method, 
the CPU places the return address on a stack. 
When the function ends, the CPU uses that return address to jump back to the caller. 
That's why if you call too many functions -- for example in a recursive function that never ends -- 
you get a so-called "stack overflow" as the CPU stack has run out of space.

스택에 관한 재미있는 사실은 매번 함수나 메소드를 호출 할 때마다 CPU는 반환 주소를 스택에 배치한다는 점이다.

*Written for Swift Algorithm Club by Matthijs Hollemans*
