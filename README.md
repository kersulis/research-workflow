# A research workflow
*Jonas Kersulis*

##  What is research?
If you suddenly disappear (read: graduate), would someone be able to understand the work you've done? What would that work consist of?

* Technical/communication work
    * Scratch notes
    * Semi-formal documentation
    * Research papers
    * Posters
    * Presentations
* Practical work
    * Source code
    * Input data for code to work on
    * Scripts for running code on data
    * Output from code execution
    * Figures to help interpret results

These categories are distinct yet often inseparable. A certain script file may load data, call source code to generate output, and generate a figure for inclusion in a research paper. The pieces must be kept organized yet together.

## Organization
Here's a master directory for a project I've been working on:

```
temporal-instanton/
```

Now give each type of research output a place:

```
temporal-instanton/
    nb/
    src/
    data/
    images/
    papers/
    posters/
    presentations/
```

Let's look at each directory. 

### Notebook directory: `nb/`
Here is the February portion of my notebook directory:

```
nb/
    2016-02-03-change-line-data-input.ipynb
    2016-02-04-updating-figures.ipynb
    2016-02-05-normalized-performance-figure.ipynb
    2016-02-09-abstraction.ipynb
    2016-02-10-new-interface.md
    2016-02-18-clean-start.md
    2016-02-22-parametric-analysis.ipynb
    2016-02-22-translation-revisited.ipynb
    report-2016-01-19.ipynb
```

Each file is a [Jupyter notebook][1]. The naming scheme ensures the most recent notebook is always at the bottom (reports being the exception). I make the file names as long as they need to be to ensure I can reliably guess their contents a few months later. Each notebook whose name begins with a date represents work on a particular feature or exploration of a certain topic. The contents are flexible -- some notebooks are heavy on written documentation, others contain only code, and still others contain a little of everything. I create`report-` notebooks less frequently; they contain semi-formal documentation that summarizes several scratch work notebooks. Report notebooks are often created to be shared with my advisor, and pieces of them tend to make it to research papers.

### Source code directory: `src/`
`src/` contains all source code. Mine is a little cluttered right now, but here's what I wish it looked like:

```
src/
    TemporalInstanton.jl
    dataload.jl
    solvetmpinst.jl
    matrixbuilding.jl
    manipulations.jl
    plot.jl
    powerflow.jl
    thermalmodel.jl
```

Without going into painful detail about the handful of files here, I'll just mention the role each plays. `TemporalInstanton.jl` defines a Julia module, making it easy to load all the other code with one command. `dataload.jl` contains functions used to translate raw data (from, say, [MatpowerCases][2]) into input my algorithm can accept. `solvetmpinst.jl` contains those functions that implement the actual algorithm (these are kept outside `TemporalInstanton.jl` to keep that file brief and easier to read). `matrixbuilding.jl` contains functions that turn input data (mostly vectors) into matrices defining an instance of a quadratically-constrained quadratic program. `plot.jl` is self explanatory. `powerflow.jl` contains functions used to process input and output data to interpret them in terms of injections and flows. `thermalmodel.jl` does the same thing for transmission line temperatures.

One key benefit of developing all source code in one directory is version control. You can use git to track changes to your code and push everything to a remote ([here's][3] a good remote option for umich students). Every time you get important results or generate a useful plot, you can record the most recent commit hash. Later on you can reproduce your results by returning to that commit.

### Data directory: `data/`
My `data/` directory is kind of cluttered, but that's also its purpose. Keeping an algorithm implementation separate from data used to test it is essential for code reuse and portability. An important tip in the context of `data/`: strive to use plaintext rather than binary files wherever possible. A .csv or .txt file is better than a .jld or .mat file. It is to your great credit if someone else can inspect and understand your datasets using just a text editor, without firing up Julia or MATLAB.


### Images directory: `images/`
So yeah, I put all the images here. When the time comes to polish and image and include it in a paper, poster, or presentation, I copy it to that paper's directory, which brings me to the remaining three directories.

### Papers, posters, and presentations
Each paper, poster, or presentation I produce in conjunction with a particular project gets its own folder. Each of these folders is self-contained so I can transfer everything needed to regenerate or modify a paper or presentation (including .tex files, images, etc.) by copying one directory. I nest these folders in directories called `papers/`, `posters/`, and `presentations/`.

Here are the contents of my `papers/` directory:

```
papers/
    conference-powertech
    journal-transactions-power-systems
```

The contents of `journal` and `conference` are pretty typical of LaTeX directories. There are .tex and .bib files, a folder for images, and all those silly auxiliary files LaTeX really shouldn't generate but does anyway just to bother us. `posters/` and `presentations/` are similarly self-explanatory.


[1]: https://jupyter.org/
[2]: https://github.com/kersulis/MatpowerCases.jl
[3]: https://gitlab.eecs.umich.edu/users/sign_in
