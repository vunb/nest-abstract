<h1 align="center">Nestjs Abstract</h1>

<p align="center">Abstraction component for NestJs.</p>

Fair warning: Please do not use this package as of the moment. Published version is to test the actual `npm publish` command. 

Thank you! Stay tune!

## Features
- Provides **Abstractions** for your `NestJS` **RESTfulAPI**.
- Includes: `AbstractModule`, `AbstractService`, and `AbstractControllerFactory` along with `AbstractModel` (`mongoose`) and `AbstractEntity` (`typeorm`).
- [ ] Supports `@nestjs/swagger`

## Motivations

I am a big fan of `TypeScript` and **abstraction** overall. One of the biggest motivations is to create a `BaseController` to work with `Swagger`'s decorators that `@nestjs/swagger` provides which is on the todo list. Main reason is I want to roll out a version of the package that will make it work with `non-swagger` applications first as this is my first attempt at an `npm` package.

## Usage

1. Import `AbstractModule` in your `AppModule`
   ```typescript
    import { Module } from '@nestjs/common';
    import { AbstractModule } from 'nest-abstract';

    @Module({
        imports: [AbstractModule.forRoot()],
    })
    export class AppModule {}
   ```

   > By default, `AbstractModule` will use `Mongoose`. You can pass an object of type `AbstractModuleOptions` to the `forRoot()` method.

    ```typescript
    import { Module } from '@nestjs/common';
    import { AbstractModule, ObjectMapping } from 'nest-abstract';

    @Module({
        imports: [AbstractModule.forRoot({objectMapping: ObjectMapping.TypeOrm})],
    })
    export class AppModule {}
   ```
   
   > Note: `ObjectMapping.Mongoose` will require you to install `mongoose` and `@nestjs/mongoose` while `ObjectMapping.TypeOrm` will require you to install `typeorm` and `@nestjs/typeorm`.

    *Note: I will list the usage for Mongoose from step 2 on.*

2. Create your `MongooseSchema` and create an **interface** that will extend `AbstractModel`. `AbstractModel` is an **interface** that has: `createdAt`, `updatedAt` and `id`.
   
   ```typescript
   import { Schema } from 'mongoose';
   import { AbstractModel } from 'nest-abstract';
   
   const todoSchema = new Schema({
       content: {
           type: String
       }
   }, { timestamps: true });

   interface Todo extends AbstractModel {
       content: string;
   }
   ```

   > Use your `schema` to initialize your `Model` with `@nestjs/mongoose`.

3. Create your `Service` with `AbstractCoreService`.