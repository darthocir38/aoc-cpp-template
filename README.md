# Advent Of Code C++ Template

This is a template for C++ solutions to the [Advent of Code](https://adventofcode.com/) challenges.

It uses CMake to retrieve the inputs, generate unit tests and sources for each day. 

Each input is turned into a string_view inside an array of string_views, so that the input is available at compile time, one item for each day.

Unit tests are already setup for the 25 days of the advent calendar, and can be run with `ctest` or with a provided CLI.

## Requirements

- CMake > 3.20
- C++20 compiler

## Usage

### Setup

First you will need to retrieve your session cookie from the adventofcode website. It will allow to get your inputs automatically.

To do so, open the developer console of your browser, go to the network tab, and reload the page. Look for the request to `input` and copy the value of the `cookie` header.

Then, create a file named `.session` at the root of the project and paste the cookie value in it.

### Generate a new day

To generate a new day, run the following command:

```bash
cmake -D DAY=1 -P generate_day.cmake
```

This will take care of reading your input for the day, put it in a text file, and generate the sources for the day. 

The source files are put in the `src/problems` directory, and the input files in the `inputs` directory. You can access the input from the class using the `input_data` member.

Just fill out the `solve` method of the day class, it should return a value for each part of the day.

You can also fill the constructor of the day class with the test data and the expected results for each part. It will be used by unit tests to validate your solution.

Any change to the file structure will be picked up by CMake and retrigger a configure so everything is up to date.

### Build

To build the project, run the following commands:

```bash
cmake --build build --target adventofcode
```

You can then run the executable with the following command:

```bash
./build/adventofcode [--day <number>] [--alldays] [--part 1|2] [--help]
```

### Run tests

To run the tests, you must build the test target first:

```bash
cmake --build build --target solution_check
```

Then you can run the tests with the following command:

```bash
./build/solution_check [--day <number>] [--alldays] [--part 1|2] [--help]
```

Or you can use your IDE's test runner to run the tests, they should be registered automatically. There's a test for each part of each day.