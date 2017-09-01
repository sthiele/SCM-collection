# SCM-collection
Collection of posts related to reason over the transitional behavior of dynamic systems using sign consistency constraints

#### externalize tikz pictures
pdflatex -shell-escape paper.tex

#### latex from markdown
pandoc -o perturbations_g.tex perturbations.md 

#### latex 2 html
pandoc -o perturbations.html -s --webtex perturbations_g.tex


#### markdown 2 html
pandoc -o perturbations.html -s perturbations.md
