---
title: 'Valgrind - 檢查程式記憶體的小工具'
date: "2012-12-17 04:46:00"
comments: true
categories: 
---


Octopress 的第一篇文章，簡單介紹 Valgrind - 檢查程式記憶體的小工具

前陣子我對 project 進行 Debug
其中有一些 runtime error, 包含 memory leak

我使用 Valgrind 來檢查 Memory Leak



小範例，由 Valgrind 找出 test.cpp 第8行的 Bug  ( Invalid read )

{% codeblock lang:cpp %}
#include <iostream>
#include <vector>
using namespace std ;

int main()
{
    vector<double> array(1024);
    cout << array[1024] << endl ;
    return 0;
}
{% endcodeblock %}

$g++ -g test.cpp
$valgrind ./a.out


輸出訊息
{% codeblock %}
==9247== Memcheck, a memory error detector
==9247== Copyright (C) 2002-2011, and GNU GPL'd, by Julian Seward et al.
==9247== Using Valgrind-3.7.0 and LibVEX; rerun with -h for copyright info
==9247== Command: ./a.out
==9247==
==9247== Invalid read of size 8
==9247==    at 0x80487C4: main (test.cpp:8)
==9247==  Address 0x4336028 is 0 bytes after a block of size 8,192 alloc'd
==9247==    at 0x402B9B4: operator new(unsigned int) (in /usr/lib/valgrind/vgpreload_memcheck-x86-linux.so)
==9247==    by 0x8048BD1: __gnu_cxx::new_allocator<double>::allocate(unsigned int, void const*) (new_allocator.h:92)
==9247==    by 0x8048B1D: std::_Vector_base<double, std::allocator<double> >::_M_allocate(unsigned int) (in /home/stanleyhsiao/a.out)
==9247==    by 0x80489BC: std::_Vector_base<double, std::allocator<double> >::_Vector_base(unsigned int, std::allocator<double> const&) (stl_vector.h:123)
==9247==    by 0x80488D1: std::vector<double, std::allocator<double> >::vector(unsigned int, double const&, std::allocator<double> const&) (stl_vector.h:265)
==9247==    by 0x80487A3: main (test.cpp:7)
==9247==
0
==9247==
==9247== HEAP SUMMARY:
==9247==     in use at exit: 0 bytes in 0 blocks
==9247==   total heap usage: 1 allocs, 1 frees, 8,192 bytes allocated
==9247==
==9247== All heap blocks were freed -- no leaks are possible
==9247==
==9247== For counts of detected and suppressed errors, rerun with: -v
==9247== ERROR SUMMARY: 1 errors from 1 contexts (suppressed: 0 from 0)
{% endcodeblock %}

