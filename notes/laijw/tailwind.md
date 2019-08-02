# Tailwind

[官方文档](https://www.tailwindcss.cn/docs/installation/)

## 安装

```bash
# Using npm
npm install tailwindcss --save-dev

# Using Yarn
yarn add tailwindcss --dev

# 创建 Tailwind 配置文件
.\node_modules\.bin\tailwind init tailwind.js

# postcss 引入
const tailwindcss = require('./tailwind')
'tailwindcss': tailwindcss

# main.js 引入
import 'tailwindcss/tailwind.css'
```
## Display

| Class        | Properties             |
| ------------ | ---------------------- |
| block        | display: block;        |
| inline-block | display: inline-block; |
| inline       | display: inline;       |
| table        | display: table;        |
| table-row    | display: table-row;    |
| table-cell   | display: table-cell;   |
| hidden       | display: none;         |
| flex         | display: flex;         |
| inline-flex  | display: inline-flex;  |

## Floats

| Class       | Properties    |
| ----------- | ------------- |
| float-right | float: right; |
| float-left  | float: left;  |
| float-none  | float: none;  |
| clearfix    | clear: both   |

## Flex

[Flex 布局](https://www.tailwindcss.cn/docs/flex-direction)

### Flex Display
| Class       | Properties            |
| ----------- | --------------------- |
| flex        | display: flex;        |
| inline-flex | display: inline-flex; |

### Flex Direction
| Class            | Properties                      |
| ---------------- | ------------------------------- |
| flex-row         | flex-direction: row;            |
| flex-row-reverse | flex-direction: row-reverse;    |
| flex-col         | flex-direction: column;         |
| flex-col-reverse | flex-direction: column-reverse; |

### Flex Wrapping
| Class             | Properties               |
| ----------------- | ------------------------ |
| flex-no-wrap      | flex-wrap: nowrap;       |
| flex-wrap         | flex-wrap: wrap;         |
| flex-wrap-reverse | flex-wrap: wrap-reverse; |

### Align Items
| Class          | Properties               |
| -------------- | ------------------------ |
| items-stretch  | align-items: stretch;    |
| items-start    | align-items: flex-start; |
| items-center   | align-items: center;     |
| items-end      | align-items: flex-end;   |
| items-baseline | align-items: baseline;   |

### Align Content
| Class           | Properties                    |
| --------------- | ----------------------------- |
| content-start   | align-content: flex-start;    |
| content-center  | align-content: center;        |
| content-end     | align-content: flex-end;      |
| content-between | align-content: space-between; |
| content-around  | align-content: space-around;  |

### Align Self
| Class        | Properties              |
| ------------ | ----------------------- |
| self-auto    | align-self: auto;       |
| self-start   | align-self: flex-start; |
| self-center  | align-self: center;     |
| self-end     | align-self: flex-end;   |
| self-stretch | align-self: stretch;    |

### Justify Content
| Class           | Properties                      |
| --------------- | ------------------------------- |
| justify-start   | justify-content: flex-start;    |
| justify-center  | justify-content: center;        |
| justify-end     | justify-content: flex-end;      |
| justify-between | justify-content: space-between; |
| justify-around  | justify-content: space-around;  |

### Flex, Grow, & Shrink
| Class          | Properties      |
| -------------- | --------------- |
| flex-initial   | flex: initial;  |
| flex-1         | flex: 1;        |
| flex-auto      | flex: auto;     |
| flex-none      | flex: none;     |
| flex-grow      | flex-grow: 1;   |
| flex-shrink    | flex-shrink: 1; |
| flex-no-grow   | flex-grow: 0;   |
| flex-no-shrink | flex-shrink: 0; |
