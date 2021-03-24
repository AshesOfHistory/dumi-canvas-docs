# 组件总览

### 拥有常用的几个基础布局组件，能够支持日常开发所需

#### Button 组件

```tsx
import React from 'react';
import { Button } from '@wilson_p/rock_ui';
export default () => {
  return (
    <Button btnType={'primary'} size={'lg'}>
      primary large
    </Button>
  );
};
```

#### input 组件

```tsx
import React, { useState } from 'react';
import { Input } from '@wilson_p/rock_ui';
export default () => {
  const [InputValue, setInputValue] = useState('');
  return (
    <Input
      value={InputValue}
      onChange={e => {
        setInputValue(e.target.value);
      }}
    ></Input>
  );
};
```

#### Icon 组件

```tsx
import React from 'react';
import { Icon } from '@wilson_p/rock_ui';
export default () => {
  return <Icon icon="check-circle" theme="primary" size="3x" />;
};
```

#### autocomplete

```tsx
import React from 'react';
import { AutoComplete } from '@wilson_p/rock_ui';
export default () => {
  const handleFetch = (query: string) => {
    return fetch(`https://api.github.com/search/users?q=${query}`)
      .then(res => res.json())
      .then(({ items }) => {
        const formatItems = items
          .slice(0, 10)
          .map((item: any) => ({ value: item.login, ...item }));
        return formatItems;
      });
  };
  return <AutoComplete fetchSuggestions={handleFetch}></AutoComplete>;
};
```

#### menu

```tsx
import React from 'react';
import { Menu } from '@wilson_p/rock_ui';
export default () => {
  return (
    <Menu
      defaultIndex="2"
      mode={'horizontal'}
      onSelect={index => console.log(index)}
      defaultOpenSubMenus={['2']}
    >
      <Menu.Item> link</Menu.Item>
      <Menu.Item disabled> link2</Menu.Item>
      <Menu.SubMenu title="dropdown">
        <Menu.Item>dropdown 1</Menu.Item>
        <Menu.Item>dropdown 2</Menu.Item>
      </Menu.SubMenu>
      <Menu.Item> link3</Menu.Item>
    </Menu>
  );
};
```

#### upload

```tsx
import React from 'react';
import { Upload, Icon } from '@wilson_p/rock_ui';
export default () => {
  return (
    <Upload
      action="https://www.mocky.io/v2/5cc8019d300000980a055e76"
      onChange={() => console.log('changed')}
      onRemove={() => console.log('removed')}
      name="fileName"
      multiple
      drag
    >
      <Icon icon="upload" size="5x" theme="secondary" />
      <br />
      <p>Drag file over to upload</p>
    </Upload>
  );
};
```
