# Bikram Sambat

[![npm version](https://badge.fury.io/js/%40nakarmi23%2Fbikram-sambat.svg)](https://badge.fury.io/js/%40nakarmi23%2Fbikram-sambat)
[![Jest](https://img.shields.io/badge/tested_with-jest-99424f.svg)](https://github.com/facebook/jest)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/facebook/jest)

> FIX: Fixed a major issue related to importing the package in CommonJS.

## Introduction

The Bikram Sambat library is a utility for working with Nepali (Bikram Sambat) Dates, allowing conversion between AD dates and BS dates. It supports robust parsing, formatting, manipulation, and comparison of BS dates, covering years from 1970 to 2111.

## Table of Contents

1. [Installation](#installation)
2. [Example](#example)
3. [Methods](#methods)
   - [Static Methods](#static-methods)
   - [Instance Methods](#instance-methods)

## Installation

### Package Manager

Using npm:

```bash
npm install @nakarmi23/bikram-sambat
```

Using yarn:

```bash
yarn add @nakarmi23/bikram-sambat
```

Using pnpm:

```bash
pnpm add @nakarmi23/bikram-sambat
```

Once the package is installed, you can import the library using `import` or `require` approach:

```typescript
import BikramSambat from '@nakarmi23/bikram-sambat';
```

or

```typescript
const BikramSambat = require('@nakarmi23/bikram-sambat').default;
```

## Example

```typescript
import BikramSambat from '@nakarmi23/bikram-sambat';

console.log(BikramSambat.now());
/**
 * OUTPUT:
 * {
 *  bsYear: 2081
 *  bsMonth: 3
 *  bsDay: 14
 *  weekDay: 5
 *  adDate: Javascript Date Instance
 *  bsMonthName: 'Ashadh'
 * }
 **/

console.log(BikramSambat.fromAD('2021-06-28'));
/**
 * OUTPUT:
 * {
 *  bsYear: 2081
 *  bsMonth: 3
 *  bsDay: 14
 *  weekDay: 5
 *  adDate: Javascript Date Instance
 *  bsMonthName: 'Ashadh'
 * }
 **/

console.log(BikramSambat.parse('2081-03-14'));
/**
 * OUTPUT:
 * {
 *  bsYear: 2081
 *  bsMonth: 3
 *  bsDay: 14
 *  weekDay: 5
 *  adDate: Javascript Date Instance
 *  bsMonthName: 'Ashadh'
 * }
 **/
```

## Methods

### Static Methods

#### .now() -> instance of BikramSambat

Returns an instance of BikramSambat for today's date.

- Returns: instance of BikramSambat
- Example:

  ```typescript
  const bsDate = BikramSambat.now();
  console.log(bsDate);
  ```

#### .parse(bsDate) -> instance of BikramSambat

Parses and validates the given BS date and returns an instance of BikramSambat for that date. BS Year must be between 1970 and 2111.

- Parameters:
  - `bsDate` (string): BS Date string to be parsed. Valid pattern: YYYY-MM-DD.
- Returns: instance of BikramSambat
- Example:

  ```typescript
  const bsDate = BikramSambat.parse('2081-03-14');
  console.log(bsDate);
  ```

#### .fromAD(adDate) -> instance of BikramSambat

Parses and validates the give AD date and returns an instance of BikramSambat for that date.

- Parameters:
  - `adDate` (string | Date): AD Date to be converted. Accepts string in 'YYYY-MM-DD' format or JavaScript Date object.
- Returns: instance of BikramSambat
- Example:

  ```typescript
  const bsDate = BikramSambat.fromAD('2021-06-28');
  console.log(bsDate);
  ```

#### .getBikramSambatMonths(bsYear) -> {month, monthName, numberOfDays}[]

Returns the list of BS months and also returns the number of days for th month according to the year provided.

- Parameters:
  - `bsYear` (number): BS Year. Must be between 1970 and 2111.
- Returns: Array of objects containing month, monthName, and numberOfDays
- Example:

  ```typescript
  const months = BikramSambat.getBikramSambatMonths(2081);
  console.log(months);
  ```

### Instance Methods

#### .clone() -> instance of BikramSambat

Creates a new instance of BikramSambat with the same values.

- Returns: instance of BikramSambat
- Example:

  ```typescript
  const bsDate = BikramSambat.parse('2081-03-14');
  const clonedDate = bsDate.clone();
  console.log(clonedDate);
  ```

#### .format(formatString) -> string

Get the formatted date according to the string of tokens passed in.

- Parameters:
  - `formatString` (string): String of tokens for formatting the date.
- Returns: string
- Example:

  ```typescript
  const bsDate = BikramSambat.parse('2081-03-14');
  console.log(bsDate.format('YYYY MMMM DD')); // 2081 Ashadh 14
  ```

##### List of all available formats

| Format | Output             | Description                           |
| ------ | ------------------ | ------------------------------------- |
| YYYY   | 2081               | Four-digit year                       |
| MMMM   | Baishakh - Chaitra | The BS full month name                |
| MM     | 01-12              | The month, 2-digits                   |
| M      | 1-12               | The month, beginning at 1             |
| DD     | 01-31              | The day of the month, 2-digit         |
| D      | 1-31               | The day of the month                  |
| dddd   | Sunday-Saturday    | The name of the day of the week       |
| ddd    | Sun-Sat            | The short name of the day of the week |
| dd     | Su-Sa              | The min name of the day of the week   |
| d      | 0-6                | The day of the week, with Sunday as 0 |

#### .startOf(unit) -> instance of BikramSambat

Returns a cloned BikramSambat object and set it to the start of a unit of time.

- Parameters:
  - `unit` (string): Unit of time. Valid values are year and month.
- Returns: instance of BikramSambat
- Example:

  ```typescript
  const bsDate = BikramSambat.parse('2081-03-14');
  console.log(bsDate.startOf('year')); // 2081-01-01
  ```

##### List of all available units

| Unit  | Description                 |
| ----- | --------------------------- |
| year  | Baishakh 1st                |
| month | The first day of this month |

#### .endOf(unit) -> instance of BikramSambat

Returns a cloned BikramSambat object and set it to the end of a unit of time.

Returns a cloned BikramSambat object and set it to the end of a unit of time.

- Parameters:
  - `unit` (string): Unit of time. Valid values are year and month.
- Returns: instance of BikramSambat
- Example:

  ```typescript
  const bsDate = BikramSambat.parse('2081-03-14');
  console.log(bsDate.endOf('month')); // 2081-03-31
  ```

##### List of all available units

| Unit  | Description                 |
| ----- | --------------------------- |
| year  | Baishakh 1st                |
| month | The first day of this month |

#### .add(value, unit) -> instance of BikramSambat

Returns a cloned BikramSambat object with a specified amount of time added.

- Parameters:
  - `value` (number): Amount of time to add.
  - `unit` (string): Unit of time. Valid values are year, month, and day.
- Returns: instance of BikramSambat
- Example:

  ```typescript
  const bsDate = BikramSambat.parse('2081-03-14');
  console.log(bsDate.add(1, 'month')); // 2081-04-14
  ```

##### List of all available units

| Unit  | Description |
| ----- | ----------- |
| year  | Year        |
| month | Month       |
| day   | Day         |

#### .sub(value, unit) -> instance of BikramSambat

Returns a cloned BikramSambat object with a specified amount of time subtracted.

- Parameters:
  - `value` (number): Amount of time to subtract.
  - `unit` (string): Unit of time. Valid values are year, month, and day.
- Returns: instance of BikramSambat
- Example:

  ```typescript
  const bsDate = BikramSambat.parse('2081-03-14');
  console.log(bsDate.sub(1, 'month')); // 2081-02-14
  ```

##### List of all available units

| Unit  | Description |
| ----- | ----------- |
| year  | Year        |
| month | Month       |
| day   | Day         |

#### .isSame(date, unit) -> boolean

Return true if provided BikramSambat object is the same as the other supplied BikramSambat date.

- Parameters:
  - `date` (BikramSambat): The BikramSambat object to compare against.
  - `unit` (string): Optional. Unit of comparison. Defaults to `day`.
- Returns: boolean
- Example:

  ```typescript
  const bsDate1 = BikramSambat.parse('2081-03-14');
  const bsDate2 = BikramSambat.parse('2081-03-14');
  const bsDate3 = BikramSambat.parse('2081-03-15');

  console.log(bsDate1.isSame(bsDate2)); // true
  console.log(bsDate1.isSame(bsDate3)); // false
  ```

##### List of all available units

| Unit  | Description |
| ----- | ----------- |
| year  | Year        |
| month | Month       |
| day   | Day         |
| week  | Week        |

#### .isBefore(date, unit) -> boolean

Return true if provided BikramSambat object is before the other supplied BikramSambat date.

- Parameters:
  - `date` (BikramSambat): The BikramSambat object to compare against.
  - `unit` (string): Optional. Unit of comparison. Defaults to `day`.
- Returns: boolean
- Example:

  ```typescript
  const bsDate1 = BikramSambat.parse('2081-03-14');
  const bsDate3 = BikramSambat.parse('2081-03-15');

  console.log(bsDate1.isBefore(bsDate3)); // true
  console.log(bsDate3.isBefore(bsDate1)); // false
  ```

##### List of all available units

| Unit  | Description |
| ----- | ----------- |
| year  | Year        |
| month | Month       |
| day   | Day         |
| week  | Week        |

#### .isAfter(date, unit) -> boolean

Return true if provided BikramSambat object is after the other supplied BikramSambat date.

- Parameters:
  - `date` (BikramSambat): The BikramSambat object to compare against.
  - `unit` (string): Optional. Unit of comparison. Defaults to `day`.
- Returns: boolean
- Example:

  ```typescript
  const bsDate1 = BikramSambat.parse('2081-03-14');
  const bsDate3 = BikramSambat.parse('2081-03-15');

  console.log(bsDate1.isAfter(bsDate3)); // false
  console.log(bsDate3.isAfter(bsDate1)); // true
  ```

##### List of all available units

| Unit  | Description |
| ----- | ----------- |
| year  | Year        |
| month | Month       |
| day   | Day         |
| week  | Week        |

#### .toString() -> string

Returns the BikramSambat object as a string.

- Returns: string
- Example:

  ```typescript
  const bsDate = BikramSambat.parse('2081-03-14');
  console.log(bsDate.toString()); // "Ashadh 3 14"
  ```
