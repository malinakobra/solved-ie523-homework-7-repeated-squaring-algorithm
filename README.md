Download Link: https://assignmentchef.com/product/solved-ie523-homework-7-repeated-squaring-algorithm
<br>
Later on in the course, when we deal with the problem of computing the price of an <em>European Option </em>efficiently using the method of <em>Dynamic Programming</em>, we will have to deal with the problem of taking an <em>n </em>× <em>n </em>matrix <strong>A </strong>and raising it to a large number. That is, we will have to compute <strong>A</strong><em><sup>k </sup></em>for large values of <em>k</em>.

You could compute it by multiplying <strong>A </strong>over with it self <em>k </em>times. That is,

(with <em>NEWMAT</em>) something along the lines of

1: C = A;

2: <strong>for </strong>int <em>i </em>= 1; <em>i &lt; k</em>; <em>i</em>++ <strong>do</strong>

3:                 C = A*C;

4: <strong>end for</strong>

Assuming you are doing straightforward matrix multiplication (nothing clever like Strassen’s method, etc.) then the above procedure will take <em>O</em>(<em>n</em><sup>3</sup><em>k</em>) steps, as each matrix multiplication is <em>O</em>(<em>n</em><sup>3</sup>) and there are <em>k</em>-many of them.

A candidate algorithm that is more efficient than the one shown above goes by the name of <em>Repeated Squaring</em>, and it described below.

<h1>Repeated Squaring Algorithm</h1>

Suppose you want to compute <strong>A</strong><sup>11</sup>, you write the exponent 11 in binary – which is h1 0 1 1i<sub>2</sub>. That is, 11 = 1×2<sup>3 </sup>+0×2<sup>2 </sup>+1×2<sup>1 </sup>+1×2<sup>0</sup>. You then compute all dlog<sub>2 </sub>11e-many powers of <strong>A</strong>. That is, you compute <strong>A</strong><em>,</em><strong>A</strong><sup>2</sup><em>,</em><strong>A</strong><sup>4</sup><em>,</em><strong>A</strong><sup>8</sup>, then add the appropriate components as per the binary expansion of the exponent. In our case, we add <strong>A</strong><sup>8 </sup>×<strong>A</strong><sup>2 </sup>×<strong>A </strong>to get the final product. It turns out that these constituent powers of <strong>A </strong>(i.e. 8, 2 and 1) can be computed in a recursive manner quite efficiently. Here is something from the following <a href="http://www.algorithmist.com/index.php/Repeated_Squaring">link</a> that computes <em>n<sup>k </sup></em>for integers <em>n </em>and <em>k</em>.

1: int power( int <em>n</em>, int <em>k </em>)

2: <strong>if </strong><em>k </em>== 0 <strong>then</strong>

3:              return 1

4: <strong>end if</strong>

5: <strong>if </strong><em>k </em>is odd <strong>then</strong>

6:               return (<em>n </em>* power (

7: <strong>else</strong>

8:               return (power(

9: <strong>end if</strong>

A similar approach can be used to compute <strong>A</strong><em><sup>k </sup></em>for a square matrix <strong>A</strong>. I leave the nitty-gritty details for you to figure out. Keep in mind that with NEWMAT on your side, the matrix operations are structurally the same as that for scalars.

<h1>Complexity of Repeated Squaring vs. Brute Force Multiplication</h1>

If you have to compute <strong>A</strong><em><sup>k</sup></em>, and assuming each multiplication is <em>O</em>(<em>b</em><sup>3</sup>) (nothing clever here, straightforward matrix multiplication), and since we have log<sub>2 </sub><em>k</em>many of these to do (or, since log we can replace log<sub>2 </sub><em>k </em>with

<em>O</em>(log<em>k</em>)), this entire operation takes <em>O</em>(<em>b</em><sup>3 </sup>log<em>k</em>). This is in contrast to the <em>O</em>(<em>b</em><sup>3</sup><em>k</em>) procedure for multiplying <strong>A </strong>with itself <em>k </em>times. Resulting in a total complexity of <em>O</em>(<em>b</em><sup>3 </sup>ln<em>k</em>). If we used <em>Strassen</em>’s method for matrix multiplication we would have a procedure that is <em>O</em>(<em>b</em><sup>2<em>.</em>8<a href="#_ftn1" name="_ftnref1">[1]</a> </sup>ln<em>k</em>).

<h1>The Programming Assignment</h1>

<ol>

 <li>(Using <em>NEWMAT</em>) I want you to write a recursion routine</li>

</ol>

Matrix repeated squaring(Matrix A, int exponent, int no rows)

which takes a (no rows × no rows) matrix A and computes A<sup>exponent </sup>using the <em>Repeated Squaring Algorithm</em>.

<ol start="2">

 <li>Your code should be able to take as input the size and exponent as input on the command line. That is, if we want to compute <strong>A</strong><em><sup>k</sup></em>, where <strong>A </strong>is an (<em>n</em>×<em>n</em>) square matrix, I want to be able to read <em>n </em>and <em>k </em>on the commandline. It should fill the entries of the matrix <strong>A </strong>with random entries in the interval (−5<em>,</em>5)<sup>1</sup>.</li>

 <li>The output should indicate: (1) The number of rows/columns in <strong>A </strong>(that is read from the command line), (2) The exponent <em>k </em>(that is read from the command line), (3) The result <u>and </u>the amount of time it took to compute <strong>A</strong><em><sup>k </sup></em>using repeated squaring, and (4) The result <u>and </u>the amount of time it took to compute <strong>A</strong><em><sup>k </sup></em>using brute force multiplication. A sample output is shown in figure 1.</li>

 <li>I want you to provide a plot of the computation time (in seconds) for the two methods as a function of the size of the matrix. That is, I am looking for something along the lines of figure 2. For this, you will have to place timer objects before and after appropriate portions of your code and do the needful – as the following lines of code illustrate.</li>

</ol>

time before = clock();

B = repeated squaring(A, exponent, dimension); time after = clock(); diff = ((float) time after – (float) time before);

cout <em>&lt;&lt; </em>”It took ” <em>&lt;&lt; </em>diff/CLOCKS PER SEC <em>&lt;&lt; </em>” seconds to complete” <em>&lt;&lt; </em>endl;

In terms of the value of the exponent, tell me the regions where one algorithm performs better than the other, as far as computation time is concerned.

Figure 1: A sample output for different exponents and matrix-dimensions.

Figure 2: A comparison of the computation-time (obtained experimentally) for brute-force exponentiation and the method of repeated squares of a random 5 × 5 matrix as a function of the exponent.

<a href="#_ftnref1" name="_ftn1">[1]</a> See strassen.cpp for ideas.