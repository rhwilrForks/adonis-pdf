# adonis-pdf

Service provider for building PDFs using [pdfmake](http://pdfmake.org/).

:exclamation: **WARNING! This package is heavily in development and is therefore unstable. It may not work correctly or at all. When it is working the way that it needs to I will bump it up to 0.1.0!**

## Installation
* Run `npm i adonis-pdf` or `yarn add adonis-pdf`
* Add `'adonis-pdf/providers/PdfProvider'` to the `providers` array within `start/app.js`

## Configuration
Configuration is done through `config/pdf.js`. This file should have automatically been copied to your project during installation if you installed it via adonis-cli. If you installed it with npm or Yarn, or the file was not copied across correctly, you may copy the [config file](config/pdf.js) from this package or run the following command to create it:
```bash
adonis pdf:getconfig
```

By default all configuration options are `null` (i.e. we use the pdfmake defaults) but feel free to override them as per the [pdfmake documentation](http://pdfmake.org/#/gettingstarted):

| Option | Description |
|:---|:---|
| fonts | Customise the fonts used in your PDFs; if no fonts are specified this package will automatically load default Roboto fonts |
| styles | Custom style dictionaries allowing you to maintain consistent styles across each PDF |
| header | Custom header for each page within your PDFs |
| footer | Custom footer for each page within your PDFs |
| background | Custom background for each page within your PDFs |
| page.size | Set the page size to be used |
| page.orientation | Set the page orientation |
| page.margins | Set up the page margins |

## Usage
Add `const PDF = use('PDF')` to whatever file you wish to use it, then call `PDF.create()`. This method accepts two parameters:

* `content`: Array representing the PDF content
* `stream`: A Readable or Writeable Stream the PDF will be piped to

## Example
```js
'use strict'

const PDF = use('PDF')

class MyController {

  async generatePdf ({ response }) {

    const content = [
      { text: 'test' }
    ]

    PDF.create(content, response.response)

    return response
  }

}

module.exports = MyController
```
