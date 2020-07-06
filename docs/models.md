# Editing Models

The neural network model editor is the core of PrototypeML.  It allows you to design a neural network model by
drawing the graph of the network, incorporating already-written components like the PyTorch library and
community-contributed [blocks](#concepts.md#blocks), [mutators](concepts.md#mutators), or other
[files](concepts.md#files), with (optionally) components you write. You create blocks using a drag-and-drop
interface, you drag desired components into the [block editor](#block-editor), then draw arcs using
point-and-click to connect the outputs of one component to the inputs of another, thus showing your desired
data flow.  You create mutators by writing Python PyTorch code using the [mutator
editor](#mutator-editor). You can also write code in other languages.

When you are satisfied with your model design, PrototypeML provides one-click code generation that outputs
human readable, easily debuggable and maintainable code for your model, on par with neural network libraries,
although of course the quality of the code exported largely depends upon the quality of the user-implemented
code.

**Important**: Changes to components are saved automatically as you type or draw; there is no "save" button.

## Overview of model editor

The model editor window has three main sections: the [library bar](#library-bar), which lists the components
in your model, and allows you to create new components, including adding components from other PrototypeML
projects and libraries; the [editor window](#editor-window), where you can create and edit blocks, mutators,
and other files; and the properties bar, where you can specify various properties of blocks and mutators.

### Library Bar

On the left-hand side of the model editor is the Library Bar, listing the components (blocks, mutators, files,
and package dependencies) currently in your project.  You can locate files in your project using the search
box, or by navigating the folder structure.

### Editor Window

In the middle of the model editor is the editor window displaying the contents of the current component
(block, mutator, or file) being edited.  When editing a mutator, the editor window displays
the [mutator editor](#mutator-editor).  When editing a block, the editor window displays the [block
editor](#block-editor).  When editing a file, the editor window displays the [file editor](#file editor).
Across the top of the editor window are tabs showing the names of the components currently being
edited. Clicking on a tab opens the component in the editor window, and changes the properties bar contents to
display the properties of that component.

### Properties Bar

The properties bar displays various properties of the current block or mutator being edited, and allows you to
set or change those properties.

## Using the Library Bar

The library bar is where you can create new mutators, blocks, or files for your project, or incorporate
libraries or components from the PrototypeML project repository.  It is also the place where you initiate
editing any of those components. At the top of the library bar is a search box, where you can search through
your components located anywhere in your PrototypeML directory structure.  Below the search box is a blue
"Add" button, which when clicked, brings up a drop-down menu of items you can create or add to your project:
block, mutator, folder, file, or package dependency.

### Creating components

Selecting block, mutator, folder, or file from the "Add" menu in the library bar creates that new component in
the current directory of your project.  A pop-up window requests the name of your new component; enter the
desired name, and click "Ok" to finish creating the new component.  Blocks, mutators, and files can then be
edited by clicking on the component in the library bar.  When creating a file, you are asked to select a file
type, one of (.py, .txt, or .md).

Folders can be renamed or removed, as desired, by clicking the 3-dot icon in the folder, which displays a
pop-up menu of those choices.  Select rename or remove, as desired. Rename displays a pop-up window allowing
you to edit the name; click "Ok" when done.  Remove displays a pop-up window confirming that you really want
to remove the folder; click "Ok" if you want to remove the folder.  Folder removal is irreversible.

### Adding a package from the projects repository

Selecting "Package Dependency" from the "Add" menu in the library bar allows you to add any project from the
projects repository to your project.  Unlike when you add a block, mutator, file, or folder, package
dependencies are added to a special folder at the root (`/`) of your directory structure, the Packages folder.
When you choose to add a package dependency, a pop-up search window appears, allowing you to search the
repository using free-text, or by tag, or by choosing a project from the complete list, which is displayed
sorted either by most-liked, or by date (newest first). Selecting a package from the list opens a project page
for that project, showing the complete list of components, including [blocks](concepts.md#blocks),
[mutators](concepts.md#mutators), [files](concepts.md#files] (including the [Readme
file](projects.md#the-readme-file)), and [folders](concepts.md#folders); a bar across the top allows you to
select a version (set to "Dev" by default), to [star](projects.md#starring-a-project) the project, or to "Use"
the project.  When you click "Use", the project is added into the "Packages" folder in your project's root
(`/`) directory.

### Adding components from your package dependencies

To insert a component from your package dependencies into a block, first click on the block in the library bar
to open up the block editor.  Then from the library bar, navigate to the package and then component you'd like
to add, and drag it into the code graph.  Connect the input and output ports, specify the properties, and
you're done.

### Organizing your project

You can use [folders](concepts.md#folders) to organize your project.  Just as you would for any project, you
can keep related files including mutators, blocks, and other files together in a single folder.  You can nest
folders, as well.

## Mutator editor

To edit a mutator, click on the mutator in the library bar.  The code for the mutator will appear in the
[editor window](#editor-window), and its properties will appear in the [properties bar](#properties-bar).

### Program sections of a mutator

The mutator editor window is divided into several sections.  The [imports](#imports) section is where you
write Python import statements for libraries and files (modules) needed by your mutator.  The [init](#init)
section is where you write Python code for the `init` routine of your mutator.  The [forward](#forward)
section is whee you write Python code for the `forward` routine of your mutator.  Finally, the [additional
functions](#additional-functions) section is where you write other Python code that your mutator will need, if
any.

### Properties of a mutator

Mutators have several properties (attributes): name, default repeat count, input and output [ports](#ports),
parameters, and Python package dependencies.  The default repeat count specifies the number of times this
mutator will be repeated at execution time. The input ports are the input arguments to the mutator.  The
output ports are the output arguments from the mutator.  Parameters are constants that can be defined
differently for each use (instance) of the mutator, for example, `kernel_size`, `stride` or `dilation`.

#### Default Repeats

Repeating a mutator means to take the outputs of the mutator and feed them back into the inputs of the
mutator.  Not all mutators can be repeated: The mutator has to have the same number of inputs as outputs, and
they have to be compatible.  The default repeat count specifies the number of times the mutator should be
repeated, by default.  This default can be overridden when the mutator is used by changing the
[repeat](#instance-repeat) count property of the mutator instance.

#### Ports

The input and output ports of a mutator are the connection between the data flow shown in the code graph and
the actual code. Every mutator has at least one input port and at least one output port.  You can define more
than one input or output port.  The ports are displayed as large dots on the mutator icon shown in the code
graph. By default, the input port is named "input" and the output port is named "output", but these can be
modified by clicking the "pencil" icon next to the port and entering a different name in the pop-up form.

Additional input and output ports can be added by clicking the "plus" icon next to "Ports", which will display
a pop-up form.  Enter the desired name for the new port, specify whether it is an input port or an output
port, and click the "Add Port" button.

Code within a mutator accesses input and output port values using [magic variables](#magic-variables].

#### Parameters

To make reuse of mutators easier, input parameters can be defined, which can be specified differently for each
instance (use) of the mutator.  Code within a mutator accesses parameter values using [magic
variables](#magic-variables].

Parameters can be added by clicking the "plus" icon next to "Parameters", which will display
a pop-up form.  Enter the desired name for the new port, which will help form the identifier used within the
code to access the parameter value; the prompt is the string displayed in the properties of any instances of
the mutator requesting a value for the parameter; indicate whether the parameter is required or optional, and
specify a default value for the parameter, if one. Click the "Add Parameter" button to create the parameter.

#### Python packages

Here you can specify any Python packages (dependencies) required by the mutator.  PrototypeML will create
installation scripts to install those packages on your development machine.

Python package dependencies can be added by clicking the "plus" icon next to "Python Packages", which will
display a pop-up form. Specify how the dependency should be installed, ie. via "pip", "conda", "conda-forge", or
"other". If you choose one of the known package repositories, then you also need to enter the installation
string.  If you choose "other", then you need to enter a download URL for the package.

### Imports

This section is where you write Python `import` statements for libraries and files (modules) needed by your
mutator.  If you specify paths in any of the import statements, they should be relative to the project root
directory, shown as `/` in the path shown near the top of the library bar.  Standard libraries like PyTorch or
NumPy don't need paths, e.g.

    import PyTorch
    import NumPy

But, for example, if you have a file `bluefin.py` located in the `/tuna` subdirectory of your project, and you
want to import it, you would write:

    import tuna/bluefin

### Init

This section is where you write the initialization code for your mutator.  Since all of the `init` sections
from all mutators in a block are concatenated into a single `__init__` routine in the class of the block
containing the mutator, all definitions (and therefore, uses) of constants, variables, and functions within
the `init` routine must be unique to each instance of the mutator.  This is accomplished by means of [magic
variables](#magic-variables).

In addition, you access the values of input and output ports, parameters, the repeat count for the mutator,
and the repeat_index (which indicates which iteration of the repeat count you are currently executing) via
[magic variables](#magic-variables).

Magic variables that access the values of input and output ports and parameters are NOT accessible
within the `forward` routine of a mutator, so if you need access to these values within `forward`, the `init`
routine will need to save them to class variables.

#### Magic variables

Magic variables provide programmatic access to the inputs, outputs, and parameters of a mutator.  The actual
values for these magic names are substituted during code-generation. Here are the available magic variables:

* `${params}` - This is a list of all parameters to a given mutator or block.<br>
   Usage example:
~~~
    ** Fill this in **
~~~

* `${params.<name>}` - This has the value of parameter with name `name`.<br>
   Usage example:
~~~
    if (${params.kernel_size} > 1000):

    # If kernel_size parameter is set to 2000, this will generate:
    if (2000 > 1000):
~~~

* `${instance}` - This is a unique string generated by PrototypeML for each instance of a mutator or block.
  You can use it to construct unique variable names in a mutator or block.<br>
   Usage example:
~~~
    dilation_${instance} = ${params.dilation}

    # If the dilation parameter is set to 1, this might generate:
    dilation_a2e43bcf = 1
~~~

* `${ports.<name>}` - This has the value of the port with name `name`.<br>
   Usage example:
~~~
    ${ports.output} = ${ports.input} * ${ports.weights}
~~~

* `${repeat}` - This has the value of the repeat count for the mutator or block.<br>
   Usage example:
~~~
    if (${repeat} > 20):

    # If repeat count is set to 40, this will generate:
    if (40 > 20):
~~~

* `${repeat_index}` - This has the value of the repeat index for a repeated mutator or block.  The repeat
   index varies from 0 to `repeat-1` inclusively.<br>
   Usage example:
~~~
    if (${repeat_index} == ${repeat}-1):
       (last loop iteration)
~~~

### Forward

This section is where you write the code for the PyTorch `forward` routine for your mutator.  Since all of the
`forward` sections from all mutators in a block are concatenated into a single `forward` routine in the class
of the block containing the mutator, all definitions (and therefore, uses) of constants, variables, functions,
etc. within the `forward` routine must be unique to each instance of the mutator. This is accomplished by
means of the `${instance}` [magic variable](#magic-variables).

In the `forward` routine, only certain [magic variables](#magic-variables) are accessible, specifically
`${instance}`, `${repeat}` (the repeat count for the mutator), and `${repeat_index}` (the loop index of the
current iteration in a repeated mutator).  If the `forward` routine needs access to other magic variables, the
`init` routine will need to save them to (unique, using `${instance}`) class variables.

### Additional Functions

This section holds any additional functions, that you want to add to the class.  It can contain
any other code that would be valid inside a class, and is inserted after the `__init__` and `forward`
routines.  To use functions you've written in the additional functions section, you need to
`import` them in the import section.

The `${instance}`, `${repeat}`, and `${repeat_index}` [magic variables]($magic-variables) are accessible
within the additional functions section.

## Block editor

To edit a block, click on the block in the library bar.  The code-graph for the block  will appear in the
[editor window](#editor-window), and its properties will appear in the [properties bar](#properties-bar).

From here, you can drag in new components from the library bar and add arcs to connect them to existing
components in the code graph; edit any of the block properties in the properties bar, or by clicking on a
component in the code graph, you can change the properties of that instance of the component in the properties
bar.  Clicking on an empty area of the code graph will change the properties bar to show the block properties
instead of the component instance properties.

Across the top of the editor window are icons that when clicked, let you zoom in or out of the graph; reset
the graph view (useful if parts of the graph are out of the window); format the graph, which prettifies the
components and arcs; switch to code view, to see the generated code for that block; and turn on or off the
"minimap" displayed at the upper-right of the code-graph, which shows you which part of the code graph is
visible in the editor window.

### Adding components to the code graph

There are three steps to add a component to the code graph:

1. Drag the component from the library bar onto the code graph

2. Drag arcs from the output(s) of other components to the input of the new component, and likewise, drag arcs
   from the output(s) of the new component to the input(s) of other components.

3. Set the properties of the new component, including how to combine two or more outputs connected to a single
   input port, if any

### Connecting components together (links, input ports, and output ports)

Arcs in the code graph show the data flow between components.  To draw an arc connecting a new component, click
on the output port of an existing component and hold the mouse down, then drag it to the input port on the
new component, and release the mouse.  Do the same from the output port of the new component to the input port
of an existing component.

You are allowed to draw two (or more) arcs to the same input port of some component.  In this case, you need
to define how the two data streams should be combined.  If you click directly on the dot representing the
input port, the properties tab of the editor will change to show the properties of that component instance. 

### Setting component instance properties
#### Instance name
#### Instance repeat
#### Instance comment
#### Instance parameters
#### Looping via Repeats
### Sorting graph
### Navigating within the graph (minimap, zoom)
### Attributes of a block
#### Ports
#### Parameters
#### Variables

## File editor
### Types of files