# 18.330-Problem-set-2
18.330 Problem set 2

**Download Link:https://programming.engineering/product/18-330-problem-set-2/**

Description
5/5 – (2 votes)
Exercise 1: Fixed-point iteration In this question we will find the roots of the function

√

( , ) = 3 − + 2

by using fixed-point iterations.

Define a Julia function for and draw it; make an interactive visualization as changes. [Make sure to fix the plot limits so as to be able to see what’s going on.]

When varies, the number of real roots can change. For which approx-imate value of does the number of real roots change? How many real roots are there?

When = 2.5, approximately where are the roots? From now on fix to this value.

The simplest thing we can try is ( ) = + ( , ), since then a fixed point of is a root of .

Plot the function ( ) and the function = . Taking into account the results stated in the slides, which root do you expect to be able to calculate by iterating ? Fix an initial condition and show that it does converge there.

What is the rate of convergence to that root?

What happens with the initial condition = 1.1? Why?

Draw a cobweb diagram to illustrate this behaviour.

By using algebraic transformations, find fixed-point iterations that con-verge to the other two roots.

There are two alternative approaches you can take here. The first is to find other iteration schemes, = ( ) by algebraically rearranging ( , ) = 0 to isolate an on one side. The second is to introduce the generalized function ( , ) = + ( ). Make an interactive plot of ( , ) and = as varies. What do you notice about the slope of ( , ) at the fixed points as changes? Can you use this to change the stabilities of the fixed points in the iteration scheme?

(Extra credit) Call the critical value of at which the number of roots changes. [This is called a bifurcation point.] Find numerically.


Exercise 2: Defining a type for Polynomials Although we have already used polynomials, we haven’t had a way to say “this object is a polynomial”. For this we need to define a new type!

1. Define a type Polynomial to represent a polynomial. It should have fields degree and coefficients.

Write a constructor function with the same name (Polynomial) that ac-cepts a vector of coefficients and builds a Polynomial object whose degree it automatically calculates.

Write a show method to display the polynomial nicely.

Write a function to evaluate the polynomial at a point x, as follows:

function (p::Polynomial)(x)

# fill in

end

Then if you have an object p of type polynomial, writing e.g. p(3) will eval-uate that polynomial at the value 3.

Write a function derivative that takes a polynomial and returns a new polynomial that is its derivative.

Julia contains a module Test (in the standard library – no installation re-quired) for testing that code is correct.

Write a few tests of the functionality you have defined using tests of the form

@test a == b

E.g. to test the sum of two Polynomials you can write

@test Polynomial([1, 2]) + Polynomial([3, 4]) == Polynomial([4, 6])

When you run these tests, you should see the message Test passed.

To create the tests, do the calculations by hand.

Exercise 3: Newton method

Write a function newton to implement the Newton method. It should take a function , its derivative ′ and an initial guess 0. It should terminate when the residual is less than some tolerance, or when the number of iterations is too large.

Write a specialised method of newton for polynomials that accepts an ob-ject of type Polynomial, written p::Polynomial and calculates its derivative automatically.


Taking the same polynomial as in exercise 1, confirm that the Newton method has quadratic convergence by verifying numerically the defining limit.

Can you find different roots by taking different initial conditions 0? How will you know if/when you have found all of the roots like this?

The Newton method works fantastically well when the starting point is close enough to a root, but can also behave very badly, as follows.

How many roots does the function ( ) = 3 − 1 have in the complex plane ℂ? Where are they?

Calculate those roots using the Newton method with complex starting points + forming a square grid in the complex plane. Store the imaginary part of the resulting root (or final value, if no root is reached) in a matrix.

Plot the matrix with the heatmap function and plot the true roots as points. What kind of object are you seeing? What does this imply for the Newton method? What happens close to the roots?

Exercise 4: Aberth method Newton’s method only finds one root at a time. The Aberth method calculates them all at once! Given estimates ( ) for all roots of a polynomial it calculates a new estimate via = − , where

=

( ′

)

.

1 −

( ′

) ( )

1

( ) ⋅ ∑ ≠

−

In order to guarantee convergence the initial guess must be chosen in a special way. Cauchy’s bound tells us that all the roots of a polynomial ( ) = 0 + 1 + ⋯ + must have absolute value less than

= 1 +

max

(∣

−1

∣ , ∣

−2

∣,…,∣

0

∣)

and a lower bound of

=

1 +

{∣ 0

∣,∣ 0

∣,…,∣

0

∣}

max

1

−1

1

The starting points should be chosen so that their absolute value lies in between these bounds.


1. Implement a function poly_bounds that takes in a Polynomial and returns

and .

Use poly_bounds to write a function initialize_points that finds a suitable starting group of points. Do this by choosing s sampled from a uniform distribution over [ , ] and s sampled from a uniform distribution over [0, 2 ]. Then calculate = .

[Hint: The rand() function generates uniform random numbers between 0 and 1. Use rand to write a function uniform(a, b) to generate uniform numbers between and .]

Implement the Aberth method for a polynomial which takes in values from initialize_points and terminates either after a certain number of iterations or when a certain tolerance is met. Test your function for the polynomials we have considered so far.

Make an interactive visualization of the progress over time on some ran-dom polynomials of degree 10 or 20.

Find numerically the order of convergence of the method.

Try polynomials with multiple roots, such as ( 2 + 1)3. What happens?
