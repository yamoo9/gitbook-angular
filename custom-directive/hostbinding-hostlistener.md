# HostBinding / HostListener



```typescript
import { Directive, HostBinding, HostListener } from '@angular/core';

@Directive({ selector: '[data-rainbow]' })
export class RainbowDirective {

  colors:string[] = [
    'darksalmon', 'hotpink', 'lightskyblue', 
    'goldenrod', 'peachpuff', 'mediumspringgreen', 
    'cornflowerblue', 'blanchedalmond', 'lightslategrey'
  ];
  
  @HostBinding('style.color') color:string;
  @HostBinding('style.font-weight') fontWeight:string;
  
  @HostListener('keydown') newColor() {
    const pick = Math.floor(Math.random() * this.colors.length);
    this.color = this.colors[pick];
    this.fontWeight = 700;
  }
}


```

