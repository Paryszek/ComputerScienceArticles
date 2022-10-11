# Angular - Change detection in a nutshell

Angular framework is a powerful tool that can be used to create single page applications. Application is based on tree of components. Individual component has it’s own template and class. 

How does the Angular framework manages to detect changes? Thanks to `NgZone`, which gets attached to everything in the browser, that can cause the variable to change (events: click; focus, addEventListener, setTimeout, setInterval, ajax requests, requestAnimationFrame etc.). 

When the change occurs, angular performs change detection run through all components in the tree, to see if the model has changed. The process begins at root component. 

Change detection don’t perform deep object comparison for models, only a simple comparison using `===`  for previous and current field values used in template. 

Change detection mechanism has two strategies:

- Default
- OnPush

Component can use one of this strategies, it just needs to be set inside `@Component` metadata object (`changeDetection` field).

```jsx
@Component({
  selector: 'my-app',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css'],
  changeDetection**: ChangeDetectionStrategy.OnPush**
})
export class AppComponent implements OnInit {
  ngOnInit(): void {}
}
```

### Default

Change detection as default uses Default Change Detection Strategy. This default strategy checks from top to bottom every component model for every change detection run. Unfortunately, this is performance costly and must be avoided, especially for large applications.

### OnPush

Blocks default check detection flow in the component and it’s being avoided during change detection cycles. Component gets updated only after becoming dirty and during change detection cycle. Component can become dirty and trigger check detection after this scenarios:

- Input value reference gets changed or value for primitive variable
- Component or it’s children triggers an event
- Change detection triggered manually using `ChangeDetectionRef` class
- Observable used in the template by async pipe emits new value

# Summary

Default Change Detection Strategy can become very performance costly, especially for large amount of components in the application. Going through every component in the tree and checking primitive variables or fields inside objects used in the template can become too overwhelming for the entire application. The preferable Change Detection Strategy is OnPush, because the components are avoided during unnecessary check detection cycles, and updated only when they are needed to. If somehow we still need trigger change detection, there is a way to do this manually using `ChangeDetectionRef`.

# Sources

- [https://www.mokkapps.de/blog/the-last-guide-for-angular-change-detection-you-will-ever-need#how-change-detection-works](https://www.mokkapps.de/blog/the-last-guide-for-angular-change-detection-you-will-ever-need#how-change-detection-works)
- [https://blog.angular-university.io/how-does-angular-2-change-detection-really-work/](https://blog.angular-university.io/how-does-angular-2-change-detection-really-work/)