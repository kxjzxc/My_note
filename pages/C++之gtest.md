tags:: #C++

- # 介绍
	- Google C++单元测试框架（简称Gtest），可在多个平台上使用（包括Linux, Mac OS X, Windows, Cygwin和Symbian），它提供了丰富的断言、致命和非致命失败判断，能进行值参数化测试、类型参数化测试、“死亡测试”。
- # 用法
	- ## 宏
		- ## `TEST(TestSuiteName, TestName)`
			- 用于组织不同场景的cases
			- 案例
				- ```cpp
				  // 下面三个 TEST 都是属于同一个 test suite，即 FactorialTest
				  // 正数为一组
				  TEST(FactorialTest, Negative) {
				    EXPECT_EQ(1, Factorial(-5));
				    EXPECT_EQ(1, Factorial(-1));
				    EXPECT_GT(Factorial(-10), 0);
				  }
				  // 0
				  TEST(FactorialTest, Zero) {
				    EXPECT_EQ(1, Factorial(0));
				  }
				  // 负数为一组
				  TEST(FactorialTest, Positive) {
				    EXPECT_EQ(1, Factorial(1));
				    EXPECT_EQ(2, Factorial(2));
				    EXPECT_EQ(6, Factorial(3));
				    EXPECT_EQ(40320, Factorial(8));
				  }
				  
				  ```
			- 在main函数中，添加RUN_ALL_TESTS函数即可
				- ```cpp
				  int main(int argc, char **argv) {
				    printf("Running main() from %s\n", __FILE__);
				    testing::InitGoogleTest(&argc, argv);
				    return RUN_ALL_TESTS();   
				  }
				  ```
		- ## `TEST_P(TestFixtureName, TestName)`
			- ```cpp
			  TEST_P(MyTestSuite, DoesSomething) {
			    ...
			    EXPECT_TRUE(DoSomething(GetParam()));
			    ...
			  }
			  ```
			-