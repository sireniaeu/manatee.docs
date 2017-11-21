# Context Actions

The Context Actions (`/ContextAction`) endpoint can be used to execute actions in the active session of a running Manatee.

{% method %}
## Perform

The Perform method executes a named action/flow given that the arguments match

{% sample lang="js" %}
Here is how to print a message to `stdout` using JavaScript.

```js
console.log('My first method');
```

{% sample lang="go" %}
Here is how to print a message to `stdout` using Go.

```go
fmt.Println("My first method")
```

{% common %}
Whatever language you are using, the result will be the same.

```bash
$ My first method
```
{% endmethod %}
