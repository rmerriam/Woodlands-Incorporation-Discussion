# Trace - Header Only Logging Using IOStreams #

### Table of Contents

[TOC]

Trace developed over a number of years to meet my, perhaps idiosyncratic, needs for debugging C++. The requirements were never formally stated but some of them are:

1. Act like iostreams using the *operator<<*,
2. Use the *iomanip* capability for formatting, 
3. Provide a time stamp that is CSV for importing to spreadsheet

The original version was a collection of function calls. This evolved to the class Trace that handled plain old data (POD) and anything that iostream could handle. In 2020 the need to handle some standard library (STD) classes, e.g., std::array, led to a deep dive into some nooks and crannies of C++17. I'd stagnated a bit after C++14 and started to learn more about C++17 and C++20 during 2019 and 2020. What really motivated the change was the ability to do run-time polymorphism with lambdas. 

The only compiler used is GCC. Current version is GCC 11 but tests using online compilers indicate compilation with versions after GCC 9 and Clang 10. If *-pendantic* is set some warnings are generated compiling with C++17 specified. These compilers unofficially supported some C++20 template capabilities. 

*Trace* is not designed be lightweight or efficient. It is just meant to provide logging output. 

## How to Use

Include the header file *Trace.h*. If you use the repository file structure I typically set up an include path to the directory *trace/inc* which load the header. The trace capability is in the namespace *mys*.

#### Trace Streams

Basically use it the same as iostreams except use the four Trace streams: 

- *mys::terr* - outputs to *std::cerr*. Prefix character is 'E'.
- *mys::tout* - outputs to *std::cout*. Prefix character is 'O'.
- *mys::tlog* - outputs to *std::clog*.  Prefix character is 'L'.
- *mys::ttmp* - output to *std::cout*.  Prefix character is 'T'.
  - This is used to insert temporary output when debugging. It is provided so a global search can easily find all occurrences for removal. 

There is no priority to these output streams. Each operates separately. Output may be intermixed from the streams per the C++ specification. See the [details](https://en.cppreference.com/w/cpp/io) for each stream. 

#### Output Format

Each output trace statement begins with one of the trace streams.

```cpp
mys::terr << "hello world";
```

which generates:

```cpp
E,210802,162852,435: hello world
```

The prefix character is the first character output on each line to identify the type of trace stream. Next is a time stamp in the form of:

```cpp
YYMMDD,HHMMSS,MS:<sp>
```

As mentioned above the time stamp is separated by commas to allow loading output into a spreadsheet. A new line is sent for every statement.

#### Multi-Threading

*Trace* uses an *std::osyncstream* to avoid breaking lines of output apart. As a new line is started the previous line is flushed to the underlying output stream. Users can call *Trace::flush()* to accomplish this, also. One example would be at the end of a function containing *Trace* statements to keep all those outputs relatively in one place.

#### Using iomanip

The *std::iomanip* and their underlying methods are usable with trace streams. Not all have been tested. Note that the *Trace* constructor sets up for consistency the output stream with:

```cpp
mOs << std::boolalpha << std::fixed << std::setprecision(3);
```

This can be overridden by the user in *main()*.

##### *std::setw()*

This *iomanip* is a challenge. It only holds for the *<<* immediately to its right. The width then resets to default. In trace stream *std::setw* is made sticky. It holds until the next invocation of it or the end of a statement. 

Note that using *iomanip* affects the underlying stream, also. So setting *mys::tout* to *std::hex* also changes *std::cout*. *Trace* resets some manipulators to default but may not do all. 

#### Creating a Trace Stream

Users can create their own trace stream by invoking the *Trace* constructor:

```cpp
mys::Trace tstrm { std::stringstream, 'S' };
```

This stream is used during unit tests to capture trace output as a string for comparison with the desired output. The constructor takes a stream and a prefix character as inputs. 

#### Turning Trace On and Off

Two utility class are provided: *TraceOn* and *TraceOff*. As their names imply they enable or disable trace output. A typical usage is:

```c++
void func A() {
    mys::TraceOff t_ctrl{mys::tout};
    msy::tout << ...
}
```

In the above, tracing to *mys::tout* will be disabled until the end of the function. The previous state  will be restated when the function exits when the destructor for *TraceOff* is invoked. By default tracing is enabled but can be disabled as needed. 

#### Useful Character Symbols

There are a few characters provided for use. Mainly I find typing the quote marks in  *'\n'* awkward so created this substitutes even though they require more characters. 

```c++
namespace mys {
    constexpr char tab { '\t' };
    constexpr char nl { '\n' };
    constexpr char sp { ' ' };
    constexpr char comma[] { ", " };
}
```

#### Helpful Defines

As much as I dislike using defines there are a few defined to add information 

```cpp
#define code_line __FUNCTION__ << mys::sp << std::dec << __LINE__ << mys::tab
#define code_entry __FUNCTION__ << " entry" << mys::tab
#define code_exit __FUNCTION__ << " exit" << mys::tab
#define code_return __FUNCTION__ << " return" << mys::tab
```

They are not in the namespace so the *mys* prefix is not required. They may be replaced in the future by standardized capabilities. 

## Example Output

The following is example output to *mys::tout* as indicated by the prefix character of **O** .

```cpp
// boolean false and trueO,210803,131937,096: falseO,210803,131937,096: true// char 'A' and 0x00O,210803,131937,096: AO,210803,131937,096: 0// uint8_t as hexO,210803,131937,096: 0x42// int16_t as decO,210803,131937,096: 1234// uint16_t as hexO,210803,131937,096: 0x1234// floatO,210803,131937,096: 12.340// doubleO,210803,131937,096: 12.340// char*O,210803,131937,096: Hello World// char[]O,210803,131937,096: Hello World// uint8_t[] as hexO,210803,131937,096:  0x40 0x41 0x42 0x43// std::array charO,210803,131937,096: ABCDE// std::array char as hexO,210803,131937,096:  0x51 0x52 0x48 0x17 0x23// std::array unsigned int as hexO,210803,131937,096:  0xdead  0xfeed  0xceed   0xcab   0xbad// std::array int (INT_MAX, INT_MIN, 1, 0, -1)O,210803,131937,096:  2147483647 -2147483648           1           0          -1// std::stringO,210803,131937,096: Hello World Test// std::string_base with unsigned char as hexO,210803,131937,096: 0x20  0x21// std::vector with intsO,210803,131937,096:  32 33
```



## Implementation Details

There are four classes in *Trace*:

1. *explicit TraceBase(std::ostream& os, char const ch);*
   - The constructor is protected so users cannot directly create this class
2. *Trace(std::ostream& os, char const ch);*
   - *Trace* is derived from *TraceBase*: *class Trace : protected TraceBase...*
3. Classes *TraceOn* and *TraceOff*.

*Trace* begins a trace statement. It outputs the prefix character and the time stamp. The remainder of the statement is processed by *TraceBase*.

