# Lionel oAuth Client for React [![Project Status: WIP – Initial development is in progress, but there has not yet been a stable, usable release suitable for the public.](https://www.repostatus.org/badges/latest/wip.svg)](https://www.repostatus.org/#wip)

This package adds browser based oAuth with or without Open ID Connect. It wraps the functionality from [Lionel oAuth Client](https://github.com/Aventyret/lionel-oauth-client) into the React hooks api.

## Browser Support

The library works with modern browsers. Also works with IE11, but it users `Promise` and `TextEncoder`, so you will need to implement solutions for those if you want Internet Explorer support.

## How to get going

### Installation

```bash
npm install lionel-oauth-client lionel-oauth-client-react
```

```bash
yarn add lionel-oauth-client lionel-oauth-client-react
```

### API

This package only exposes functions from lionel-oauth-client into a React friendly hook. Checkout [the online documentation for lionel-oauth-client](https://aventyret.github.io/lionel-oauth-client/) to see specifics of these functions.

Note that this package (just as Lionel oAuth Client) is for browser based oAuth, so these methods will not work in SSR (however no errors are thrown if you call them on the server).

### Example

```
import { useEffect, useState } from "react";
import { useLionelOauthClient } from "lionel-oauth-client-react";

import oidcConfig from "./constants/oidc-config";

function App() {
  const [accessToken, setAccessToken] = useState(null);
  const [user, setUser] = useState(null);
  const { setupOidc, signIn, signInSilently, subscribe } = useLionelOauthClient(oidcConfig);

  useEffect(() => {
    setupOidc();
    subscribe('tokenLoaded', setAccessToken);
    subscribe('userLoaded', setUser);
    subscribe('tokenUnloaded', () => setAccessToken(null));
    subscribe('userUnloaded', () => setUser(null));
    signInSilently();
  }, []);

  return (<div>
    {user ? <h1>Hello {user.name}</h1> : <h1>Hello</h1>}
    {!user ? <button type="button" onClick={signIn}>Sign in</button> : null}
  </div>);
}

```

## Sponsors

Lionel oAuth Client for React is an MIT-licensed open source project made possible by [Äventyret](https://aventyret.com).

## Questions

You can use the issue list for bug reports and feature requests.

Note that this is only a wrapper for [Lionel oAuth Client](https://github.com/Aventyret/lionel-oauth-client) so questions that not directly concern the React api might be better suited to pose there.

## License

[MIT](https://opensource.org/licenses/MIT)

Copyright (c) 2022-present, Äventyret Sweden AB
