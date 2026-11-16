# CPP09

A set of three C++98 exercises focused on associative containers, stack-based expression evaluation, and sorting with different sequence containers. Each exercise builds independently from its own directory; there is no top-level Makefile.

## Exercises

| Directory | Program | Main idea |
| --- | --- | --- |
| ex00/ | btc | Look up Bitcoin exchange rates by date and convert values from an input file. |
| ex01/ | RPN | Evaluate a whitespace-separated Reverse Polish Notation expression with a stack. |
| ex02/ | PmergeMe | Sort positive integers with a Ford–Johnson-style merge-insertion algorithm using std::vector and std::deque. |

## Requirements

- make
- A C++ compiler with C++98 support

Each exercise Makefile uses c++ -Wall -Wextra -Werror -std=c++98.

## Build

Build each program from its own folder:

~~~sh
cd ex00 && make
cd ../ex01 && make
cd ../ex02 && make
~~~

Each exercise supports the standard targets all, clean, fclean, and re.

## ex00 — Bitcoin exchange

Build and run from ex00/:

~~~sh
make
./btc input.txt
~~~

The program reads its reference exchange-rate database from data.csv in the current working directory and reads requested date/value rows from the file passed as its argument.

The reference database is a comma-separated file with a header and rows in date,exchange_rate form. The input file uses a header followed by rows in date | value form. For each input value, the program finds the rate for that date or the closest available earlier date, then prints the converted amount. Values below zero or above 1,000 are rejected.

## ex01 — Reverse Polish Notation

Pass one quoted expression as the program argument. Separate every number and operator with whitespace:

~~~sh
make
./RPN "8 9 * 9 - 9 - 9 - 4 - 1 +"
~~~

The expression is evaluated from left to right using a stack; each operator consumes the previous two values. Supported operators are +, -, *, and /. Division is integer division, division by zero is rejected, and the expression must leave exactly one result on the stack.

## ex02 — PmergeMe

Pass a sequence of distinct positive integers as separate arguments:

~~~sh
make
./PmergeMe 3 5 9 7 4
~~~

The program prints the input and sorted sequence, then reports processing time for std::vector and std::deque. The implementation uses a Ford–Johnson merge-insertion strategy with a Jacobsthal-guided insertion order. Inputs must be positive, within the range of int, and unique.

## Project layout

~~~text
.
├── ex00/
│   ├── BitcoinExchange.cpp
│   ├── BitcoinExchange.hpp
│   ├── main.cpp
│   └── Makefile
├── ex01/
│   ├── RPN.cpp
│   ├── RPN.hpp
│   ├── main.cpp
│   └── Makefile
└── ex02/
    ├── PmergeMe.cpp
    ├── PmergeMe.hpp
    ├── main.cpp
    └── Makefile
~~~

## Clean generated files

Run from an exercise directory:

~~~sh
make clean   # remove object files
make fclean  # remove object files and executable
make re      # clean and rebuild
~~~
