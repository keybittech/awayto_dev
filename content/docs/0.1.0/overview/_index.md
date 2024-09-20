---
title: "Overview"
weight: 2
---

## [&#128279;](#overview) Overview

### Quick Installation

Make sure your console session can perform AWS CLI commands with Administrator role access.
```
npm i -g @keybittech/awayto

mkdir proj
cd proj
awayto install <name> <environment> "<description>"
```

### Prerequisites

Any AWS tasks are performed on an AWS account with the Administrator role.

- An AWS Account

- AWS CLI 2.0.42

- Node 16.3.0

- NPM 7.15.1

- Postgres 13.4

- Python 3.7.9

### Utility Commands

- `npm run start` -- Start a local dev server at `localhost:3000` which only serves the webapp, and uses the `settings.development.env` file.

- `npm run start-stack` -- Same as above, but if you opted for local-testing in the installation, this will start `sam local` using the `env.json` and `template.sam.yaml` files in the main directory. SAM Local starts up a docker contanerized instance of your Lambda function at `localhost:3001`. The webapp will pick up the `settings.local.env` file in this case.

- `npm run start-api` -- Starts just the api with the same above configuration.

- `npm run start-local` -- Starts just the webapp with the `settings.local.env` configuration. We use AWS SAM to run the local API, this requires Docker. AWS SAM, while extremely convenient, has gone through some growing pains; so if you ever run into issues, ask on the [Discord](https://discord.gg/KzpcTrn5DQ). We use the `--warm-containers LAZY` option, so when your api starts make sure to make a couple requests to get the Lambda initialized.

- `npm run watch-api` -- Start a webpack watcher on just the api.

- `npm run build-api` -- Build the api with webpack using `api.webpack.js`. As a result of the build, a minified index.js containing the Lambda handler will be placed into the `apipkg` folder.

- `npm run build-web` -- Build the webapp using react-app-rewired. As a result of this build, a `build` folder will be generated.

- `npm run build-deploy` -- Build both the api and webapp, in the event you are preparing to deploy a full stack update.

- `npm run install-stack` -- In the event you are installing a re-packaged version of Awayto, you can use this command to install the related AWS resources into your own AWS account.

- `npm run db-create-migration <name>` -- Autogenerate a migration in the `src/api/scripts/db` folder.

- `npm run db-update` -- Deploy any un-deployed `.sql` files in the `src/api/scripts/db` folder. You can see what's been deployed by reviewing the seed file `bin/data/seeds`.

- `npm run db-update-file <name>` -- If a script fails while updating, you can fix it then specifically-redeploy it with this command.

- `npm run invoke-event <name>` -- Use an event from `src/api/scripts/events` and run it against the live deployed lambda for your Awayto install.

- `npm run invoke-event-local <name>` -- Run Lambda events locally using AWS SAM.

- `npm run release` -- Run a release script which will deploy both the api (`apipkg` folder) and webapp (`build` folder) to s3. Then the script will request a CloudFront distribution invalidation on the entire webapp bucket. As well, the Lambda function will be re-deployed with the built handler.

### Typescript Suite
Type reference can be found [here](https://awayto.dev/docs/modules.html). 

### Hooks
There are a few hooks offered out of the box, core to the Awayto UI design experience.

#### useRedux
Hook into the fully typed redux store. Access your redux state using this hook.

```ts
import { useRedux } from 'awayto';

const profile = useRedux(state => state.profile); // e.g. returns the currently logged in IUserProfile
```

#### useAct

`useAct` is a wrapper for dispatching actions. Give it an [IActionTypes](https://awayto.dev/docs/modules.html#iactiontypes), a loader boolean, and the action payload if necessary.

```ts
import { useAct, IUtilActions } from 'awayto';

const { SET_SNACK } = IUtilActions;

const act = useAct();

act(SET_SNACK, { snackOn: 'Success!', snackType: 'success' }); // e.g. send a notification to the toast popup component
```

#### useApi
The `useApi` hook provides type-bound api functionality. By passing in a [IActionTypes](https://awayto.dev/docs/modules.html#iactiontypes) (e.g. [IUtilActionTypes](https://awayto.dev/docs/enums/iutilactiontypes.html), [IManageUsersActionTypes](https://awayto.dev/docs/enums/imanageusersactiontypes.html), etc...) we can control the structure of the api request, and more easily handle it on the backend.

```ts
import { useApi, IManageUsersActions, useRedux } from 'awayto';

const { GET_MANAGE_USERS, GET_MANAGE_USERS_BY_ID } = IManageUsersActions;

const api = useApi();
const users = useRedux(state => state.users);

api(GET_MANAGE_USERS); // Kickoff a GET/manage/users call, which will populate our redux state later
```

As long as we have setup our model, `GET_MANAGE_USERS` will inform the system of the API endpoint and shape of the request/response.

If the endpoint takes path parameters (like `GET/manage/user/id/:id`), or if the request requires a body, we can pass these as the third parameter. Pass a boolean as the second argument to show or hide a loading screen.

```ts
api(GET_MANAGE_USERS_BY_ID, false, { id }); // Get a user profile by a specified ID, refresh it in redux state, and do not show a loading screen
```
 
#### useCognitoUser
Use this hook to get access to Cognito functionality once the user has logged in, or to check if the user is logged in.

```ts
import { useCognitoUser } from 'awayto';

const cognitoUser = useCognitoUser();

await cognitoUser.getSession();

cognitoUser.isLoggedIn == true
```

#### useComponents
`useComponents` takes advantage of [React.lazy](https://reactjs.org/docs/code-splitting.html#reactlazy) as well as the [Proxy API](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy). By combining these functionalities, we end up with a tool that makes it easy to work in an expanding and quickly changing code base.

As new files are added to the project while the developer is working, they will be automatically discovered and made lazily available through `useComponents`. The only need is to refresh the browser page once the component has been added to the render cycle. If the developer tries to destructure a component that does not exist in the group of lazy loaded components, `useComponents` will return an empty `div`. This is configurable.

```ts
import { useComponents } from 'awayto';

function ParentComponent(props: IProps): JSX.Element {

  const { SomeComponent } = useComponents();

  return <SomeComponent {...props} />;

}
```

#### useFileStore
 `useFileStore` is used to access various types of pre-determined file stores. All stores allow CRUD operations for user-bound files. Internally default instantiates {@link AWSS3FileStoreStrategy}, but you can also pass a {@link FileStoreStrategies} to `useFileStore` for other supported stores.
 
 ```ts
 import { useFileStore } from 'awayto';
 
 const files = useFileStore();
 
 const file: File = ....
 const fileName: string = '...';
 
 // Make sure the filestore has connected
 if (files)
  await files.post(file, fileName)
 
 ```
