

# yarle: Yet Another Rope Ladder from Evernote

A tool that converts enex note(s) into Markdown format in order to let you escape from Evernote universe with all your belongings.

## Features:

- Works with enex files that contain single or multiple notes also.
- Works with notes that contain pictures too.
- Puts `title`, `creation time`, `update time`, `tags`, and `latlong` meta-information into md as metadata.
- Updates md files' access and modification timestamps according to the notes' update time.
- Organizes all attachments into a _resources subfolder (to keep the notes' folder as simple as possible).

## Installation

 - [install Node.js](https://nodejs.org/en/download/). Please use Node 10.18.1 because of 3rd party dependencies rebuild problems. 
  
 - clone or download this repo
 - npm i
 
## Usage:

Those markdown notes that contains external resources such pictures or files, are stored in `/<outputDir>/complexNotes` subfolder, the simple plain-text ones go to `/<outputDir>/simpleNotes` folder.

## Options:

 - ```--enexFile=<your-enex-file>``` , specifies the exported Evernote notebook
 - ```--outputDir=<relative_output_dir>``` , this is the main output dir in where the extracted markdown files are going to be created
 - ```--include-metadata``` , if it's set, then every markdown file will be extended by metadata (tags, time of creation, time of last update, lat-lon coordinates) 
 - ```--zettelkasten``` , puts Zettelkasten Id (based on time of creation) at the beginning of the file name
 - ```--plaintext-notes-only``` , skips those notes, which has attachment, or picture in it.
 - ```--wikistyle-media-links```, links are generated in wiki-style
 - ```--skip-latlng```, does not include location into metadata section
 - ```--skip-creation-time```, does not include creation time into metadata section
 - ```--skip-update-time```, does not include update time into metadata section
 - ```--skip-tags``` , does not include tags into metadata section
       

### Using cmd: 
```shell
  npm run start -- --enexFile=GeneralNotes.enex --outputDir=./out --include-metadata --zettelkasten --plaintext-notes-only
```

### In program: 

```javascript
 const options: YarleOptions = {
        enexFile: 'enexFile',
        outputDir: 'outputDir',
        isZettelkastenNeeded: true,
        isMetadataNeeded: false ,
    };
 yarle.dropTheRope(options);
```

## Release notes

### Version 2.3.0

 - Skipping parts of metadata in configurable via options
  
### Version 2.2.0

 - Links are generated in wiki-style links ([[link]]) if `--wikistyle-media-links` option is set
 - Bugfix: Notes with single resources are exported fine 
 - Codebase refactored


### Version 2.1.1

 - Conversion of tables, lists, numbered lists and checkboxes are supported.

### Version 2.0.4

 - plaintext-notes-only command line argument added, that enables you to skip converting notes with any resources, pictures, pdf, etc.

### Version 2.0.1: 

 - The whole tool is reimplemented in Typescript
 - ZettelKasten ID is an option for filename generation (format is <id>|(pipe) <title>.md or <id>.md if there is no title)

### version 1.2.0, fixes and improvements:

- File name conventions changed (whitespaces are generated instead of underscores)
- Metadata is moved at the end of the text and transformed as code snippet (looks better in Ulysses)
- Fix on HTML to MD conversion (turndown package is configured better to do not add multiple newline characters )