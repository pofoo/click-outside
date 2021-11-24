# React useClickOutsideRef Hook
Lightweight, accessible, clickoutside React ref

## 🚀 Features 🚀
* [x] Call onClick function when user **clicks outside of component**
* [x] Call onClick function when user **presses the escape key**
* [x] Support **multiple refs** with the same onClick function

## Basic Usage
Refs are always returned in an array of 1 or more refs.

```
import { useClickOutisdeRef } from '@pofo/click-outside';

const MyComponent = () => {
    
    const onClick = () => {
        // ... do something
    }

    /* CLICKOUTSIDE REF */
    const [ ref ] = useClickOutsideRef( onClick );

    return (
        <div ref={ref}>
            Click outisde of me to trigger the onClick function!
        </div>
    )
}
```

### Getting More Than One Ref
If you want more than one ref attached to the same onClick function, specify the number of refs you want.

```
import { useClickOutisdeRef } from '@pofo/click-outside';

const MyComponent = () => {
    
    const onClick = () => {
        // ... do something
    }

    /* CLICKOUTSIDE REF */
    const [ ref1, ref2 ] = useClickOutsideRef( onClick, {}, 2 );

    return (
        <div ref={ref1}>
            Click outside of me to trigger the onClick function!
        </div>
        <div ref={ref2}>
            Clicking outside of me will also trigger the same onClick function!
        </div>
    )
}
```

### Customizing Options
By default, pressing the escape key will call the onClick function as well. If you wish to disable this functionality, pass an options object with `enableEscape` as `false`.

```
import { useClickOutisdeRef } from '@pofo/click-outside';

const MyComponent = () => {
    
    const onClick = () => {
        // ... do something
    }

    /* CLICKOUTSIDE REF */
    const [ ref ] = useClickOutsideRef( onClick, { enableEscape: false } );

    return (
        <div ref={ref}>
            Pressing escape will not trigger the onClick, but clicking outside me will!
        </div>
    )
}
```

## API
```
useClickOutsideRef(
    // requried
    onClick: () => void,
    // optional
    options: {
        enableEscape?: boolean,
    },
    // optional
    numRefs: number,
)
```

| Parameter | Description |
| ----------- | ----------- |
| onClick: () => void | onClick function that gets called when user clicks off the component. By default, also gets called when user clicks the escape key | 
options: { enableEscape?: boolean; } | Optional options object. enableEscape: When set to true, pressing the escape key *will trigger* the onClick function. If set to false, pressing the escape key *will not* trigger the onClick function. Defaults to true. |
numRefs: number | Specifies number of refs to return in the array.

## Typescript
You can specify what kind of HTML Element your ref is going to be attached to.

```
const [ ref ] = useClickOutsideRef<HTMLDivElement>( () => {} );
```

If you are returning multiple refs that are different kinds of HTML Elements.

```
import { RefObject } from 'react';
import { useClickOutsideRef } from '@pofo/click-outside';

const MyComponent = () => {

    const onClick = () => {
        // ...do something
    }

    const [ ref1, ref2 ] = useClickOutsideRef( onClick );

    return (
        <section>
            <div ref={ref1 as RefObject<HTMLDivElement>}>
                I am a div!
            </div>
            <span ref={ref2 as RefObject<HTMLSpanElement>}>
                I am a span!
            </span>
        </section>
    )
}
```

*IF YOU KNOW A BETTER WAY TO SUPPORT TYPESCRIPT, PLS HELP AND CREATE A PULL REQUEST*