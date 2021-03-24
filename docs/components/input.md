## Input

各种类型的 input

```tsx
import React, { useState } from 'react';

import { Input } from '@wilson_p/rock_ui';

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
  const [InputValue, setInputValue] = useState('');
  return (
    <div>
      <div style={title}>普通input</div>
      <div style={flexCenter}>
        <Input
          value={InputValue}
          onChange={e => {
            setInputValue(e.target.value);
          }}
        />
      </div>
      <div style={title}>带icon的input</div>
      <div style={flexCenter}>
        <Input
          icon="address-book"
          value={InputValue}
          onChange={e => {
            setInputValue(e.target.value);
          }}
        />
      </div>
      <div style={title}>prepend icon input</div>
      <div style={flexCenter}>
        <Input
          prepend="http://"
          icon="address-book"
          value={InputValue}
          onChange={e => {
            setInputValue(e.target.value);
          }}
        />
      </div>

      <div style={title}>append input</div>
      <div style={flexCenter}>
        <Input
          append=".com"
          value={InputValue}
          onChange={e => {
            setInputValue(e.target.value);
          }}
        />
      </div>
    </div>
  );
};
```

按钮的属性说明如下：

| 属性     | 说明                                       | 类型                                                                                                      | 默认值 | 版本 |
| -------- | ------------------------------------------ | --------------------------------------------------------------------------------------------------------- | ------ | ---- |
| disabled | 是否禁用状态，默认为 false                 | boolean                                                                                                   | false  |      |
| prepend  | 带有前缀图标的 input                       | ReactNode \| 设置 Icon 的图标的类型，具体类型请参考 [fontawesome 官网](https://fontawesome.dashgame.com/) | -      |      |
| append   | 带有后缀图标的 input                       | ReactNode \| 设置 Icon 的图标的类型，具体类型请参考 [fontawesome 官网](https://fontawesome.dashgame.com/) | -      |      |
| size     | 控件大小。注：标准表单内的输入框大小限制为 | `lg` \| `sm` \| `${number}x`                                                                              | -      |      |
| onChange | 点击按钮时的回调                           | (event) => void                                                                                           | -      |      |

支持原生 input 的其他所有属性。
