---
title: "Creating a Component"
weight: 5
---

### [&#128279;](#creating-a-component) Creating a Component

React components live inside the `/ts/src/modules` folder. Begin by creating a new file in `/ts/src/modules/example/Todos.tsx`. The UI is implemented primarily using React functional components. Here we'll provide a sample component using basic React constructs with Material-UI:

```typescript
import React, { useState } from 'react';
import TextField from '@mui/material/TextField';

import { siteApi, useUtil } from 'awayto/hooks';

export function Todos (): React.JSX.Element {

  const { setSnack } = useUtil();
  const [postTodo] = siteApi.useTodoServicePostTodoMutation();

  const [todo, setTodo] = useState({
    task: ''
  });
  
  const handleSubmit = () => {
    const { task } = todo;

    if (!task) {
      setSnack({ snackType: 'error', snackOn: 'You must have something todo!' });
      return;
    }
    
    postTodo({ task });
  }

  return <>
    <TextField
      id="task"
      label="Task"
      name="task"
      value={todo.task}
      onKeyDown={e => {
        if ('Enter' === e.key) {
          void handleSubmit();
        }
      }}
      onChange={e => setTodo({ task: e.target.value })}
    />
  </>;
}

export default Todos;
```
