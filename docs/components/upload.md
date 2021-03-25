# upload

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
