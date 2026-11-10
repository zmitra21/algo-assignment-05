# CMPS 2200 Assignment 5
## Answers

**Name:**Zack Mitra

Place all written answers from `assignment-05.md` here for easier grading.


**1: Fixed-Length vs. Variable-Length Codes**

- **1d. (5 pts)** What trend do you see?

Fixed-length cost:  1039367
Huffman cost:  676374
Fixed-length cost:  876253
Huffman cost:  606448
Fixed-length cost:  1340
Huffman cost:  826
Fixed-length cost:  78050
Huffman cost:  56206
Fixed-length cost:  26047
Huffman cost:  17356

Huffman encoding consistently requires fewer bits than fixed-length encoding. This is because Huffman coding assigns shorter codes to frequently occurring characters and longer codes to less common characters, reducing the overall encoding cost. The compression ratio varies depending on the distribution of character frequencies in each file. Across these five files, Huffman coding saves approximately 28% to 38% of the bits compared with fixed-length encoding.


- **1e. (4 pts)** What is the expected
  cost of a Huffman encoding for the document? Is it consistent across
  documents?

  If every character has the same frequency, Huffman coding produces a balanced or nearly balanced tree because no character has a frequency advantage. For an alphabet of size k, the expected number of bits per character is approximately log₂(k). If k is a power of 2, each character receives exactly log₂(k) bits, giving a total cost of n log₂(k) for a document of n characters, the same as fixed-length encoding.

  The total cost is not necessarily consistent across documents because it depends on the document length and alphabet size. However, for documents with the same alphabet size and equally frequent characters, the average number of bits per character is consistent.



**2: Making Change**

- **2a. (5 pts)** Given a $N$ dollars, state a greedy algorithm for producing
as few coins as possible that sum to $N$.

A greedy algorithm for making change is to repeatedly select the largest available coin denomination that is less than or equal to the remaining amount N. Subtract the selected coin's value from N and repeat until N = 0.

Since the denominations are powers of 2, this method produces the minimum number of coins by selecting the largest possible denomination at each step.

For example, if N = 27, the algorithm selects 16, 8, 2, and 1, requiring only 4 coins.


- **2b. (5 pts)** Prove that this algorithm is optimal by proving the greedy
  choice and optimal substructure properties.

The greedy algorithm selects the largest available coin denomination that does not exceed the remaining amount. Since the denominations are powers of 2, any two coins of denomination 2^i can be replaced by one coin of denomination 2^(i+1), as long as the larger denomination is available. This reduces the number of coins without changing the total value.

Therefore, an optimal solution uses at most one coin of each denomination below the largest available denomination. It follows that an optimal solution must use as many coins of the largest available denomination as possible, followed by the denominations needed for the remaining amount. Therefore, the greedy choice is optimal.

After selecting the largest possible coin of value c, the remaining amount is N - c. Suppose an optimal solution to N did not use an optimal solution for the remaining amount. We could replace the coins representing N - c with a solution using fewer coins, producing a better solution for N. This contradicts the optimality of the original solution.

Therefore, the remaining amount must also be solved optimally. Since the greedy-choice property and optimal substructure both hold, repeatedly selecting the largest available coin produces a minimum-coin solution.


- **2c. (4 pts)** What is the work and span of your algorithm?

Let k represent the exponent of the largest available coin denomination, 2^k, and let c represent the total number of coins produced.

The algorithm examines k + 1 denominations, requiring O(k) work. It also performs one operation for each coin selected, contributing O(c) work. Therefore, the total work is O(k + c).

Since the algorithm selects coins sequentially and each decision depends on the remaining amount, the span is equal to the work.

Thus, W = O(k + c) and S = O(k + c).

In the worst case, c can be O(N), giving W = S = O(k + N). If N < 2^(k+1), each denomination is selected at most once, and both work and span simplify to O(k), or O(log N) when k = Theta(log N).

3a:

Minimum Edit Distance has optimal substructure because the optimal solution for transforming one string into another depends on optimal solutions to smaller substring problems.

If either string is empty, the edit distance equals the length of the remaining string. If the first characters match, no operation is necessary, and we recursively compute the edit distance of the remaining suffixes.

If the first characters differ, we consider three operations, each with cost 1:

Insertion: 1 + MED(S, T[1:])

Deletion: 1 + MED(S[1:], T)

Substitution: 1 + MED(S[1:], T[1:])

We choose the minimum of these three possibilities. The remaining substring problem must be solved optimally. Otherwise, replacing its solution with a better one would reduce the total edit distance.