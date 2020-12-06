# ra-data-lb4

![Travis (.org) branch](https://img.shields.io/travis/ckoliber/ra-data-lb4/master)
![npm](https://img.shields.io/npm/v/ra-data-lb4)
![npm bundle size](https://img.shields.io/bundlephobia/min/ra-data-lb4)
![GitHub](https://img.shields.io/github/license/ckoliber/ra-data-lb4)

React Admin Loopback4 CRUD DataProvider

## Installation

```bash
npm i --save ra-data-lb4
```

## Usage

```tsx
// in src/App.tsx
import React from "react";
import { Admin, Resource } from "react-admin";
import lb4Provider from "ra-data-lb4";

import { PostList } from "./posts";

const App = () => (
    <Admin dataProvider={lb4Provider("http://path.to.my.api/")}>
        <Resource name="posts" list={PostList} />
    </Admin>
);

export default App;
```

---

## Model Aggregation

**Loopback4** supports model aggregations using **inclusion resolvers**, you can pass your `include` params per model:

```tsx
// in src/App.tsx
import { Admin, Resource } from "react-admin";
import lb4Provider from "ra-data-lb4";

const aggregate = (resource: string) => {
    if (resource === "posts") {
        return [
            {
                relation: "author",
            },
        ];
    }

    return [];
};

const provider = lb4Provider("http://path.to.my.api/", aggregate);
```

---

## Customizing Http Client

```tsx
// in src/App.tsx
import { fetchUtils, Admin, Resource } from "react-admin";
import lb4Provider from "ra-data-lb4";

const httpClient = (url, options = {}) => {
    if (!options.headers) {
        options.headers = new Headers({ Accept: "application/json" });
    }
    // add your own headers here
    options.headers.set("X-Custom-Header", "foobar");
    return fetchUtils.fetchJson(url, options);
};

const provider = lb4Provider("http://path.to.my.api/", undefined, httpClient);
```

---

## Contributors

-   [KoLiBer](https://www.linkedin.com/in/mohammad-hosein-nemati-665b1813b/)

## License

This project is licensed under the [MIT license](LICENSE.md).  
Copyright (c) KoLiBer (koliberr136a1@gmail.com)
