Namespace: `core/notices`

In modular system of **Blocks**, we must handle the notices with Notices Data because it use Redux state.

### Selectors

**getNotices**
Returns all notices as an array, optionally for a given context. Defaults to the global context.

```js
declare var wp: any;
export const { subscribe, select, dispatch } = wp.data;

select('core/notices').getNotices('wc/checkout');

```

_Parameters_
- _context_ `?string`: grouping context. 
	- When you create a createNotice, there will be a parameter called context, usually 'wc/checkout' and 'wc/cart'.
	- **It is not detailed what contexts are available, you can see the contexts through Redux data state**.

_Returns_
- `WPNotice[]`: Array of notices.

### Actions

**createNotice**
Returns an action object used in signalling that a notice is to be created.
```js
declare var wp: any;
export const { dispatch } = wp.data;

dispatch('core/notices').createNotice('error', 'message', {
  context: 'wc/checkout',
  type: 'default'
});
```

_Parameters_
- _status_ `string|undefined`: Notice status (“info” if undefined is passed).
- _content_ `string`: Notice message.
- _options_ `[Object]`: Notice options.
- _options.context_ `[string]`: Context under which to group notice.
- _options.id_ `[string]`: Identifier for notice. Automatically assigned if not specified.
- _options.isDismissible_ `[boolean]`: Whether the notice can be dismissed by user.
- _options.type_ `[string]`: Type of notice, one of `default`, or `snackbar`.
- _options.speak_ `[boolean]`: Whether the notice content should be announced to screen readers.
- _options.actions_ `[Array<WPNoticeAction>]`: User actions to be presented with notice.
- _options.icon_ `[string]`: An icon displayed with the notice. Only used when type is set to `snackbar`.
- _options.explicitDismiss_ `[boolean]`: Whether the notice includes an explicit dismiss button and can’t be dismissed by clicking the body of the notice. Only applies when type is set to `snackbar`.
- _options.onDismiss_ `[Function]`: Called when the notice is dismissed.

_Returns_
- `Object`: Action object.

**removeAllNotices**
Removes all notices from a given context. Defaults to the default context.
```js
declare var wp: any;
export const { dispatch } = wp.data;

dispatch('core/notices').removeAllNotices('default', 'wc/checkout');
```

_Parameters_
- _noticeType_ `string`: The context to remove all notices from.
- _context_ `string`: The context to remove all notices from.

_Returns_
- `Object`: Action object.

**removeNotice**
Returns an action object used in signalling that a notice is to be removed.
```js
declare var wp: any;
export const { dispatch } = wp.data;

dispatch('core/notices').removeNotice(id, 'wc/checkout');
```

_Parameters_
- _id_ `string`: Notice unique identifier.
- _context_ `[string]`: Optional context (grouping) in which the notice is intended to appear. Defaults to default context.

_Returns_
- `Object`: Action object.

**removeNotices**
Returns an action object used in signalling that a notice is to be removed.
```js
declare var wp: any;
export const { dispatch } = wp.data;

dispatch('core/notices').removeNotices(ids, 'wc/checkout');
```

_Parameters_
- _ids_ `string[]`: List of unique notice identifiers.
- _context_ `[string]`: Optional context (grouping) in which the notices are intended to appear. Defaults to default context.

_Returns_
- `Object`: Action object.
## Resource
[Data Module Reference - Notices Data](https://developer.wordpress.org/block-editor/reference-guides/data/data-core-notices/)
