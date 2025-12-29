---
displayed_sidebar: docs
---

# EXECUTE AS

Use the IMPERSONATE privilege with EXECUTE AS statements to switch the execution context of the current session to the impersonated user.

This command is supported from v2.4.

## Syntax

```SQL
EXECUTE AS user WITH NO REVERT
```

## Parameters

`user`: The user must already exist.

## Usage notes

- The current login user (who calls the EXECUTE AS statement) must be granted the privilege to impersonate another user. For more information, see [GRANT](../account-management/GRANT.md).
- The EXECUTE AS statement must contain the WITH NO REVERT clause, which means the execution context of the current session cannot be switched back to the original login user before the current session ends.

### Examples

1. Create a user for testing.

    ```sql
    CREATE USER 'test_impersonate'@'%' IDENTIFIED BY '123456';
    ```

2. Switch the execution context of the current session to the user `test_impersonate`.

    ```sql
    EXECUTE AS 'test_impersonate' WITH NO REVERT;
    ```

3. After the switch succeeds, run `SELECT CURRENT_USER()` to confirm the identity change.

    ```sql
    SELECT CURRENT_USER();
    +------------------------+
    | CURRENT_USER()         |
    +------------------------+
    | 'test_impersonate'@'%' |
    +------------------------+
    ```
