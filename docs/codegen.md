# Code generation

After you have edited all of the pieces of your project to your satisfaction, you can generate compilable code
for the project in one click of your computer mouse.  You can then build and run this code on your preferred
development machine.

Code generation proceeds as follows:

* A Python class is created for each block

* PrototypeML concatenates all of the mutator sections (import, init, forward, additional code) from each
  mutator in each block into a single set of `import` statements in the class, a single `__init__` routine,
  and a single `forward` routine. The additional code section is added to the class after the `__init__` and
  `forward` routines.

* Code is generated to implement repeat counts and activations

* All of the references to [magic variables](models.md#magic-variables) are textually substituted with the
  actual variables that will contain their values, including parameters, variables, inputs, and outputs,
  repeat counts, repeat indices, etc. and all references to input and output port values within each block are
  resolved.

This process is analagous to a linker concatenating the program sections from different objects and resolving
references.
