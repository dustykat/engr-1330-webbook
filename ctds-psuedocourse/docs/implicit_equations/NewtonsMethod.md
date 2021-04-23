```python
# Environment Check -- Deactivate on a working host
import sys
print(sys.executable)
print(sys.version)
print(sys.version_info)
```

    /opt/jupyterhub/bin/python3
    3.8.5 (default, Jan 27 2021, 15:41:15) 
    [GCC 9.3.0]
    sys.version_info(major=3, minor=8, micro=5, releaselevel='final', serial=0)


# Numerical Methods - Single Variable Newtons Method
The application of fundamental principles of modeling and mechanics often leads to an
algebraic or transcendental equation that cannot be easily solved and represented in a closed
form. In these cases a numerical method is required to obtain an estimate of the root or
roots of the expression.

Newton's method is an iterative technique that can produce good estimates of solutions to
such equations. The method is employed by rewriting the equation in the form `f(x) = 0`,
then successively manipulating guesses for `x` until the function evaluates to a value close
enough to zero for the modeler to accept.

   ![figure](newton1.png)

The figure above is a graph of some function whose intercept with the `x-axis` is unknown. The goal
of Newton's method is to find this intersection (root) from a realistic first guess. Suppose
the first guess is `x1`, shown on the figure as the right-most specific value of `x`. The value
of the function at this location is `f(x1)`. Because `x1` is supposed to be a root the difference
from the value zero represents an error in the estimate. Newton's method simply provides a
recipe for corrections to this error.

Provided `x1` is not near a minimum or maximum (slope of the function is not zero) then a
better estimate of the root can be obtained by extending a tangent line from `x1, f(x1)` to
the `x-axis`. The intersection of this line with the axis represents a better estimate of the
root.  This new estimate is `x2`. A formula for `x2` can be derived from the geometry of the triangle
`x2,f(x1),x1`. Recall from calculus that the tangent to a function at a particular point is
the first derivative of the function. Therefore, from the geometry of the triangle and the
definition of tangent we can write, 

\begin{equation}
tan(\theta)=\frac{df}{dx}\Biggr\vert_{x_1} = \frac{f(x_1)}{x_1 - x_2}
\end{equation}

Solving the equation for `x`2 results in a formula that expresses `x2` in terms of the first guess
plus a correction term.

\begin{equation}
x_2=x_1 - \frac{f(x_1)}{\frac{df}{dx}\vert_{x_1}} 
\end{equation}

The second term on the right hand side is the correction term to the estimate on the right
hand side. Once `x2` is calculated we can repeat the formula substituting `x2` for `x1` and `x3` for
`x2` in the formula. Repeated application usually leads to one of three outcomes:
1. a root;
2. divergence to +/- $\inf$ ; or
3. cycling.

These three outcomes are discussed below in various subsections along with some remedies.
The generalized formula is

\begin{equation}
x_{k+1}=x_{k} - \frac{  f(x_{k})  }{   \frac{df}{dx}\rvert_{x_k} } 
\label{eqn:NewtonFormula}
\end{equation}

If the derivative is evaluated using analytical derivatives the method is called Newton's
method, if approximations to the derivative are used, it is called a quasi-Newton method.

## Newton's Method --- Using analytical derivatives
This subsection is an example in Python of implementing Newton's method with analytical derivatives.   

The recipe itself is:
1) Write the function in proper form, and code it into a computer.
2) Write the derivative in proper form and code it into a computer.
3) Make an initial guess of the solution (0 and 1 are always convenient guesses).
4) Evaluate the function, evaluate the derivative, calculate their ratio.
5) Subtract the ratio from the current guess and save the result as the update.
6) Test for stopping:
     i) Did the update stay the same value? Yes, then stop, probably have a solution.
    ii) Is the function nearly zero?  Yes, then stop we probably have a solution.
    iii) Have we tried too many updates? Yes, then stop the process is probably cycling, stop.
7) If stopping is indicated proceed to next step, otherwise proceed back to step 4.
8) Stopping indicated, report last update as the result (or report failure to find solution), and related information about the status of the numerical method.


The following example illustrates these step as well as an ipython implementation of Newton's method.

Suppose we wish to find a root (value of `x`) that satisfies:

\begin{equation}
f(x) = e^x - 10 cos(x) -100
\end{equation}

Then we will need to code it into a script.   Here is a code fragment that will generate the prototype function


```python
#  import built in function for e^x, cosine
from math import exp, cos, sin
# Define the function
def func(x):
    func = exp(x) - 10*cos(x) - 100  #using the name as the temp var
    return func
```

Notice in the code fragment we import three built-in functions from the Python math package, specifically $\exp()$, $\sin()$, and $\cos ()$.
The next step is to code the derivative.   In this case the derivative is 

\begin{equation}
\frac{df}{dx}\vert{(x)} = e^x + 10 \sin(x)
\end{equation}

and the prototype function is coded as 


```python
def dfdx(x):
    dfdx = exp(x) + 10*sin(x)
    return dfdx
```

Next we will need script to read in an initial guess, and ask us how many trials we will use to try to find a solution, as well as how close to zero we should be before we declare victory.


```python
# Now for the Newton Method Implementation
# Get initial guess, use a simple error trap
yes=0
while yes == 0:
    xnow = input("Enter an initial guess for Newton method \n")
    try:
        xnow = float(xnow)
        yes =1
    except:
        print ("Value should be numeric, try again \n")
# Get number trials, use a simple error trap
yes=0
while yes == 0:
    HowMany = input("Enter iteration maximum \n")
    try:
        HowMany = int(HowMany)
        yes =1
    except:
        print ("Value should be numeric, try again \n")
# Get stopping criterion
yes=0
while yes == 0:
    HowSmall = input("Enter a solution tolerance (e.g. 1e-06) \n")
    try:
        HowSmall= float(HowSmall)
        yes =1
    except:
        print ("Value should be numeric, try again \n")
```

    Enter an initial guess for Newton method 
    1
    Enter iteration maximum 
    3
    Enter a solution tolerance (e.g. 1e-06) 
    1e-6


The use of `HowSmall` is called a zero tolerance.   
We will use the same numerical value for two tolerance tests.   
Also notice how we are using error traps to force numeric input.   
Probably overkill for this example, but we already wrote the code in an earlier essay, so might as well reuse the code.  
Professional codes do a lot of error checking before launching into the actual processing - especially if the processing part is time consuming, its worth the time to check for obvious errors before running for a few hours then at some point failing because of an input value error that was predictable.

Now back to the tolerance tests. 
The first test is to determine if the update has changed or not.   
If it has not, we may not have a correct answer, but there is no point continuing because the update is unlikely to move further.   
The test is something like

\begin{equation}
\text{IF}~\lvert x_{k+1} - x_{k} \rvert < \text{Tol.~ THEN Exit and Report Results}
\end{equation}  

The second test is if the function value is close to zero.   
The structure of the test is similar, just an different argument.   The second test is something like

\begin{equation}
\text{IF}~\lvert f(x_{k+1}) \rvert < \text{Tol.~ THEN Exit and Report Results}
\end{equation} 

One can see from the nature of the two tests that a programmer might want to make the tolerance values different.   
This modification is left as a reader exercise.

Checking for maximum iterations is relatively easy, we just include code that checks for normal exit the loop.

Here is code fragment that implements the method, makes the various tests, and reports results.


```python
# now we begin the process
count = 0
for i in range(0,HowMany,1):
    xnew = xnow - func(xnow)/dfdx(xnow)
# stopping criteria -- update not changing
    if abs(xnew - xnow) < HowSmall:
        print ("Update not changing \n")
        print("Function value =",func(xnew))
        print(" Root value    =",xnew)
        break
    else:
        xnow = xnew
        count = count +1
        continue
# stopping criteria -- function close to zero
    if abs( func(xnew) ) < HowSmall:
        print ("Function value close to zero \n")
        print("Function value =",func(xnew))
        print(" Root value    =",xnew)
        break
    else:
        xnow = xnew
        count = count +1
        continue
# next step, then have either broken from the loop or iteration counted out
if count == HowMany:
    print(" Iteration Limit Reached ")
    print("Function value =",func(xnew))
    print(" Root value    =",xnew)
print("End of NewtonMethod.py ")
```

     Iteration Limit Reached 
    Function value = 3676.8081814664183
     Root value    = 8.235647852860856
    End of NewtonMethod.py 


Now we simply connect the three fragments, and we would have a working Python script that implements Newton's method for the example equation.  The example is specific to the particular function provided, but the programmer could move the two functions `func` and `dfdx` into a user specified module, and then load that module in the program to make it even more generic.   The next section will use such an approach to illustrate the ability to build a generalized Newton method and <em>only have to program the function itself</em>

## Newton's Method --- Using finite-differences to estimate derivatives}
A practical difficulty in using Newton's method is determining the value of the derivative in cases where differentiation is difficult.  
In these cases we can replace the derivative by a finite difference equation and then proceed as in Newton's method. 

Recall from calculus that the derivative was defined as the limit of the difference quotient:

\begin{equation}
\frac{df}{dx}\vert_{x} = \lim_{\Delta x \rightarrow 0}\frac{f(x + \Delta x) - f(x) }{\Delta x}
\end{equation}

A good approximation to the derivative should be possible by using this formula with a small, but non-zero value for $\Delta x$.

\begin{equation}
\frac{df}{dx}\vert_{x} \approx \frac{f(x + \Delta x) - f(x) }{\Delta x}
\end{equation}

When one replaces the derivative with the difference formula the root finding method the resulting update formula is

\begin{equation}
x_{k+1}=x_k - \frac{f(x_k) \Delta x}{f(x_k + \Delta x)-f(x_k)} 
\end{equation}

This root-finding method is called a quasi-Newton method.

Here is the code fragment that we change by commenting out the analytical derivative and replacing it with a first-order finite difference approximation of the derivative.  The numerical value $1e-06$ is called the step size ($\Delta x$)  and should be an input value (rather than built-in to the code as shown here) like the tolerance test values, and be passed to the function as another argument.


```python
# reset the notebook
%reset
```

    Once deleted, variables cannot be recovered. Proceed (y/[n])? y



```python
#  import built in function for e^x, cosine
from math import exp, cos, sin
# Define the function
def func(x):
    func = exp(x) - 10*cos(x) - 100  #using the name as the temp var
    return func
def dfdx(x):
#    dfdx = exp(x) + 10*sin(x)
    dfdx = (func(x + 1e-06) - func(x) )/ (1e-06)
    return (dfdx)
```


```python
# Now for the Newton Method Implementation
# Get initial guess, use a simple error trap
yes=0
while yes == 0:
    xnow = input("Enter an initial guess for Newton method \n")
    try:
        xnow = float(xnow)
        yes =1
    except:
        print ("Value should be numeric, try again \n")
# Get number trials, use a simple error trap
yes=0
while yes == 0:
    HowMany = input("Enter iteration maximum \n")
    try:
        HowMany = int(HowMany)
        yes =1
    except:
        print ("Value should be numeric, try again \n")
# Get stopping criterion
yes=0
while yes == 0:
    HowSmall = input("Enter a solution tolerance (e.g. 1e-06) \n")
    try:
        HowSmall= float(HowSmall)
        yes =1
    except:
        print ("Value should be numeric, try again \n")
```

    Enter an initial guess for Newton method 
    2
    Enter iteration maximum 
    33
    Enter a solution tolerance (e.g. 1e-06) 
    1e-9



```python
# now we begin the process
count = 0
for i in range(0,HowMany,1):
    xnew = xnow - func(xnow)/dfdx(xnow)
# stopping criteria -- update not changing
    if abs(xnew - xnow) < HowSmall:
        print ("Update not changing \n")
        print("Function value =",func(xnew))
        print(" Root value    =",xnew)
        break
    else:
        xnow = xnew
        count = count +1
        continue
# stopping criteria -- function close to zero
    if abs( func(xnew) ) < HowSmall:
        print ("Function value close to zero \n")
        print("Function value =",func(xnew))
        print(" Root value    =",xnew)
        break
    else:
        xnow = xnew
        count = count +1
        continue
# next step, then have either broken from the loop or iteration counted out
if count == HowMany:
    print(" Iteration Limit Reached ")
    print("Function value =",func(xnew))
    print(" Root value    =",xnew)
print("End of NewtonMethod.py ")
```

    Update not changing 
    
    Function value = 1.4210854715202004e-14
     Root value    = 4.593209147284144
    End of NewtonMethod.py 


Pretty much the same result, but now we dont have to determine the analytical derivative.


```python

```
