# Icon

## 示例

```tsx
import React, { useState } from 'react';

import { Icon } from '@wilson_p/rock_ui';

export default () => {
  const IconGroupWrapper = {
    display: 'flex',
    justifyContent: 'space-between',
    alignItems: 'center',
    flexWrap: 'wrap',
  };
  const IconWrapper = {
    display: 'flex',
    flexDirection: 'column',
    alignItems: 'center',
    justifyContent: 'spaceAround',
  };
  const IconGroupTitle = {
    fontWeight: 'bold',
    fontSize: '22px',
    marginBottom: '10px',
  };

  const themeGroup = [
    'primary',
    'info',
    'success',
    'secondary',
    'warning',
    'danger',
  ];
  const iconGroup = [
    'check-circle',
    'bath',
    'adjust',
    'address-card',
    'anchor',
    'mouse-pointer',
    'spinner',
  ];

  const IconThemeGroup = (themeGroup, iconGroup) => {
    const iconGroupRow = [];
    themeGroup.forEach((theme, themeIndex) => {
      const iconWrapperArr = [];
      iconGroup.forEach((icon, iconIndex) => {
        iconWrapperArr.push(
          <div key={iconIndex} style={IconWrapper}>
            <Icon icon={icon} theme={theme} size="3x" />
            <div>{icon}</div>
          </div>,
        );
      });
      iconGroupRow.push(
        <div key={themeIndex}>
          <div style={IconGroupTitle}>{theme} theme</div>
          <div style={IconGroupWrapper}>{iconWrapperArr}</div>
        </div>,
      );
    });
    return <div>{iconGroupRow}</div>;
  };
  return (
    <div>
      {/*<div>点击复制图标</div>*/}
      {IconThemeGroup(themeGroup, iconGroup)}
    </div>
  );
};
```

## API

icon 的属性说明如下：

| 属性  | 说明                          | 类型                                                                                         | 默认值  | 版本 |
| ----- | ----------------------------- | -------------------------------------------------------------------------------------------- | ------- | ---- |
| theme | icon 的主题颜色，默认为 false | primary \| info \| success \| secondary \| warning \| danger                                 | primary |      |
| icon  | 带有前缀图标的 input          | 设置 Icon 的图标的类型，具体类型请参考 [fontawesome 官网](https://fontawesome.dashgame.com/) | -       |      |
