---
title: Ideas
---

# Ideas

This is a dump for things we could implement in the future

## Status

A system to store temp status data, for example a form field error.

Can be subscribed to by a component for easy UI implementation

```js
App.status.set('username').invalid().message('Username is already taken');

App.status.remove('username');
App.status.clear();

App.status.state; // state instance containing all current errors / messages
// can be used in components with usePulse

App.status.get('username'); // returns StatusObject
```

The data would be stored and available as follows:

```ts
interface StatusData {
  [key: string]: {
    message: string | null;
    status: 'invalid' | 'success' | 'error';
  };
}
```

## Data Model

```js
App.Model((model, data) => {
  return {
    id: model.index(),
    thumbnail_hash: model.string().max(100).min(100).hidden().optional()
    thumbnail: model.compute(() => AppState.URL.value + data.thumbnail_hash).if(data.thumbnail_hash)
    connections: model.relate(Connections)
    settings: model.level('owner'),
  }
})
```



# Collection Relations
```ts
Users.relate(Posts, 'posts')
```
- posts property will be deleted and auto collected into posts
- group will be created automatically on Posts as the user id
- users output will contain posts