# 📦 php-duration-formatter

**Advanced PHP library for parsing, formatting, converting, and humanizing time durations.**

Supports intuitive input formats like `1h 30m`, `01:30:00`, or `5400` and provides custom formatting, JSON serialization, and accurate conversion to seconds and minutes.

> 🛠️ Built as an enhanced and modernized alternative to [kevinkhill/php-duration](https://github.com/kevinkhill/php-duration), offering expanded feature support, token-based formatting, custom hours-per-day handling, and complete PHPUnit test coverage.

---

## ✅ Features:

- Flexible input support: parse durations from strings, numbers, or colon-formatted time
- Conversion to seconds, minutes, arrays, strings, and JSON
- Custom formatting with tokens (`d`, `hh`, `mm`, `ss`, etc.)
- Support for days with customizable `hoursPerDay`
- Human-readable output (`1h 30m`)
- Chainable and reusable instance
- Implements `JsonSerializable` and `Stringable`
- Fully tested with 100% PHPUnit coverage (61 tests, 134 assertions)

---

## 📥 Installation

Install via [Composer](https://getcomposer.org):

```bash
composer require demirkaric/php-duration-formatter
```

---

## 🚀 Usage

### ✅ Basic Usage

```php
use Demirk\PhpDurationFormatter\TimeDuration;

$duration = new TimeDuration('1h 42m 30s');

echo $duration->toSeconds();      // 6150.0
echo $duration->toMinutes();      // 102.5
echo $duration->humanize();       // "1h 42m 30s"
echo $duration->format();         // "01:42:30" (default format)
echo (string) $duration;          // "01:42:30"

echo json_encode($duration);      // {"seconds":6150,"values":{"days":0,"hours":1,"minutes":42,"seconds":30},"formatted":"01:42:30","humanized":"1h 42m 30s"}
```

---

### 🧩 Supported Input Formats

- `"1h 30m"`  
- `"1d 4h 5m 2.5s"`  
- `"01:30"` or `"01:30:45"`  
- `3600` or `3661.5`  
- `"2d"`  

---

## 🧠 Custom Format Tokens

Use `format(string $pattern)` to generate custom formatted strings.

| Token | Meaning                         | Example  |
|-------|----------------------------------|----------|
| `d`   | Days (non-padded)                | 1        |
| `dd`  | Days (zero-padded)               | 01       |
| `h`   | Hours (non-padded)               | 2        |
| `hh`  | Hours (zero-padded)              | 02       |
| `H`   | Total hours (including days)     | 26       |
| `HH`  | Total hours (zero-padded)        | 26       |
| `m`   | Minutes                          | 5        |
| `mm`  | Minutes (zero-padded)            | 05       |
| `s`   | Seconds                          | 4.5      |
| `ss`  | Seconds (zero-padded)            | 04.5     |
| `S`   | Rounded seconds                  | 4        |
| `SS`  | Rounded seconds (zero-padded)    | 04       |

```php
$duration = new TimeDuration('1d 2h 5m 30s');

echo $duration->format('dd hh:mm:ss'); // 01 02:05:30
echo $duration->format('H:mm');        // 26:05
```

> ⚠️ `format()` will throw an exception if both `d` and `H` are used together (conflict between relative and absolute hours).

---

## 🔄 Conversion Methods

```php
$duration->toSeconds();                // float/int
$duration->toSeconds('1h 5s');         // pass string directly
$duration->toMinutes();                // in float
$duration->toMinutes(null, 0);         // rounded to int
$duration->toMinutes(null, 2);         // rounded to 2 decimal places
```

---

## 📚 Humanized Output

```php
$duration = new TimeDuration('2d 3h 15m');

echo $duration->humanize(); // "2d 3h 15m"
```

---

## 🧪 Tests

This library is tested with [PHPUnit](https://phpunit.de):

- ✅ 111 tests
- ✅ 191 assertions
- ✅ Covers parsing, formatting, rounding, edge cases, and serialization

To run tests:

```bash
vendor/bin/phpunit
```

---

## 🛠 Requirements

- **PHP >= 8.1**
- **Composer**

---

## 👏 Credits

This library is inspired by and originally based on [Kevin Hill’s `php-duration`](https://github.com/kevinkhill/php-duration), with significant improvements in architecture, extensibility, and formatting capabilities.  
Parsing, formatting, and conversion logic has been modernized and tested.

---

## 📄 License

MIT © Demir Karić  
See `LICENSE` file for details.
