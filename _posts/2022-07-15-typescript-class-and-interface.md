---
title: typescript class and interface
date: 2022-07-16 00:20:00 +09:00
categories: [TS]
tags: [typescript]
---

## Class

### class and this
`````
class Department {
  name: string;

  constructor(n: string) {
    this.name = n;
  }

  describe(this: Department) {
    console.log('Department: ' + this.name);
  }
}

const accounting = new Department('Accounting');

accounting.describe();
`````

### private and public
`````
class Department {
  public name: string;
  private employees: string[] = [];	// private 설정으로 외부의 직접적인 접근 forbid

  constructor(n: string) {
    this.name = n;
  }

  describe(this: Department) {
    console.log('Department: ' + this.name);
  }

  addEmployee(employee: string) {	// private 인자는 내부 메소드로 접근
    // validation etc
    this.employees.push(employee);
  }

  printEmployeeInformation() {
    console.log(this.employees.length);
    console.log(this.employees);
  }
}

const accounting = new Department('Accounting');

accounting.addEmployee('Max');
accounting.addEmployee('Manu');
`````

### shorter init
`````
class Department {
  // private id: string;
  // private name: string;
  private employees: string[] = [];
  
	// 바로 명시하여 this 통하여 주입할 필요 x
  constructor(private id: string, public name: string) {
    // this.id = id;
    // this.name = n;
  }

  describe(this: Department) {
    console.log(`Department (${this.id}): ${this.name}`);
  }

  addEmployee(employee: string) {
    // validation etc
    this.employees.push(employee);
  }

  printEmployeeInformation() {
    console.log(this.employees.length);
    console.log(this.employees);
  }
}
`````

### Inheritance
`````
class Department {
  // private readonly id: string;
  // private name: string;
  private employees: string[] = [];

  constructor(private readonly id: string, public name: string) {
    // this.id = id;
    // this.name = n;
  }

  describe(this: Department) {
    console.log(`Department (${this.id}): ${this.name}`);
  }

  addEmployee(employee: string) {
    // validation etc
    // this.id = 'd2';
    this.employees.push(employee);
  }

  printEmployeeInformation() {
    console.log(this.employees.length);
    console.log(this.employees);
  }
}

class ITDepartment extends Department {
  admins: string[];
  constructor(id: string, admins: string[]) {	// extends시 super호출 필요
    super(id, 'IT');
    this.admins = admins;
  }
}

class AccountingDepartment extends Department {
  constructor(id: string, private reports: string[]) {
    super(id, 'Accounting');
  }

  addReport(text: string) {
    this.reports.push(text);
  }

  printReports() {
    console.log(this.reports);
  }
}

const it = new ITDepartment('d1', ['Max']);

it.addEmployee('Max');
it.addEmployee('Manu');
`````

### getters and setters
`````
class AccountingDepartment extends Department {
  private lastReport: string;	//private 지정하여 외부에서 접근 forbid

  get mostRecentReport() {	// getter 설정
    if (this.lastReport) {
      return this.lastReport;
    }
    throw new Error('No report found.');
  }

  set mostRecentReport(value: string) {	// setter 설정
    if (!value) {
      throw new Error('Please pass in a valid value!');
    }
    this.addReport(value);
  }

  constructor(id: string, private reports: string[]) {
    super(id, 'Accounting');
    this.lastReport = reports[0];
  }

  addEmployee(name: string) {
    if (name === 'Max') {
      return;
    }
    this.employees.push(name);
  }

  addReport(text: string) {
    this.reports.push(text);
    this.lastReport = text;
  }

  printReports() {
    console.log(this.reports);
  }
}
`````

### Abstract
`````
abstract class Department {
  static fiscalYear = 2020;
  protected employees: string[] = [];

  constructor(protected readonly id: string, public name: string) {
  }

  static createEmployee(name: string) {
    return { name: name };
  }

  abstract describe(this: Department): void;	// 추상클래스 선언

  addEmployee(employee: string) {
    // validation etc
    // this.id = 'd2';
    this.employees.push(employee);
  }

  printEmployeeInformation() {
    console.log(this.employees.length);
    console.log(this.employees);
  }
}

class ITDepartment extends Department {
  admins: string[];
  constructor(id: string, admins: string[]) {
    super(id, 'IT');
    this.admins = admins;
  }

  describe() {	// 추상클래스 구현 (미구현시 error)
    console.log('IT Department - ID: ' + this.id);
  }
}

class AccountingDepartment extends Department {
  private lastReport: string;

  get mostRecentReport() {
    if (this.lastReport) {
      return this.lastReport;
    }
    throw new Error('No report found.');
  }

  set mostRecentReport(value: string) {
    if (!value) {
      throw new Error('Please pass in a valid value!');
    }
    this.addReport(value);
  }

  constructor(id: string, private reports: string[]) {
    super(id, 'Accounting');
    this.lastReport = reports[0];
  }

  describe() {	// 추상클래스 구현 (미구현시 error)
    console.log('Accounting Department - ID: ' + this.id);
  }

  addEmployee(name: string) {
    if (name === 'Max') {
      return;
    }
    this.employees.push(name);
  }

  addReport(text: string) {
    this.reports.push(text);
    this.lastReport = text;
  }

  printReports() {
    console.log(this.reports);
  }
}
`````

### Singletone
`````
class AccountingDepartment extends Department {
  private lastReport: string;
  private static instance: AccountingDepartment;

  ...

  static getInstance() {
    if (AccountingDepartment.instance) {	// Instance 생성됐으면 바로 리턴
      return this.instance;
    }
    this.instance = new AccountingDepartment('d2', []); // 없으면 새로 생성
    return this.instance;
  }

}
`````

## Interface

### basic
`````
interface Person {	//interface 선언
  name: string;
  age: number;

  greet(phrase: string): void;
}

let user1: Person;

user1 = {	//interface 구현
  name: 'Max',
  age: 30,
  greet(phrase: string) {
    console.log(phrase + ' ' + this.name);
  }
};

user1.greet('Hi there - I am');
`````

### Implementing
`````
interface Greetable {
  name: string;

  greet(phrase: string): void;
}

class Person implements Greetable {
  name: string;
  age = 30;	// Implement하면 interface에 없는 요소도 추가가능

  constructor(n: string) {
    this.name = n;
  }

  greet(phrase: string) {
    console.log(phrase + ' ' + this.name);
  }
}
`````


## References
[https://www.typescriptlang.org/docs/handbook/tsconfig-json.html](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)   
[https://www.udemy.com/course/best-typescript-21/](https://www.udemy.com/course/best-typescript-21/)   
