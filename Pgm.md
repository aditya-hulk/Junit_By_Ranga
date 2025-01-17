# 7
### StringHelper
```java
package com.in28minutes.junit.helper;

public class StringHelper {

	public String truncateAInFirst2Positions(String str) {
		if (str.length() <= 2)
			return str.replaceAll("A", "");

		String first2Chars = str.substring(0, 2);
		String stringMinusFirst2Chars = str.substring(2);

		return first2Chars.replaceAll("A", "") 
				+ stringMinusFirst2Chars;
	}

	public boolean areFirstAndLastTwoCharactersTheSame(String str) {

		if (str.length() <= 1)
			return false;
		if (str.length() == 2)
			return true;

		String first2Chars = str.substring(0, 2);

		String last2Chars = str.substring(str.length() - 2);

		return first2Chars.equals(last2Chars);
	}

}
```
------------
---
# 8
### StringHelperTest
```java
package com.in28minutes.junit.helper;

import static org.junit.Assert.assertEquals;

import org.junit.Test;

public class StringHelperTest {

	@Test
	public void test() {
		StringHelper helper = new StringHelper();
		
		assertEquals("CD", helper.truncateAInFirst2Positions("AACD"));
		assertEquals("CD", helper.truncateAInFirst2Positions("ACD"));
		assertEquals("CDEF", helper.truncateAInFirst2Positions("CDEF"));
		assertEquals("CDAA", helper.truncateAInFirst2Positions("CDAA"));		
		
	}
}
```
---
---
# 9
### StringHelperTest
```java
package com.in28minutes.junit.helper;

import static org.junit.Assert.assertEquals;

import org.junit.Test;

public class StringHelperTest {

	StringHelper helper = new StringHelper();

	@Test
	public void testTruncateAInFirst2Positions_AinFirst2Positions() {

		assertEquals("CD", helper.truncateAInFirst2Positions("AACD"));

	}

	@Test
	public void testTruncateAInFirst2Positions_AinFirstPosition() {

		assertEquals("CD", helper.truncateAInFirst2Positions("ACD"));

	}
}
```
----
----
# 10
### StringHelperTest
```java
package com.in28minutes.junit.helper;

import static org.junit.Assert.assertEquals;
import static org.junit.Assert.assertFalse;
import static org.junit.Assert.assertTrue;

import org.junit.Test;

public class StringHelperTest {

	StringHelper helper = new StringHelper();

	@Test
	public void testTruncateAInFirst2Positions_AinFirst2Positions() {

		assertEquals("CD", helper.truncateAInFirst2Positions("AACD"));

	}

	@Test
	public void testTruncateAInFirst2Positions_AinFirstPosition() {

		assertEquals("CD", helper.truncateAInFirst2Positions("ACD"));

	}
	
	//ABCD ==> false, ABAB ==> true, AB => true, A ==> false
	@Test
	public void testAreFirstAndLastTwoCharactersTheSame_BasicNegativeScenario() {
		
		assertFalse(helper.areFirstAndLastTwoCharactersTheSame("ABCD"));
	}
	
	@Test
	public void testAreFirstAndLastTwoCharactersTheSame_BasicPositiveScenario() {
		
		assertTrue(helper.areFirstAndLastTwoCharactersTheSame("ABAB"));
	}
}
```
--------
-------
# 12
###
```java
package com.in28minutes.junit.helper;

import static org.junit.Assert.*;

import org.junit.After;
import org.junit.Before;
import org.junit.Test;

public class QuickBeforeAfterTest {
	
	//Let's say this is either setting up some test data before executing the test.
	
	@Before
	public void setup() {
		System.out.println("Before Test");
	}

	@Test
	public void test1() {
		System.out.println("test1 executed");
	}

	@Test
	public void test2() {
		System.out.println("test2 executed");
	}
	
	/* Let's say I created a lot of data set up for my test 
	         and I would want to tear down, tear it down after every test.
	 */
	@After
	public void tearDown() {
		System.out.println("After Test");
	}
}
```
---
---
# 13
### QuickBeforeAfterTest
```java
package com.in28minutes.junit.helper;

import org.junit.After;
import org.junit.AfterClass;
import org.junit.Before;
import org.junit.BeforeClass;
import org.junit.Test;

public class QuickBeforeAfterTest {
	

	@BeforeClass
	public static void beforeClass() {
		System.out.println("Before class");
	}
	
	@AfterClass
	public static void afterClass() {
		System.out.println("After class");
	}
	
	@Before
	public void setup() {
		System.out.println("Before Test");
	}

	@Test
	public void test1() {
		System.out.println("test1 executed");
	}

	@Test
	public void test2() {
		System.out.println("test2 executed");
	}

	@After
	public void tearDown() {
		System.out.println("After Test");
	}
}
```
---
---
# 14
### ArraysCompareTest
```java
package com.in28minutes.junit.helper;

import static org.junit.Assert.*;

import java.util.Arrays;

import org.junit.Test;

public class ArraysCompareTest {

	@Test
	public void testArraySort_RandomArray() {
		int[] numbers = { 12, 3, 4, 1 };

		int[] expected = { 1, 3, 4, 12 };

		Arrays.sort(numbers);
		assertArrayEquals(expected, numbers);

	}
}
```
---
---
# 15 & 16
### ArraysCompareTest
```java
package com.in28minutes.junit.helper;

import static org.junit.Assert.*;

import java.util.Arrays;

import org.junit.Test;

public class ArraysCompareTest {

	//15
	@Test
	public void testArraySort_RandomArray() {
		int[] numbers = { 12, 3, 4, 1 };

		int[] expected = { 1, 3, 4, 12 };

		Arrays.sort(numbers);
		assertArrayEquals(expected, numbers);
	}

	@Test(expected = NullPointerException.class)
	public void testArraySort_NullArray() {
		
		int[] numbers = {};
		Arrays.sort(numbers);
	}
	
	
	//16
	@Test(timeout = 100)
	public void testSort_Performance() {
		
		int[] array = {12,23,4};
	
		for(int i=1; i<=1000000;i++) {
			
			array[0] = i; 
			Arrays.sort(array);
			
		}
	}
}
```
---
---
# 17
### StringHelperParameterizedTest
```java
package com.in28minutes.junit.helper;

import static org.junit.Assert.assertEquals;

import java.util.Arrays;
import java.util.Collection;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Parameterized;
import org.junit.runners.Parameterized.Parameters;
//1)	We need to say this class runs parameterized test
@RunWith(Parameterized.class)
public class StringHelperParameterizedTest {
	StringHelper helper = new StringHelper() ;	
	//3.
	private String input;
	private String expectedOutput;

	public StringHelperParameterizedTest(String input, String expectedOutput) {	
		this.input = input;
		this.expectedOutput = expectedOutput;
	}
	//2.
	//yaha se parameter milenge... 
	@Parameters
	public static Collection<String[]> testCondition(){
		String expectedOutput [][]={
									{"AACD","CD"},
									{"ACD","CD"}
								};
		//Convert arrray to collection
		return Arrays.asList(expectedOutput);
	}	
	//4	
	@Test
	public void testTruncateAInFirst2Positions_AinFirst2Positions() {

		assertEquals(expectedOutput, helper.truncateAInFirst2Positions(input));
	}	
}
```
---
---
