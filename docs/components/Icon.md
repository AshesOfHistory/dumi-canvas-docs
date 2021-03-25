# Icon

```tsx
import React, { useState } from 'react';

import { Icon } from '@wilson_p/rock_ui';

export default () => {
  const IconGroupWrapper = {
    display: 'flex',
    justifyContent: 'spaceBetween',
    alignItems: 'center',
  };
  const IconWrapper = {
    display: 'flex',
    flexDirection: 'column',
    alignItems: 'center',
    justifyContent: 'spaceAround',
  };
  return (
    <div style={IconGroupWrapper}>
      {/*<div>点击复制图标</div>*/}
      <div style={IconWrapper}>
        <Icon icon="check-circle" theme="primary" size="3x" />
        <div>check-circle</div>
      </div>
    </div>
  );
};
```
