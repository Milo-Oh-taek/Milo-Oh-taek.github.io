---
title: React router dom V6
date: 2022-03-16 15:07:00 +09:00
categories: [REACT]
tags: [react]
---

### Installation
`````
npm install react-router-dom@6
`````

### Configuring Routes

`````
import { BrowserRouter, Routes, Route } from "react-router-dom";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="chat" element={<Chat />} />
      </Routes>
    </BrowserRouter>
  );
}
`````

### Navigation
`````
import { Link } from "react-router-dom";

function Home() {
  return (
    <div>
      <h1>Home</h1>
      <nav>
        <Link to="/">Home</Link> |{" "}
        <Link to="about">About</Link>
      </nav>
    </div>
  );
}
`````

`````
import { useNavigate } from "react-router-dom";

function Invoices() {
  let navigate = useNavigate();
  return (
    <div>
      <NewInvoiceForm
        onSubmit={async (event) => {
          let newInvoice = await createInvoice(
            event.target
          );
          navigate(`/invoices/${newInvoice.id}`);
        }}
      />
    </div>
  );
}
`````

### URL parameters
`````
import { Routes, Route, useParams } from "react-router-dom";

function App() {
  return (
    <Routes>
      <Route
        path="invoices/:invoiceId"
        element={<Invoice />}
      />
    </Routes>
  );
}

function Invoice() {
  let params = useParams();
  return <h1>Invoice {params.invoiceId}</h1>;
}
`````

### Not Found Routes
`````
function App() {
  return (
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="dashboard" element={<Dashboard />} />
      <Route path="*" element={<NotFound />} />
    </Routes>
  );
}
`````
### Nested Route 중첩 라우팅
### Common layout
#### 공통 레이아웃의 경우 기존 {children} 과 같이 썼다면,   
#### Outlet을 import하고 children 대신 쓰면 된다.

#### Method 1.
`````
<BrowserRouter>
  <Routes>
    <Route path="/" element={<App />}>
      <Route path="expenses" element={<Expenses />} />
      <Route path="invoices" element={<Invoices />} />
    </Route>
  </Routes>
</BrowserRouter>

//App.js
import { Outlet, Link } from "react-router-dom";

export default function App() {
  return (
    <div>
      <h1>Bookkeeper</h1>
      <nav
        style={{
          borderBottom: "solid 1px",
          paddingBottom: "1rem",
        }}
      >
        <Link to="/invoices">Invoices</Link> |{" "}
        <Link to="/expenses">Expenses</Link>
      </nav>
      <Outlet />
    </div>
  );
}
`````
#### Method 2.
`````
const App = () => {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/workspace/*" element={<Workspace />} />
      </Routes>
    </BrowserRouter>
  );
};

const Workspace= () => {
  return (
    <Routes>
      <Route path="channel" element={<Channel />} />
      <Route path="dm" element={<DirectMessage />} />
    </Routes>
  );
};
`````







