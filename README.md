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
   resolutionStrategy.force ‘junit:junit:4.8+’
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
