# How to Edit the Draft for Publication

In each sub directory, you can find the relevant files for the publication process.
In general, you should always consult the W3C Guide page at <https://www.w3.org/Guide>.

## Checklist

* Make sure that you update the recent specification changes
* For Proposed Recommendation Transition, create an issue at X.

## Files

* Overview.html - static HTML for publication
* diff.html - diff between the [previous published version](https://www.w3.org/TR/2023/CR-wot-thing-description11-20230119/) and Overview.html
* index.html - same as the index.html at <https://w3c.github.io/wot-thing-description/> ([or at the root of the repository](../index.html)), except for changing the respec option from ED to the version you are aiming at such as CR, WD, etc.
* static.html - static HTML generated by ReSpec from the index.html above
* testing folder contains the implementation report from the [testing folder](../testing/report11.html) of the repository. 
* visualization folder contains pngs of the images from the editor's draft

## How to Generate Each File

Overview.html is generated as follows:

1. Copy index.html from [the root of the repository](../index.html). Add errata link.
2. Change `specStatus` to `"NOTE"` from `"ED"` (or `"REC"`, `"PR"`, etc.).
3. Generate static.html by ReSpec from <https://w3c.github.io/wot-thing-description/> (click "ReSpec" top right and choose "Export" then export as "HTML"). Make sure that you disable browser extensions or open in private window.
4. Output Overview.html as a result of [HTML Tidy](https://www.html-tidy.org/). Use the following command (`tidy -ashtml -i static.html > Overview.html`). The `-ashtml` option is needed until [this issue](https://github.com/htacg/tidy-html5/issues/660) is resolved at HTML Tidy.

## How to Add your Edits based on the Pubrules Errors and Warnings

After checking Overview.html using the [Pubrules checker](https://www.w3.org/pubrules/), we have to edit index.html and then
regenerate the static HTML based on the procedure above to make it easier to generate a Pull Request to update the original
at <https://w3c.github.io/wot-thing-description/> later.

1. Edit index.html,
2. Generate static.html by ReSpec from the index.html (click "ReSpec" top right and choose "Export" then export as "HTML",
3. copy static.html to Overview.html and tidy it up,
4. If there are any remaining errors/warnings with the Pubrules checker results, repeat the edit by going back to #1.
5. Generate diff.html via <http://services.w3.org/htmldiff>

* Note1: You cannot use a tool like <https://htmlpreview.github.io> since they do not have static html as a resource that the pubrule
checkers can use.
* Note2: You can use the validator in a CLI environment. See <https://validator.github.io/validator/#usage>

## Manual Link Corrections

Some redirects come from [specref](https://www.specref.org/) not being up to date. In those cases, you need to manually update the final Overview.html.

*s None

## Converting Automatically Generated SVGs to PNGs

All SVG files under [visualization](../visualization) are generated automatically when running the `npm run render` command.
Before publication, PNGs version of the figures should be generated.
A tool like [Inkscape](https://inkscape.org/) can be used to do that.

* You should not add or remove any element, or change types of vocabulary terms unless the automatic figures have a bug due to toolchain
* You can adjust the overall organization of the elements by moving them around. This should be done to have a better layout, e.g. split a very long horizontal picture into two levels.

## REC Version Extras

When publishing the REC version, you need to do additional steps:

* Move a static version of all ontology files, the context file, and schemas to [wot-resources](https://github.com/w3c/wot-resources) repository following the rules there. Before you do that make sure to:
  * Check for respec errors in the HTML version of the ontologies
  * Set static publication date for ontology HTML versions
  * Check for the date or version within JSON Schema files
  * Generate static versions of the ontology HTML files
  * Generate tidied versions of the ontology HTML files
