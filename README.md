Minimal template of a gatsby blog hosted on Github pages where some pages can be authored on https://observablehq.com:
- Some pages contain interactive observable notebooks.  User can select which cells to include in what order using
- Some pages are created from a json file (`src/data/mydata.json`)

## Workflow

- Build a notebook on observabehq.com and publish it
- `yarn add` the notebook to this repo using e.g. `https://api.observablehq.com/@robinl/gatsby-test.tgz\?v\=3`
- run `refresh_notebooks.sh`
- add a new page to `src/pages` using `gatsby-test-2.js` as a template
- push code back to Github and site will build to master, which is then rendered as a github page

Note you can choose which named cells to include in the blog using `output_order` (see [here](https://github.com/RobinL/gasby_observable_blog/blob/dev/src/pages/gatsby-test-2.js) or leave it blank to include everything see [here](https://github.com/RobinL/gasby_observable_blog/blob/dev/src/pages/gatsby-test.js))

Cells which are views need to also include `viewof` e.g.
```
let output_order = [
    "first_cell",
    "viewof myview",
    "third_cell"
    ]
```


## Notes/Issues

- User must install the notebook from the version 3 runtime e.g. `yarn add https://api.observablehq.com/@robin
l/gatsby-test.tgz\?v\=3`.  This will make sure you can import `define` (rather than `notebook`) from the node package.  Some tangential discussion [here](https://talk.observablehq.com/t/runtime-v3-modules/1767).

- For some reason, the yarn integrity check fails for observable notebook modules when they're installed from the `yarn.lock` file on github actions (`Integrity check failed for "mypackage" (computed integrity doesn't match our records,`).  Current solution is to delete the `resolved` line from `yarn.lock`.  This happens automatically when you run `refresh_notebooks.sh`