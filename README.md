This is a starter template for 'GO TO Canal Hacké' Sprint Review.

## How did we arrive here ?

```bash
$ ionic start AutocompleteApp blank
$ cd AutocompleteApp
$ cordova plugin add ~/dev/CDVNavitiaSDK
$ ionic cordova emulate android --livereload
```

Add this to platforms/android/build.gradle if the build fails
```groovy
configurations.all {
   resolutionStrategy.force 'junit:junit:4.8+'
}
```

## Search bar
```xml
<ion-searchbar (ionInput)="getItems($event)"></ion-searchbar>
```

## Items list
```xml
<ion-list>
  <ion-item *ngFor="let item of items">
    {{ item }}
  </ion-item>
</ion-list>
```

## Add Zones
```typescript
import { Component, NgZone } from '@angular/core';
import { NavController } from 'ionic-angular';

@Component({
  selector: 'page-home',
  templateUrl: 'home.html'
})
export class HomePage {

  constructor(public navCtrl: NavController, private zone: NgZone) {

  }

}
```

## Typescript likes to have declarations for all the vars
```typescript
declare var NavitiaSDK: any;
```

## Classe des enfers
```typescript
export class HomePage {
  items;

  constructor(public navCtrl: NavController, private zone: NgZone) {
  	this.items = [];
  	NavitiaSDK.init('0de19ce5-e0eb-4524-a074-bda3c6894c19');
  }

  getItems(ev) {
  	this.items = [];

  	// set val to the value of the ev target
	var val = ev.target.value;

	var that = this;
    NavitiaSDK.endpoints.places.newRequestBuilder().withQ(val).get(function(success) {
        that.zone.run(function () {
               	for (var item of success.places) {
                    that.items.push(item.name);
                }
            })
    }, function(error) {
        alert("error");
    });
  }
}
```
