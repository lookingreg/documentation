# Trigger's Values Types

Trigger's values is a list of parameters that must be filled in for the trigger to work. Each value has a type, for convenient management and validation of input data.

## Primitive types

- String

    ```yaml
    value: { type: string }
    ```

- Number

    ```yaml
    value: { type: number }
    ```

- Boolean

    ```yaml
    value: { type: boolean }
    ```

- Null

    ```yaml
    value: { type: "null" }
    ```

- Object

    ```yaml
    value:
        type: object
        properties:
            foo: { type: string }
            bar: { type: number }
    ```

- Array

    ```yaml
    value:
        type: array
        items: { type: string }
    ```

- Tuple

    ```yaml
    value:
        type: tuple
        items:
            - { type: string }
            - { type: number }
    ```

<!-- ## Special Types

- Threshold

    Used if in a trigger, in addition to equality with a number, values greater or less are needed.

    ```yaml
    value: { type: threshold }
    ```

- Conditions

    Used to filter trigger activation by some parameters that are described in the spec.

    ```yaml
    value: 
        type: conditions
        spec:
            from: 
                type: address 
                format: evm
            to: 
                type: address
                format: evm
            amount: 
                type: number
    ``` -->

## Address Type

For convenient management of the address book in the Web3alert, addresses have been divided into different groups. Here is a list of supported address formats:

- Plain

    ```yaml
    address-plain: { type: address }
    ```

- SS58 _(Substrate)_

    ```yaml
    address-ss58:
        type: address
        format: ss58
        prefix: 0
    ```

- EVM

    ```yaml
    address-evm:
        type: address
        format: evm
    ```

- Bitcoin

    ```yaml
    address-bitcoin:
        type: address
        format: bitcoin
    ```

- SUI

    ```yaml
    address-sui:
        type: address
        format: sui
    ```

- Cosmos

    ```yaml
    address-cosmos:
        type: address
        format: cosmos
        prefix: celestia
    ```
