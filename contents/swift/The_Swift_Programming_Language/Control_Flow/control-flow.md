# Swift μ μ΄λ¬Έ(Control Flow)

π μ€μννΈ μ μ΄λ¬Έ : `while`, `if guard`, `switch`, `for-in`

## β For-In λ¬Έ(For-In Loops)

- `for-in` : λ°°μ΄, μ«μμ λ²μ, λ¬Έμμ΄μ λ°λ³΅νλ€.

```swift
//λ°°μ΄ λ°λ³΅
let names = ["Anna", "Alex", "Brian", "Jack"]
for name in names {
	print("Hello, \(name)!")
}
```
π» μΆλ ₯ :
> Hello, Anna!
Hello, Alex!
Hello, Brian!
Hello, Jack!

```swift
//λμλλ¦¬ λ°λ³΅
let numberOfLegs = ["spider" : 8, "ant" : 6, "cat" : 4]
for (animalName, legCount) in numberOfLegs {
	print("\(animalName)s have \(legCount) legs")
}
```
π» μΆλ ₯ :
> cats have 4 legs
ants have 6 legs
spiders have 8 legs

- `μ¬μ (dictionary)`μμ λ°νλ `ν€(key)-κ°(value)` μμΌλ‘ κ΅¬μ±λ ννμ μννλ©° μ μ΄
- `μ¬μ (dictionary)`μ λ΄κΈ΄ μ½νμΈ λ `μ λ ¬μ΄ λμ§ μμ μν`. μ¬μ μ λ£μλ μμλλ‘ μνλμ§ μμ

```swift
//1,2,3,4,5 λ°λ³΅
for index in 1...5 {
    print("\(index) times 5 is \(index * 5)")
}
```
π» μΆλ ₯ :
> 1 times 5 is 5
 2 times 5 is 10
 3 times 5 is 15
 4 times 5 is 20
 5 times 5 is 25
 
 - `for-in` λ¬Έμ μμλλ‘ μ μ΄ν  νμκ° μλ€λ©΄, λ³μμλ¦¬μ `_`ν€μλλ₯Ό μ¬μ©νλ©΄ μ±λ₯μ λμΌ μ μμ
 
```swift
//3μ 10μ κ³±
let base = 3
let power = 10
var answer = 1
for _ in 1...power { //μ¬μ© μ νλ©΄ λΉμλ¬λ λ¨
    answer *= base
}
print("\(base) to the power of \(power) is \(answer)")
```
π» μΆλ ₯ :
>3 to the power of 10 is 59049

```swift
//0λΆν° 60κΉμ§, 60μ ν¬ν¨νμ§ μμ. 0~59 -> 60λ² λ°λ³΅
let minutes = 60
for tickMark in 0..<minutes {
    // render the tick mark each minute (60 times)
}
```

```swift
let minuteInterval = 5
for tickMark in stride(from: 0, to: minutes, by: minuteInterval) {
    // render the tick mark every 5 minutes (0, 5, 10, 15 ... 45, 50, 55)
}
```
- `stride(from:to:by:)` : from - μμνλ μ, to - λλλ μ, by - κ΅¬κ°


```swift
let hours = 12
let hourInterval = 3
for tickMark in stride(from: 3, through: hours, by: hourInterval) {
    // render the tick mark every 3 hours (3, 6, 9, 12)
}
```
- `stride(from:to:by:)` : λ€μμ κ΅¬κ°μ 3μΌλ‘ μ€μ ν κ²½μ°


## β While λ¬Έ(While Loops)

π while loops : `while`, `repeat-while`

### 1οΈβ£ while
```swift 
while condition {
    statements
}
```
- `μ‘°κ±΄(condition)`μ΄ `κ±°μ§(false)`μΌ λκΉμ§ `κ΅¬λ¬Έ(statements)`μ λ°λ³΅


![](https://images.velog.io/images/devjay/post/79a6adfe-a62f-4f4b-87df-a8be58157598/image.png)//GAME
πGAME RULE
- 25κ° μ μ¬κ°ν, 0μμ μμνμ¬ 25κΉμ§ λλ¬νλ κ²μ΄ λͺ©ν
- λ§μ½ μ¬λ€λ¦¬ μμμ§μ μμ λ©μΆλ©΄ μ¬λ€κΈ° λ¨Έλ¦¬λ‘ μ¬λΌκ° μ μμ
- λ§μ½ λ±μ λ¨Έλ¦¬μμ λ©μΆλ©΄ λ±μ κΌ¬λ¦¬λ‘ λ΄λ €κ°μΌ ν¨
```swift
let finalSquare = 25
var board = [Int](repeating: 0, count: finalSquare + 1)
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02; 
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08; 

var square = 0
var diceRoll = 0
while square < finalSquare {
    // roll the dice
    diceRoll += 1
    if diceRoll == 7 { diceRoll = 1 }
    // move by the rolled amount
    square += diceRoll
    if square < board.count {
        // if we're still on the board, move up or down for a snake or a ladder
        square += board[square]
    }
}
print("Game over!")
```
π» μΆλ ₯(μ€κ°μ μ²΄ν¬νλ μΆλ ₯λ¬Έ μΆκ°νμ¬ μΆλ ₯) :
>1λ²μ§Έ λ°λ³΅
square : 0 diceRoll : 1
square(square+diceRoll) : 1
square(square+board[square]) : 1
2λ²μ§Έ λ°λ³΅
square : 1 diceRoll : 2
square(square+diceRoll) : 3
square(square+board[square]) : 11
3λ²μ§Έ λ°λ³΅
square : 11 diceRoll : 3
square(square+diceRoll) : 14
square(square+board[square]) : 4
4λ²μ§Έ λ°λ³΅
square : 4 diceRoll : 4
square(square+diceRoll) : 8
square(square+board[square]) : 8
5λ²μ§Έ λ°λ³΅
square : 8 diceRoll : 5
square(square+diceRoll) : 13
square(square+board[square]) : 13
6λ²μ§Έ λ°λ³΅
square : 13 diceRoll : 6
square(square+diceRoll) : 19
square(square+board[square]) : 8
7λ²μ§Έ λ°λ³΅
square : 8 diceRoll : 7
square(square+diceRoll) : 9
square(square+board[square]) : 18
8λ²μ§Έ λ°λ³΅
square : 18 diceRoll : 2
square(square+diceRoll) : 20
square(square+board[square]) : 20
9λ²μ§Έ λ°λ³΅
square : 20 diceRoll : 3
square(square+diceRoll) : 23
square(square+board[square]) : 23
10λ²μ§Έ λ°λ³΅
square : 23 diceRoll : 4
square(square+diceRoll) : 27
Game over!
Program ended with exit code: 0



### 2οΈβ£ repeat-while
```swift
repeat {
    statements
} while condition
```
- λ€λ₯Έ μΈμ΄μ `do-while`κ³Ό λΉμ·ν¨

```swift
//μμ κ²μμ repeat-whileλ‘ κ΅¬ν
repeat {
    // move up or down for a snake or ladder
    square += board[square]
    // roll the dice
    diceRoll += 1
    if diceRoll == 7 { diceRoll = 1 }
    // move by the rolled amount
    square += diceRoll
} while square < finalSquare
print("Game over!")
```

## β μ‘°κ±΄λ¬Έ(Conditional Statements)
π `if`, `switch` λ κ°μ§ μ‘°κ±΄λ¬Έ
### 1οΈβ£ Ifλ¬Έ
```swift
//ifλ§ μ¬μ©
var temperatureInFahrenheit = 30
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
}

```
π» μΆλ ₯ :
>It's very cold. Consider wearing a scarf.

```swift
//elseλ μ¬μ©
temperatureInFahrenheit = 40
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
} else {
    print("It's not that cold. Wear a t-shirt.")
}

```
π» μΆλ ₯ :
>It's not that cold. Wear a t-shirt.

```swift
//else, else-if μ¬μ©
temperatureInFahrenheit = 90
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
} else if temperatureInFahrenheit >= 86 {
    print("It's really warm. Don't forget to wear sunscreen.")
} else {
    print("It's not that cold. Wear a t-shirt.")
}

```
π» μΆλ ₯ :
>It's really warm. Don't forget to wear sunscreen.


```swift
//else-ifλ§ μ¬μ©
//μλ¬΄κ²λ μΆλ ₯λμ§ μμ
temperatureInFahrenheit = 72
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
} else if temperatureInFahrenheit >= 86 {
    print("It's really warm. Don't forget to wear sunscreen.")
}
```
π» μΆλ ₯ :
>


### 3οΈβ£ Switchλ¬Έ
```swift
switch some value to consider {
case value 1:
    respond to value 1
case value 2,
     value 3:
    respond to value 2 or 3
default:
    otherwise, do something else
}
```
- `switch` λ¬Έμ κΈ°λ³Έ νν

```swift
//λ¬Έμλ₯Ό λΉκ΅ν΄ μ²λ¦¬νλ κ²½μ°
let someCharacter: Character = "z"
switch someCharacter {
case "a":
    print("The first letter of the alphabet")
case "z":
    print("The last letter of the alphabet")
default:
    print("Some other character")
}

```
π» μΆλ ₯ :
>The last letter of the alphabet

### 4οΈβ£ No Implicit Fallthrough

π `C`μ `Objective-C`μ `switch` κ΅¬λ¬Έκ³Όλ λ¬λ¦¬ `Swift`μ `switch`κ΅¬λ¬Έμ μμμ μΈ μ§νμ νμ§ μμ. `C`λ `Objective-C`μμλ `switch ` κ΅¬λ¬Έμ΄ κΈ°λ³Έμ μΌλ‘ λͺ¨λ  `case`λ₯Ό μννμ¬ `default`λ₯Ό λ§λ  λκΉμ§ μ§ν. κ·Έλμ κ·Έκ²μ μ§ννμ§ μκΈ° μν΄ `break`λΌλ λ¬Έκ΅¬λ₯Ό λͺμμ μΌλ‘ μ μ. `Swift`μμλ `break`λ₯Ό μ μ§ μμλ νΉμ  `case`κ° μλ£λλ©΄ μλμΌλ‘ `switch`κ΅¬λ¬Έμ λΉ μ Έ λμ΄. μ΄λ° μ¬μ©λ²μΌλ‘ μΈν΄ μ€μλ‘ `break`λ₯Ό μ μ§μμ μλνμ§ μμ `case`λ¬Έμ΄ μ€νλλ κ²μ λ°©μ§.


```swift
let anotherCharacter: Character = "a"
switch anotherCharacter {
case "a": // Invalid, caseλ¬Έμ bodyκ° μμΌλ―λ‘ μλ¬κ° λ°μ.
case "A":
    print("The letter A")
default:
    print("Not the letter A")
}
// μ»΄νμΌ μλ¬ λ°μ!
```
- `case` μμ μ΅μ νλμ `μ€ν κ΅¬λ¬Έ`μ΄ λ°λμ μμ΄μΌ ν¨.


```swift
let anotherCharacter: Character = "a"
switch anotherCharacter {
case "a", "A":
    print("The letter A")
default:
    print("Not the letter A")
}

```
π» μΆλ ₯ :
>The letter A

- `case` μμ `μ½€λ§(,)`λ‘ κ΅¬λΆν΄μ λ³΅μμ `case` μ‘°κ±΄μ `νΌν©(compound)`ν΄ μ¬μ©

### 5οΈβ£ Interval Matching
```swift
let approximateCount = 62
let countedThings = "moons orbiting Saturn"
let naturalCount: String
switch approximateCount {
case 0:
    naturalCount = "no"
case 1..<5:
    naturalCount = "a few"
case 5..<12:
    naturalCount = "several"
case 12..<100:
    naturalCount = "dozens of"
case 100..<1000:
    naturalCount = "hundreds of"
default:
    naturalCount = "many"
}
print("There are \(naturalCount) \(countedThings).")

```
π» μΆλ ₯ :
>There are dozens of moons orbiting Saturn.

- μ«μμ νΉμ  λ²μλ₯Ό `μ‘°κ±΄`μΌλ‘ μ¬μ©

### 6οΈβ£ Tuples
![](https://images.velog.io/images/devjay/post/b2fd8da4-ce4e-40d4-bc8b-7fde07cfe142/image.png)
```swift
let somePoint = (1, 1)
switch somePoint {
case (0, 0):
    print("\(somePoint) is at the origin")
case (_, 0):
    print("\(somePoint) is on the x-axis")
case (0, _):
    print("\(somePoint) is on the y-axis")
case (-2...2, -2...2):
    print("\(somePoint) is inside the box")
default:
    print("\(somePoint) is outside of the box")
}

```
π» μΆλ ₯ :
>(1, 1) is inside the box

- `νν`μ `μ‘°κ±΄`μΌλ‘ μ¬μ©
### 7οΈβ£ Value Bindings
![](https://images.velog.io/images/devjay/post/9f6a1b00-3d4a-42b5-b8ea-b3d432bf82ee/image.png)

```swift
let anotherPoint = (2, 0)
switch anotherPoint {
case (let x, 0):
    print("on the x-axis with an x value of \(x)")
case (0, let y):
    print("on the y-axis with a y value of \(y)")
case let (x, y):
    print("somewhere else at (\(x), \(y))")
}

```
π» μΆλ ₯ :
>on the x-axis with an x value of 2

- `value bindings` : νΉμ  x, y κ°μ κ°κ° λ€λ₯Έ `case`μ μ μνκ³  κ·Έ μ μλ μμλ₯Ό λ λ€λ₯Έ `case`μμ μ¬μ©

### 8οΈβ£ Where
![](https://images.velog.io/images/devjay/post/63612b3b-ee04-4edc-b839-4cfdf725e5a4/image.png)

```swift
let yetAnotherPoint = (1, -1)
switch yetAnotherPoint {
case let (x, y) where x == y:
    print("(\(x), \(y)) is on the line x == y")
case let (x, y) where x == -y:
    print("(\(x), \(y)) is on the line x == -y")
case let (x, y):
    print("(\(x), \(y)) is just some arbitrary point")
}

```
π» μΆλ ₯ :
>(1, -1) is on the line x == -y

- `case`μ `where` μ‘°κ±΄μ μ¬μ©

### 9οΈβ£ Compound Cases
```swift
let someCharacter: Character = "e"
switch someCharacter {
case "a", "e", "i", "o", "u":
    print("\(someCharacter) is a vowel")
case "b", "c", "d", "f", "g", "h", "j", "k", "l", "m",
     "n", "p", "q", "r", "s", "t", "v", "w", "x", "y", "z":
    print("\(someCharacter) is a consonant")
default:
    print("\(someCharacter) is not a vowel or a consonant")
}

```
π» μΆλ ₯ :
>e is a vowel

- `case`μ `μ½€λ§(,)`λ‘ κ΅¬λΆν΄ `μ¬λ¬ μ‘°κ±΄μ νΌν©`ν΄ μ¬μ©

```swift
let stillAnotherPoint = (9, 0)
switch stillAnotherPoint {
case (let distance, 0), (0, let distance):
    print("On an axis, \(distance) from the origin")
default:
    print("Not on an axis")
}

```
π» μΆλ ₯ :
>On an axis, 9 from the origin

- νΌν© μΌμ΄μ€μμλ `κ°-λ°μΈλ©`μ μ¬μ©
## β μ μ΄ μ μ‘ κ΅¬λ¬Έ(Control Transfer Statements)
π 5κ°μ§ μ μ΄ μ μ‘ κ΅¬λ¬Έ : `continue`, `break`, `fallthrough`, `return`, `throw`
π μ μ΄ μ μ‘ κ΅¬λ¬Έμ μ½λμ μ§νμ κ³μ ν μ§ λ§μ§λ₯Ό κ²°μ νκ±°λ, μ€νλλ μ½λμ νλ¦μ λ°κΎΈκΈ° μν΄ μ¬μ©

### 1οΈβ£ Continue
```swift
let puzzleInput = "great minds think alike"
var puzzleOutput = ""
let charactersToRemove: [Character] = ["a", "e", "i", "o", "u", " "]
for character in puzzleInput {
    if charactersToRemove.contains(character) {
        continue
    } else {
        puzzleOutput.append(character)
    }
}
print(puzzleOutput)

```
π» μΆλ ₯ :
>grtmndsthnklk

- `continue`λ¬Έμ νμ¬ `loop`λ₯Ό μ€μ§νκ³  λ€μ `loop`λ₯Ό μν
### 2οΈβ£ Break
```swift
let numberSymbol: Character = "δΈ"  // μ€κ΅­μ΄λ‘ 3μ μλ―Ένλ λ¬Έμ
var possibleIntegerValue: Int?
switch numberSymbol {
case "1", "Ω‘", "δΈ", "ΰΉ":
    possibleIntegerValue = 1
case "2", "Ω’", "δΊ", "ΰΉ":
    possibleIntegerValue = 2
case "3", "Ω£", "δΈ", "ΰΉ":
    possibleIntegerValue = 3
case "4", "Ω€", "ε", "ΰΉ":
    possibleIntegerValue = 4
default:
    break
}
if let integerValue = possibleIntegerValue {
    print("The integer value of \(numberSymbol) is \(integerValue).")
} else {
    print("An integer value could not be found for \(numberSymbol).")
}
```
π» μΆλ ₯ :
>The integer value of δΈ is 3.

- `break`λ¬Έμ μ μ²΄ μ μ΄λ¬Έμ μ€νμ μ¦κ° μ€μ§. `break`λ¬Έμ `loop`λ `switch`λ¬Έμμ μ¬μ©

### 3οΈβ£ Fallthrough
```swift
let integerToDescribe = 5
var description = "The number \(integerToDescribe) is"
switch integerToDescribe {
case 2, 3, 5, 7, 11, 13, 17, 19:
    description += " a prime number, and also"
    fallthrough
default:
    description += " an integer."
}
print(description)

```
π» μΆλ ₯ :
>The number 5 is a prime number, and also an integer.

- `fallthrough` ν€μλλ μ΄νμ `case`μ λν΄μλ μ€ν. μμμ μΈκΈνλ κ² μ²λΌ `Swift`μμλ νλ² νΉμ  `case`λ₯Ό νλ©΄ λ°λ‘ κ·Έ `switch` λ¬Έμ μ’λ£. λ§μΉ `case` μμ `break`λ₯Ό μλμΌλ‘ λ£μ κ²κ³Ό κ°μ κΈ°λ₯. νμ§λ§ μ΄ `fallthrough` λ₯Ό μ¬μ©νλ©΄ μ΄ μλμΌλ‘ `break`κ° μ¬μ©λλ κ²μ λ§λ ν¨κ³Ό.
- `fallthrough` λ `case` μ‘°κ±΄μ νμΈνμ§ μκ³  κ·Έλ₯ λ€μ `case`λ₯Ό μ€ννκ² λ§λ­λλ€.

### 4οΈβ£ Labeled Statements
```swift
label name: while condition {
    statements
}
```
- `label` μ΄λ¦κ³Ό `while `μ‘°κ±΄μ λ£μ΄ `νΉμ  κ΅¬λ¬Έμ μ€ν`νλ κ΅¬λ¬ΈμΌλ‘ μ¬μ©

```swift
gameLoop: while square != finalSquare {
    diceRoll += 1
    if diceRoll == 7 { diceRoll = 1 }
    switch square + diceRoll {
    case finalSquare:
        // diceRoll will move us to the final square, so the game is over
        break gameLoop
    case let newSquare where newSquare > finalSquare:
        // diceRoll will move us beyond the final square, so roll again
        continue gameLoop
    default:
        // this is a valid move, so find out its effect
        square += diceRoll
        square += board[square]
    }
}
print("Game over!")
```
- `switch` λ¬Έκ³Ό ν¨κ» μ¬μ©

## β μ΄λ₯Έ νμΆ(Early Exit)
```swift
func greet(person: [String: String]) {
    guard let name = person["name"] else {
        return
    }

    print("Hello \(name)!")

    guard let location = person["location"] else {
        print("I hope the weather is nice near you.")
        return
    }

    print("I hope the weather is nice in \(location).")
}

greet(person: ["name": "John"])
greet(person: ["name": "Jane", "location": "Cupertino"])
```
π» μΆλ ₯ :
>Hello John!
I hope the weather is nice near you.
Hello Jane!
I hope the weather is nice in Cupertino.

- `guard`λ¬Έμ μ΄μ©ν΄ νΉμ  μ‘°κ±΄μ λ§μ‘±νμ§ μμΌλ©΄ μ΄ ν μ½λλ₯Ό μ€ννμ§ μλλ‘ `λ°©μ΄μ½λ`λ₯Ό μμ±
## β μ΄μ©κ°λ₯ν API λ²μ  νμΈ(Checking API Availability)
```swift
//κ΅¬λ¬Έμ κΈ°λ³Έ νν
if #available(platform name version, ..., *) {
    statements to execute if the APIs are available
} else {
    fallback statements to execute if the APIs are unavailable
}
```
- `Swift`μμλ κΈ°λ³ΈμΌλ‘ νΉμ  νλ«νΌ (iOS, macOS, tvOS, watchOS)κ³Ό νΉμ  λ²μ μ νμΈνλ κ΅¬λ¬Έμ μ κ³΅. μ΄ κ΅¬λ¬Έμ νμ©ν΄ νΉμ  νλ«νΌκ³Ό λ²μ μ μ¬μ©νλ κΈ°κΈ°μ λν μ²λ¦¬λ₯Ό λ°λ‘ ν  μ μμ. 

```swift
//μ€μ  μ¬μ© μμ
if #available(iOS 10, macOS 10.12, *) {
    // Use iOS 10 APIs on iOS, and use macOS 10.12 APIs on macOS
} else {
    // Fall back to earlier iOS and macOS APIs
}
```

