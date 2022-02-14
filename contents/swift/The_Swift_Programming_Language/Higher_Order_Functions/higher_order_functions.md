= **다른 함수를 전달인자로 받거나 함수 실행의 결과를 함수로 반환하는 함수**

스위프트의 함수(클로저)는 일급시민(일급객체)이기 때문에 함수의 전달인자로 전달할 수 있고

함수의 결과 값으로 반환할 수 있다.

스위프트에서 제공하는 map, filter, reduce 고차 함수가 있고 컨테이너 타입(Array, Set, Dictionary 등) 에 구현되어 있다.

## ✅ **map : 변형**

map 함수는 컨테이너 내부의 기존 데이터를 변형하여 새로운 컨테이너를 생성한다.

for 구문과 비슷하게 사용할 수 있지만 map 을 사용하게 되면 클로저 상수를 통해 코드의 재사용이 용이해지고 컴파일러 최적화 측면에서 성능이 좋아진다.

다음 예를 통해 확인해보자.

```swift
let numbers: [Int] = [0, 1, 2, 3 ,4]
var doubledNumbers: [Int]
var strings: [String]

```

각 배열을 생성해주었다. 그리고 for 구문을 통해 배열 안의 값을 추가해보았다.

```swift
doubledNumbers = [Int]()
strings = [String]()

// 기존 for 구문을 통해 값을 추가해줬다.
for num in numbers {
    doubledNumbers.append(num * 2)
    strings.append("\(num)")
}

print(doubledNumbers)
print(strings)

========== 출력 결과 ==========
[0, 2, 4, 6, 8]
["0", "1", "2", "3", "4"]
```

for 구문을 통해서 값을 추가할 수 있지만다음과 같이 map 메서드를 사용해서 배열 안의 값을 추가할 수 있다.

```swift
// map 메서드 사용
// numbers 의 각 요소를 2배하여 새로운 배열 반환
doubledNumbers = numbers.map({ (num: Int) -> Int in
    return num * 2
})
// nubmers 의 각 요소를 문자열로 변환하여 새로운 배열 반환
strings = numbers.map*({(num: Int) -> String in
    return "\(num)"*
})

print(doubledNumbers)
print(strings)

========== 출력 결과 ==========
[0, 2, 4, 6, 8]
["0", "1", "2", "3", "4"]
```

map 메서드를 통해서 값을 하나씩 받아와 클로저를 통해 값을 반환해준다.그리고 지난 번에 배웠던 후행 클로저를 사용해 매개변수와 반환타입, 반환 키워드를 생략해 값을 반환해줄 수 있다.

```swift
// 매개변수, 반환 타입, 반환키워드(return) 생략 가능, 후행 클로저 사용
doubledNumbers = numbers.map { $0 * 2}
print(doubledNumbers)

========== 출력 결과 ===========
[0, 2, 4, 6, 8]
```

## ✅ **filter : 추출**

filter 함수는 컨테이너 내부의 값을 걸러서 새로운 컨테이너로 추출한다.filter 의 매개변수로 전달되는 함수의 반환 타입은 Bool 이다.true 면 값을 포함하고, false 면 값을 배재한다.map 과 마찬가지로 새로운 컨테이너를 생성하여 값을 반환한다.다음 예를 통해 확인해보자.

```swift
let numbers: [Int] = [0, 1, 2, 3 ,4]

// for 구문
// 변수 사용에 주목할 것
var filtered: [Int] = [Int]()

for num in numbers {
    if num % 2 == 0 {
        filtered.append(num)
    }
}

print(filtered)

========== 출력 결과 ==========
[0, 2, 4]
```

for 구문을 통해 조건에 맞는 값을 넣어줄 수 있다.이 부분을 filter 메서드를 사용해서 값을 넣어줄 수 있다.

```swift
// filter 메서드 사용
// numbers의 요소 중 짝수를 걸러내 새로운 배열로 반환, 클로저 사용
let evenNumbers: [Int] = numbers.filter { (num: Int) -> Bool in
    return num % 2 == 0
}

print(evenNumbers)

========== 출력 결과 ==========
[0, 2, 4]
```

클로저를 사용해 짝수인지 아닌지 확인해 true 이면 값을 넣어준다.클로저를 사용했기 때문에 후행 클로저를 통해 간단하게 작성할 수 있다.

```swift
let oddNumbers: [Int] = numbers.filter { $0 % 2 != 0 }

print(oddNumbers)

========== 출력 결과 ===========
[1, 3]
```

추가적으로 map 과 같이 사용할 수도 있다.

```swift
let sumOddNumbers: [Int] = numbers.map { $0 + 3 }.filter{ $0 % 2 == 0 }
print(sumOddNumbers)

========== 출력 결과 =========
[4, 6]
```

## ✅ **reduce : 결합**

reduce 함수는 컨테이너 내부의 콘텐츠를 하나로 통합해준다.정수 배열이면 전달 받은 함수의 연산 결과로 합쳐주고, 문자열 배열이면 문자열을 하나로 합쳐준다.첫 번째 매개변수를 통해 초깃값을 정해줄 수 있다. 초깃값을 클로저를 통해 $0 로 사용할 수 있다.다른 고차 함수들과 연결해서 사용할 수 있다.다음 예를 통해 확인해보자.

```swift
let someNumbers: [Int] = [2, 4, 6]

// for 구문 사용
var result: Int = 0

// someNumbers 의 모든 요소를 더한다.
for num in someNumbers {
    result += num
}

print(result)

========== 출력 결과 ==========
12
```

```swift
// reduce 메서드 사용
// 초깃값이 0, someNumbers 내부의 모든 값을 더한다.
let sum: Int = someNumbers.reduce(0, {
    (first: Int, second: Int) -> Int in
    return first + second
})

print(sum)

// 초깃값 0, someNumbers 내부의 모든 값을 밴다.
let subtract: Int = someNumbers.reduce(0, {
    (first: Int, second: Int) -> Int in
    return first - second
})

print(subtract)

========== 출력 결과 ==========
12
-12
```

```swift
// 초깃값이 3, someNumbers 의 모든 값을 더한다.
let sumFromThree = someNumbers.reduce(3) { $0 + $1 }

print(sumFromThree)
```

출처: [https://jaynamm.tistory.com/entry/Swift-28-고차-함수-map-filter-reduce](https://jaynamm.tistory.com/entry/Swift-28-%EA%B3%A0%EC%B0%A8-%ED%95%A8%EC%88%98-map-filter-reduce)
