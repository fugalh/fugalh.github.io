# Reduce compilation time with template magic.

It is a common belief that templates must be implemented in header files, a lamentable situation that greatly increases build times because those full-blown headers must be compiled every time they are included. It also makes the headers less useful as brief documentation, which one of the things about headers that is actually good.

But that is not strictly true. You can separate template declarations and implementations. With a simple pattern and just a little thought, you can compile your template code once and link it just like you do regular objects or functions.

Let us begin with a function `foo` which just prints the `T` it was given to `cout`. Here is the header:

    // foo.h
    #pragma once

    template <class T> void foo(T);

Now let's try to use it:

    // a.cc
    #include "foo.h"

    int main(void) {
        foo(42);
        return 0;
    }

And compile:

    $ c++ -std=c++11 -c a.cc
    $ c++ a.o
    Undefined symbols for architecture x86_64:
      "void foo<int>(int)", referenced from:
          _main in a.o
    ld: symbol(s) not found for architecture x86_64
    collect2: error: ld returned 1 exit status

The object file compiles fine, but linking fails because `void foo<int>(int)` is undefined. So, let's define it:

    // foo-tmpl.h
    #pragma once
    
    #include "foo.h"
    #include <iostream>
    
    template <class T> void foo(T t)
    {
        std::cout << t << std::endl;
    }

Now if we change `a.cc` to include `foo-tmpl.h` instead of `foo.h`, the implicit instantiation will work fine. But instead, let's explicitly instantiate the `int` specialization in `foo.cc`, because we believe everyone and their dog will want the `int` specialization, and we want to save compile time:

    // foo.cc
    #include "foo-tmpl.h"
    
    template <int> foo(int);

And compile:
    
    $ c++ -std=c++11 -c a.cc
    $ c++ -std=c++11 -c foo.cc
    $ c++ a.o foo.o
    $ ./a.out
    42

Success!

Ok, but what about implicitly instantiating templates? We don't want to give up this unique power of templates. We can do it. This is why I put the implementation of `foo` in `foo-tmpl.h` instead of `foo.cc`. When we need to instantiate, we include the `-tmpl.h` instead of the `.h`. We should try to avoid doing this in other headers, and prefer to do it (once) in an implementation file. To demonstrate let's introduce a new function `bar`:

    // bar.h
    #pragma once
    
    void bar();

And its implementation:

    // bar.cc
    #include "bar.h"
    #include "foo-tmpl.h"
    
    void bar()
    {
        foo("bar");
    }

Now we are implicitly instantiating `void foo<const char*>(const char*)`, but that's ok because we included `foo-tmpl.h`. Now we can use `bar`:

    // b.cc
    #include "bar.h"

    int main(void) {
        bar();
        return 0;
    }

Compile and run:

    $ c++ -std=c++11 -c b.cc
    $ c++ -std=c++11 -c bar.cc
    $ c++ b.o bar.o
    $ ./a.out
    bar

And finally, let's use them together

    // c.cc
    #include "foo.h"
    #include "bar.h"

    int main(void) {
        foo(42);
        bar();
        return 0;
    }

Compile and run:

    $ c++ -std=c++11 -c c.cc
    $ c++ c.o foo.o bar.o
    $ ./a.out 
    42
    bar

Just to make sure we understand what's going on under the covers, let's look at the symbols with `nm`, and make sure things are defined where we expect them to be:

    $ nm *.o | c++filt  # manually-filtered output follows
    a.o:
                     U void foo<int>(int)
    
    b.o:
                     U bar()
    
    c.o:
                     U bar()
                     U void foo<int>(int)
    
    foo.o:
    0000000000000000 T void foo<int>(int)
    
    bar.o:
    0000000000000000 T bar()
    0000000000000075 S void foo<char const*>(char const*)

I performed these explorations with gcc 4.8.

    $ c++ --version
    c++ (MacPorts gcc48 4.8-20130210_0) 4.8.0 20130210 (experimental)
    Copyright (C) 2013 Free Software Foundation, Inc.
    This is free software; see the source for copying conditions.  There is NO
    warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

With C++11 you also have `extern template` at your disposal, which lets you avoid implicit instantiation. So if you have many files which instantiate the `MyClass` specialization, and don't want `foo.cc` to even be aware of `MyClass`, you can add this to `MyClass.h`:

    // MyClass.h
    #include "foo.h"
    class MyClass {
        //...
    };

    extern template void foo<MyClass>(MyClass);

And then `MyClass.cc` looks something like this:

    // MyClass.cc
    #include "MyClass.h"
    #include "foo-tmpl.h"
    
    // explicitly instantiate templates
    template void foo<MyClass>(MyClass);
    
    MyClass::MyClass() {
        // ...
    }
    
    // ...

Now the `MyClass` instantiation of `foo` will only be compiled once in `MyClass.cc`, but can be used in umpteen other files.
