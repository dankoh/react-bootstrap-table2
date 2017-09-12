# Definition of columns props on BootstrapTable

Available properties in a column object:

* [dataField (**required**)](#dataField)
* [text (**required**)](#text)
* [hidden](#hidden)
* [formatter](#formatter)
* [headerFormatter](#headerFormatter)
* [formatExtraData](#formatExtraData)
* [classes](#classes)
* [style](#style)
* [title](#title)
* [events](#events)
* [align](#align)
* [attrs](#attrs)
* [headerTitle](#headerTitle)
* [headerEvents](#headerEvents)
* [headerAlign](#headerAlign)
* [headerClasses](#headerClasses)
* [headerStyle](#headerStyle)
* [headerAttrs](#headerAttrs)

Following is a most simplest and basic usage:

```js
const rows = [ { id: 1, name: '...', price: '102' } ];
const columns = [ {
    dataField: id, 
    text: Production ID
  }, {
    dataField: name,
    text: Production Name
  }, {
    dataField: price,
    text: Production Price
  }
];
```

Let's introduce the definition of column object

## <a name='dataField'>column.dataField (**required**) - [String]</a>
Use `dataField` to specify what field should be apply on this column. If your raw data is nested, for example:

```js
const row = {
  id: 'A001',
  address: {
    postal: '1234-12335',
    city: 'Chicago'
  }
}
```
You can use `dataField` with dot(`.`) to describe nested object:

```js
dataField: 'address.postal'
dataField: 'address.city'
```

## <a name='text'>column.text (**required**) - [String]</a>
`text` will be apply as the column text in header column, if your header is not only text and you want to customize your header column, please check [`column.headerFormatter`](#headerFormatter)

## <a name='hidden'>column.hidden - [Bool]</a>
`hidden` allow you to hide column when `true` given.

## <a name='formatter'>column.formatter - [Function]</a>
`formatter` allow you to customize the table column and only accept a callback function which take four arguments and a JSX/String are expected for return.

* `cell`
* `row`
* `rowIndex`
* [`formatExtraData`](#formatExtraData)

## <a name='headerFormatter'>column.headerFormatter - [Function]</a>
`headerFormatter` allow you to customize the header column and only accept a callback function which take two arguments and a JSX/String are expected for return.

* `column`: column object itself
* `colIndex`

## <a name='formatExtraData'>column.formatExtraData - [Any]</a>
It's only used for [`column.formatter`](#formatter), you can define any value for it and will be passed as fourth argument for [`column.formatter`](#formatter) callback function.

## <a name='classes'>column.classes - [String | Function]</a>
It's availabe to have custom class on table column:

```js
{
  // omit...
  classes: 'id-custom-cell'
}
```
In addition, `classes` also accept a callback function which have more power to custom the css class on each columns. This callback function take three arguments and a string is expect to return: 

* `cell`
* `row`
* `colIndex`

## <a name='headerClasses'>column.headerClasses - [String | Function]</a>
It's availabe to have customized class on table header column:

```js
{
  // omit...
  headerClasses: 'id-custom-cell'
}
```
In addition, similar to [`column.classes`](#classes), `headerClasses` also accept a callback function which have more power to custom the css class on header column. This callback function take two arguments and a string is expect to return: 

* `column`
* `colIndex`

## <a name='style'>column.style - [Object | Function]</a>
It's availabe to have custom class on table column:

```js
{
  // omit...
  style: { backgroundColor: 'green' }
}
```
`style` like [`column.classes`](#classes), it accept a callback function too and have same arguments: `cell`, `row` and `colIndex`.

## <a name='headerStyle'>column.headerStyle - [Object | Function]</a>
It's availabe to have customized inline-style on table header column:

```js
{
  // omit...
  headerStyle: { backgroundColor: 'green' }
}
```
`headerStyle` like [`column.headerClasses`](#headerClasses), it accept a callback function as well and have same arguments: `column` and `colIndex`.

## <a name='title'>column.title - [Bool | Function]</a>
`react-bootstrap-table2` is disable [`HTML title`](https://www.w3schools.com/tags/tag_title.asp) as default. You can assign `title` as `true` to enable the HTML title on table column. In addition, you can custom the title via a callback function:

```js
{
  // omit...
  title: (cell, row, colIndex) => {
    // return custom title here
  }
}
```

## <a name='headerTitle'>column.headerTitle - [Bool | Function]</a>
`headerTitle` is only for the title on header column, default is disable. The usage almost same as [`column.title`](#title), it's also availabe to custom via a callback function:

```js
{
  // omit...
  headerTitle: (column, colIndex) => {
    // column is an object and perform itself
    // return custom title here
  }
}
```

## <a name='align'>column.align - [String | Function]</a>
You can configure the [CSS text-align](https://www.w3schools.com/cssref/pr_text_text-align.asp) for table column by `align` property. However, `align` also accept a callback function for customizable reason and this function take fore arguments:

* `cell`
* `row`
* `colIndex`

## <a name='headerAlign'>column.headerAlign - [String | Function]</a>
It's almost same as [`column.align`](#align), but it's for the [CSS text-align](https://www.w3schools.com/cssref/pr_text_text-align.asp) on header column. Also, you can custom the align by a callback function:

```js
{
  // omit...
  headerAlign: (column, colIndex) => {
    // column is an object and perform itself
    // return custom title here
  }
}
```

## <a name='events'>column.events - [Object]</a>
You can assign any [HTML Event](https://www.w3schools.com/tags/ref_eventattributes.asp) on table column via event property:

```js
{
  // omit...
  events: {
    onClick: e => { ... }
  }
}
```

## <a name='headerEvents'>column.headerEvents - [Object]</a>
`headerEvents` same as [`column.events`](#events) but this is for header column.

## <a name='attrs'>column.attrs - [Object | Function]</a>
Via `attrs` property, You can costomize table column [HTML attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes) which allow user to configure the elements or adjust their behavior. It takes `Object` and `callback function` is also acceptable.

```js
{
  // omit...
  attrs: (cell, row, colIndex) => ({
    // return customized HTML attribute here
  })
}
```

#### * Caution

If `column.classes`, `column.style`, `column.title`, `column.hidden` or `column.align` was given at the same time, property `attrs` has lower priorty and it will be overwrited.

```js
{
  // omit...
  title: true, // it will be chosen.
  attrs: { title: 'test' }
}
```

## <a name='headerAttrs'>column.headerAttrs - [Object | Function]</a>
`headerAttrs` is similiar to [`column.attrs`](#attrs) but it's for header column.

```js
{
  // omit...
  headerAttrs: (column, colIndex) => ({
    // return customized HTML attribute here
  })
}
```