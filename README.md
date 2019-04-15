# SYNOPSIS
Functions that make dealing with typical string operations easier.


# USAGE
This module is designed to work with the [`datcxx`][0] build tool. To add this
module to your project us the following command...

```bash
build add heapwolf/cxx-tap
```


# TEST

```bash
build test
```


# FUNCTIONS

```c++
string f = "/test/parallel/test-path.js";
```

### SEARCH
Search a string for regular expression matches, returns a `vector<string>`.

```c++
vector<string> r = Util::String::search(f, "\\w+");
ASSERT("search results == 5", r.size() == 5);
```

### SPLIT
Split on a regular expression.

```c++
vector<string> r = Util::String::split(f, "/");
ASSERT("parts after split == 4", r.size() == 4);
```

### MATCH
If not empty, returns an array of matches starting with the complete input
at index `0`.

```c++
cmatch r = Util::String::match(f, "/(\\w+)/(.*)");
ASSERT("parts after match == 2", r.size() == 3);
```

### TEST
Test if a string is an exact match.

```c++
bool r = Util::String::test(f, "^/(\\w+)/(\\w+)/(\\w+)-path.js$");
ASSERT("test exact", r == true);
```

### TRIM, RTRIM, LTRIM

```c++
string r = Util::String::trim("/foobar//", "/");
ASSERT("parts after split == 4", r.trim() == "foobar");

string r = Util::String::rtrim("!Hello, World!!", "!");
ASSERT("rtrim", r == "!Hello, World");

string r = Util::String::ltrim("!Hello, World!!", "!");
ASSERT("ltrim", r == "Hello, World!!");
```

### REPLACE

```c++
string r = Util::String::replace("Hello, World!", "o", "x");
ASSERT("replaced letters in string", r == "Hellx, Wxrld!");
```

### REPLACE BY TOKEN

```c++
const string s = "Hello, World!";

string r = Util::String::replace_token(s, "l", [&](string const& m, int index) {
  return string("L" + to_string(index));
});

ASSERT("replaced tokens in string", r == "HeL0L1o, WorL2d!");
```

[0]:https://github.com/datcxx/build
