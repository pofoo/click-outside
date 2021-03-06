# React useClickOutsideRef Hook
Lightweight and accessible clickoutside React ref

## Install
```
yarn add @pofo/click-outside
npm i @pofo/click-outside
```

# Jump Around
- [Basic Usage](#Basic-Usage)
- [Multiple Refs](#Multiple-Refs)
- [Customizing Options](#Customizing-Options)
- [API](#API)
- [Typescript](#Typescript)

## 🚀 Features 🚀
* [x] Call onClick function when user **clicks outside of component**
* [x] Call onClick function when user **presses the escape key**
* [x] Support **multiple refs** with the same onClick function

## Basic Usage
Refs are always returned in an array of 1 or more refs.

```typescript
import useClickOutisdeRef from '@pofo/click-outside';

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

### Multiple Refs
If you want more than one ref attached to the same onClick function, specify the number of refs you want in the optional options object.

```typescript
import useClickOutisdeRef from '@pofo/click-outside';

const MyComponent = () => {
    
    const onClick = () => {
        // ... do something
    }

    /* CLICKOUTSIDE REF */
    const [ ref1, ref2 ] = useClickOutsideRef( onClick, { numRefs: 2 } );

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

```typescript
import useClickOutisdeRef from '@pofo/click-outside';

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
```typescript
useClickOutsideRef(
    // requried
    onClick: () => void,
    // optional
    options: {
        numRefs?: number,
        enableEscape?: boolean,
    },
)
```

| Parameter | Default | Type | Description |
| ----------- | ----------- | ----------- | ----------- |
| `onClick` | `REQUIRED` | `() => void`| onClick function that gets called when user clicks off the component. By default, also gets called when user clicks the escape key | 
`options` | `{ numRefs: 1, enableEscape: true }` | `{ numRefs: number, enableEscape: boolean }` | Optional options object.<br/><br/> **numRefs**: Specifies the number of refs you would like returned.<br/><br/> **enableEscape**: When set to true, pressing the escape key *will trigger* the onClick function. If set to false, pressing the escape key *will not* trigger the onClick function. Defaults to true.

## Typescript
You can specify what kind of HTML Element your ref is going to be attached to.

```typescript
const [ ref ] = useClickOutsideRef<HTMLDivElement>( () => {} );
```

If you are returning multiple refs that are different kinds of HTML Elements.

```typescript
import { RefObject } from 'react';
import useClickOutisdeRef from '@pofo/click-outside';

const MyComponent = () => {

    const onClick = () => {
        // ...do something
    }

    /* CLICKOUTSIDE REF */
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


## Extra
This library plays well with [useFocusTrap](https://github.com/pofoo/focus-trap)

## LICENSE
MIT