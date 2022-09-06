# Prodigy web interface customization
This repo documents how to change the appearance of the prodigy web interface.
## What to edit?
Copy the file ```~/.prodigy/prodigy.json``` to your project folder:
```bash
cp ~/.prodigy/prodigy.json path/to/project
```

## Customizing
By default, this json comes empty.
To edit the web appearance using css, add a key named ```global-css```, and as value the css you want.
Prodigy comes with [premade and human readable css classes](https://prodi.gy/docs/custom-interfaces#css)
## Options
To easily manage options, we have used a css-grid instead of the dedault flex display.
We've only applied it to the container holding all options (class: prodigy-options)
```css
.prodigy-options {
  width: 100%; // To expand the available surface for the options
  display: grid; // This was 'flex' before
  padding: 20px 20px 10px; // This is de default value
  grid-auto-flow: column; // To fill the grid top-down instead of left-right
}
```
To add responsiveness to the page, on arbitrary screen sizes (700px, 1200px, 1560px) the number of max rows changes:
```css
// The more width, the less rows are needed
@media (min-width: 700px) {
  .prodigy-options { grid-template-rows: repeat(24, 1fr); gap: 7px; }
}
@media (min-width: 1200px) {
  .prodigy-options { grid-template-rows: repeat(16, 1fr); gap: 7px; }
}
@media (min-width: 1560px) {
  .prodigy-options { grid-template-rows: repeat(12, 1fr); gap: 7px; }
}
```

------------------------
To change the size of the options text we have to edit the ```prodigy-content``` class.
Be aware editing this class will also change the size of the annotation target.
Since both use the same class, we have to specify the parent node:
```css
a>div.prodigy-content { css } // For the labels
div>div.prodigy-content { css } // For the annotation target
```
### Moving the metadata container
To move the metada container, we edited the class ```prodigy-meta```. moved it to about 70px under the top.
```css
.prodigy-meta {
   position: absolute;
   top: 70px;
   font-size: 16px;
}
```
To move the elements it clips down, we incremented the margin from the annotation target.
Since the container for the annotaion target shares class with the options, we must specifiy it's parent:
```css
div > div.prodigy-content { // Parent is a div
   margin-bottom: 65px // The desired margin
}
```
## Running with this config
To use this config, just run prodigy normally, from the root of your project where ```prodigy.json``` is saved.
To use it as the default, save it to ```~/.prodigy``` folder, as ```prodigy.json```
