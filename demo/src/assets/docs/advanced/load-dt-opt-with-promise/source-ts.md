```typescript
import { Component, Inject, OnInit } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Config } from 'datatables.net';

@Component({
  selector: 'app-load-dt-options-with-promise',
  templateUrl: 'load-dt-options-with-promise.component.html'
})
export class LoadDtOptionsWithPromiseComponent implements OnInit {

  dtOptions: Promise<Config>;

  constructor(@Inject(HttpClient) private httpClient: HttpClient) {}

  ngOnInit(): void {
  this.dtOptions = this.httpClient.get<Config>('data/dtOptions.json')
      .toPromise()
      .catch(this.handleError);
  }

  private handleError(error: any): Promise<any> {
    console.error('An error occurred', error); // for demo purposes only
    return Promise.reject(error.message || error);
  }
}
```
