# AzureAD OAUTH2 setup

1. Install kafka-ui Helm Chart from https://kafbat.github.io/helm-charts repository.
2. Append the provided configuration to your ```yamlApplicationConfig``` in yours values.yaml

When logging in, you should see the following in the logs:

```log
2025-08-15 17:25:20,219 TRACE [reactor-http-epoll-4] i.k.u.s.r.e.OauthAuthorityExtractor: Extracting OAuth2 user authorities
2025-08-15 17:25:20,221 DEBUG [reactor-http-epoll-4] i.k.u.s.r.e.OauthAuthorityExtractor: Principal name is: [user.name@memelords.lol]
2025-08-15 17:25:20,225 DEBUG [reactor-http-epoll-4] i.k.u.s.r.e.OauthAuthorityExtractor: Matched roles by username: []
2025-08-15 17:25:20,227 TRACE [reactor-http-epoll-4] i.k.u.s.r.e.OauthAuthorityExtractor: The field is either a set or a list, returning as is
2025-08-15 17:25:20,228 DEBUG [reactor-http-epoll-4] i.k.u.s.r.e.OauthAuthorityExtractor: Token's groups: [admin]
2025-08-15 17:25:20,231 DEBUG [reactor-http-epoll-4] i.k.u.s.r.e.OauthAuthorityExtractor: Matched group roles: [admin]
```
