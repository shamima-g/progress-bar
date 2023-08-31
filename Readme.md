# Vertical Progress Bar


[sabz](https://github.com/shamima-g/progress-bar/blob/main/Stadium6/releases/download/ProgressBarSample.sapz)
[zip](https://github.com/shamima-g/progress-bar/blob/main/Stadium6/releases/download/ProgressBarSample.zip)
## Description
A sample application that contains a vertical progress bar to show workflow steps in 'done', 'current' or 'todo' states. The sample contains a static implementation as well as one that is generated on page load from data provided in a list. The look and feel is customisable using the variables provided in the *progress-bar-variables.css* file. 



https://github.com/stadium-software/progress-bar/assets/2085324/111b1d76-1987-40e3-b0ee-1548c729423c



## Version
1.0

## Application Setup
1. Check the *Enable Style Sheet* checkbox in the application properties

## Static Page Setup
1. Drag a *Flexbox* control to a page and name it "ProgressBarContainer"
2. Add a class called "progress-bar-container" to the "ProgressBarContainer" control *Classes* property 

### Creating a step
1. Drag a *Flexbox* control into the "ProgressBarContainer" control and name it "ProgressBarItemContainer"
2. Add a class called "progress-bar-item-container" to the "ProgressBarItemContainer" control *Classes* property 
3. Drag a *Container* control into the "ProgressBarItemContainer" control and name it "ProgressBarStepIcon"
4. Add a class called "progress-bar-step-icon" to the "ProgressBarItemContainer" control *Classes* property 
5. Drag a *Label* control into the "ProgressBarStepIcon" control and name it "ProgressBarStepIconLabel"
6. Optional: Add the step number into the *Text* property of the "ProgressBarStepIconLabel" control. This number will display on steps in the *ToDo* state
7.  Drag a *Label* control into the "ProgressBarItemContainer" and place it next to the "ProgressBarStepIcon" control, then name it "ProgressBarStepLabel"
8. Add a class called "progress-bar-step-label" to the "ProgressBarStepLabel" control *Classes* property 
9. Add a description for this step into the *Text* property of the "ProgressBarStepLabel" control

When you have added one step into your "ProgressBarContainer" control, it should look like this<br>
![StadiumDesigner_8seIX8j0xH](https://github.com/stadium-software/progress-bar/assets/2085324/d73af593-e096-4eb0-b2ea-9cec0ba84a12)
<br>Place as many steps as you need underneath each other

### Static Controls Map
| | Control | Location | Name | class | Text |
| --- | --- | --- | --- |--- |---
| 1. | Flexbox | page | ProgressBarContainer| progress-bar-container | |
| 2. | Flexbox | ProgressBarContainer | ProgressBarItemContainer| progress-bar-item-container | |
| 3. | Container | ProgressBarItemContainer | ProgressBarStepIcon| progress-bar-step-icon | |
| 4. | Label | ProgressBarStepIcon | ProgressBarStepIconLabel|  | Step description |
| 5. | Label | Next to "ProgressBarStepIcon" | ProgressBarStepLabel| progress-bar-step-label | Step number |

## Dynamic Page Setup
1. Drag a *Flexbox* control to a page and name it "ProgressBarContainer"
2. Add a class called "progress-bar-container" to the "ProgressBarContainer" control *Classes* property 
3. Create a new type in Types in the Application Explorer called "ProgressBarItem"
4. Add two properties to this type. Both properties must be of type *Any*
   1. status
   2. label
5. Create a script under the page and call it "CreateProgressBarElement"
6. Add two *Input Parameters* to the script
   1. status
   2. label
7. Drag a Javascript action into the script and add the Javascript below into the *Code* property
```
let container = document.createElement("div");
container.classList.add("progress-bar-item-container");
container.classList.add(~.Parameters.Input.status);
container.style.display = "flex";
container.style.flexDirection = "row";

let icon = document.createElement("div");
icon.classList.add("progress-bar-step-icon");
let allPBars = document.querySelectorAll(".progress-bar-item-container");
icon.innerHTML = allPBars.length + 1;

let description = document.createElement("div");
description.classList.add("progress-bar-step-label");
description.innerHTML = ~.Parameters.Input.label;

container.appendChild(icon);
container.appendChild(description);

let progressbar = document.querySelector(".progress-bar-container");
progressbar.appendChild(container);
```
7. Drag a List from the Toolbox into the page.load event handler
8. In the *Item Type* property of the list, select "ProgressBarItem" under *Types*
9. Add values to the list *Value* property as required
10. Drag a *ForEach* action below the List and assign the List to the *List* property
11. Drag the *CreateProgressBarElement* script into the *Loop* of the *ForEach* action
    1.  Assign the *ForEach.label* value to the *label* script *Input Parameters* property
    2.  Assign the *ForEach.status* value to the *status* script *Input Parameters* property

## StyleSheet CSS
1. Open the CSS file called *progress-bar-variables.css* from this repo in an editor of your choice (I recommend [VS Code](https://code.visualstudio.com/))
2. Adjust the variables in the *:root* element as you see fit

## Applying the CSS
How to apply the CSS to your application

### Stadium 6 (versions 6.6 and above)
1. Add the two CSS files to the Embedded Files of your application
2. Paste the link tags below into the *head* property of your application
```
<link rel="stylesheet" href="{EmbeddedFiles}/progress-bar.css">
<link rel="stylesheet" href="{EmbeddedFiles}/progress-bar-variables.css">
``` 

## Upgrading
To upgrade this module
1. Pull the latest repo
2. If you have made changes to the *progress-bar-variables.css* file in your local repo, merge them
3. You can drag the *progress-bar.css* file into the EmbeddedFiles folder of your application as is
4. Select "Overwrite" when prompted in Stadium
5. Open the *progress-bar-variables.css* file 
6. If new variables were added, change the variables as you see fit 
7. Drag the updated *progress-bar-variables.css* file into the EmbeddedFiles folder of your application
