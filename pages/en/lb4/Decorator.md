---
lang: en
title: 'Decorators'
keywords: LoopBack 4.0, LoopBack-Next
tags:
sidebar: lb4_sidebar
permalink: /doc/en/lb4/Decorators.html
summary:
---

A decorator allows you annotate or modify your class declarations and members with metadata.

## Introduction

*To get familiar with this TypeScript feature, try read [Understand TypeScript Decorator](#understand-typescript-decorator)*

Decorator is a good strategy to keep your code loosely coupled and modifies metadata at runtime. Currently LoopBack core provides built-in decorator functions you can use directly by `@myDecorator`, e.g. Route decorators that introduces in section Route-Decorators, and implements a dependency injection system that can apply a decorator by `@inject('myDecorator')`. 

Some components also exports decorators for you:
- [authentication](#authentication-decorators)
- [repository](#repository-decorators)

*Janny: Most examples are documented in a certain concept that a decorator works closely with, I am not sure should I turn this page to something like a reference:*

- some usage are well documented, I linked to certain section
- some usage can be found in unit test, while integration example is missing, should I create on this page?
- some have integration test, modify it and add on this page?
- Do I need to document what metadata each decorator adds to the reflector and document in the reference?
- I am confused with some decorator can be used by either @mydecorator or @inject(‘mydecorator’), are they equal? 

## Route Decorators
- @get, @post, @put, @patch, @del

  Register route for a controller by rest decorator, for their usage, refer to [Routing to Controllers](controller.htm#Routing-to-Controllers)

- @api

  Register route for a controller by api decorator, more details and example refer to [Specifying Controller APIs](controllers.htm#Specifying Controller APIs)

- @operation

  Expose a Controller method as a REST API operation. Usage refer to [code](https://github.com/strongloop/loopback-next/blob/debe221ee7eb07b6d6962416b79592c8f13d1e91/packages/core/src/router/metadata.ts#L230-L234)

  *Janny: Need example in doc?*

- @param

  Describe an input parameter of a Controller method. An example can be found in [Writing Controller methods](controller.htm#Writing-Controller-methods), more usage refer to [tsDoc](https://github.com/strongloop/loopback-next/blob/debe221ee7eb07b6d6962416b79592c8f13d1e91/packages/core/src/router/metadata.ts#L252-L272)

  *Janny: Change link to tsDoc page when it's done*
  
## Dependency Injection

@inject is a decorator to annotate method arguments for automatic injection by LoopBack IoC container. It can only be applied on a **method parameter** or a **property**. Basiclly it defines a reflector metadata for the target class.

A quick example can be found in [test case](https://github.com/strongloop/loopback-next/blob/9769e85306a8a866d71f133b1d0c013dde0d43c2/packages/context/test/unit/inject.test.ts#L21-L28)

It's been documented as a LoopBack core concept in [Dependency Injection](Dependency-Injection.htm)

*Janny: we miss a list of all metadata keys we can inject*

## Authentication Decorators

- @authenticate

Mark a controller method as requiring authenticated user, it takes in a strategy name. Example refer to [test case](https://github.com/strongloop/loopback-next/blob/9769e85306a8a866d71f133b1d0c013dde0d43c2/packages/authentication/test/acceptance/basic-auth.ts#L104)

## Repository Decorators

### Model decorators

- @model

Define a model in a repository, see [define-models](http://loopback.io/doc/en/lb4/Repositories.html#define-models)

- @property

Define a property in a model, see [define-models](http://loopback.io/doc/en/lb4/Repositories.html#define-models)

### Relation decorators

*Since relation is still in design phase, we only have unit test but no integration example. Refer to [test case](https://github.com/strongloop/loopback-next/blob/9769e85306a8a866d71f133b1d0c013dde0d43c2/packages/repository/src/decorators/relation.ts) for usage*

- @relation

Register a general relation

- @belongsTo @hasOne @hasMany @embedsOne @embedsMany @referencesOne @referencesMany

Register a specific relation

### Repository decorators

- @repository

A Repository is a type of _Service_ that represents a collection of data within a DataSource, the decorator takes in a model class(or its name) and a datasource instance(or its name). For usage, refer to [test case](https://github.com/strongloop/loopback-next/blob/9769e85306a8a866d71f133b1d0c013dde0d43c2/packages/repository/test/unit/decorator/repository.ts#L90)

## Compose and customize decorators

TBD 

- Use chitchat as an example of compose decorators
- for customize decorators, I expect to create some validation or hook functions as example

## Understand TypeScript Decorator

There are 5 types of decorators: class, method, property, method parameter. 

Janny: TDB, I am creating a repo(TBD) to explain it: https://github.com/jannyHou/typescript-decorator-playground/tree/master


## Others

*Copied from original wiki*

Potential topics:

What is a decorator? Allows you annotate your classes with metadata.
simple example @authenticate
How to use decorators (what are the features)
Define routes (@api)
Define access controls
Compose and customize decorators
Note: you have to use Babel or TypeScript for decorator support
A Repository is a type of _Service_ that represents a collection of data within a DataSource.