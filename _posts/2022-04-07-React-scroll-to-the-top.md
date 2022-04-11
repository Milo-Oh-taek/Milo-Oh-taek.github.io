---
title: Scroll to the top(react-router-dom useLocation)
date: 2022-04-07 21:07:00 +09:00
categories: [REACT]
tags: [react, useLocation]
---

### Install react-router-dom
`````
npm i react-router-dom
`````

### create a file called 'ScrollToTop'
`````
import { useEffect } from 'react';
import { useLocation } from 'react-router-dom';

const ScrollToTop = () => {
  const {pathname} = useLocation();
  
  useEffect(() => {
    window.scrollTo(0,0);
  },[pathname])
}
`````

### Then, put in the router
`````
function App() {
  return (
    <BrowserRouter>
      <ScrollTotop />
      <Routes>
        <Route element={<Layout />}>
          <Route path="/" element={<Home />} />
          <Route path="/about" element={<About />} />
          <Route path="/business" element={<Biz />} />
          <Route path="/career" element={<Career />} />
        </Route>
      </Routes>
    </BrowserRouter>
  );
}
`````

### What useLocation has
>hash: "#product"
key: "g1vriyme"
pathname: "/business"
search: ""
state: null
[[Prototype]]: Object

- pathname: strings after domain
- search: strings after '?' of pathname
- hash: strings after '#' of pathname
- state: location object will be sent
- key: can find location object in history stack with











