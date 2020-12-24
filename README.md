# rules_nodejs v3 Sass binary timeout

# FIXED!

The fix was using a different Sass setup in the `WORKSPACE` file. Like [here](https://github.com/bazelbuild/rules_nodejs/blob/b53e31c4bd769481eb9d42db3bb1ef6c44e2814d/examples/angular/WORKSPACE#L36).

## Setup

```
yarn
```

## Issue

```
yarn build
```

Works fine with rules_nodejs v2.3.2 but Sass times out with rules_nodejs v3.0.0. (you can change it in the `WORKSPACE` file)
