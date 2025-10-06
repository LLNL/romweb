# romweb

This repo contains the libROM website [MkDocs](http://www.mkdocs.org/) sources.

To make changes to the website:

- use MkDocs v1.0.4 with Markdown v2.6.8, PyYAML v3.13 and futures v3.3.0, e.g.
  * `pip install --upgrade --user mkdocs==1.0.4`
  * `pip install --upgrade --user Markdown>=3.5`
  * `pip install --upgrade --user PyYAML==3.13`
  * `pip install --upgrade --user futures==3.3.0`
- clone this repo,
- edit or add some ```.md``` files (you may also need to update the ```mkdocs.yml``` config),
- preview locally with ```mkdocs serve``` (Windows users may need to specify a port, such as ```mkdocs serve --dev-addr 127.0.0.1:4000```),
- publish with ```mkdocs gh-deploy```.

To run the website locally:
 
- Clone the repo
- In the parent directory of the repo, run 'python3 -m venv web'
- 'source web/bin/activate' for bash or 'source web/bin/activate.csh' for tcsh. You must make sure you are in the 'web' virtual environment which you can see on the left side of your terminal as (web) to run the website locally.
- pip install mkdocs
- Go into the directory of romweb
- mkdocs serve
- When you run mkdocs serve, you should see a line that looks like: "Browser Connected: http://127.0.0.1:8000/"
- You can open up another terminal, run ‘firefox’ and type in that link and you will be able to see the webpage along with any changes you’ve made the repo.

Checklist for adding examples:

- Add an image file in `src/img/examples/`, e.g. `src/img/examples/poisson.png`
- Add a brief description in `src/examples.md` following the description at the top of the C++ file
- Add a "showElement" line with the appropriate categories for the example in the `update` function at the end of `examples.md`

