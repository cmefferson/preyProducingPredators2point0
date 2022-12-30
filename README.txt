The following files pertain to the full model in the paper.  Run them in the order listed here.

1) findSteadyStatesRanParamValues.txt

This file chooses random points in parameter space and finds the associated steady states.  It saves the results as a data frame called 'steadyStates.RData'.

2) findSteadyStatesRanParamValues_jacobianStability.txt

This file loads steadyStates.RData from (1) and calculates the eigenvalues of the Jacobian matrix evaluated at each steady state.  It saves the results as a data frame called 'steadyStates.RData', and according it overwrites the previous version of this file.  That said, running (2) only adds columns to the data frame produced by (1), so all the original information is still there.

3) runSimsRanParamValues.txt

This file loads steadyStates.RData from (2) and simulates the dynamics from initial conditions randomly distributed around each steady state.  Importantly, this file expects to find a directory called 'figsRanParamValues'.  Create this directory before running the file, and it will put the figures there.  When finished, it will back out to your working directory again.

Important, when simulating dynamics under randomly selected points in parameter space, it can be hard to configure the program so that the ode solver reliably runs under all conditions without failing.  For example, if the system converges on a steady state, you can simulate as long as you want without problem.  If it grows exponentially, however, you cannot do this b/c the simulated values will exceed the finite capabilities of your computer eventually.

Accordingly, this file is programmed to print the current steady state from steadyStates.RData to the terminal when running.  If the ode solver fails for a particular steady state, you can usually get it to work if you simply reduce maxTime, with the obvious cost that you cannot see dynamics over longer time frames.  You just need the index for the steady state that failed to do so as explained immediately below. 

Let's illustrate by assuming that index 10 fails.  In this case, record the value 10 in the array I on line 39.  This array remains commented out.  Then change the lower limit of the loop that begins on line 41 to the next index.  In this example, where steady state 10 fails, do the following.

for (i in 11:nrow(steadyStates))

Now run the file again, and it will pick up with steady state 11.  Repeat as necessary until you've made it through all the rows (i.e. steady states) in steadyStates.RData.  Then implement the following procedure.

- Reduce maxTime to some smaller value on line 11.
- Uncomment line 39.
- Comment line 41.
- Uncomment line 42.
- Run file again.

With this procedure, you'll only run the simulations for the steady states that originally failed, and you'll rerun the simulations for these steady states under your now reduced value of maxTime.  



The following files pertain to the reduced model explained in the paper.  Unlike the routines above, the files here define specific combinations of parameter values and work only with those combinations.  Run the files in the order listed here.

1) findSteadyStatesSpecificParamValuesLinearFunResV2.txt

Begins by defining the points in parameter space of interest and then finds the steady states.  Saves the results as a data frame called 'steadyStatesLinearFunResSpecValuesV2.RData'.

2) findSteadyStatesSpecificParamValuesLinearFunResV2_jacobianStability.txt

Loads the data frame from (1) and calculates the eigenvalues of the Jacobian evaluated at the steady states.

3) runSimsSpecificParamValuesLinearFunResV2SS.txt

Loads the data from from (1) and simulates dynamics from random initial conditions distributed around the steady states.  This file expects a directory called 'figsSpecificParamValuesLinearFunResVS22', so create that directory first.  Returns to working directory after running.

Finally, you can also run runSimsSpecificParamValuesLinearFunResV2NotSS.txt at any time.  This file does not work with steady states.  It simply defines a set of points in parameter space (e.g. the same points used in (1)), picks random initial conditions, and simulates the dynamics.  This file expects a directory called figsSpecificParamValuesLinearFunResV2NotSS.  Create this directory before running.  Returns to working directory after running.