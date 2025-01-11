+++
title = 'Grep'
date = 2024-12-19T19:27:46+05:30
draft = false
description = "Information on Grep command"
+++

- line with the word or phrase: `cat some_file | grep "word_or_phrase"`
- line without the word or the phrase: `cat some_file | grep -v "word_or_phrase"`
- output N lines (here 10 lines) after matching word or prase: `grep -A10 word_or_prase`

- Search work in a directory: `grep -r "SEARCH_TERM" DIRECTORY_PATH`
