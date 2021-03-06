# GoogleCodeLabs Tutorials Deployed To Static Web Apps

Create, build and deploy a Google Codelabs formatted tutorial to Azure Static Web Apps. For consistency, I'll going to explore using the [Markdown format](https://github.com/googlecodelabs/tools#ok-how-do-i-use-it) for creating the tutorial. I am using [this example](https://raw.githubusercontent.com/googlecodelabs/tools/main/sample/codelab.md) as guidance.


 * [Tutorial 1: Create & Deploy Codelab to SWA](deploy-codelab-to-swa.md)



## Key Resources

 * [GoogleCodelabs Tools Repository](https://github.com/googlecodelabs/tools)
 * [Publishing in Google Codelabs format](https://medium.com/@zarinlo/publish-technical-tutorials-in-google-codelab-format-b07ef76972cd)
 * [Codelabs Formatting Guide](https://github.com/googlecodelabs/tools/blob/main/FORMAT-GUIDE.md)
 * [Codelabs Google Group](https://groups.google.com/forum/#!forum/codelab-authors)
 * [claat Commandline tool](https://github.com/googlecodelabs/tools/tree/main/claat)
 * [Example PWA Codelab: Google Doc Format](https://docs.google.com/document/d/1E6XMcdTexh5O8JwGy42SY3Ehzi8gOfUGiqTiUX6N04o/edit)
 * [Codelab: Markdown Format Guidelines](https://github.com/googlecodelabs/tools/tree/main/claat/parser/md)
 * [Codelab: Create Landing Page](https://github.com/googlecodelabs/tools#how-do-i-generate-my-own-landing-page)
 * [Codelab: Create Custom View](https://github.com/googlecodelabs/tools#how-do-i-generate-a-custom-view)
 * [Codelab: Publish Codelabs](https://github.com/googlecodelabs/tools#how-do-i-publish-my-codelabs)
 * [Codelab Preview: Chrome Extension](https://chrome.google.com/webstore/detail/preview-codelab/lhojjnijnkiglhkggagbapfonpdlinji)


## Troubleshooting

```bash
Oryx was unable to determine the build steps. Continuing assuming the assets in this folder are already built. If this is an unexpected behavior please contact support.
Finished building app with Oryx

Failed to find a default file in the app artifacts folder (/). Valid default files: index.html,Index.html.

If your application contains purely static content, please verify that the variable 'app_location' in your workflow file points to the root of your application.

If your application requires build steps, please validate that a default file exists in the build output directory.
```

Added Placeholder index.html