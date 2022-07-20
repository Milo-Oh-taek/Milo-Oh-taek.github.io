---

title: typescript generic

date: 2022-07-18 23:20:00 +09:00

categories: [TS]

tags: [typescript]

---



## Generic

### basic

`````
function merge(objA: object, objB: object) {
  return Object.assign(objA, objB);
}

const mergedObj = merge({ name: "Milo" }, { sex: "M" });
mergedObj.name	// Error!

// typescript는 두 object를 결합하여 return 한다는 것만 알고 있지,
// return된 값 안에 어떤 속성이 있는지 알 수 없다.

function merge<T, U>(objA: T, objB: U) {  // generic을 지정해준다
  return Object.assign(objA, objB);
}

const mergedObj = merge({ name: "Milo" }, { sex: "M" });
mergedObj.name;  // OK
mergedObj.sex;  // OK

// 제약조건 추가(두 인자 모두 객체여야 한다)
function merge<T extends object, U extends object>(objA: T, objB: U) {
  return Object.assign(objA, objB);
}

`````

### keyof
`````
function extractAndConvert<T extends object, U extends keyof T>(
  obj: T,
  key: U
) {
  return 'Value: ' + obj[key];
}

extractAndConvert({ name: 'Max' }, 'name');

// keyof를 통하여 두번째 인자가 첫번째 객체의 키에 존재 하는지 검사
`````

### classes
`````
class DataStorage<T extends string | number | boolean> {  // 원시타입으로 제약
  private data: T[] = [];

  addItem(item: T) {
    this.data.push(item);
  }

  removeItem(item: T) {
    if (this.data.indexOf(item) === -1) {
      return;
    }
    this.data.splice(this.data.indexOf(item), 1); // -1
  }

  getItems() {
    return [...this.data];
  }
}

const textStorage = new DataStorage<string>();  // generic setting
textStorage.addItem('Max');
textStorage.addItem('Manu');
textStorage.removeItem('Max');
console.log(textStorage.getItems());
`````

### Partial
`````
interface CourseGoal {
  title: string;
  description: string;
  completeUntil: Date;
}

function createCourseGoal(title: string, description: string, date: Date): CourseGoal {
  let courseGoal: Partial<CourseGoal> = {};  // CourseGoal interface가 모두 optional이 됨
  courseGoal.title = title;
  courseGoal.description = description;
  courseGoal.completeUntil = date;
  return courseGoal as CourseGoal;
}
`````


## References

[https://www.typescriptlang.org/docs/handbook/tsconfig-json.html](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)   

[https://www.udemy.com/course/best-typescript-21/](https://www.udemy.com/course/best-typescript-21/)   

