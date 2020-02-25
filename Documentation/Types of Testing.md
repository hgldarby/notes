# Types of Testing

- Saving test cases and running them again after changes to other components of the program is known as regression testing.



### Black-box Testing

- Input/output driven testing has a goal of being completely unconcerned about the internal behavior and structure of the program, instead concentrate on finding circumstances in which the program doesn't behave according to its specs. 
- Test data is derived from the specs not taking advantage of the internal structure of the program.
- To find all errors in a program using black-box testing the criterion is **exhaustive input testing**.
- **Exhaustive input testing** - Not possible on large programs. Cannot guarantee that the program is error free
- Maximise yield on testing environment by maximising the number of errors found by a finite number of test cases.



### White-box Testing

- Logic driven testing requires examination of the internal structure of the program. 
- This derives test data from an examination of the programs logic and often the neglect of the spec.
- Goal -  to establish for this strategy the analog to exhaustive input testing in the black-box approach. 
- The analog is usually **exhaustive path testing**
- **Exhaustive path testing** - If you execute via test cases all possible paths of control flow through the program, then possible the program has been completely tested.
- Exhaustive path testing appears impractical
- Every path in a program could be tested but the program might still be loaded with errors.
- It in no way guarantees that a program matches its spec.
- A program may be incorrect because of missing paths - method would not detect the absence of necessary paths.
- May not uncover data-sensitivity errors.





