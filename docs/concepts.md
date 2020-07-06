# Concepts

This section introduces the main concepts in PrototypeML: [Neural networks as code
graphs](#representing-neural-network-models-as-code-graphs); [Projects](#projects); [Mutators](#mutators);
[Blocks](#blocks); [Files](#files); [Code Generation](#code-generation), and [PrototypeML accounts](#prototypeml-accounts).

## Representing Neural Network Models as Code Graphs

PrototypeML lets you design a neural network by drawing the graph of the network, incorporating
already-written components like the PyTorch library and community-contributed components, with (optionally)
components you write. Using a drag-and-drop interface, you drag desired components into the editor, then draw
arcs using point-and-click to connect an [output port](models.md#ports) of one component to an [input
port](models.md#ports) of another, thus showing your desired data flow.

Components can be repeated using a repeat count. You can define parameters to customize their behavior, and
commonly-used activations can be automatically applied to their outputs.

"Skip connections" are easily handled just by drawing an arc directly from the input of a graph of components
directly to the output.

Multiple outputs from different components can be combined automatically at the input to a following
component, either by concatenating them (you can specify the order and the concatenation dimension), or by
adding them.

Components can also be nested: Once you've created a component, you can reuse it within another component.

You can write your own components using any programming language you wish. PrototypeML provides specific
support for writing your own Python-based components that use PyTorch: You write the init and forward code, and
PrototypeML takes care of inserting parameters (if any), and connecting the inputs and outputs of your
component to other components in the graph.

When you are satisfied with your design, PrototypeML provides one-click code generation that outputs human
readable, easily debuggable and maintainable code for your model, on par with neural network libraries,
although of course the quality of the code exported largely depends upon the quality of the user-implemented
code.

## Projects

Neural network designs are organized into projects.  A project contains all of the components needed to build
the neural network model, including any external libraries used, along with whatever training data,
pre-trained weights, and documentation you provide.

To begin using PrototypeML, you first need to [create a project](projects.md#project-creation).  Then you can
add components to that project, either components you write, or components that come from another
project&mdash;which could be another one of your projects, or a project created by someone else.

All PrototypeML projects reside in a public project repository.  You can search for relevant projects by
category (tag), e.g. Computer Vision, Natural Language Processing, etc., or use free-text search.  Each
project has a Readme file describing the project. Once you find a project you're interested in, you can
incorporate components from the current version of that project, or you can specify an earlier version if you
wish, or specify a range of versions that are acceptable, using [semantic
versioning](https://semver.org/spec/v2.0.0.html) [coming soon]. You can also rate a project, by assigning it a
[star](projects.md#starring-a-project), giving recognition to the author.

Projects (including projects created by others) can be [forked](projects.md#forking-a-project), meaning a copy
of the entire project is made and the copy is added to your list of projects, where you can modify it.  You
can choose to fork the current version of the project, or you can specify an earlier version if you wish.  The
forked version is a snapshot made at the time it was forked; this snapshot is *not* updated automatically when
the original project is changed.

You can assign a version number to the current ("dev") version of any of your own projects by [creating a new
release](projects.md#creating-a-release).  Once you create a versioned release, that version of your project
cannot be changed.

While all projects are public and available for anyone else to use, please see the the PrototypeML [Terms of
Use](http://www.prototypeml.com/terms) for the details, there are requirements for using components from other
people's projects.

## Mutators

Mutators are the fundamental computational components of the neural network model. Mutators can be defined
once, and reused as many times in as many places in your neural network as desired.  To make reuse easier,
input parameters can be defined, which can be specified differently for each instance (use) of the mutator.

The aim of the mutator is to wrap all the code necessary to initialize and execute a specific segment of
functionality, such as a PyTorch layer, matrix operation, existing 3rd-party library or any arbitrary Python
code using the PyTorch `init()` and `forward()` pattern.  In your project, you can use mutators that you
write, or mutators you obtain from the PrototypeML [projects repository](#projects).

PrototypeML supports creating and editing mutators written in Python, following the coding model required for
use with Pytorch, for example, that every mutator contains an `init` routine and a `forward` routine.  The
specifics of how to use PyTorch are beyond the scope of this manual; they can be found in the [PyTorch
Documentation](https://pytorch.org/docs/stable/index.html).  You can also write mutators in other programming
languages, but PrototypeML does not provide editor support for them other than as text files <span
style="color:red">*** whose functions can be `imported` into other mutators?? ***</span>.

Any instance of a mutator can be executed repeatedly just by specifying a repeat count for the mutator
instance.  The outputs of the mutator instance are fed back in to the inputs, and execution is repeated the
specified number of times before allowing execution to continue to a downstream component.

In the code graph, a mutator is represented as a rectangle with labeled input ports (inputs) and output ports
(outputs).  Multiple outputs from upstream components can be combined at the input to a mutator instance,
either by concatenating them, or adding them.  If they are to be concatenated, the concatenation dimension
must be specfied.

You can easily apply any commonly-used activation to the output of a mutator instance, as well. Currently
supported activations include: ReLU, Sigmoid, Tanh, Softmax, and Softmax2d.

The [mutator editor](models.md#mutator-editor) is used to create and/or edit a Python/PyTorch mutator.  It
allows you to specify the imports, init code, forward code, and any additional code you need, as required for
using the PyTorch library.  Mutators can be written in other languages, but PrototypeML does not provide
editor support for them other than as text files.

## Blocks

Blocks contain code graphs whose nodes are [mutators](#mutators) and/or other blocks. Like mutators, blocks
can be defined once, and reused as many times in as many places in your neural network as desired. Blocks can
also define input parameters which can be specified differently for each instance (use) of a block.  Unlike
mutators, blocks can also define input variables, which can be arbitrary Python expressions and can use any of
the input parameters defined.

Like mutators, any instance of a block can be executed repeatedly just by specifying a repeat count for the
block instance.  The outputs of the block instance are fed back in to the inputs, and execution is repeated the
specified number of times before allowing execution to continue to a downstream component.

As with mutators, in the code graph, a block is represented as a rectangle with labeled input ports (inputs)
and output ports (outputs).  Multiple outputs from upstream components can be combined at the input to a block
instance, either by concatenating them, or adding them.  If they are to be concatenated, the concatenation
dimension must be specfied.

Also like mutators, you can easily apply any commonly-used activation to the output of a block instance, as
well. Currently supported activations include: ReLU, Sigmoid, Tanh, Softmax, and Softmax2d.

The [block editor](models.md#block-editor) is used to create and/or edit a block.  Using a drag-and-drop
interface, it allows you to you drag mutators or other blocks into the editor, then draw arcs using
point-and-click to connect the outputs of one component to the inputs of another, thus showing your desired
data flow.

Every project has an <span style="color:red">*** implicit?? ***</span> outermost block that contains all other
blocks and mutators in the project.

## Files

In addition to [mutators](#mutators) and [blocks](#blocks), your project can contain files, including Python
(.py), Markdown (.md), and text (.txt) files [coming soon: other types of files]. Any Python files are
included with the rest of the generated code when you click the [export code](#code-generation) button.
Mutators can *import* Python (.py) files contained in the project, using relative imports.  Files containing
code written in other languages can be made accessible to the project by turning the code into a Python
library and then *import*ing the library.

## Folders

PrototypeML provides you with a virtual directory structure in which to store your components.  The root of this
virtual directory structure is designated `/`, and new projects are created with only that folder.  You can
create as many folders inside `/` as you wish, and additionally, you can create folders inside folders.  Any
folder can contain any of the file types PrototypeML supports.

## Code Generation

After you have edited all of the pieces of your project to your satisfaction, you can [generate compilable
code](codegen.md) for the project in one click of your computer mouse.  You can then build and run this code
on your preferred development machine.

Code generation proceeds as follows:

* A Python class is created for each block

* PrototypeML concatenates all of the mutator sections (import, init, forward, additional functions) from each
  mutator in each block into a single set of `import` statements in the class, a single `__init__` routine,
  and a single `forward` routine. Additional functions are added to the class after the `__init__` and
  `forward` routines.

* Code is generated to implement repeat counts and activations

* All of the references within the code to properties like parameters, variables, repeat counts, and input
  &amp; output ports are resolved.

## PrototypeML Accounts

You will need to be logged in to your own account on PrototypeML in order to create and manage projects.  It
is free to create a PrototypeML account.  

If you do not already have an account on PrototypeML, click on "Login/Register" in the main menu on any page,
which will display a login form.  Click the "Create a new account" link below the login form. This will
display a registration form, allowing you to register using either your Github login (if you have one), or by
specifying new account credentials (username, login email address, and password) directly to PrototypeML. The
username is the name that will appear publicly on all of your projects.

If you register using Github, your PrototypeML username will be the same as your Github username, and you need
to login to PrototypeML using your Github credentials every time you wish to log in.

To login to an existing account, click on the "Login/Register" button in the main menu on any page, which will
display a login form. You may log in using either your Github login (if you used it when you registered), or
using your PrototypeML account login email address and password that you specified when you created your
PrototypeML account.  Fill out the form and click the "Sign In" button.
