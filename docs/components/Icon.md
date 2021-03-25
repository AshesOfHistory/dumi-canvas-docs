# Icon

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
