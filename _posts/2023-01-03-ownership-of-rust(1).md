---
title: ownership of rust(1)
date: 2023-01-03 12:40:00 +09:00
categories: [RUST]
tags: [rust, ownership]
---

## Ownership
Ownership이란 Rust만의 유니크한 특성이며, gc없이도 안전하게 메모리를 사용하게 해주는 개념이다.

## What is Ownership?
Ownership은 Rust가 어떻게 memory를 관리할 지 통제하는 규칙들의 set이다.   

어떤 언어들은 garbage collection이 주기적으로 더이상 사용하지 않는 메모리들을 관리해주고(Java, JS, Python, GO)
어떤 언어들은 프로그래머가 직접 할당과 해제를 하여 메모리를 관리해야 한다.(C, C++)   

**Rust는 그 외의 방식: compiler가 체크하는 규칙들의 set인 ownership 시스템에 의해 관리된다.**   
>> 규칙이 위배된다면, compile되지 않는다!

### The Stack and the Heap
대부분의 언어들은 작업할 때 stack과 heap에 대해 신경쓰지 않아도 된다.   
하지만 Rust는 value가 stack or heap 어디에 있는 값인지에 따라 다르게 작동한다.   
따라서 여기서 간단하게 짚고 넘어가겠다.   
#### Stack
- Last in, First out (접시쌓기와 같다)
- data는 known, fixed size 
- fast

#### Heap
- Allocator가 heap에서 충분한 자리를 찾고 pointer을 return(Allocating: 레스토랑의 자리 안내와 같다)
- Compile시 unknown size => Heap
- slow
- more work

### Ownership Rules
다음의 규칙들은 기억하고 예제를 봅시다!   

- Rust에서 각 Value는 owner가 있다.
- 한 번에 한 owner만 있을 수 있다.
- owner가 scope를 벗어나면 value는 drop된다.

### Variable Scope
`````
fn main() {
    {                      // s is not valid here, it’s not yet declared
        let s = "hello";   // s is valid from this point forward

        // do stuff with s
    }                      // this scope is now over, and s is no longer valid
}

`````
이 코드에서 중요한 사실 두가지:   
- scope 안에서 s는 valid하다.
- scope를 벗어나면 no longer valid하다.

### The String Type
위의 예제는 string literals로 많은 상황에 맞지 않고, 변형불가능하다.   
우리는 String을 사용하여 unknown한 값을 저장할 수 있다.   
`````
let s = String::from("hello");
`````
변형 또한 가능하다.
`````
let mut s = String::from("hello");

s.push_str(", world!"); // push_str() appends a literal to a String

println!("{}", s); // This will print `hello, world!`
`````

왜 String은 변형 가능하지만 literals는 불가능할까?    
이는 두 타입의 메모리 저장 방식이 다르기 때문이다.   

### Memory and Allocation
변형가능하며 늘어날 수 있는 text를 위해서 우리는 heap에 메모리를 할당해야 한다.   
이것은 곧   
- runtime에 allocator에 의해 메모리가 요청되어야 한다.
- 우리가 해당 String에 관하여 업무가 끝났을 때 이 메모리는 allocator에게 반환 되어야 한다.

을 의미한다.   

첫번째 부분은 String::from 을 호출 함으로 해결된다.   
두번째 부분이 쉽지않다. GC가 존재하지않으니 우리가 직접 메모리를 관리해야 한다.   
너무 빨리 정리하면 invalid해지고, 두번 실행해도 bug이다.   
**우리는 딱 한번의 allocate와 딱 한번의 free로 매치해야 한다.**

변수가 해당 scope 밖으로 나가면 Rust는 'drop'이라는 함수를 call하여 메모리를 정리한다.

#### Variables and Data interacting with Move
`````
let s1 = String::from("hello");
let s2 = s1;
`````
해당 코드는 s2에 s1의 value를 단순히 복사할 것 같지만 그렇지 않다.   
![trpl04-01](https://user-images.githubusercontent.com/56327550/210301736-0f644f72-106f-4426-ad62-13b870f0b6a7.svg)   

왼쪽의 ptr, len, capacity의 정보들은 stack에 저장되고,   
우측의 contents는 heap 메모리에 저장된다.

s2에 s1을 할당할 때, contents가 아닌 해당 정보가 담긴 stack의 값만 복사된다.(아래의 사진)

![trpl04-02](https://user-images.githubusercontent.com/56327550/210301989-694fc816-c695-4185-be72-6d6b3c68ce5d.svg)   

따라서 두개의 포인터가 같은 곳을 바라보고 있게 된다는 뜻인데,   
앞서 말했듯 scope를 벗어나면 free 시킬 것이고 그렇다면 두개의 포인터 모두    
같은 메모리에 대해 중복으로 처리를 시도하게 된다. 이는 한번 allocate - 한번 free를 위해된다.

이러한 메모리 safety를 위해서 rust는 let s2 = s1 실행시 s1은 더이상 valid하지 않다고 여긴다.
`````
let s1 = String::from("hello");
let s2 = s1;

println!("{}, world!", s1); // Error!
`````

이는 다른 언어의 shallow copy, deep copy의 원리와 비슷하다.   
또한 이 경우 우리는 s1에서 s2로 이동했다고 표현한다.

![trpl04-04](https://user-images.githubusercontent.com/56327550/210302828-a02f1105-a5f4-48c4-a4f7-e1ea88797988.svg)   
(s1 invalid, scope 벗어날 시 s2는 memory free 실행)

#### Variables and Data interacting with Clone
위와는 달리 heap data까지 deep copy를 하고 싶으면 우리는 Clone을 사용할 수있다.

`````
let s1 = String::from("hello");
let s2 = s1.clone();

println!("s1 = {}, s2 = {}", s1, s2);
`````

#### Stack-Only Data: Copy
`````
let x = 5;
let y = x;

println!("x = {}, y = {}", x, y);
`````   
다음과 같은 integer값은 clone 필요없이 잘 작동한다.   
integers 같은 값은 정해진 size이며 전체 값이 stack에 저장된다.   
따라서 실제값을 copy하는 데에도 굉장히 빠르다.   

Rust는 'Copy'라는 special annotation을 갖고있는데, 만약 type이 Copy를 implements한다면   
위 예제의 '이동'이 발생하지않고 평범하게 copy되고 할당 후에도 계속 valid하다.   

Copy를 implements하는 타입 목록은 다음과 같다.   
- All the integer types.
- The Boolean type
- All the floating-point types
- The character type
- Tuples, if they only contain types that also implement Copy.(둘다 Copy를 implement하는 경우)


### Ownership and Functions
함수에 값을 전달하는 것도 변수에 초기화 하는 것과 비슷하다.   
move or copy. 

`````
fn main() {
    let s = String::from("hello");  // s comes into scope

    takes_ownership(s);             // s's value moves into the function...
                                    // ... and so is no longer valid here

    let x = 5;                      // x comes into scope

    makes_copy(x);                  // x would move into the function,
                                    // but i32 is Copy, so it's okay to still
                                    // use x afterward

} // Here, x goes out of scope, then s. But because s's value was moved, nothing
  // special happens.

fn takes_ownership(some_string: String) { // some_string comes into scope
    println!("{}", some_string);
} // Here, some_string goes out of scope and `drop` is called. The backing
  // memory is freed.

fn makes_copy(some_integer: i32) { // some_integer comes into scope
    println!("{}", some_integer);
} // Here, some_integer goes out of scope. Nothing special happens.
`````
takes_ownership(s); 이후에 s를 호출하면 compile-time Error!   


### Return Values and Scope
`````
fn main() {
    let s1 = gives_ownership();         // gives_ownership moves its return
                                        // value into s1

    let s2 = String::from("hello");     // s2 comes into scope

    let s3 = takes_and_gives_back(s2);  // s2 is moved into
                                        // takes_and_gives_back, which also
                                        // moves its return value into s3
} // Here, s3 goes out of scope and is dropped. s2 was moved, so nothing
  // happens. s1 goes out of scope and is dropped.

fn gives_ownership() -> String {             // gives_ownership will move its
                                             // return value into the function
                                             // that calls it

    let some_string = String::from("yours"); // some_string comes into scope

    some_string                              // some_string is returned and
                                             // moves out to the calling
                                             // function
}

// This function takes a String and returns one
fn takes_and_gives_back(a_string: String) -> String { // a_string comes into
                                                      // scope

    a_string  // a_string is returned and moves out to the calling function
}
`````
함수를 사용하면서 소유권을 갖는 것과 반납하는 것은 매우 성가시다.   
Rust에서는 이를 위해서 references를 제공한다!

Ref: <https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html>