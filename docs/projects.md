# Project management

Neural network models are organized into projects.  A project contains all of the components needed to build
the neural network model, including any external libraries used, along with whatever training data, pre-trained
weights, and documentation you provide.  From the [projects repository page](#projects-repository-page), you
can search for projects that interest you, and examine the contents of the project.

If you are logged in to your [PrototypeML account](concepts.md#prototypeml-accounts), you can also [create
projects](#project-creation), [edit project settings](#editing-project-settings), [fork a
project](#forking-a-project) (make a copy of a project that you can edit), [star a
project](#starring-a-project) (rate the project), build a project [Readme file](#the-readme-file), [tag the
project](#project-tags) with appropriate categories to make it easier for others to find your work, and
finally, you can [delete a project](#deleting-a-project) you no longer want.

## Projects Repository Page

To reach the projects repository page, click the Projects link from the main menu on the PrototypeML website.
On the projects repository page is a sampling of some of the projects that have already been created by people
in the PrototypeML community, sorted by popularity ("Greatest") by default.  You can also sort by "Latest" to
see the newest projects, using the "Sort-By" drop-down menu.  If you're logged in to your PrototypeML account,
you will also see a "Show" drop-down list, where you can select either "All Projects" (the default), which
displays all projects contributed by the entire PrototypeML community); or "My Projects", which displays only
your projects.

Using the left sidebar on the page, you can search for projects that might interest you, using either free-text
search, or by category (tag).  To search by free-text, just type the desired search string into the search
box, and click the magnifying-glass icon (or hit &lt;Enter&gt;).  Free-text search looks for the search string
in project names and project descriptions.  To search by tag, just click the desired tag.  You can specify
*both* a tag and a free-text search string, in which case you will be shown projects that match both criteria,
that is, they have been tagged using the specified tag, *and* they match the search string specified.  To
clear a search, click on "All Tags" *and* delete the search string from the search box.  If you're viewing
only your projects, these search tools are used to search only your projects.  To search through all projects,
select "All Projects" from the "Show" menu.

## Project creation

To create a new project, click the "New Project" button on the [projects repository
page](#projects-repository-page). You need to specify a name for the project, a description, and one or more tags
(categories). These will help other people find your work. Click "Submit" to finish creating the project.

After the project has been created, PrototypeML displays the project page for your new project.  Running
across the top are the name of your project; the version number (set to "Dev" initially, but you can [create a
numbered version release](#creating-a-release) later; the number of [stars](#starring-a-project) your project
has been given by the PrototypeML community (yes, you can star your own project!); the number of times your
project has been [forked](#forking-a-project), an ["Edit Model"](models.md) button, and drop-down menu of
additional operations (marked with a "gear" icon) from where you can [create a new
release](#creating-a-release), [edit your project settings](#editing-project-settings), or [delete the
project](deleting-a-project).

Below this top line are three or four tabs, one labeled "Model" (the default), one labeled "Releases", which
won't appear until there are [versioned releases](#creating-a-release] of the model, one labeled "Issues", and
one labeled "Model Weights".  The "Model" tab shows the top-level components of the project, including any
[mutators](concepts.md#mutators), [blocks](concepts.md#blocks), and [files](concepts.md#files). When you first
create a project, only the [Readme file](#the-readme-file) is shown.

The "Issues" tab (coming soon) is for users of your project to post problems or questions about your project,
and your replies to their posts.

The "Model Weights" tab (coming soon) is for you to post pre-trained weights, if appropriate, for your
network, to allow people to use your project out-of-the box, without training, to apply to some machine learning
application.

## Editing project settings

To change the project name, the description, or the tags associated with your project, open the project page
for your project, click the "gear" icon, and select "Edit Project Settings".  These are the same settings you
had to provide when you first created the project.

## Forking a project

To make a copy of any project (including your own), click the "Fork" button on the page for that project.  You
will be asked to specify a name for that copy (fork) of the project, and it will be added to your list of
projects.  The forked version is a snapshot made at the time it was forked; this snapshot is *not* updated
automatically when the original project is changed.  You can edit this copy of the project.

## Starring a project

You can also rate a project, by assigning it a [star](projects.md#starring-a-project), giving recognition to
the author.  Yes, you can "star" your own project!

## The Readme file

The [Readme file](concepts.md#the-readme-file) is a [Markdown](https://daringfireball.net/projects/markdown/) file in
which you should put a description of your project, along with instructions on how to use it, and any other
information a user of your project would find helpful, including links to relevant material.

## Creating a release

Be default when you create a project, the version number of your project is set to "Dev".  To allow other
people to have a stable version of your project to use, with specific functionality you have defined, you can
create a copy of the Dev branch of your project and assign it a version number using [semantic
versioning](https://semver.org/spec/v2.0.0.html) [coming soon].  People can then include that specific version
of your project in their projects.  Creating a versioned copy of a project is called "creating a
release".  The versioned copy **cannot** be changed.

To create a release, find the drop-down menu of additional operations (marked with a "gear" icon) on the page
for the project you want to release, and select "Create New Release".  The pop-up form requests a version
number, which should conform to the [semantic versioning](https://semver.org/spec/v2.0.0.html) specification.
You also need to enter some release notes telling users what is new or changed in this release.  Once you
create a release, a fourth tab ("Releases") will appear on the page for that project, listing all of the
releases; clicking on a version number will display the notes for that release.

## Deleting a project

If you want to delete a project you created, find the drop-down menu of additional operations (marked with a
"gear" icon) on the page for the project you want to delete.  Select "Delete Project" from the menu. A
confirmation box will appear requiring you to verify that you do indeed want to delete the project. Click "Ok"
to delete the project.  Project deletion is irreversible, that is, projects cannot be "undeleted", so be sure
you really want to delete the project first.  Note that deleting a project will **not** remove it from other
projects that have already used it.

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
