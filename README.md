# mfem / web

This repo contains the MFEM website [MkDocs](http://www.mkdocs.org/) sources.

To make changes to the website:

- use MkDocs v1.0.4 with Markdown v2.6.8, PyYAML v3.13 and futures v3.3.0, e.g.
  * `pip install --upgrade --user mkdocs==1.0.4`
  * `pip install --upgrade --user Markdown==2.6.8`
  * `pip install --upgrade --user PyYAML==3.13`
  * `pip install --upgrade --user futures==3.3.0`
- clone this repo,
- edit or add some ```.md``` files (you may also need to update the ```mkdocs.yml``` config),
- preview locally with ```mkdocs serve``` (Windows users may need to specify a port, such as ```mkdocs serve --dev-addr 127.0.0.1:4000```),
- publish with ```mkdocs gh-deploy```.

To run the website locally:
 
- Clone the repo
- Checkout the 'website-setup' branch.
- In the parent directory of the repo, run 'python3 -m venv web'
- 'source web/bin/activate' for bash or 'source web/bin/activate.csh' for tcsh. You must make sure you are in the 'web' virtual environment which you can see on the left side of your terminal as (web) to run the website locally.
- pip install mkdocs
- Go into the directory of laghosromweb
- mkdocs serve
- When you run mkdocs serve, you should see a line that looks like: "Browser Connected: http://127.0.0.1:8000/"
- You can open up another terminal, run ‘firefox’ and type in that link and you will be able to see the webpage along with any changes you’ve made the repo.



Checklist for adding examples:

- Add a one-line summary of the example in `features.md`
- Add an image file in `img/examples/`, e.g. `img/examples/ex1.png`
- Add a brief description in `examples.md` following the description at the top of the C++ file
- Add a "showElement" line with the appropriate categories for the example in the `update` function at the end of `examples.md`

To add a new Application / Finite Elements / Discretization / Solver category:

- Add an `<option>` tag at the top of `examples.md`, e.g.
  ```<option id="wave">Wave</option>```
- Use the `id` in filter expressions of appropriate examples in `update`, e.g.
  ```showElement("ex25", (maxwell || wave) && hcurl && galerkin && (gmres || ams));```

Checklist for adding miniapps:

- Consider adding a one-line summary of the example in `features.md` (if we want to advertise the miniapp to users)
- Add an image file in `img/examples/`, e.g. `img/examples/shaper.png`
- Add a brief description in `examples.md` following the description at the top of the C++ file
- Add a "showElement" line with the appropriate categories for the miniapp in the `update` function at the end of `examples.md`


