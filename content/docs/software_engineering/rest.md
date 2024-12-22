+++
title = 'REST'
date = 2024-12-22T05:08:33+05:30
draft = false
+++

REST (Representational State Transfer)

# REST constraints

1. Client/Server
2. Stateless
3. Cache
4. Uniform Interface
5. Layered System
6. Code on Demand (optional)

# Cache

1. When caching is utilized and resource is requested from a server,
  - if the content is modified then we send `200 Ok` HTTP status in response.
  - if the content is not modified then we send `304 Not Modified` HTTP status in response.

# Best Practices

## Resources

1. We only need 2 base URLs per resource
  - collection (`/cars`)
  - element (`/cars/1244`)

2. 4 operations (CRUD)
  - POST (Create)
    - `/cars`: create a new car
    - `/cars/1244`: create a new car with id `1244` or fail
  - GET (read)
    - `/cars`: list cars
    - `/cars/1244`: show car 1244
  - PUT (update)
    - `/cars` : replace cars
    - `/cars/1244`: if exists update car 1244, if not, create car 1244 or fail
  - DELETE (delete)
    - `/cars` : delete all cars
    - `/cars/1244`: delete car 1244

3. Avoid verbs to name your resources. Use plural nouns.
4. Use verbs only if the functionality provided by the call is an operation and not a resource, such as:
  - Calculate
  - Convert
  - Translate
5. Be consistent
6. Use concrete resource names instead of abstract ones. e.g., `/cars`, `/cats`

## Response format

1. Use the Accept header
  - `accept: application/header`
2. Use JSON as default response format

Few examples how respose format:

1. Google: `?alt=json`
2. foursqare: `\venue.json`
3. digg: `Accept: application/json` or `?type=json`

## Pagination

1. Use `?offset=10&limit=50`
2. Assume default if no parameters are provided. e.g., `limit=10&offset=0`

Few examples of pagination:

1. Facebook: `?offset=10&limit=50`
2. Twitter(x): `?offset=10&limit=50`
3. Linkedin: `?start=10&count=50`

## Attribute names

1. Use lowerCamalCase for readability

## Errors, HTTP status codes

1. Avoid having more than 8 error codes
  - `200 201 304 400 401 403 404 500`
2. Use the same error codes accross all different API's

## Error Responses

1. Incorporating hints about how to fix errors and a link to get more infomation.

```json
{
  "code": 23213,
  "message": "MESSAGE",
  "info": "https://SOME_DOMAIN/docs/error/CODE"
}
```

Examples by different orgs:

Facebook
```json
{
  "type": "OAuthExeption",
  "message": "----"
}
```

Twillo
```json
{
  "status": 401,
  "message" "",
  "code": 20003,
  "more_info": "http://twillo.com/docs/erros/20003"
}
```

## Assosiations

Assosiations used to represent relationships between entities

1. Create for assosiations resource

```
POST `/owners/1234/cars`
GET `/owners/1234/cars/1244`
```

## Complex variations

1. Sweep variations behind the `?` in the query string

`GET /cars?color=red&location=newyork`

## Versioning

1. Recommed way `/v1/cars`
2. Maintain at least one version back.
3. Give developers atleast one cycle to react before obsoleting a version.

Examples by different orgs:

1. Twillow: `/2010-04-01/Accounts`
2. Salesforce: `/services/data/v20.0/subjects/account`
3. Facebook: `/?v=1.0`
4. Linkedin: `/v1`
5. Foursquare: `/v2`
6. Etsy: `/v1`

## Partial responses

1. `/cars?fields=name,color,regitryLocation.postalCode`

Examples by different orgs:

1. Linkedin: `/people:(id,first-name,last-name,industry)`
2. facebook: `/joe.smith/friends?fields=id,name,picture`
3. Google: `?fields=title,media:group(media:thumbnail)`

## Search

1. Global: `/search?q=short+hair`
2. Scoped-1 Object: `/cars?q=red+color`
3. Scoped-Multiple Objects: `/search?q=red-color&scope=cars,owners`

## Domain names

1. API gateway : `api.domain.com`
2. Developers Portal: `developers.domain.com`
3. Configure web redirects:
  - api -> developers (if from browser)
  - dev -> developers
  - developers -> developers

Examples by different orgs:

1. Foursquare
  - `api.foursquare.com`
  - `developers.foursquare.com`
2. Twitter (X)
  - `api.twitter.com`
  - `search.twitter.com`
  - `stream.twitter.com`
  - `dev.twitter.com`
3. Facebook
  - `graph.facebook.com`
  - `api.facebook.com`
  - `developers.facebook.com`

## Authentication

1. OAuth 2.0

Examples by different orgs:

1. Facebook: OAuth 2.0
2. Twitter (X): OAuth 1.0a
3. Paypal: OAuth 2.0
4. Google: OAuth 2.0

# References

1. [RESTful API Design Best Practices You Need To Know - YouTube](https://www.youtube.com/watch?v=BB1Y_wHyKGM&ab_channel=apiguru)
