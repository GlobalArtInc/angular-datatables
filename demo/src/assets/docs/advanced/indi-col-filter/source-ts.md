```typescript
import { AfterViewInit, Component, OnInit, ViewChild } from '@angular/core';

import { DataTableDirective } from 'angular-datatables';
import { Config } from 'datatables.net';

@Component({
  selector: 'app-individual-column-filtering',
  templateUrl: 'individual-column-filtering.component.html'
})
export class IndividualColumnFilteringComponent implements OnInit, AfterViewInit {

  @ViewChild(DataTableDirective, {static: false})
  datatableElement: DataTableDirective;

  dtOptions: Config = {};

  ngOnInit(): void {
    this.dtOptions = {
      ajax: 'data/data.json',
      columns: [{
        title: 'ID',
        data: 'id'
      }, {
        title: 'First name',
        data: 'firstName'
      }, {
        title: 'Last name',
        data: 'lastName'
      }]
    };
  }

  ngAfterViewInit(): void {
    this.datatableElement.dtInstance.then(dtInstance => {
      dtInstance.columns().every(function () {
        const that = this;
        $('input', this.footer()).on('keyup change', function () {
          if (that.search() !== this['value']) {
            that
              .search(this['value'])
              .draw();
          }
        });
      });
    });
  }
}

```
