---
title: "React-Beautiful-DnD 簡單示範"
date: 2020-04-30T22:56:17+08:00
draft: false
isCJKLanguage: true
weight: 0
tags:
  - 前端
  - JavaScript
  - React
cover:
  # image: "<image path/url>" # image path/url
  # alt: "<alt text>" # alt text
  # caption: "<text>" # display caption under cover
  # relative: false # when using page bundles set this to true
  # hidden: false # only hide on current single page
---

`React-Beautiful-DnD`是一個很有人氣的 DnD 套件，除了基本的 Drag & Drop 功能之外，還有優雅的拖曳動畫、鍵盤拖曳支援等，使用起來也很容易入手。

## 基本要素

`React-Beautiful-DnD`由三種要素組成，分別為：`<DragDropContext />`、`<Draggable />`、`<Droppable />`

下圖為官方的示意圖：

![Structure](https://user-images.githubusercontent.com/2182637/53607406-c8f3a780-3c12-11e9-979c-7f3b5bd1bfbd.gif)

### DragDropContext

開發 React 的人對於`<DragDropContext />`應該不難理解，
看到`context`這個關鍵字就能領略箇中含義，
`<DragDropContext />`所定義的是要實作拖拉功能的範圍

### Draggable

定義拖曳元件，將所要拖曳的元件包在`<Draggable />`裡面，結構如下：

```javascript
import { Draggable } from "react-beautiful-dnd";

<Draggable draggableId={taskId} index={taskIndex}>
  {(provided, snapshot) => {
    const { draggableProps, dragHandleProps, innerRef } = provided;
    const { isDragging } = snapshot;

    return (
      <div ref={innerRef} {...draggableProps} {...dragHandleProps} data-is-dragging={isDragging}>
        <h4>I can DRAG! ✋</h4>
      </div>
    );
  }}
</Draggable>;
```

要拖曳的元件不能直接作為`children`直接包在`<Draggable />`中間，
必須是一個函式（官方的教學影片說裡面是放一個`renderProps`），並在`return`的時候返回我們要拖拉的元件，
而函式的參數中，有`<Draggable />`的兩個物件：`provided`及`snapshot`

#### `provided`

`provided`物件中包含`draggableProps`、`dragHandleProps`及`innerRef`

- `innerRef`：用來綁定拖曳的 DOM 元素
- `draggableProps`：提供拖曳元件的`props`
- `dragHandleProps`：則可另外定義拖拉的範圍，像是綁定一個 Icon 做這個拖曳元件的拖拉

#### `snapshot`

`snapshot`物件中，我目前使用到的只有`isDragging`，在拖曳的狀態下，可以用來做樣式上的變換

### Droppable

定義放置的元件，如同`<Draggable />`一樣的結構，只是是加上放置的屬性，結構如下：

```javascript
import { Droppable } from "react-beautiful-dnd";

<Droppable droppableId={columnId} type="task">
  {(provided, snapshot) => {
    const { droppableProps, innerRef, placeholder } = provided;
    const { isDraggingOver } = snapshot;

    return (
      <div ref={innerRef} {...droppableProps} data-is-over={isDraggingOver}>
        <h2>Drop on ME!! 🙌</h2>
        {placeholder}
      </div>
    );
  }}
</Droppable>;
```

#### `provided`

`provided`物件中包含`droppableProps`、`placeholder`及`innerRef`

- `innerRef`：用來綁定可放置的 DOM 元素
- `droppableProps`提供放置元件的`props`
- `placeholder`就如其名，是一個佔位元素，在拖曳（但尚未 drop）的時候，提供一個放置的空間

#### `snapshot`

`snapshot`物件中，我目前使用到的只有`isDraggingOver`，在被拖曳元件 hover 的狀態下，用來做樣式上的變換

最後附上[範例連結](https://kazettique.github.io/react-beautiful-dnd-example/)

## 參考資料

- [atlassian/react-beautiful-dnd: Beautiful and accessible drag and drop for lists with React](https://github.com/atlassian/react-beautiful-dnd)
- [Beautiful and Accessible Drag and Drop with react-beautiful-dnd from @alexandereardon on @eggheadio](https://egghead.io/courses/beautiful-and-accessible-drag-and-drop-with-react-beautiful-dnd)
- [vertical list with multiple drop targets - CodeSandbox](https://codesandbox.io/s/ql08j35j3q?file=/index.js:3964-3965)
