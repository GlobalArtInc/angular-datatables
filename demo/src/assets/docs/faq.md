> Deprecation of "Angular way" usage

This was done to address few issues:

1. The usage of `*ngFor` and setting AJAX callback's `data` property as empty, we're essentially tricking the library to consider "non-existent" data. (non-existent because AJAX callback is called with empty array and totalRecords* values don't match)

2. It breaks DT extensions that perform additional data processing like exporting tabular data to a PDF or CSV, etc.

We have introduced better ways to allow same level of control over rendering your data via [TemplateRef](https://globalartinc.github.io/angular-datatables/#/advanced/using-template-ref) and [Pipes](https://globalartinc.github.io/angular-datatables/#/advanced/using-pipe)

> Error encountered resolving symbol values statically.

Please update your `tsconfig.json` as shown below. For more info, check the GitHub issue [here](https://github.com/GlobalArtInc/angular-datatables/issues/937)

```json
{
  "compilerOptions": {
    ...
    "paths": {
      "@angular/*": [
        "../node_modules/@angular/*"
      ]
    }
  }
}
```

> Columns do not resize when using ColReorder extension

Grab a copy of [this](https://github.com/shanmukhateja/adt-resize-col-demo) project, update it to suit your needs and see if it works.
If it won't work, check these similar issues:
- [#1496](https://github.com/GlobalArtInc/angular-datatables/issues/1496)
- [#1485](https://github.com/GlobalArtInc/angular-datatables/issues/1485)

If it still didn't work, open a GitHub [issue](https://github.com/GlobalArtInc/angular-datatables/issues/new) and we'll look into it. 

> Column data doesn't move with column header when re-ordering

It could be many things but in general it could be because you're using "Angular way" to display data. In this case, look at the suggested changes on this [comment](https://github.com/GlobalArtInc/angular-datatables/issues/1496#issuecomment-764692564) 

> 'Warning: Unable to fully load <project> for sourcemap flattening; ENOENT: no such file or directory* '

This has been fixed in newer version of `angular-datatables`. You can find latest releases for your project's Angular version on [Releases](https://github.com/GlobalArtInc/angular-datatables/releases) page.

> 'DataTables warning: table id=xx - Cannot reinitialise DataTable. For more information about this error, please see http://datatables.net/tn/3*'

This error occurs when you're trying to change `dtOptions` on a table which has been previously initialised by DataTables.
If you're using a shared table component, just call `destroy()` method on `ngOnDestroy` of the component.
If you're using DataTables v1.10.4 or later, you can add `destroy: true` to `dtOptions` when initialising the table to let the table be destroyed automatically when new changes arrive. 

> 'DataTables warning (table id = x): Requested unknown parameter y from the data source for row z* http://datatables.net/tn/4' or similar

This usually occurs when your `dtOptions` are configured incorrectly. Make sure your AJAX response matches to our AJAX example [here](http://localhost:4200/#/basic/with-ajax). 
We highly recommend checking out DataTables.net [documentation](https://datatables.net/manual/tech-notes/4) on this issue for more troubleshooting information. 

> Blank screen when using `visible: true` on TemplateRef or Pipes

This is a known issue with the library. Please upgrade to atleast [v15.0.1](https://github.com/GlobalArtInc/angular-datatables/releases/tag/v15.0.1) for the fix.
