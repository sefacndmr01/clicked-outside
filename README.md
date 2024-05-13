# Simple Clicked Outside Function

A simple function that detects when a click occurs outside of an HTML element.

## Function

```typescript
/**
 * @param element - Target element
 * @param callback - Callback function: triggers when user clicked outside of target element
 * @return stop: () => void
**/
export function clickedOutside(element: HTMLElement | Element, callback: (target: EventTarget) => void): { stop: () => void }{
    const event = (event: Event) => {
        if(!event.target) return;
        if(!(element == event.target || element.contains(event.target as Node))) return callback(event.target)
    }
    document.addEventListener("click", event);
    const stop = () => { document.removeEventListener("click", event) }
    return { stop }
}
```

## Usage

----

```typescript
const el = document.getElementById('el');
const co = clickedOutside(el, () => console.log('Clicked outside of #el'));

// Stop listeners
co.stop(); 
```




