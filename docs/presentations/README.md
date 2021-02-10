# Metal3 Presentations

## Goal

The motivation behind this initiative is to provide easy to use presentation
templates for Metal3 projects, which can then be imported and built-upon to
create presentation for Meetups, Conferences or any other platforms. This can
serve as a supplement to existing documentation for new users, and also help
spread the project by helping presenters save time and focus on their content.

## Framework

We are using the [Revealjs](https://revealjs.com/) framework to create the
presentation. To contribute a presentation please create a directory, at the
`meta3-docs/docs/presentations` path, with your files associated with the
presentation, for example :-

```bash
ls metal3-docs/docs/presentations/test-presentation
test-image1.png  test-image2-capi.png test-presentation.html test-
presentation.md
```

To use this with revealjs, follow these steps (for more details refer
  [here](https://revealjs.com/installation/#full-setup)) :

```bash
## Clone revealjs repository

cd ${to_your_presentation_directory} && git clone https://github.com/hakimel/reveal.js.git

## Optional steps

cd reveal.js && npm install
npm start
```

Now you can simply edit the presentation html, markdown files to build upon the
presentation

For exporting the presentation in pdf format, you can use
[decktape](https://github.com/astefanutti/decktape#install), for example :

```bash
decktape reveal test-presentation.html test_deck.pdf
```

Exporing to .odp or .pptx formats is not supported but
this [issue](https://github.com/hakimel/reveal.js/issues/1702) might help.

## Example

Lets see this example of the `metal3-overview` presentation.
First, let's see the list of files under the `metal3-overview` directory :

```diff
tree metal3-overview/

metal3-overview/
├── metal3-components.png
├── metal3-integration-capi.png
├── metal3-overview.html
└── metal3-overview-slides.md
```

* `metal3-overview.html` : this file is rendered with revealjs to create the slides
* `metal3-overview-slides.md` : this file contains the slides' content and is used by the the above `.html` file
* `.png files` : images that we created to be used in the slides

In this example we have used an external markdown file for slides' content via
`<section data-markdown="metal3-overview-slides.md">`, but we can also include
that inline by leaving the field empty like `<section data-markdown>`.
There are variety of features available in the revealjs framework, for detailed
documentation visit [revealjs official website](https://revealjs.com/).
