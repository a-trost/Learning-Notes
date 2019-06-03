# SVG Animation

These notes were mostly created when reading SVG Animation by Sarah Drasner.

## Basics

SVG stands for Scalable Vector Graphics
They're in a XML file format

SVG paths have `d` for data, and always start with `d="M..."` for moveTo

### Path Syntax

```
**LINE COMMANDS
M				moveTo				Start of the path
L 			lineTo				Draws a line to a point
H				Horizontal line from current position
V				Vertical line from current position
Z				Joins to the nearest M, closes the path
**CURVE COMMANDS
C				Cubic Bezier				(Half S)
S				Reflecting Cubic Bezier 	(S)
Q				Quadratic Bezier - both sides share the same control point
T				Command control point that's been reflected
A				Elliptical Arc
```

You group SVG elements with `<g>`

You can give any of the elements a CSS class or ID, just like HTML. Like normal CSS, inline styles will always beat out class-given styles. If you want to do something like change the fill color of an element, make sure you remove any fill colors from the inline SVG elements.

## Chapter 5: UI/UX Animations with No External Libraries

We don't actually look all over images. We look at things in _saccades_ and create mental images of them. That's the little eye twitching when you look back and forth.

### Methods of Animation

Don't overuse animations - they can get distacting.

Drasner's good example here: https://codepen.io/sdras/full/qOdwdB

#### Morphing

Morphing is when one element becomes multiple other things. On click, a button can shrink into a circle and display a check to show it was successful. This is really good for keeping context. Jumping from page to page without any transition can be jarring for the user. But if the elements morph in logical ways, it can make the UX nice and smooth.

SVG and CSS can do this. GreenSock's MorphSVG plugin is really good for this, Drasner says. Chapter 10 has more.

#### Revealing

Drasner says that things like typical modals break the context of where the information 'lives' and can confuse users. Something like this: https://codepen.io/sdras/full/yOjWdO where you can see where the modal comes from and returns to, allows for the user to have more spatial awareness.

#### Isolation

Removing extra noise can help users understand what the page is about as well as make decisions easier. Remember: More isn't better. Users don't do well with a ton of options. Simplify things, present less on the page, and when you need multiple things like here: https://codepen.io/sdras/full/qOdWEP you can use things like hover states to help users isolate parts of the page.

This is also isolating the steps of a form into its parts instead of putting the entire thing on one page.

#### Style

The ease that you choose for animations communicates things about your brand. Fun brands can have fun, bouncy transitions. Serious brands should have simpler transitions. Some resources for eases:

- CSS: http://cubic-bezier.com/ and http://easings.net
- GSAP: http://greensock.com/ease-visualizer
- React-Motion: http://bit.ly/2mH7nvT

#### Accents in Eases

Drasner recommends that in the same way you use an accent color to draw attention to things, you can use an accent ease that is different from your standard `ease-in-out` to draw attention to something.

#### Anticipatory Cues

Animation can help users feel like the task didn't take as much time as it actually did. When there are no animations or indications while waiting, users over-estimate the wait time by 36%.

You can use anticipation states for things like loading states, or waiting for the login to get rejected/accepted, or data getting saved.

These custom loading states can make the app feel like it performs better than it does.

#### Interaction

You want users to actually use your app and get a tactile, real world feel for it if possible. Drasner gives examples of dragging files to a 'bottom' drawer so that users know where their files are in the space of your app. Of course, they're not actually there, but it's helpful for users.

https://tympanus.net/Development/DragDropInteractions

#### Space Conservation

Hiding things away by using animation is useful. Think of the hamburger menus that unfold to show multiple options. Saves space on small devices.

### Pulling it all Together

Now we'll be building out an SVG icon that transforms.

Make sure these kinds of animations are subtie, not too long or flashy or distracting. Think about what you're trying to do for the user, not how you're showing off. Keep it between 0-300ms.

If it's something they see all the time, don't make it obnoxious after the 5th time seeing it.

To make animations where objects transform from one thing to the next, we start with transforming the items with zero or neutral properties that don't change the object. Like this:

```css
.magnifier {
  line {
    transform: rotate(0deg) translateY(0px);
  }
  clrcle {
    transform: scale(1)
  }
}
```

Then you can just use transforms, if you're going from point A to point B. 

You can use Javascript's `Element.setAttribute()` to change SVG.

Drasner says that `ease-out` functions are great for enterances, and `ease-in` is great for exits.

Using `transform-origin: 50% 50%;` seems to be about the same as `center center` but I could be wrong on that. 

**QuickTip:** There are issues across browsers with animating SVGs, but GreenSock clears up a lot of those cross browser issues for you. 
