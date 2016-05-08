# Tkinter ToolTips in Python

A standalone python class that will handle showing and hiding tooltips for single or multiple tkinter widgets.

The code will show the tooltip when a widget is hovered over and will dynamically adjust the tooltip's position and size to make sure it fits the window.

## Instructions

### Setup

In order to use this class you need to:

1. Place a copy of **ToolTips.py** in your program's folder.
2. On the file(s) you want to use the tooltips import this class with `import ToolTips`.
3. Instantiate the class providing a List of widgets, a List of tooltip text strings and an optional Tkinter Font object, in the form `tooltip_obj = ToolTips.ToolTips(widgets, tooltip_text, font_obj)`

There are several class variables that can be used to customize the tooltip's styles and position.

### Parameters

The class constructor receives **3 parameters**, 2 mandatory and 1 optional.

1. A list of widget references. These widgets are the ones you want tooltips on.
2. A list of strings with the tooltip text for each of the widgets on the list
3. [OPTIONAL] A tkinter font object to be used for the tooltip text.

If a font isn't provided, the tooltips will use the default font family and font size set on the respective class variables.  
By default the font family is "Helvetica" and the font size is 12.

Regarding the List of widgets and the List of strings, they should have **matching indexes**, i.e., the first string on the list should be the tooltip of the first widget on the other list, and so on.

### Demo

The file `demo.py` contains a simple tkinter GUI integrating the tooltip code, which can be used as a reference on how to use this class, if needed.

## Technical Information

### Binds and Events

The constructor will set 3 binds for each of the supplied widgets.

- **&lt;Enter&gt;** --> When the mouse enters the widget area the tooltip will be displayed.
- **&lt;Leave&gt;** --> When the mouse leaves the widget area the tooltip will be removed.
- **&lt;Button-1&gt;** --> When the widget is clicked with the LMB the tooltip will be removed.

You can set your own binds for showing and removing a widget's tooltips, by calling the `showToolTips()` method to show the tooltip and calling the `hideToolTips()` method to remove the tooltip.

**NOTE:**  
If your code is adding binds for the same widgets and events, make sure to add them to the bind list, rather than replacing the tooltip's binds.  
This can be done using the following syntax `widget.bind("event", callback, add="+")`

### Placement of the ToolTip

By default the tooltip will be placed below the respective widget and aligned with it's west border.  
The code will also add line breaks to the tooltip string in order to avoid overflowing the window.

However, if there isn't enough space on the window for the default placement, the code will try moving the tooltip around the widget to check if it fits on the window.  
If no position can be found, then the tooltip will try using the entire window width, i.e., it will no longer be aligned with the widget's west border.  
If it still doesn't fit the window, then the code will start reducing the font size of the tooltip text until it either fits or the font size reaches 1.

### Other Information

The code will try using as much of the window's width to show the tooltip, but there will be some unused space as a safeguard.  
This is needed due to the dynamics of fonts, specifically the width of it's characters and how many characters can be inserted in each of the tooltip's lines.  
In order to avoid using a more complex algorithm, that would slow down your program, a simpler solution was used with the downside of requiring a safety margin.
