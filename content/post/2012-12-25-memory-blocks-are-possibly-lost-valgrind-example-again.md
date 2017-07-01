---
title: 'Memory blocks are possibly lost (Valgrind example again!!)'
date: "2012-12-25 01:47:00"
comments: true
categories: 
---


今天讀到的文章 [Using Valgrind to debug memory leaks](http://www.linuxprogrammingblog.com/using-valgrind-to-debug-memory-leaks)
{% codeblock lang:c %}
#include <stdio.h>
#include <string.h>
#include <ctype.h>
 
char *lower;
 
char *to_lower (const char *str)
{
	char *l = strdup (str);
	char *c;
 
	for (c = l; *c; c++) {
		if (isupper(*c))
			*c = tolower(*c);
	}
 
	return l;
}
 
int main (int argc, char *argv[])
{
	lower = to_lower (argv[1]);
 
	while (*lower)
		putchar (*(lower++));
	puts ("");
 
	return 0;
}
{% endcodeblock %}

輸出訊息
{% codeblock %}
==28578== 5 bytes in 1 blocks are possibly lost in loss record 1 of 1
==28578==    at 0x4025D2E: malloc (vg_replace_malloc.c:207)
==28578==    by 0x40D805F: strdup (in /lib/tls/i686/cmov/libc-2.8.90.so)
==28578==    by 0x8048504: to_lower (test2.c:9)
==28578==    by 0x804857F: main (test2.c:22)
{% endcodeblock %}

This time memory is possibly lost. Why it's not sure? Because at the program exit time we didn't completely lost the pointer to the allocated memory, we've only advanced it to print the lower string in a funny way. It's theoretically possible that we have a variable, a counter that tells us how much we've advanced, so we could compute the pointer to the memory to free it.



文章還提到了 Valgrind In practice. 很值得一看

At the beginning of using Valgrind to debug my programs I used to think this way: It's just an automatic, dumb tool that tracks memory allocations and can be wrong. I looked at the code and there can be no memory leak at this point, it's one of the cases when Valgrind is wrong.. But I was wrong! After years of using it I can see that 99,9% of it's messages are right but it's often hard to see it in the code.

One real world case was when I was writing a multi-threaded program that used libmysqlclient library and valgrind showed memory leaks in mysql_real_connect()/mysql_init(). It's clear from documentation that the memory allocated by the library when using those functions should be freed by mysql_close(). From the code it was clear that I do it properly: every created connection was closed. I even added a counter to the places when I create connection and destroy it and saw all connections were destroyed. I started to think that there is a memory leak in the libmysqlclient_r library (a thread-safe version) but when I separated the code (wrote a simple program that allocates conenctions and free them) Valgrind showed no errors. So there are no leaks in the library. If I had less believe in Valgrind I would give up at this moment, but I knew it's right. As I found out there is a special requirement by libmysqlclient_r, I just didn't read the documentation. If you are creating MYSQL objects in different threads the library automatically allocates per-thread global data, but to free them you must use mysql_thread_end(). It's not done 


