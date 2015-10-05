# Salesforce Static Developement Environments made Easy

## Build & development

### Initial Build & Pre Reqs

Pull down the code and switch to the branch:

`git clone https://mbowen000@bitbucket.org/mbowen000/smbblocks-angularvf.git`
`git fetch && git checkout che`

Install nodejs (tested on 0.12.0 on windows)

Run `npm install` to install all dev deps
Run `bower install` to get all the static deps

### Dev & Deployment

Run `grunt serve` for developer tasks. This will:

- Deploy a copy of the vfpage.page to vfpage_dev.page (this will be your development version)
- Stands up a local node server that hosts dev files
- Auto-reloads changes to dev files
  - Can optionally run `grunt serve:skipdeploy` to skip deployment of VF page to salesforce if you know its up-to-date.

Run `grunt buildSalesforce` to deploy to Salesforce. This will:

- Package all static resources in app/scripts, app/styles etc into Static resource (after minification and renaming)
- Deploy the static resource
- Process the HTML using usemin to reference new assets in the static resources
- Deploy a .page for your application

## Testing

Running `grunt test` will run the unit tests with karma.

## Salesforce Integration

### Current:
- Dev assets are linked va baseurl configuration
- Templates are put into a templateCache/ directory on the static resource server
- Basic angular w/ routing capabilities
- Deployable to 'real production' version w/ `grunt buildSalesforce`
- Minifies code to vendor.js and scripts.js and then includes the templates into static resource
- Can stand up development environment and make live changes to static files (and deploy .page files when server stood up)

### Future Items:

#### High Priority

- High priority: Watch changes to /views directory and use ngtemplate grunt task to rebuild templateCache.js

- High priority: Configuration: Developer name (so we can have multiple developers uploading vfpage_dev_mike.page vs. vfpage_dev_sal.page )

#### Low Priority

- Stop auto-loading index.html when server stands up

- Auto-reload salesforce page on dev changes... (!?!? could be awesome & very possible i would think)

- Low Priority: ditch ant metadata deployment and use Nodejs: https://github.com/tstachl/metaforce (can use metaforce and create grunt task that deploys - even does ZIP deploy!)

- Add yeoman custom scaffolding that will allow us to additional generate salesforce items automatically so that the visualforce page and static resource, in addition to what yeoman does now which is name the angular modules, etc. Eg.
  - All the module names would be dynamic
  - Page name would be dynamic (and dev page name)

- Initial setup for dev (copying VF page to salesforce) could be optionally ran once up front but then on would not re-upload unless forced? Have to think about this.

