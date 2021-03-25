# autocomplete

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
