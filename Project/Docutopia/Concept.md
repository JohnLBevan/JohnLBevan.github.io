# Docutopia

## An architectural approach to documentation

For discussion, please see related [Hacker News Thread](https://news.ycombinator.com/?tbd).

### Background

I work for a large company with a mix of monolithic off-the-shelf applications, bespoke micro-services, and everything in between; like many large companies.  Our documentation (both technical and user facing) is fairly unstructured; teams will create documents they feel are useful; then in some cases email that document to the current users and forget about it, in others put them on one of several SharePoint/intranet sites, will write the documents in Confluence, or will write markdown inside the project's GitHub repo, but with that being unpublished / just browsable via the repo.

There has to be a better way... Does anyone have one?

### Proposal

Here are some of my thoughts on what a good solution may look like... It's quite similar to how one may approach micro-service architecture:

- Use markdown; it helps you focus on content over style when writing and is simple enough for non-technical folk to contribute to.
- Use git; this keeps things versioned, allows you to work with multiple branches to cater for how your system behaves (e.g. so you can have documentation for new features/changes progress alongside those features' own progress through your SDLC process).  This isn't great for non-technical users, but most people involved in creating this documentation are likely to be fairly techy; and you can provide a "1-page cheat-sheet" to present them with all they'd need for the standard workflow.
- Present the documentation on a website; e.g. as HTML; so users don't hold out of date copies.
- Have a publish pipeline; as documentation is updated, those updates appear in the published version.  This pipeline will perform various activities to convert the markdown to its presentable format.
- Diagrams should be written in code/markdown; e.g. https://medium.com/technical-writing-is-easy/diagrams-in-documentation-markdown-guide-4e78419e8d2f.  
- Code for diagrams should be contained in separate files and imported into documents where needed.  This allows the diagrams' code to be dynamically generated if required, for any functionality required to support that flavour of markdown to be focussed on that sole use case (e.g. not have to work out what's diagram vs what's part of the documentation's markdown), and increases the reusability of the content.
- Each markdown file should follow the single responsibility principal.  They should have markers showing where to import other markdown files so that the published document is built up of a collection of these files.
- The documentation should be spread across multiple repositories.  Dependencies can exist between repositories / should be managed by a package manager.  This allows you to have your generic IT tasks (e.g. how to create a mapped drive in Windows) documented in one repo, then referenced from repos which are focussed on 
- Styles should be held in a separate repo to markdown; content should have no awareness of style.  The publish pipeline brings content and style together.
- Images / binary content should be stored in the same repo as the markdown referencing it.  Where a relationship exists between repositories (e.g. OurProductDocs references CommonWindowsTaskDocs) there should be no direct reference to binary content; rather to import an image from the other repository the markdown pointing to that image should be referenced; bringing the image with it.  This approach effectively means images/binary content is treated as private / is accessed via the public properties of the markdown files.  This ensures that context can always be included alongside the resource.

### Feedback

- How does that sound / is anyone doing similar today?  
- Are there tools which could help with this process?  
- Are there pieces you'd add / remove / dispute?

Please share your thoughts here: [Hacker News Thread](https://news.ycombinator.com/?tbd).
