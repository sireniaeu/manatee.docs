# Context Actions

The v1 *context actions* endpoint (with base at `/v1/ContextAction`)  can be used to execute actions in the active session of a running Manatee.

{% method %}
## Perform

The *perform* method executes a named action/flow given that the arguments match the configured flow.

The *identifier* of the flow is given as part of the url:

```
http://.../v1/ContextAction/Perform/<action-id>
```

Arguments can be given as form-data or as a JSON document when the `Content-Type` is set to `application/x-www-form-urlencoded` for the former and  `application/json` for the latter.

The result of performing an action will *always* be returned as a JSON document. If the execution of the action takes longer than 5 min it will be aborted and an exception returned.

{% sample lang="bash" %}
Example using `curl`- assumes token is found in `token.jwt` file.

```bash
$ curl -XPOST -d "arg1=value1" -d "arg2=value2" -H "Authorization: Bearer $(cat token.jwt)"".../v1/ContextAction/Perform/[eu.sirenia]Action.Id.Random"
```

## Errors

If an action cannot be identified (e.g. because it does not exist) a `404` statuscode will be returned.

{% sample lang="bash" %}
```bash
$ curl -XPOST -H "Authorization: Bearer $(cat token.jwt)"".../v1/ContextAction/Perform/[eu.sirenia]Action.Id.DoesNotExist" -v

> POST /v1/ContextAction/Perform/[eu.sirenia]Action.Id.DoesNotExist HTTP/1.1
> Host: ...
> User-Agent: curl/7.54.0
> Accept: */*
>
< HTTP/1.1 404 Not Found
< Transfer-Encoding: chunked
< Content-Type: text/html
< Server: Microsoft-HTTPAPI/2.0
< Date: Tue, 28 Nov 2017 13:50:27 GMT
<

          _/  _/      _/    _/  _/
         _/  _/    _/  _/  _/  _/
        _/_/_/_/  _/  _/  _/_/_/_/
           _/    _/  _/      _/
          _/      _/        _/

```

If the arguments given does not match the arguments configured for the action an `417` (Expectation Failed) status code will be returned along with a JSON object containing information about the failure.

```bash
$ curl -XPOST -H "Authorization: Bearer $(cat token.jwt)"".../v1/ContextAction/Perform/[eu.sirenia]Action.Id.RequiresArguments" -v


> POST /v1/ContextAction/Perform/[eu.sirenia]Action.Id.RequiresArguments HTTP/1.1
> Host: ...
> User-Agent: curl/7.54.0
> Accept: */*
>
< HTTP/1.1 417 Expectation Failed
< Transfer-Encoding: chunked
< Content-Type: application/json; charset=utf-8
< Server: Microsoft-HTTPAPI/2.0
< Access-Control-Allow-Origin: *
< Date: Tue, 28 Nov 2017 13:54:45 GMT
<

{"errorMessage":"Missing argument for the [eu.sirenia]Action.In.Arg1 parameter in request","fullException":null,"errors":null}
```
{% endmethod %}

{% method %}
### Perform the DEMO action

The *Demo* action has `[eu.sirenia]Action.Id.Demo` as its id. 

It needs the following arguments:

 * `[eu.sirenia]Action.In.CPR` (string) the patient identifier (CPR)


{% sample lang="bash" %}
Example using `curl` and form-data.

```bash
$ curl -XPOST -d "[eu.sirenia]Action.In.CPR=12345678" -H "Authorization: Bearer $(cat token.jwt)" ".../v1/ContextAction/Perform/[eu.sirenia]Action.Id.Demo"
```

{% sample lang="bash" %}
Example using `curl` and JSON.

```bash
$ curl -XPOST -d "{'[eu.sirenia]Action.In.CPR': '12345678'}" -H  "Content-Type=application/json" -H "Authorization: Bearer $(cat token.jwt)" ".../v1/ContextAction/Perform/[eu.sirenia]Action.Id.Demo"
```

{% endmethod %}