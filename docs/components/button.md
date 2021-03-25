---
title: Button
---

## Button

各种类型的 button

```tsx
import React from 'react';

import { Button } from '@wilson_p/rock_ui';

export default () => {
  const flexCenter = {
    display: 'flex',
    justifyContent: 'space-between',
    flexWrap: 'wrap',
    marginBottom: '20px',
    alignItems: 'center',
  };
  const title = {
    fontWeight: 'bold',
    fontSize: '22px',
    marginBottom: '10px',
  };
  const linkUrl = 'www.baidu.com';
  return (
    <div>
      <div style={title}>large size</div>
      <div style={flexCenter}>
        <Button btnType={'primary'} size={'lg'}>
          primary large
        </Button>
        <Button btnType={'danger'} size={'lg'}>
          danger large
        </Button>
        <Button btnType={'default'} size={'lg'}>
          default large
        </Button>
        <Button btnType={'warning'} size={'lg'}>
          warning large
        </Button>
        <Button btnType={'link'} size={'lg'} href={linkUrl}>
          link large
        </Button>
      </div>
      <div style={title}>large disabled</div>
      <div style={flexCenter}>
        <Button disabled btnType={'primary'} size={'lg'}>
          primary disabled
        </Button>
        <Button disabled btnType={'danger'} size={'lg'}>
          danger disabled
        </Button>
        <Button disabled btnType={'default'} size={'lg'}>
          default disabled
        </Button>
        <Button disabled btnType={'warning'} size={'lg'}>
          warning disabled
        </Button>
        <Button disabled btnType={'link'} size={'lg'} href={linkUrl}>
          link disabled
        </Button>
      </div>
      <div style={title}>small size</div>
      <div style={flexCenter}>
        <Button btnType={'primary'} size={'sm'}>
          primary small
        </Button>
        <Button btnType={'danger'} size={'sm'}>
          danger small
        </Button>
        <Button btnType={'default'} size={'sm'}>
          default small
        </Button>
        <Button btnType={'warning'} size={'sm'}>
          warning small
        </Button>
        <Button btnType={'link'} size={'sm'} href={linkUrl}>
          link small
        </Button>
      </div>

      <div style={title}>small disabled</div>
      <div style={flexCenter}>
        <Button disabled btnType={'primary'} size={'sm'}>
          primary disabled
        </Button>
        <Button disabled btnType={'danger'} size={'sm'}>
          danger disabled
        </Button>
        <Button disabled btnType={'default'} size={'sm'}>
          default disabled
        </Button>
        <Button disabled btnType={'warning'} size={'sm'}>
          warning disabled
        </Button>
        <Button disabled btnType={'link'} size={'sm'} href={linkUrl}>
          link disabled
        </Button>
      </div>
    </div>
  );
};
```

<!-- <API src="../../node_modules/@wilson_p/rock_ui/dist/components/Button/button.d.ts"></API> -->

<!-- <API src="../../src/Button/button.tsx"></API> -->

按钮用于开始一个即时操作。

## 何时使用

标记了一个（或封装一组）操作命令，响应用户点击行为，触发相应的业务逻辑。

在 rock_ui 中我们提供了四种按钮。

- 主按钮：用于主行动点，一个操作区域只能有一个主按钮。
- 默认按钮：用于没有主次之分的一组行动点。
- 文本按钮：用于最次级的行动点。
- 链接按钮：用于作为外链的行动点。

以及四种状态属性与上面配合使用。

- 危险：删除/移动/修改权限等危险操作，一般需要二次确认。
- 链接：用于链接跳转。
- 禁用：行动点不可用的时候，一般需要文案解释。
- 默认：默认为朴素颜色。

## API

通过设置 Button 的属性来产生不同的按钮样式，推荐顺序为：`btnType` -> `size` -> `disabled`。

按钮的属性说明如下：

| 属性     | 说明                                                                                                                                 | 类型                                                      | 默认值    | 版本 |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------- | --------- | ---- |
| danger   | 设置危险按钮                                                                                                                         | boolean                                                   | false     |      |
| disabled | 按钮失效状态                                                                                                                         | boolean                                                   | false     |      |
| href     | 点击跳转的地址，指定此属性 button 的行为和 a 链接一致                                                                                | string                                                    | -         |      |
| type     | 设置 `button` 原生的 `type` 值，可选值请参考 [HTML 标准](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button#attr-type) | string                                                    | `button`  |      |
| size     | 设置按钮大小                                                                                                                         | `lg` \| `sm`                                              | -         |
| target   | 相当于 a 链接的 target 属性，href 存在时生效                                                                                         | string                                                    | -         |      |
| btnType  | 设置按钮类型                                                                                                                         | `primary` \| `warning` \| `link` \| `danger` \| `default` | `default` |      |
| onClick  | 点击按钮时的回调                                                                                                                     | (event) => void                                           | -         |      |

支持原生 button 的其他所有属性。
