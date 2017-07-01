---
title: 'Boost Unit Test Framework in UVa Online Judge'
date: "2013-03-27 08:07:00"
comments: true
categories: 
---


利用 Boost Unit Test Framework，可以方便的進行單元測試。
而在 UVa Online Judge 的練習中，我們也可以導入 Boost Unit Test Framework 來對我們寫的 function 進行測試。
不過 UVa Online Judge 的編譯環境是不支援 Boost 的，但在編譯時，它會給一個特別的編譯參數 -DONLINE_JUDGE。
所以我們可以利用Uva 這個特有的編譯參數，在導入 Boost Unit Test Framework 時，又不會發生Compiler Error.


單元測試時：
``` bash
$ g++ 530.cpp -lboost_unit_test_framework
$ ./a.out 
Running 2 test cases...

*** No errors detected
``` 

以測資做為輸入的測試：
``` bash
$ g++ 530.cpp -DONLINE_JUDGE
$ ./a.out <input.txt
6
252
13983816
``` 

程式碼：
``` cpp
//============================================================================
// Name        : 530.cpp
// Author      :
// Version     :
// Copyright   : copyright notice
//============================================================================

#include <iostream>
#include <cstdlib>
#include <string>
using namespace std;

#ifndef ONLINE_JUDGE
#define BOOST_TEST_DYN_LINK
#define BOOST_TEST_MODULE acm
#include <boost/test/unit_test.hpp>
#endif

long long combinations(long long int n, long long int k) {
	long long int ans = 1;
	if (k > n - k) {
		k = n - k;
	}

	for (long long int idx = 1; idx <= k; idx++) {
		ans *= (n - idx + 1);
		ans = ans / idx;
	}
	return ans;
}

#ifdef ONLINE_JUDGE
int main() {
	long long int n, k;
	while (cin >> n >> k) {
		if (n == 0 && k == 0) {
			break;
		}

		cout << combinations(n, k) << endl;
	}
	return 0;
}
#else
BOOST_AUTO_TEST_SUITE(test)

BOOST_AUTO_TEST_CASE(testSmall) {
	BOOST_CHECK(combinations(0, 0) == 1);
	BOOST_CHECK(combinations(2, 2) == 1);
	BOOST_CHECK(combinations(2, 1) == 2);
	BOOST_CHECK(combinations(4, 2) == 6);
	BOOST_CHECK(combinations(6, 3) == 20);
	BOOST_CHECK(combinations(10, 5) == 252);
}

BOOST_AUTO_TEST_CASE(testLarge) {
	BOOST_CHECK(combinations(49, 6) == 13983816);
}

BOOST_AUTO_TEST_SUITE_END()
#endif
```
