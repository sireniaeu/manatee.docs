# Authentication

Authentication is done by using [JWT](https://jwt.io). Each API invocation must include a token in its header, e.g.  


```
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ...30RMHrHDcEfxjoYZgeFONFh7HgQ 
```

The token contains information about which endpoints the requestor is allowed to use as well as other meta-information. Tokens are issued manually upon request.

