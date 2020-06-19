[![Analytics](https://ga-beacon.appspot.com/UA-8535255-2/unosquare/tubular-react/)](https://github.com/igrigorik/ga-beacon)
[![npm version](https://badge.fury.io/js/tubular-react.svg)](https://badge.fury.io/js/tubular-react)
![Buils status](https://github.com/unosquare/tubular-react/workflows/Node.js%20Package/badge.svg)

![Tubular-React](https://unosquare.github.io/assets/tubular.png)

:star: _Please star this project if you find it useful!_

**Tubular-React** is a [Material-UI](https://material-ui.com/) table (or data grid) with local or remote data-source. Featuring:

-   Define a custom layout for columns and cells using `render` methods.
-   Use a remote or local datasource. Remote datasource use a specific Request and Response format.
-   Sort and filter multiple columns.
-   Free-text search of string columns.
-   Page data. Remote data is paged in the server side.
-   Export data to a CSV file.
-   Print data.

You can try a [CodeSandbox demo](https://codesandbox.io/s/818mwv72ll).

Please visit the [Tubular GitHub Page](http://unosquare.github.io/tubular) to learn how quickly you can start coding. See [Related projects](#related-projects) below to discover more Tubular libraries and backend solutions.

## Table of contents

-   [Installation](#installation)
-   [Usages](#datagrid)
    -   [DataGrid](#datagrid)
    -   [Using a remote data source](#using-a-remote-data-source)
    -   [Using a local data source](#using-a-local-data-source)
    -   [How to include functionality buttons](#how-to-include-functionality-buttons)
    -   [Run integrated sample](#run-integrated-sample)
-   [i18n Support](#i18n-support)
-   [Related projects](#related-projects)

## Installation

```sh
$ npm install tubular-react --save
```

## Usages

You can check the documentation of the components at [https://unosquare.github.io/tubular/tubular-react](https://unosquare.github.io/tubular/tubular-react)

### `DataGrid`

You can start using `DataGrid` with this sample code. The grid will connect to a remote datasource or have a local datasource depending on what it's passed in the dataSource property.

To create Column you have to use **createColumn** function and have to pass the desired name of column as string.
```js
import React from 'react';
import ReactDOM from 'react-dom';

import { DataGrid } from 'tubular-react';
import {createColumn} from "tubular-common";

const columns = [createColumn('OrderID'), createColumn('CustomerName'), createColumn('ShipperCity')];

const SampleGrid = () => (
    <DataGrid columns={columns} dataSource={'https://tubular.azurewebsites.net/api/orders/paged'} gridName="Grid" />
);

ReactDOM.render(<SampleGrid />, document.getElementById('root'));
```

This is a preview of the previous code:

![DataGrid](https://user-images.githubusercontent.com/25437790/57318742-a7a2b200-70c0-11e9-8d5b-aaf2107bd059.gif)

### Using a remote data source

You will need both a URL and a `createColumn` array.

```js
<DataGrid columns={columns} dataSource={'https://tubular.azurewebsites.net/api/orders/paged'} gridName="Grid" />
```

#### Example
You can try a CodeSandbox demo for RemoteDataGrids:

[![Edit tubular-react - dataGrid](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/tubular-react-template-gyjo8)

### Using a local data source

You will need both an array of data objects and a `createColumn` array. See this [example](https://github.com/unosquare/tubular-react/blob/master/sample/src/data/localData.ts) of how to define the array of objects.

```js
<DataGrid columns={columns} dataSource={localData} gridName="Grid" />
```
#### Use of Filter and Aggregate Function
To include filter and aggregate function you have to pass the an object filter type and aggregate as second argument of `createColumn`
please refer the below code.

```js
import {
  AggregateFunctions,
  ColumnDataType,
  createColumn,
  ColumnSortDirection
} from "tubular-common";
import { DataGrid } from "tubular-react";

const columns = [
  createColumn("OrderID", {
    dataType: ColumnDataType.NUMERIC,
    filtering: true,
    isKey: true,
    label: "Id",
    sortDirection: ColumnSortDirection.ASCENDING,
    sortOrder: 1,
    sortable: true
  }),
  createColumn("CustomerName", {
    aggregate: AggregateFunctions.COUNT,
    filtering: true,
    searchable: true,
    sortable: true
  }),
  createColumn("ShippedDate", {
    dataType: ColumnDataType.DATE_TIME,
    filtering: true,
    sortable: true
  }),
  createColumn("ShipperCity")
];

export const GridExample = () => {
  return (
    <div>
      <DataGrid
        gridName="Tubular-React"
        columns={columns}
        dataSource="https://tubular.azurewebsites.net/api/orders/paged"
      />
    </div>
  );
};


```
#### Example
You can try a CodeSandbox demo for LocalDataGrid

[![Edit tubular-react - localDataGrid](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/tubular-react-template-gyjo8)

### How to include functionality buttons

You can add functionalities to the `DataGridProvider` including extra buttons that can perform an action according to your requirements. Just need include an IconButton Component from @material-ui and define the icon or button that you need between `DataGridProvider` tags and specify the action to perform.

The following snippet shows how to include an Add Button:

```tsx
import * as React from 'react';
import AddIcon from '@material-ui/icons/Add';
import IconButton from '@material-ui/core/IconButton';
import { DataGrid } from 'tubular-react';

const LocalDataGrid = () => (
    <DataGrid columns={columns} dataSource={'https://tubular.azurewebsites.net/api/orders/paged'} gridName="Grid">
        <IconButton color="default" onClick={() => alert('I can help you to add features to your datagrid.')}>
            <AddIcon />
        </IconButton>
    </DataGrid>
);
```

### Run integrated sample

There is a sample included in this project, you can run it just by doing the following.

```shell
// Install all the dependencies
npm install
// Run the sample project
npm start
```

## i18n Support

Tubular React now includes a brand new Language Service that will translate the content of the grid to a preferred language.
Devs can also implement content on their language and import it to use this language.
By default, Tubular React comes with implementations in **English** and **Spanish**.
If any key content needs parameters to include in the translation, devs can pass the parameters in the `translate` function.

```ts
import { Lang } from 'tubular-react';

Lang.translate('PageNum', 16);
// => 'Page 16'
```

## Related Projects

| Name                                                                                                 | Type            | Language/tech         | Description                                                                                                                                                                       |
| ---------------------------------------------------------------------------------------------------- | --------------- | --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Tubular for AngularJS (formerly Tubular)](https://github.com/unosquare/tubular)                     | Library         | AngularJs             | Tubular provides a set of directives and services using AngularJS as framework.                                                                                                   |
| [Tubular for Angular6 (formerly Tubular2)](https://github.com/unosquare/tubular2)                    | Library         | Angular6              | New Tubular2 with Angular6 (Angular2) and Angular Material 2.                                                                                                                     |
| [Tubular React](https://github.com/unosquare/tubular-react)                                          | Library         | React                 | Tubular-React is a DataGrid component using Material-UI                                                                                                                           |
| [Tubular Common](https://github.com/unosquare/tubular-common)                                        | Library         | Javascript/Typescript | Tubular Common provides TypeScript and Javascript models and data transformer to use any Tubular DataGrid component with an array of Javascript objects.                          |
| [Tubular Dotnet](https://github.com/unosquare/tubular-dotnet)                                        | Backend library | C#/.NET Core          | Tubular provides .NET Framework and .NET Core Library to create REST service to use with Tubular Angular Components easily with any WebApi library (ASP.NET Web API for example). |
| [Tubular Nodejs](https://github.com/unosquare/tubular-nodejs)                                        | Backend Library | Javascript            | Tubular Node.js provides an easy way to integrate Tubular Angular Components easily with any Node.js WebApi library.                                                              |
| [Tubular Boilerplate C#](https://github.com/unosquare/tubular-boilerplate-csharp)                    | Boilerplate     | C#                    | Tubular Directives Boilerplate (includes AngularJS and Bootstrap)                                                                                                                 |
| [Tubular Boilerplate](https://github.com/unosquare/tubular-boilerplate)                              | Boilerplate     | Javascript/AngularJS  | Tubular Directives Boilerplate (includes AngularJS and Bootstrap).                                                                                                                |
| [Tubular ASP.NET Core 2.0 Boilerplate](https://github.com/unosquare/tubular-aspnet-core-boilerplate) | Boilerplate     | C#/.NET Core          | Tubular Directives Boilerplate (includes AngularJS and Bootstrap).                                                                                                                |
