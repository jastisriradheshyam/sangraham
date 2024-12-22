+++
title = 'AWK'
date = 2024-12-15T03:57:09+05:30
draft = false
+++

- intended for simple data processing and analysis:
    - selection, validation
        - "print all lines longer than 80 characters"
        - `length > 80`
    - transforming, rearranging
        - "Replace the 2nd field by its logarithm"
        - `{ $2 = log($2); print }`
    - report generation
        - "Add up numbers in first field, print sum and average"
        - ```text
                { sum += $1}
            END { print sum, sum/NR }
          ```

## structure of an awk program
- A program is a sequence of pattern-action statements
    ```text
    pattern {action}
    pattern {action}
    ...
    ```
- A pattern is a regular expression, numeric expression, string expression or combination
- An action is executable code, similar to C
- usage:
    `awk 'program' [ file1 file2 ...]`
    `awk -f progfile [ file1 file2 ... ]`
- operation
    ```text
    for each file
        for each input line
            for each pattern
                if pattern matches input line
                    do the action
    ```

## awk features for 1-liners
- input is read automatically across multiple files
    - lines are split into fields ($1,...,$NF; $0 for whole line)
- variables contain string or numeric values (or both)
    - no declarations: type determined by context and use
    - initialized to 0 and empty string
    - built-in variables for frequently-used values
- operators work on strings or numbers
    - coerce type / value according to context
- associative arrays (arbitrary subscripts)
- regular expressions (like egrep)
- control flow statements similar to C: if-else, while, for, do
- useful built-in functions
    - arithmetic, string, regular expression, text edit, ...

## Associative Arrays
- array subscripts can have any value, not just integers
- canonical example: adding up name-value pairs

- input:
    ```text
    pizza 200
    beer 100
    pizza 500
    beer 50
    ```

- output:
    ```text
    pizza 700
    beer 150
    ```

- program
    ```text
    { amount[$1] += $2 }
    END { for (name in amount)
        print name,amount[name] | "sort -k1 -nr"
    }
    ```

# References:

1. [Computer Science - Brian Kernighan on successful language design - YouTube](https://www.youtube.com/watch?v=Sg4U4r_AgJU)
