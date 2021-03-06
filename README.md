[![NPM version](https://img.shields.io/npm/v/@reactway/api-builder.svg?logo=npm)](https://www.npmjs.com/package/@reactway/api-builder)
[![Build Status](https://img.shields.io/azure-devops/build/reactway/reactway/7/master.svg?logo=azuredevops)](https://dev.azure.com/reactway/ReactWay/_build?definitionId=7)
[![Code coverage](https://img.shields.io/azure-devops/coverage/reactway/reactway/7/master.svg)](https://dev.azure.com/reactway/ReactWay/_build?definitionId=7)
[![Dependencies](https://img.shields.io/david/reactway/api-builder.svg)](https://david-dm.org/reactway/api-builder)
[![Dev dependencies](https://img.shields.io/david/dev/reactway/api-builder.svg)](https://david-dm.org/reactway/api-builder?type=dev)

# @reactway/api-builder

An easy api client builder for applications with identity.

## Features

-   API builder is ready for SPA development
-   OAuth identity mechanism included

## Get started

```sh
$ npm install @reactway/api-builder
```

To start using api builder first it needs to make an `ApiConfiguration` with structure (**host** field is **required**). Then initiate class with created configuration.

```ts
interface ApiConfiguration {
    host: string;
    path?: string;
    defaultHeaders?: { [index: string]: string };
    defaultAuthRequired?: boolean;
    identity?: IdentityMechanism;
    defaultQueryParams?: QueryParams;
    requestQueueLimit?: number;
}

const apiConfiguration: ApiConfiguration = {
    host: "https://example.com"
};

const ApiClient = new ApiBuilder(apiConfiguration);
```

To make request you have create an `ApiRequest` typed object or arrow function if you want to pass parameters. `method` and `requestPath` fields are **required** for `ApiRequest`.

```ts
const getExample: ApiRequest = {
    method: HttpMethods.GET
    requestPath: PATH_GET
};

const getExample = (id: number): ApiRequest => {
    return {
        method: HttpMethods.GET,
        requestPath: `/${id}`
    };
};
```

Only http(s) method `GET` does not take `body` param. Rest of methods takes passed typed `body`. To pass typed `body` to a request here is an example.

```ts
interface Person {
    name: string;
    surname: string;
}

const getExample = await apiBuilder.post<Person>({
    requestPath: "/post",
    body: {
        name: "John",
        surname: "Snow"
    }
});
```

Also you can pass `QueryParams`.

```ts
type QueryParams = { [key: string]: string | number | Array<string | number> };

const getExample: ApiRequest = {
    method: HttpMethods.GET
    requestPath: PATH_GET,
    queryParams: {
        page: 2
    }
};
```

## API

WIP

## Documentation

WIP

## License

Released under the [MIT license](LICENSE).
