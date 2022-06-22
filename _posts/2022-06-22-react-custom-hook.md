---
title: react custom hook
date: 2022-06-22 23:30:00 +09:00
categories: [REACT]
tags: [react]
---

## Custom hook   
### 반복되는 로직의 재사용   

### Rule
1. custom hook은 use로 시작한다.   
2. 최상위(at the Top Level)에서만 Hook을 호출해야 한다.
	- 반복문, 조건문 or 중첩된 함수 내에서 Hook호출 X
3. 오직 React함수 내에서 Hook을 호출해야 한다.
	- 일반 Javascript 함수에서 호출 X

### React custom hook vs Javascript Util function 차이점
#### useState, useEffect 등의 React 내장 함수를 사용하고자 한다면 custom hook으로 사용해야한다.   

App.js
`````
function App() {
  const [name, setName] = useLocalStorage("name", "");

  return (
    <input type="text" value={name} onChange={(e) => setName(e.target.value)} />
  );
}

export default App;
`````

useLocalStorage.js
`````
function getSavedValue(key, initialValue) {
  const savedValue = JSON.parse(localStorage.getItem(key));
  if (savedValue) return savedValue;

  if (initialValue instanceof Function) return initialValue();
  return initialValue;
}

export default function useLocalStorage(key, initialValue) {
  const [value, setValue] = useState(() => {
    return getSavedValue(key, initialValue);
  });

  useEffect(() => {
    localStorage.setItem(key, JSON.stringify(value));
  }, [value]);

  return [value, setValue];
}
`````

## Reference
[React Hook Rule](https://ko.reactjs.org/docs/hooks-rules.html)   
[Example Code](https://www.youtube.com/watch?v=6ThXsUwLWvc)
