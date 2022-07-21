---

title: typescript decorator

date: 2022-07-18 16:20:00 +09:00

categories: [TS]

tags: [typescript]

---

## setting
### tsconfig.json
`````
{
  "compilerOptions": {
	...
    "experimentalDecorators": true
  }
}
`````

## basic
`````
function Logger(constructor: Function) {
  console.log('Logging...');
  console.log(constructor);
}

@Logger
class Person {
  name = 'Max';

  constructor() {
    console.log('Creating person object...');
  }
}

const pers = new Person();

console.log(pers);


-----Log-----
Logging...
app.ts:3 class Person {
    constructor() {
        this.name = 'Max';
        console.log('Creating person object...');
    }
}
app.ts:11 Creating person object...
app.ts:17 Person {name: 'Max'}
-----
`````

## decorator factory
`````
function Logger(logString: string) {
  return function (constructor: Function) {
    console.log(logString);
    console.log(constructor);
  };
}

@Logger("LOGGING - PERSON")
class Person {
  name = "Max";

  constructor() {
    console.log("Creating person object...");
  }
}
`````

## useful decorator
`````
// 전달받은 'app' element에 name 삽입하는 예제

function WithTemplate(template: string, hookId: string) {
  return function (constructor: any) {
    const hookEl = document.getElementById(hookId);
    const p = new constructor();
    if (hookEl) {
      hookEl.innerHTML = template;
      hookEl.querySelector("h1")!.textContent = p.name;
    }
  };
}

@WithTemplate("<h1>My Person Object</h1>", "app")
class Person {
  name = "Max";

  constructor() {
    console.log("Creating person object...");
  }
}
`````







## References

[https://www.typescriptlang.org/docs/handbook/tsconfig-json.html](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)   

[https://www.udemy.com/course/best-typescript-21/](https://www.udemy.com/course/best-typescript-21/)   

