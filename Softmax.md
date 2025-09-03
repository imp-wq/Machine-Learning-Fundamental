[The Softmax : Data Science Basics](https://www.youtube.com/watch?v=8ps_JEW42xs)
- a couple of laws:
	- $P_i\in[0, 1]$
	- the sum of $P_1\ldots P_i$ needs to add up to 1
- Problems with the easier solution:
	- The right one only added a constant (100), but the distribution changed a lot.
	$$
	\begin{bmatrix}
0 \\
1 \\
2
\end{bmatrix}
\to
\begin{bmatrix}
0 \\
\frac{1}{3} \\
\frac{2}{3}
\end{bmatrix}

\begin{bmatrix}
100 \\
101 \\
102
\end{bmatrix}
\to
\begin{bmatrix}
0.33 \\
0.33 \\
0.34
\end{bmatrix}

	$$
- softmax:
	$$
	P_i = \frac{e^{S_i}}{\sum e^{S_j}}
	$$
	- If we add or subtract a constant C, it doesn't change the probablity:
		$$
		P_i'  = \frac{e^{s_i+C}}{\sum_j e^{s_j+C}} = \frac{e^{s_i} e^{C}}{\sum_j e^{s_j} e^{C}} = P_i
		$$
	- Partial derivative of Softmax: $P_i(1-P_i)$
		- when $P_i$ is something near 1 or 0, the derivative will be near to 0
			which means if I'm very confident in the student will (not) choose math, the score changing a little bit won't change the fact.
		- derivation achieves maximum is $P_i$ is equal to 1/2.
			I'm equally likely that the student will choose math vs all the other majors in my vector. If you change my score y a little bit, that's going to give me a lot of confidence 
		- cross term derivative:
			$$
			\frac{\partial P_i}{\partial S_j} = -P_i P_j
			$$





