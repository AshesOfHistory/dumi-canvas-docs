# menu

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
