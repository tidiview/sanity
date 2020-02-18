# Differs

There needs to be two kinds of differs:
1. Summary Differs: These can be handed down to the diff algorithm. These decide what the edit summaries coming back from differ contains. At the moment, I can't see the perfect use-case for overriding these yet, need to research some more
2. Visual Differs: These control how the change is rendered. Will be useful in all sorts of cases


# bateson.js

## Questions

What's up with both the global and local contect/ctx? The local context (the one passed to the recursive diff algo) isn't mutated, so I'm thinking rename the global one to options (assembled outside) then pass it as context to the first diff call. Then have the diff algo only used the local instance

## Bugs

That early return while evaluating `object` makes the next line unreachable

`extractText` should probably not join spans using whitespace, because you can have spans inside a word

It seems image isn't handled at all


## Operations

- `modifyField` - something on this field has changeed
- `replaceImage` - image asset reference has changed
- `editText` - a string (or text in block) has changed
- `replace` - object type has changed
- `remove` - a value has been removed
- `set` - a value has appeared where there was none
- `modifyEntry` - an entry in an array (with the given key) has changed
- `edit` - a plain value (number, booelan, null/undefined) has changed

Operations (`op: 'something'`) should have the verb first. `modifyEntry` is nice. I've renamed `textEdit` --> `editText`

