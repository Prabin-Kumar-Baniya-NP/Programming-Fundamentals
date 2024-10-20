# Lazy Loading / Dynamic Bundling / Code Splitting

```js
import React, {lazy, Suspense} from "react";
const CMS = lazy(() => import("./components/CMS") )

// In router
<Suspense fallback={<h1>Loading</h1>}><CMS/></Suspense>
```

A difference js files will be bundled for this CMS component.