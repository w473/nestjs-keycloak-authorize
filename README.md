# nestjs-keycloak-authorize
## Description
NestJS package to authorize by role from Keycloak JWT (payload). 

It is designed to work in Kubernetes cluster
with [Istio](https://istio.io/) and [Keycloak](https://www.keycloak.org/)

JWT should be generated by Keycloak

Roles are expected to be in payload of token in
```json
"realm_access": {
    "roles": [
      "ADMIN",
      "SYS"
    ]
  },

```
Decorators:
- for methods:
  - HasRole(roles)
    - e.g @HasRole('ADMIN', 'SYS')
  - IsPublic()
- for parameters
  - GetUser()
    - returns User object or throws UserNotFoundException 


## Installation

```bash
$ npm i nestjs-keycloak-authorize
```
NestJS module:
```ts
providers: [
    {
      provide: AUTHORIZATION_HEADER_NAME,
      useValue: 'x-authz'
    },
    {
      provide: APP_GUARD,
      useClass: RolesGuard,
    },
  ]

export class AppModule implements NestModule {
  configure(consumer: MiddlewareConsumer): any {
    consumer.apply(AuthenticationMiddleware).forRoutes('*');
  }
}
```

## Test

```bash
# unit tests
$ npm run test

# tests coverage
$ npm run test:cov
```
