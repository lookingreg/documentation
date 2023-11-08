# Basic Blocks

The Pipeline Processor has a built-in set of blocks that can be used when configuring a Pipeline. Here is a list describing these basic blocks.

## Accumulate

A block that makes it possible to accumulate data in the state. It is used, for example, to detect changes between old and new data.

#### Params:

* **state**: `object | undefined`

    Specifies what data should be saved.
* **output**: `object | object [] | undefined`

    Describes the output data of the block.

#### Output:

`params.output` or `[params.output]`

## Filter

A block that is used to filter the output data of the previous block in the pipeline according to a given condition.

#### Params:

* **expr**: `boolean`

    Parameter describing the condition by which the data should be filtered. Must always return `true` or `false`.

#### Output:

If the condition is true, it returns `[input]`, if not, it returns nothing.

## Request

The block executes any given HTTP request.

#### Params:

* **method**: `string`

    Method of HTTP request: `GET`, `HEAD`, `POST`, `PUT`, `DELETE`, `CONNECT`, `OPTIONS`, `TRACE`, `PATCH`.

* **url**: `string`

    Web address where the HTTP request will be sent.

* **headers**: `Record<string, string>` _(optional)_

    Headers of HTTP request.

* **body**: `string | JsonObject` _(optional)_

    Body of HTTP request.

#### Output:

Returns the server's response.

## Schedule

Block initiator. Starts the Pipeline once in a given time interval.

#### Params:

* **interval**: `string` 

    Human readable duration. The lib [parse_duration](https://github.com/jkroso/parse-duration) is used for conversion.

#### Output:

* **now**: `string` 

    Current datetime.

## Transform

Block converting the output data of the previous block according to the specified algorithm.

#### Params:

* **output**: `object | object []`

    Describes the output data of the block.

#### Output:

`params.output` or `[params.output]`