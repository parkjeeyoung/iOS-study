# ์ด๊ฑฐํ(Enumerations)
***
๐ ์ฐ๊ด๋ ํญ๋ชฉ๋ค์ ๋ฌถ์ด์ ํํํ  ์ ์๋ ํ์
๐ ๋ฐฐ์ด์ด๋ ๋์๋๋ฆฌ ๊ฐ์ ํ์๊ณผ ๋ค๋ฅด๊ฒ ํ๋ก๊ทธ๋๋จธ๊ฐ ์ ์ํด์ค ํญ๋ชฉ ๊ฐ ์ธ์๋ ์ถ๊ฐ/์์ ์ด ๋ถ๊ฐ
๐ ์ ํด์ง ๊ฐ๋ง ์ด๊ฑฐํ ๊ฐ์ ์ํ  ์ ์์

๐ ๋ค์ ๊ฐ์ ๊ฒฝ์ฐ ์๊ธดํ๊ฒ ์ฌ์ฉ
โ ์ ํ๋ ์ ํ์ง๋ฅผ ์ฃผ๊ณ  ์ถ์ ๋ 
โ ์ ํด์ง ๊ฐ ์ธ์๋ ์๋ ฅ๋ฐ๊ณ  ์ถ์ง ์์ ๋
โ ์์๋ ์๋ ฅ ๊ฐ์ด ํ์ ๋์ด ์์ ๋ 

## โ ๊ธฐ๋ณธ ์ด๊ฑฐํ
- `enum` ํค์๋๋ก ์ ์ธ

```swift
enum School {
	case primary	// ์ ์น์
    	case elementary	// ์ด๋ฑ
    	case middle	// ์ค๋ฑ
        case high	// ๊ณ ๋ฑ
        case college	// ๋ํ
	case university	// ๋ํ๊ต
    	case graduate	// ๋ํ์

}
```
- `School`์ด๋ผ๋ ์ด๋ฆ์ ๊ฐ๋ ์ด๊ฑฐํ์๋ `primary`, `element`, `middle`, `high`, `college`, `university`, `graduate`๋ผ๋ ํญ๋ชฉ์ด ์์
- ๊ฐ ํญ๋ชฉ์ ๊ทธ ์์ฒด๊ฐ `๊ณ ์ ์ ๊ฐ`์ด๋ฉฐ, ํญ๋ชฉ์ด ์ฌ๋ฌ ๊ฐ์ง๋ผ์ ๋์ดํ๊ธฐ ๊ท์ฐฎ๊ฑฐ๋ ์ด๋ ต๋ค๋ฉด ํ ์ค์ ๋ชจ๋ ํํํด ์ค ์๋ ์์

```swift
enum School {
	case primary, elementary, middle, high, college, university, graduate
}
```
```swift
//School ์ด๊ฑฐํ ๋ณ์์ ์์ฑ ๋ฐ ๊ฐ ๋ณ๊ฒฝ
var highestEducationLevel: School = School.university

//์ ์ฝ๋์ ์ ํํ ๊ฐ์ ํํ
var highestEducationLevel: School = .university

//๊ฐ์ ํ์์ธ School ๋ด๋ถ์ ํญ๋ชฉ์ผ๋ก๋ง highestEducationLevel์ ๊ฐ์ ๋ณ๊ฒฝํด์ค ์ ์์
highestEducationLevel = .graduate
```

## โ ์์ ๊ฐ (Raw Value)
- ์ด๊ฑฐํ์ ๊ฐ ํญ๋ชฉ์ ์์ฒด๋ก๋ ํ๋์ ๊ฐ์ด์ง๋ง ํญ๋ชฉ์ `์์ ๊ฐ`๋ ๊ฐ์ง ์ ์์
- ํน์  ํ์์ผ๋ก ์ง์ ๋ ๊ฐ์ ๊ฐ์ง ์ ์๋ค๋ ๋ป
- ํน์  ํ์์ ๊ฐ์ ์์ ๊ฐ์ผ๋ก ๊ฐ์ง๊ณ  ์ถ๋ค๋ฉด ์ด๊ฑฐํ ์ด๋ฆ ์ค๋ฅธ์ชฝ์ ํ์์ ๋ช์
- ์์ ๊ฐ์ ์ฌ์ฉํ๊ณ  ์ถ๋ค๋ฉด `rawValue`๋ผ๋ ํ๋กํผํฐ๋ฅผ ํตํด ๊ฐ์ ธ์ฌ ์ ์์

```swift
enum School : String {
	case primary = "์ ์น์"
    	case elementary	= "์ด๋ฑํ๊ต"
    	case middle = "์คํ๊ต"
        case high = "๊ณ ๋ฑํ๊ต"
        case college = "๋ํ"
	case university	= "๋ํ๊ต"
    	case graduate = "๋ํ์"
}

let highestEducationLevel: School = School.university
print("์ ์ ์ต์ขํ๋ ฅ์ \(highestEducationLevel.rawValue) ์กธ์์๋๋ค.")
// ์ ์ ์ต์ขํ๋ ฅ์ ๋ํ๊ต ์กธ์์๋๋ค.

enum WeekDays: Character {
	case mon = "์", tue = "ํ", wed = "์", thu = "๋ชฉ", fri = "๊ธ", sat = "ํ ", sun = "์ผ"
}

let today: WeekDays = WeekDays.fri
print("์ค๋์ \(today.rawValue)์์ผ์๋๋ค.") 
//์ค๋์ ๊ธ์์ผ์๋๋ค.
```

```swift
//์ด๊ฑฐํ์ ์์ ๊ฐ ์ผ๋ถ ์ง์  ๋ฐ ์๋ ์ฒ๋ฆฌ
enum School : String {
	case primary = "์ ์น์"
    	case elementary	= "์ด๋ฑํ๊ต"
    	case middle = "์คํ๊ต"
        case high = "๊ณ ๋ฑํ๊ต"
        case college 
	case university	
    	case graduate 
}

let highestEducationLevel: School = School.university
print("์ ์ ์ต์ขํ๋ ฅ์ \(highestEducationLevel.rawValue) ์กธ์์๋๋ค.")
// ์ ์ ์ต์ขํ๋ ฅ์ university ์กธ์์๋๋ค.

print(School.elementary.rawValue)//์ด๋ฑํ๊ต

enum Numbers: Int {
	case zero
    	case one
        case two
        case ten = 10
}

print("\(Numbers.zero.rawValue), \(Numbers.one.rawValue), \(Numbers.two.rawValue), \(Numbers.ten.rawValue)")
//0 ,1, 2, 10
```
 
## โ ์ฐ๊ด ๊ฐ
```swift
//์ฐ๊ด ๊ฐ์ ๊ฐ๋ ์ด๊ฑฐํ
enum MainDish {
	case pasta(taste: String)
    	case pizza(dough: String, topping: String)
        case chicken(withSauce: Bool)
        case rice
}

var dinner: MainDish = MainDish.pasta(taste: "ํฌ๋ฆผ") //ํฌ๋ฆผ ํ์คํ
dinner = .pizza(dough: "์น์ฆํฌ๋ฌ์คํธ", topping: "๋ถ๊ณ ๊ธฐ") // ๋ถ๊ณ ๊ธฐ ์น์ฆํฌ๋ฌ์คํธ ํผ์
dinner = .chicken(withSauce: true) // ์๋ ํต๋ญ
dinner = .rice // ๋ฐฅ
```

```swift
//์ฌ๋ฌ ์ด๊ฑฐํ์ ์์ฉ
enum PastaTaste {
	case cream, tomato
}
enum PizzaDough {
	case cheeseCrust, thin, original
}
enum PizzaTopping {
	case pepperoni, cheese, bacon
}

enum MainDish {
	case pasta(taste: PastaTaste)
    	case pizza(dough: PizzaDough, topping: PizzaTopping)
        case chicken(withSauce: Bool)
        case rice
}

var dinner: MainDish = MainDish.pasta(taste: PastaTaste.tomato)
dinner = MainDish.pizza(dough: PizzaDough.cheeseCrust, topping: PizzaTopping.bacon)
```

## โ ํญ๋ชฉ ์ํ
```swift 
//CaseIterable ํ๋กํ ์ฝ์ ํ์ฉํ ์ด๊ฑฐํ์ ํญ๋ชฉ ์ํ
enum School: CaseIterable {
	case primary
    	case elementary
        case middle
        case high
        case college
        case university
        case graduate
}

let allCases: [School] = School.allCases
print(allCases)
// [School.primary, School.elementary, School.middle, School.high, School.college, School.university, School.graduate]
```
```swift 
//์์๊ฐ์ ๊ฐ๋ ์ด๊ฑฐํ์ ํญ๋ชฉ ์ํ
enum School : String, CaseIterable {
	case primary = "์ ์น์"
    	case elementary	= "์ด๋ฑํ๊ต"
    	case middle = "์คํ๊ต"
        case high = "๊ณ ๋ฑํ๊ต"
        case college = "๋ํ"
	case university	= "๋ํ๊ต"
    	case graduate = "๋ํ์"
}
let allCases: [School] = School.allCases
print(allCases)
// [School.primary, School.elementary, School.middle, School.high, School.college, School.university, School.graduate]
```

```swift
//available ์์ฑ์ ๊ฐ๋ ์ด๊ฑฐํ์ ํญ๋ชฉ ์ํ
enum School : String, CaseIterable {
	case primary = "์ ์น์"
    	case elementary	= "์ด๋ฑํ๊ต"
    	case middle = "์คํ๊ต"
        case high = "๊ณ ๋ฑํ๊ต"
        case college = "๋ํ"
	case university	= "๋ํ๊ต"
    	@available(iOS, obsoleted: 12.0)
    	case graduate = "๋ํ์"


	static var allCases: [School] = {
		let all: [School] = [.primary, 
    				.elementary, 
    				.middle, 
    				.high, 
    				.college, 
    				.university]
     	   #if os(iOS)
     	   return all
     	   #else
      	   return all + [.graduate]
      	   #endif
       }
}
  
let allCases: [School] = School.allCases
print(allCases)
// ์คํํ๊ฒฝ์ ๋ฐ๋ผ ๋ค๋ฅธ ๊ฒฐ๊ณผ
```

```swift
//์ฐ๊ด ๊ฐ์ ๊ฐ๋ ์ด๊ฑฐํ์ ํญ๋ชฉ ์ํ
enum PastaTaste: CaseIterable {
	case cream, tomato
}

enum PizzaDough: CaseIterable {
	case cheeseCrust, thin, original
}
enum PizzaTopping: CaseIterable {
	case pepperoni, cheese, bacon
}

enum MainDish: CaseIterable {
	case pasta(taste: PastaTaste)
   	case pizza(dough: PizzaDough, topping: PizzaTopping)
    	case chicken(withSauce: Bool)
        case rice
        
        static var allCases: [MainDish] {
        	return PastaTaste.allCases.map(MainDish.pasta)
           		+ PizzaDough.allCases.reduce([]) { (result, dough) -> [MainDish] in 
                		result + PizzaTopping.allCases.map { (topping) -> MainDish in 
                        		MainDish.pizza(dough: dough, topping: topping)
                                }
                        }
                        + [true, false].map(MainDish.chicken)
                        + [MainDish.rice]
        }
}

print(MainDish.allCases.count) //14
print(MainDish.allCases) // ๋ชจ๋  ๊ฒฝ์ฐ์ ์ฐ๊ด ๊ฐ์ ๊ฐ๋ ์ผ์ด์ค ์ปฌ๋ ์
```

## โ ์ํ ์ด๊ฑฐํ
```swift 
//ํน์  ํญ๋ชฉ์ ์ํ ์ด๊ฑฐํ ํญ๋ชฉ ๋ช์
enum ArithmeticExpression {
	case number(Int)
    	indirect case addition(ArithmeticExpresion, ArithmeticExpresion)
        indirect case multiplication(ArithmeticExpresion, ArithmeticExpresion)
}
```

```swift 
//์ด๊ฑฐํ ์ ์ฒด์ ์ํ ์ด๊ฑฐํ ๋ช์
indirect enum ArithmeticExpression {
	case number(Int)
    	case addition(ArithmeticExpresion, ArithmeticExpresion)
        case multiplication(ArithmeticExpresion, ArithmeticExpresion)
}
```

```swift 
//์ํ ์ด๊ฑฐํ์ ์ฌ์ฉ
let five = ArithmeticExpression.number(5)
let four = ArithmeticExpression.number(4)
let sum = ArithmeticExpression.addition(five, four)
let final = ArithmeticExpression.multiplication(sum, ArithmeticExpression.number(2))

func evaluate(_ expression: ArithmeticExpression) -> Int {
	switch expression {
    	case .number(let value):
        	return value
        case .addition(let left, let right):
        	return evaluate(left) + evaluate(right)
        case .multiplication(let left, let right):
        	return evaluate(left) + evaluate(right)
        }
}

let result: Int = evaluate(final)
print("(5 + 4) * 2 = \(result)")
// (5 + 4) * 2 = 18
```
```
