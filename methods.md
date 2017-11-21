# Context Actions

The Context Actions (`/ContextAction`) endpoint can be used to execute actions in the active session of a running Manatee.

{% method %}
## Perform

The Perform method executes a named action/flow given that the arguments match the configured flow.

The *identifier* of the flow is given as part of the url:

```
http://.../v1/ContextAction/Perform/<action-id>
```

Arguments can be given as form-data or as a JSON document when the `Content-Type` is set to `application/x-www-form-urlencoded` for the former and  `application/json` for the latter.

{% sample lang="bash" %}
Example using `curl`.

```bash
$ curl -XPOST -d "arg1=value1" -d "arg2=value2" ".../v1/ContextAction/Perform/[eu.sirenia]Id.Action.Random"
```

{% endmethod %}

{% method %}
### Perform the NNN action

The NNN action has `[]to-be-decided` as its id. 

It needs the following arguments:

 * `[]-an-arg-tbd-1` (string) the patient identifier (CPR)


{% sample lang="bash" %}
Example using `curl` and form-data.

```bash
$ curl -XPOST -d "[]-an-arg-tbd-1=12345678" ".../v1/ContextAction/Perform/[]to-be-decided"
```

{% sample lang="bash" %}
Example using `curl` and JSON.

```bash
$ curl -XPOST -d "{'[]-an-arg-tbd-1': '12345678'}" -H  "Content-Type=application/json" ".../v1/ContextAction/Perform/[]to-be-decided"
```

{% endmethod %}