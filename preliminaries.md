# Preliminary notes

**20 February, 2017**

Notes for using *Markdown*, *pandoc*, *Git*, *GitHub*.

## Create documents using Markdown

1. Create *Markdown* text document with extension `.md`. This can be done in a text editor (terminal) or in a program such as [MacDown](https://macdown.uranusjr.com)
2. An `.md` document will be automatically rendered as html in GitHub. 
3. Alternatively you can render an `.md` document as HTML either by exporting as HTML from *MacDown*, or by using `pandoc` from the terminal. For example:

`pandoc --from markdown --to html preliminaries.md --output preliminaries.html`

or

`pandoc --from markdown --to latex preliminaries.md --output preliminaries.pdf`

And to get a Word document:
`pandoc --from markdown --to docx buzz-pollination.md --output buzz2.docx`


## Creating and working with repository in GitHub

You can start by creating a new repository in GitHub. This is the easiest.
You can also create a repository directly in the terminal and then uploading it to GitHub.

For this course I created a repository called **unicamp-course**.

Either way, working in a GitHub repository usually involves the following steps:

1. First you need to create a file. Since youa re likely doing this in your computer, this will create a file that will be placed in the *local* repository.
2. You need to *add* that file to the list of tracked files in your project. 

	`git add filename`
	
	Everytime you edit this file you need to *add* it again.

3. Then you have to *commit* the file, which means that the changes in this file are set to be uploaded in the remote repository in GitHub:
	
	`git commit -m "comment-here"`
	
	Comments are required to keep track of the changes made in each commit. This is recorded in your GitHub project.
	
4. Then you need to upload the changes into the remote repository:
	
	`git push`

	
	
