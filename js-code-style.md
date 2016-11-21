# Javascript Code Style

## ESLint with the `eslint-config-airbnb-base` preset, `eslint-config-airbnb` for React projects;

We can start a project to extend one of those bases if we find we have issues with some rules.

### For tests

You should fine-tune the config for your tests folder.
First set the right environment in your eslint config (`mocha` for example).
There's also a set of rules that you should probably ignore/change. Consider the following:

  * `no-unused-expressions`: Should be `off` when using assertion libs like `chai` for example.
  * `prefer-arrow-callback`: Should be `off` when using test frameworks like mocha as stated [in their documentation](https://mochajs.org/#arrow-functions).
  * `func-names`: Taking into account the above, it is just painful to name all of your test functions
  * `import/no-extraneous-dependencies`: You should be able to import/require our dev dependencies, the default only allows you to require your `dependencies`.

## Webpack and Babel

Rollup and Bublé might be tempting but we don't have any production experience with them, as soon as someone starts getting some at home experience we can start doing safer things with this on clients and then bigger things.

