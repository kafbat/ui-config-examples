# Keycloak setup

1. Run the example compose file provided in this directory
2. Go to keycloak admin console at http://localhost:8080/admin and create a new realm (myrealm)
3. Create users "admin" and "readonly", set passwords for them
4. Create realms roles "ops" and "ronly". You can use client roles instead if you want to, but this guide won't cover this.
5. Go to users, assign ops role to admin user and ronly role to readonly user

## Creating a client

Let's create an "openid connect" client:

1. Go to "clients" menu of "myrealm" realm
2. Create a client, use name (client id) "kafbat-ui-client"
3. Set "client authentication" to "on" and "authorization" to "on", allow the "standard" (authorization code) flow. 
4. Set the redirect url to http://localhost:9091/login/oauth2/code/keycloak
Obtain client secret in "credentials" tab, save it somewhere
5. Go to "client scopes" tab in our client -> kafbat-ui-client-dedicated -> mappers tab -> add mapper -> from predefined -> find "realm roles", edit added mapper, "token claim name" = "groups", "Claim JSON Type" = String, "Multivalued" = true

This is a simple setup with users assigned to roles directly. You can use groups with roles instead, but this guide doesn't cover it.

## Kafbat UI setup

1. In config.yml example provided, replace client-id and client-secret (obtained earlier) from keycloak
2. Adjust the roles configuration if needed

When logging in, you should see the following in the logs:

```log
DEBUG [reactor-http-nio-6] i.k.u.s.r.e.OauthAuthorityExtractor: Principal name is: [name surname]
DEBUG [reactor-http-nio-6] i.k.u.s.r.e.OauthAuthorityExtractor: Token's groups: [default-roles-myrealm,ops,offline_access,uma_authorization]
DEBUG [reactor-http-nio-6] i.k.u.s.r.e.OauthAuthorityExtractor: Matched group roles: [admins]
```

If it didn't work, you can expand logging this way:
```
logging:
  level:
    io.kafbat.ui.service.rbac.extractor: TRACE
```
This will yield additional log messages.

User info is also available at http://localhost:9090/api/authorization endpoint.

Voilà!
