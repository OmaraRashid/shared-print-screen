
# Introduction

The PrintScreenComponent is a standalone, shared component in Angular that provides a button for printing a section of the document. It utilizes the [ngx-print](https://www.npmjs.com/package/ngx-print) package to handle the printing functionality . The component appears as a button in the parent component and when clicked, it prints the template passed to it.

# Getting started

To use this component, follow the steps below:

    Install the ngx-print library by running npm i ngx-print.
    Import the NgxPrintModule module in your shared.module.ts file.
    Import sharedModule in the module or in standalone componet where you want to use it .


# PrintScreenComponent

PrintScreenComponent is a standalone component in Angular that appears as a button in the parent component. When the button is clicked, the component will print the template passed to it. The component is imported from the SharedModule.
Component Details

# code 

``` TypeScript
import { Component, Input, OnInit, TemplateRef } from '@angular/core';
import { SharedModule } from '../../shared.module';

/** standalone shared componet for print screen */
@Component({
  standalone: true,
  selector: 'print-screen-button',
  imports: [ SharedModule ],
  templateUrl: 'print-screen.component.html',
})

/** 
 * Printscreen component appears as a button in the parent component
 * and will print the screen template passed to it 
 */
export class PrintScreenComponent implements OnInit {
    /** printedSectionId ngx-print directive used to link */
    @Input() public printSectionId: string;
    /** name of the button */
    @Input() public buttonName: string;
    /** printed template */
    @Input() public template: TemplateRef<any>;
    /** icon displayed beside the button */
    @Input() public icon: string;
    /** 
     * printStyle: Object of custom styles for elements inside the 
     * printed document. It's a dictionary where the key is the element 
     * selector and the value is a dictionary of CSS properties and values. 
     */
    @Input() public printStyle: { [key: string]: { [key: string]: string; } };
    /** title: The title of the printed document that will appear at the top of the document window */
    @Input() public title: string;
    /** 
     * styleSheetFile: the file name for customizing the printing window style sheet (CSS) 
     * by importing the file. Example: "assets/css/custom1.css,assets/css/custom2.css"
     */
    @Input() public styleSheetFile: string;
    /** 
     * useCss: a boolean value indicating whether to use existing CSS to avoid a black & white printed document. 
     * Default value is `true`. 
     */
    @Input() public useCss: boolean = true;
    /**  icon binding */
     public svgPath: string;
    /**  ngOnInit method */
   public ngOnInit (): void {
     this.svgPath = this.icon;
   }
}
```

HTML

``` html
<div #printSection [id]="printSectionId" [ngStyle]="{'display': 'none'}">
  <ng-container *ngTemplateOutlet="template"></ng-container>
</div>```
<button [printSectionId]="printSectionId" [printStyle]="printStyle" [printTitle]="title" [useExistingCss]="true" [styleSheetFile]="styleSheetFile" ngxPrint>
  {{buttonName}}
  <svg class="i-sml">
    <use [attr.xlink:href]="svgPath"></use>
  </svg>
</button>
```

In the HTML template, a div element with #printSection is created and has its id set to printSectionId. The ng-container directive is used to bind the passed template to the div. The button element is decorated with several inputs and the ngxPrint directive, which is used to initiate the printing process. The button displays the buttonName and the specified icon.

# Usage

you can put this in any component in your project 

``` html
<print-screen-button 
  [printSectionId]="'uniqueIdForPrintSection'" 
  [buttonName]="'Print Screen Button'"
  [template]="templateRefVariable" 
  [icon]="'iconName'" 
  [printStyle]="{'h1': {'color': 'red'}, 'h2': {'border': 'solid 1px'}}"
  [title]="'Printed Document Title'"
  [styleSheetFile]="'fileName'"
  [useCss]="true">
</print-screen-button>

<ng-template #templateRefVariable>
  <!-- Content to be printed -->
  <h1> hello Printed </h1>
  <h2> VOIS </h2>
</ng-template>

```

# Conclusion

The PrintScreenComponent is a useful tool for printing specific sections of a document in Angular applications. It can be easily integrated into any component in the project and allows for customization of the printed document through inputs such as print styles and title. With the use of the ngx-print library, the component ensures a smooth and efficient printing process .
