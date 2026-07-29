# DVWA — OS Command Injection

In this lab, I tested DVWA's **Command Injection** module across all four security levels.

The feature receives an IP address and executes a `ping` command on the server. The vulnerability appears when user-controlled input is included in an operating system command without adequate validation.

The goal was to identify which shell operators still allowed a second command to be executed at each level.

## Environment

- DVWA running locally with Docker
- Linux environment
- Web process running as `www-data`
- Tests performed only in the local lab

## Low

At the `low` level, the input is concatenated directly into `shell_exec()`:

```php
$target = $_REQUEST['ip'];
$cmd = shell_exec('ping -c 4 ' . $target);
```

There is no validation or filtering.

Payload:

```text
127.0.0.1; whoami
```

The server executed `ping` first and then `whoami`, returning:

```text
www-data
```

This confirms arbitrary OS command execution through the semicolon operator.

## Medium

The `medium` level introduces a blacklist for some shell operators. However, the pipe operator remains available.

Payload:

```text
127.0.0.1 | whoami
```

The output of `ping` was piped into `whoami`. Because `whoami` does not require standard input, it still executed and returned `www-data`.

The blacklist reduced the obvious attack surface but did not prevent command injection.

## High

The `high` level expands the blacklist, but one entry filters a pipe followed by a space rather than the pipe character itself.

Payload:

```text
127.0.0.1|whoami
```

Removing the space bypassed the filter, and `whoami` executed successfully.

This demonstrates why blacklist-based validation is fragile: a small difference between the filtered pattern and shell syntax can leave the vulnerability exploitable.

## Impossible

At the `impossible` level, the application validates the input as an IPv4 address instead of trying to block individual shell characters.

The value is split into four octets, each part must be numeric, and the command is rebuilt from the validated values. Injection payloads are rejected because they cannot satisfy the expected IP address format.

No command injection was achieved at this level.

## Remediation

The safest approach is to avoid invoking a shell with user-controlled input.

When an operating system command is unavoidable:

- Validate input using a strict allowlist and the expected data type.
- Pass arguments without shell interpretation.
- Avoid blacklist-based filtering.
- Run the application with the least privileges required.

## Conclusion

The tests showed a clear progression:

- **Low:** no protection.
- **Medium:** incomplete blacklist bypassed with `|`.
- **High:** stricter blacklist bypassed by removing a space.
- **Impossible:** strict input validation prevents shell metacharacters from reaching the command.
