# Enforces consistent naming for boolean props (react/boolean-prop-naming)

Allows you to enforce a consistent naming pattern for props which expect a boolean value.

## Rule Details

The following patterns are considered warnings:

```jsx
var Hello = createReactClass({
  propTypes: {
    enabled: PropTypes.bool
  },
  render: function() { return <div />; };
});
```

The following patterns are **not** considered warnings:

```jsx
var Hello = createReactClass({
  propTypes: {
    isEnabled: PropTypes.bool
  },
  render: function() { return <div />; };
});
```

## Rule Options

```js
...
"react/boolean-prop-naming": [<enabled>, { "propTypeNames": Array<string>, "rule": <string>, "message": <string> }]
...
```

### `propTypeNames`

The list of prop type names that are considered to be booleans. By default this is set to `['bool']` but you can include other custom types like so:

```jsx
"react/boolean-prop-naming": ["error", { "propTypeNames": ["bool", "mutuallyExclusiveTrueProps"] }]
```

### `rule`

The RegExp pattern to use when validating the name of the prop. The default value for this option is set to: `"^(is|has)[A-Z]"` to enforce `is` and `has` prefixes.

For supporting "is" and "has" naming (default):

- isEnabled
- isAFK
- hasCondition
- hasLOL

```jsx
"react/boolean-prop-naming": ["error", { "rule": "^(is|has)[A-Z]" }]
```

For supporting "is" naming:

- isEnabled
- isAFK

```jsx
"react/boolean-prop-naming": ["error", { "rule": "^is[A-Z]" }]
```

### `message`

The custom message to display upon failure to match the rule. This overrides the default message.

If you choose to use a custom message, you have access to two template variables.

* `propName` – the name of the prop that does not match the pattern
* `pattern` – the pattern against which all prop names are tested

For example, if a prop is named `something`, and if the rule's pattern is set to `"^(is|has)[A-Z]"`, you could set the custom message as follows:

```js
message: 'It is better if your prop ({{ propName }}) matches this pattern: ({{ pattern }})'
```

And the failure would look like so:

```
It is better if your prop (something) matches this pattern: (^is[A-Z])
```
