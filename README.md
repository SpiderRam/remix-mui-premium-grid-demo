# Demo of a potential bug

[Remix Docs](https://remix.run/docs)

This repo is just the basic remix starter app, with basic Mui, exceljs, and @mui/x-data-grid-premium packages installed.  

In [app/routes/index.tsx](app/routes/index.tsx), I copied the code from this [sandbox](https://codesandbox.io/s/ndcpfk?file=/demo.tsx:0-2828), without any alteration.  The sandbox works as expected.

In this app, the grid renders as expected, but when I click on Export > Download as Excel, there is no download and an error appears in the console:

> Uncaught (in promise) TypeError: excelJS.Workbook is not a constructor
    at buildExcel (excelSerializer.js:182:20)
    at async Object.exportDataAsExcel (useGridExcelExport.js:41:22)

Tracing the problem to node_modules/@mui/x-data-grid-premium/hooks/features/export/serializer/excelSerializer.js, and changing this line, the download is successful.



```ts
// const getExcelJs = () => import('exceljs');
const getExcelJs = () => require('exceljs');
```

## Running Locally

This app was built with node v16.15.1 and npm v8.11.0

From your terminal:

```sh
npm i && npm run dev
```

This starts your app in development mode, rebuilding assets on file changes.

