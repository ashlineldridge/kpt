---
title: "TypeScript Quickstart"
linkTitle: "TypeScript Quickstart"
weight: 6
type: docs
description: >
   Quickstart for Developing Config Functions
---

## Developer Quickstart

This quickstart will get you started developing a config function with the TypeScript SDK,
using an existing kpt-functions package. Config functions are any functions which implement
the `KptFunc` interface [documented here][api-kptfunc].

### Prerequisites

#### System Requirements

Currently supported platforms: amd64 Linux/Mac

#### Setting Up Your Local Environment

- Install [node][download-node]
- Install [docker][install-docker]
- Install [kpt][download-kpt] and add it to your $PATH

### Explore the Demo Functions Package

1. Get the `demo-functions` package:

   ```sh
   git clone --depth 1 https://github.com/GoogleContainerTools/kpt-functions-sdk.git
   ```

   All subsequent commands are run from the `demo-functions` directory:

   ```sh
   cd kpt-functions-sdk/ts/demo-functions
   ```

1. Install all dependencies:

   ```sh
   npm install
   ```

1. Run the following in a separate terminal to continuously build your function as you make changes:

   ```sh
   npm run watch
   ```

1. Explore the [`label_namespace`][label-namespace] transformer function. This function takes a
   given `label_name` and `label_value` to add the appropriate label to `Namespace` objects using
   the SDK's `addLabel` function.

   {{< code type="ts" >}}
   {{< readfile file="static/ts/label_namespace.ts" >}}
   {{< /code >}}

1. Run the `label_namespace` function on the `example-configs` directory:

   ```sh
   export CONFIGS=../../example-configs

   kpt fn source $CONFIGS |
   node dist/label_namespace_run.js -d label_name=color -d label_value=orange |
   kpt fn sink $CONFIGS
   ```

   As the name suggests, this function added the given label to all `Namespace` objects
   in the `example-configs` directory:

   ```sh
   git diff $CONFIGS
   ```

1. Try modifying the function in `src/label_namespace.ts` to perform other operations
   and rerun the function on `example-configs` to see the changes.

1. Explore validation functions like [validate-rolebinding]. Instead of transforming configuration,
   this function searches RoleBindings and returns a results field containing details about invalid
   subject names.

   {{< code type="ts" >}}
   {{< readfile file="static/ts/validate_rolebinding.ts" >}}
   {{< /code >}}

1. Run `validate-rolebinding` on `example-configs`.

   ```sh
   kpt fn source $CONFIGS |
   node dist/validate_rolebinding_run.js -d subject_name=alice@foo-corp.com |
   kpt fn sink $CONFIGS
   git diff $CONFIGS
   ```

1. Explore generator functions like [expand-team-cr]. This function generates a per-environment
   Namespace and RoleBinding object for each custom resource (CR) of type Team.

   {{< code type="ts" >}}
   {{< readfile file="static/ts/expand_team_cr.ts" >}}
   {{< /code >}}

1. Run `expand-team-cr` on `example-configs`.

   ```sh
   kpt fn source $CONFIGS |
   node dist/expand_team_cr_run.js |
   kpt fn sink $CONFIGS
   git diff $CONFIGS
   ```

## Next Steps

- Take a look at [these example functions][demo-funcs] to better understand how to use the typescript SDK.
- Read the complete [Typescript Developer Guide].
- Learn how to [run functions].

[download-node]: https://nodejs.org/en/download/
[install-docker]: https://docs.docker.com/v17.09/engine/installation/
[download-kpt]: ../../../../../installation/
[demo-funcs]: https://github.com/GoogleContainerTools/kpt-functions-sdk/tree/master/ts/demo-functions/src
[api-kptfunc]: https://googlecontainertools.github.io/kpt-functions-sdk/api/
[Typescript Developer Guide]: ../develop/
[run functions]: ../../../../consumer/function/
[label-namespace]: https://github.com/GoogleContainerTools/kpt-functions-sdk/blob/master/ts/demo-functions/src/label_namespace.ts
[expand-team-cr]: https://github.com/GoogleContainerTools/kpt-functions-sdk/blob/master/ts/demo-functions/src/expand_team_cr.ts
[validate-rolebinding]: https://github.com/GoogleContainerTools/kpt-functions-sdk/blob/master/ts/demo-functions/src/validate_rolebinding.ts
