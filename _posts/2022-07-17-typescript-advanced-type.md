---

title: typescript advanced type

date: 2022-07-17 23:35:00 +09:00

categories: [TS]

tags: [typescript]

---



## advanced type

### intersection type
`````
type Admin = {
  name: string;
  privileges: string[];
};

type Employee = {
  name: string;
  startDate: Date;
};

// interface ElevatedEmployee extends Employee, Admin {}

type ElevatedEmployee = Admin & Employee;

const e1: ElevatedEmployee = {
  name: 'Max',
  privileges: ['create-server'],
  startDate: new Date()
};
`````

### type guard
#### 특정 속성이나 메소드를 사용하기 전에 존재하는지 확인하거나 타입이 일치하는지 확인작업
- typeof (타입확인)
- 속성 in 객체
- instanceof (interface가 아닌 type일 때)

`````
type Combinable = string | number;
type Numeric = number | boolean;

type Universal = Combinable & Numeric;

function add(a: Combinable, b: Combinable) {
  if (typeof a === 'string' || typeof b === 'string') {
    return a.toString() + b.toString();
  }
  return a + b;
}
`````

`````
type UnknownEmployee = Employee | Admin;

function printEmployeeInformation(emp: UnknownEmployee) {
  console.log('Name: ' + emp.name);
  if ('privileges' in emp) {
    console.log('Privileges: ' + emp.privileges);
  }
  if ('startDate' in emp) {
    console.log('Start Date: ' + emp.startDate);
  }
}
`````

`````
class Car {
  drive() {
    console.log('Driving...');
  }
}

class Truck {
  drive() {
    console.log('Driving a truck...');
  }

  loadCargo(amount: number) {
    console.log('Loading cargo ...' + amount);
  }
}

type Vehicle = Car | Truck;

const v1 = new Car();
const v2 = new Truck();

function useVehicle(vehicle: Vehicle) {
  vehicle.drive();
  if (vehicle instanceof Truck) {
    vehicle.loadCargo(1000);
  }
}
`````

### discriminated union
`````
interface Bird {
  type: 'bird';
  flyingSpeed: number;
}

interface Horse {
  type: 'horse';
  runningSpeed: number;
}

type Animal = Bird | Horse;

function moveAnimal(animal: Animal) {
  let speed;
  switch (animal.type) {
    case 'bird':
      speed = animal.flyingSpeed;
      break;
    case 'horse':
      speed = animal.runningSpeed;
  }
  console.log('Moving at speed: ' + speed);
}
`````

### type casting
`````
1. <> + ! 를 통한 casting
const userInputElement = <HTMLInputElement>document.getElementById('user-input')!;

2. as + ! 를 통한 casting
const userInputElement = document.getElementById('user-input')! as HTMLInputElement;

3. as + if
const userInputElement = document.getElementById('user-input');
// !이 없으면 HTMLElement | null 이므로 if를 사용하여 null이 아닐 때 실행

if (userInputElement) {
  (userInputElement as HTMLInputElement).value = 'Hi there!';
}
`````

#### index properties
`````
interface ErrorContainer {
  [prop: string]: string;	// 정확한 속성 이름, 개수 모를 때. 속성, 속성값 string로 설정,
}
`````


## References

[https://www.typescriptlang.org/docs/handbook/tsconfig-json.html](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)   

[https://www.udemy.com/course/best-typescript-21/](https://www.udemy.com/course/best-typescript-21/)   

