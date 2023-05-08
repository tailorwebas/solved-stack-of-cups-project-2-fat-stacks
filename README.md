Download Link: https://assignmentchef.com/product/solved-stack-of-cups-project-2-fat-stacks
<br>
<h2>Operations out of Order</h2>

All around the world, mathematicians have forgotten the order of operations. No one can explain this plague that has robbed them of one of the most basic tricks in their mathematical arsenal. As a consequence, all the necessary calculations to maintain the march of commerce and further the cause of science will eventually grind to a halt. You must wield your computer wisdom to save us all.

<h2>The Mission</h2>

Your program must perform the following actions:

<ol>

 <li>Read an expression in infix notation</li>

 <li>Print a standardized version of the parsed infix expression</li>

 <li>Convert the expression to postfix and print it out</li>

 <li>Evaluate the postfix expression and print out the answer</li>

</ol>

<h2>Specification</h2>

Your <code>main()</code> method should be in a class called <code>InfixToPostfix</code>. It is expected that you will create additional classes to help manage your stacks and queues.

<h3>Input</h3>

To perform input properly, you will read in operators and operands using <code>Scanner</code>. An infix expression has the following characteristics: It will start and end with an operand. Between each operand is an operator. The exceptions to this rule are parentheses. You will see a left parenthesis <code>'('</code> when you expect to see an operand. After the left parenthesis, you will still expect an operand. You will see a right parenthesis <code>')'</code> when you expect to see an operator. After a right parenthesis, you will still expect to see an operator.

Supported operators include: <code>+</code>, <code>-</code>, <code>*</code>, and <code>/</code>.

If you are a member of the three-person group, you must support <code>%</code> (floating point modulus) as well.

If you are expecting an operand and get something that is not a correctly formatted operand, print <code>Invalid operand</code>. If you are expecting an operator and get something that is not one of the supported operators, print <code>Invalid operator: </code>followed by the symbol in question.

It is highly recommended that you store each operator and operand in an appropriate object. One possibility is that you create two separate classes, <code>Operator</code> and <code>Operand</code> designed to hold each. They may both be subclasses of a <code>Term</code> superclass or interface. Alternatively, you could create a single <code>Term</code>class capable of holding either an operator or an operand. You will want to read the entire input into a queue that will allow you to review each token of input in order. For output purposes, supporting iteration on the queue makes a lot of sense.

You will have to perform character-by-character input to correctly read in terms. It is probably easiest to read in an entire line with your <code>Scanner</code> object and then cycle through the resulting <code>String</code> one character at a time. Operands can be any legal Java 6 <code>double</code> literal that is not in scientific notation, e.g. <code>8</code>, <code>+8.4</code>, <code>-8.4</code>, <code>-8.4</code>, <code>0.0000000004</code>, <code>.51</code>, <code>2.</code> and so on. In other words, an operand may start with an optional <code>+</code> or <code>-</code>. It may optionally contain a single decimal point which has a sequence of digits <code>0</code> through <code>9</code> in front of it, behind it, or both. A legal operand must contain at least one digit. You may use the <code>Character.isDigit()</code> method to check to see if a <code>char</code> value is a digit. You should use the <code>Double</code> class to convert a <code>String</code> to a <code>double</code>.

If you are familiar with deterministic finite automata, constructing one can be a great aid to parsing operands.

<h3>Standardized Printing</h3>

Once you have read all the tokens into a queue or similar data structure, it is simple to print out each value with a single space between them.

For sample input:

<pre>(       ( -9+            8.4)     )</pre>

The standardized print version is:

<pre>( ( -9.0 + 8.4 ) )</pre>

Students are often tempted to keep the input in one large <code>String</code>. Doing so is counter-productive. It is much better to parse the data into operands and operators (and put them in a queue) when they are first read. Then, the ugly process of parsing is done once and for all. This standardized printing task is, in part, to force you to do this parsing step once and then store each operand and operator in an appropriate data structure. Doing so makes standardized printing a snap.

<h3>Conversion from Infix to Postfix</h3>

Using a stack data structure, the conversion from infix to postfix can be done with the following algorithm. The algorithm begins with a full input queue of terms, an empty stack of operators, and an empty output queue of terms.

Process the input queue, one token at a time, applying the appropriate rules depending on what kind of token you get:

<ul>

 <li style="list-style-type: none">

  <ul>

   <li><strong>Operand:</strong>Add it to the output queue.</li>

  </ul></li>

</ul>




<ul>

 <li style="list-style-type: none">

  <ul>

   <li><strong>Left Parenthesis:</strong>Push it onto the operator stack.</li>

  </ul></li>

</ul>




<ul>

 <li style="list-style-type: none">

  <ul>

   <li><strong>Right Parenthesis:</strong>Pop off everything from the operator stack and add each operator to the output queue, until you hit a left parenthesis. Then pop off the left parenthesis.</li>

  </ul></li>

</ul>




<ul>

 <li><strong>Any Other Operator:</strong>If the stack is empty, push the new operator onto the stack. If the stack is not empty, compare the precedence of the current operator with the precedence of the operator on the top of the stack. If our operator’s precedence is less than or equal to the top’s precedence, pop the the stack and put the top element into the output queue. Continue doing so until the stack is empty or we reach an operator with a lower precedence than the new operator. Finally, put the new operator on the stack. The precedences start with <code>(</code>, which has the lowest, then <code>+</code> and <code>-</code>, and finally <code>*</code> and <code>/</code>, with the highest. If you are the three-person group, <code>%</code> has the same priority as <code>*</code> and <code>/</code>. The operator <code>)</code> does not have a precedence.</li>

</ul>

After all the input has been processed, pop whatever is left in the stack and add it to the output queue. Then print the contents of the output queue.

<h3>Evaluating the Postfix Expression</h3>

Evaluating the postfix expression requires a stack as well, but this time the stack is made up of operands. Process the postfix expression term by term. If the term is an operand, push it onto the stack. If the term is an operator, pop two operands off the stack and apply the operator to them. Then, push the result back onto the stack. When you have exhausted the input, the final answer should be the only thing left on the stack.

<h3>Storing Variables (Three-person Group Only)</h3>

If you are in a three-person group, you must also provide the ability to store variables. Unlike the regular program, your program should allow multiple expressions to be entered. You should continue accepting expressions until the user enters <code>quit</code>.

In addition to the normal expressions, you also have to accept assignments. An assignment consists of a variable name followed by an equal sign (<code>=</code>), followed by an expression, as in the following.

<pre>Enter infix expression: <em>value1 = 15 - 1</em>Standardized infix: value1 = 15.0 - 1.0Postfix expression: value1 = 15.0 1.0 -Answer: 14.0</pre>

Variables do not need declaration and are all effectively of type <code>double</code>. After a variable is assigned, it can appear in future expressions anywhere that an operand could appear. When it appears in an expression, it should be treated as if it contains the value it was most recently assigned. For example, after the previous assignment, the following expression could be evaluated.

<pre>Enter infix expression: <em>2 + value1</em>Standardized infix: 2.0 + value1Postfix expression: 2.0 value1 +Answer: 16.0</pre>

Storing a variable and its value requires a symbol table, map, or dictionary. These terms all refer to a data structure that contains a list of keys (in this case, the variable name, a <code>String</code>) and the corresponding value associated with each key (in this case, the variable value, a <code>double</code>). For this project, you are not expected to implement a symbol table efficiently since that is a topic for the rest of the course. You may wish to refer to section 3.1 in the textbook, which discusses symbol tables at a conceptual level and gives a linked-list implementation of one.

Any legal Java 6 identifier can be used for a variable. A legal identifier starts with an uppercase letter, a lowercase letter, or an underscore (<code>_</code>) and is then followed by zero or more characters, which can be letters, digits, or underscores.

In addition to the errors listed in the next section, the three-person group must check for the following errors. These errors should be reported before standardized infix would normally be printed.

<ol>

 <li><strong>Illegal Assignment:</strong> If an expression contains an equal sign, the equal sign must be the second token (the first operator), and the first token must be a legal variable name. Otherwise, print <code>Illegal assignment</code>.</li>

 <li><strong>Uninitialized variable:</strong> If a variable appears in an expression (either a simple expression or the right side of an equal sign), it must have been defined before. Otherwise, if the variable name does not appear in your symbol table, print <code>Uninitialized variable</code>.</li>

</ol>

<h2>Errors</h2>

You are required to check for five possible errors:

<ol>

 <li><strong>Invalid Operand:</strong> If the next token of input should be an operand, but it is not a properly formatted float literal, print <code>Invalid operand</code> and exit the program.</li>

 <li><strong>Invalid Operator:</strong> If the next token of input should be an operator, but the symbol you find (ignoring spaces, of course) is an invalid operator character, print <code>Invalid operator: </code>and the invalid character and exit the program.</li>

 <li><strong>Missing Operand:</strong> If the last term in the input sequence is an operator other than the right parenthesis, it must be the case that the last operation has no second operand. In this case, print <code>Missing operand</code> and exit the program.</li>

 <li><strong>Unbalanced Right Parenthesis:</strong> If, while converting the infix expression to a postfix expression, you encounter a right parenthesis and pop operators off your stack but find no corresponding left parenthesis, print <code>Unbalanced right parenthesis ')'</code> and exit the program.</li>

 <li><strong>Unbalanced Left Parenthesis:</strong> If, at the end of the conversion from infix a postfix, when doing the final popping of all the remaining operators, you encounter a left parenthesis (which much not have had a corresponding right parenthesis) print <code>Unbalanced left parenthesis '('</code> and exit the program.</li>

</ol>

<h2>Sample Output</h2>

The following are a few simple cases of sample output for you to check against. User input is marked in <span class="green">green</span>.

<h3>Normal Cases</h3>

<pre>Enter infix expression: <em>(5-6)*7</em>Standardized infix: ( 5.0 - 6.0 ) * 7.0Postfix expression: 5.0 6.0 - 7.0 *Answer: -7.0</pre>

<pre>Enter infix expression: <em>602000000000000000000000 - 14.231 * +800000000000000000000</em>Standardized infix: 6.02E23 - 14.231 * 8.0E20Postfix expression: 6.02E23 14.231 8.0E20 * -Answer: 5.906152E23</pre>

<pre>Enter infix expression: <em>9</em>Standardized infix: 9.0Postfix expression: 9.0Answer: 9.0</pre>

<pre>Enter infix expression: <em>((((((6 - 42))))))</em>Standardized infix: ( ( ( ( ( ( 6.0 - 42.0 ) ) ) ) ) )Postfix expression: 6.0 42.0 -Answer: -36.0</pre>

<h3>Error Cases</h3>

<pre>Enter infix expression: <em>egg + 2</em>Invalid operand</pre>

<pre>Enter infix expression: <em>4 &amp; 5</em>Invalid operator: &amp;</pre>

<pre>Enter infix expression: <em>10 +</em>Missing operand</pre>

<pre>Enter infix expression: <em>(2 + 2</em>Standardized infix: ( 2.0 + 2.0Unbalanced left parenthesis '('</pre>

<pre>Enter infix expression: <em>2 + 2)</em>Standardized infix: 2.0 + 2.0 )Unbalanced right parenthesis ')'</pre>

<h2>Testing</h2>

In a problem like this, testing is of crucial importance. There are many different ways that your program can fail, and you want to check them all.

A short, but not nearly exhaustive list of test cases you want to cover includes:

<ul>

 <li>Each of the four operations separately</li>

 <li>Combinations of the four operations</li>

 <li>Use of parentheses to disambiguate</li>

 <li>More parentheses than are necessary</li>

 <li>Double values preceded by a minus sign</li>

 <li>Double values preceded by an optional plus sign</li>

 <li>Double values using scientific notation</li>

 <li>A single value with no operators</li>

 <li>Expressions with no spaces</li>

 <li>Expressions with unusual spacing</li>

 <li>Expressions long enough to require your stack or queue to perform a reallocation (assuming you are using array based stacks or queues)</li>

 <li>Error cases with a single bad operand</li>

 <li>Error cases with multiple bad operands</li>

 <li>Error cases with a single bad operator</li>

 <li>Error cases with multiple bad operators</li>

 <li>Error cases with unbalanced left parentheses</li>

 <li>Error cases with unbalanced right parentheses</li>

</ul>

For this project, you are required to create a large number of test cases, record them, and record the output of your program with each test case. A document containing this information is one of the items you must turn in.

<h2>Hints</h2>

<ul>

 <li style="list-style-type: none">

  <ul>

   <li>Start early. This project is tough. Do everything you can to work smoothly with your partner.</li>

  </ul></li>

</ul>




<ul>

 <li style="list-style-type: none">

  <ul>

   <li>This project is supposed to cover stacks and queues. You are required to implement at least one stack class. You’ll need stacks for both operators and operands. You can get around the problem of coding multiple stacks by making a generic stack. Or, you can make a stack able to hold a class that can contain either an operand or an operator. Or you can make operands and operators subclasses of a common superclass and hold references to the superclass in your stack. In my solution, I used a generic stack and also made operands and operators subclasses of a superclass.</li>

  </ul></li>

</ul>




<ul>

 <li style="list-style-type: none">

  <ul>

   <li>A pure stack has a very small number of methods: <code>push()</code>, <code>pop()</code>, <code>peek()</code>, and maybe <code>size()</code> or <code>isEmpty()</code>. Data structures are supposed to make our lives easier. If you want to keep everything in a stack, but occasionally access the elements like an array or with an iterator, that’s fine. You don’t have to have a pure stack. Instead of using queues, I implemented a <code>get()</code> operator on my stack class. Objects were only added or removed with <code>push()</code> and <code>pop()</code>, but I could read any of them I wanted to. Additionally, feel free to implement your stack with an array or a linked list, but I highly recommend an array. It’s easier, faster, and any element can be accessed in O(1) time.</li>

  </ul></li>

</ul>




<ul>

 <li style="list-style-type: none">

  <ul>

   <li>Work incrementally. Compile constantly. This project is nicely laid out into a few steps. Get input parsing working first. Then, implement your stack. Then, get infix to postfix working. Then, compute the answer. Write some kind of printing function early so that it’s easy to see the current state of your terms.</li>

  </ul></li>

</ul>




<ul>

 <li style="list-style-type: none">

  <ul>

   <li>Write clean code.</li>

  </ul></li>

</ul>




<ul>

 <li style="list-style-type: none">

  <ul>

   <li>No outside classes other than <code>Scanner</code>, <code>String</code>, and the <code>Double</code> and <code>Character</code> wrapper classes should be used.</li>

  </ul></li>

</ul>




<ul>

 <li>There are lots of error cases to detect, and most of them happen while in the middle of doing something else. How can you handle all these errors? Well, exception handling is a great tool. In my implementation, I created five custom exception classes corresponding to each of the errors: <code>InvalidOperandException</code>, <code>InvalidOperatorException</code> (which takes a <code>char</code> value in its constructor to hold the unexpected operator), <code>MissingOperandException</code>, <code>UnbalancedLeftParenthesisException</code>, and <code>UnbalancedRightParenthesisException</code>. You don’t have to make your own exceptions, but it makes handling the errors easy, mostly because you can handle them all in one place.</li>

</ul>