# PHP CSV Extension

A small PHP extension to add/improve the handling of CSV strings which follows
RFC 4180 https://tools.ietf.org/html/rfc4180

## Functionality
There are currently three functions which are inspired from ``fputcsv()`` and
``fgetcsv()`` namely ``csv_array_to_row()``, ``csv_collection_to_file()``,
``csv_row_to_array()``, and ``csv_file_to_collection()`` respectively.

These functions are binary safe (i.e. accepts nul bytes) and accept multi-bytes
strings as the delimiter, enclosure, and the EOL sequence.

The reason for being able to set these three arguments is that it allows the
support of non ASCII compatible character encodings (e.g. UTF-16).
Indeed, it's possible to provide the multi-byte sequence for each of the
corresponding components such that it can treat a file in a different encoding
(or write to a file of different encoding).

One limitation is that non ASCII compatible character encodings (e.g. UTF-16)
are not supported. However, this is already the case with the current CSV
functions, thus no support for those is currently planned.

```php
function csv_array_to_row(array $fields, string $delimiter = ',', string $enclosure = '"', string $eolSequence = "\r\n"): string
```
Formats a CSV row with the given delimiter, enclosure (the field escape
sequence), and the EOL sequence.

```php
function csv_collection_to_file(array $collection, string $delimiter = ',', string $enclosure = '"', string $eolSequence = "\r\n"): string
```
Formats a collection (an array of arrays) into valid RFC 4180 CSV file.
Indeed it checks that each subarray has the same number of fields as the
previous ones. If not it throws an ``Error``.

```php
function csv_row_to_array(string $row, string $delimiter = ',', string $enclosure = '"', string $eolSequence = "\r\n"): array
```
Returns an array containing the fields provided from the ``$row`` string.
This string should follow RFC 4180.

```php
function csv_file_to_collection(string $file, string $delimiter = ',', string $enclosure = '"', string $eolSequence = "\r\n"): array
```
Returns a collection (an array of arrays) containing the fields of each row
from the string ``$file``. This file should follow RFC 4180.
This function will check that each row has the same number of fields, if not
it will throws an ``Error`` indicating the offending line.

## Future scope

The plan is to propose an RFC and add this extension to the core of PHP with
a timeline on deprecating the non-compliant ``str_getcsv()``, ``fputcsv()``,
and ``fgetcsv()`` functions.

Another reason to deprecate ``fputcsv()``, and ``fgetcsv()`` is that they have
multiple responsibilities.

## Bug reports

To report a bug, please provide a reproducible test script, in preference as a
PHPT test file and open an issue on Gitlab at
https://gitlab.com/Girgias/csv-php-extension/issues

For security issues please email me directly at girgias@php.net
