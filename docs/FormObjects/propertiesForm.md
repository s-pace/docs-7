---
id: propertiesForm
title: Form Properties
---

---



## Assigning a menu bar to a form  

When you create an application, you can create custom menus. Custom menus allow you to add menu commands for automating specific tasks in the database, such as, for example, creating a report.

Custom menus are created in the Menu Bar editor. Each menu bar that you create includes at least one menu and is assigned a unique ID number and name. For more information on creating menu bars, menus and menu commands, refer to the chapter *Menus and menu bars* in the *4D Design Reference*.

To assign a menu bar to a form, select a menu bar from the “Associated Menu Bar” List in the Property List. The **[...]** button lets you access the menu bar editor directly. In the Application environment, a menu bar that is assigned to a form is added to the right of the current menu bar.

 If the menu bar of the form is identical to the current menu bar, it is not added. The form menu bar will operate for both input and output forms.


#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|menuBar|string|Name of the menu bar to apply|


---



## Window Title  

The window title is used when the form is opened using the `Open window` and `Open form window` functions in the Application environment. The window title appears in the Title bar of the window. To set the  window title, enter it in the Window Title entry area of the Property List.

You can use dynamic references to set the window titles for forms, *i.e.*:

*	A standard XLIFF reference (see `PICTURE TO BLOB`).
*	A table or field label: The syntax to apply is <?[TableNum]FieldNum> or <?[TableName]FieldName>. The reference is resolved when the `FORM SET INPUT` command is called (if the * parameter is passed and if it is followed by a call to Open window) and when the Open form window command is called.
*	A variable or a field: The syntax to apply is <VariableName> or <[TableName]FieldName>. The current value of the field or variable will be displayed in the window title.
Notes:

The number of characters for a window title is limited to 31.

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|windowTitle |string |Name of the default window when a form is opened|

---

## Form Name




#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
| | ||

---



## Form Type  

You can change a form's type, *i.e.* its destination, depending on the form's architecture:

|Genre|Destination Type|
|---|---|
|Project forms|<li>Detail Form </li><li>Detail Form for Printing</li>|
|Table forms|<li>List Form</li><li>List Form for Printing</li>

The `Form Type` property determines the options that are available for the form. 

It also allows you to restrict the number of forms displayed in the current Input and Output form selection lists (the List of tables window, see Browsing different tables and forms): only forms whose type corresponds to the list are displayed. 

The `Form Type` property is found at the top of the Property List. When the form type is None, it is displayed in both menus of the List of tables. 


#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|destination |string |"detailScreen", "listScreen", "detailPrinter", "listPrinter" |

---

## Form and Window Size 
 
A form is always displayed in a window. 4D lets you set the size of both the form and the window. These properties are interdependent and your application interface results from their interaction. 
 
### Form Size
 
To set the form size properties, the following choices are available:

*	**Size based on automatic size**: The size of the form will be that which is necessary to display all of the objects and to which will be added the  horizontal (`sizingX`) and vertical (`sizingY`)  margin values.
*	**Size based on Set size**: The size of the form will be based on what you enter (in pixels) in the `width` and `height` values.
*	**Size based on object**: The size of the form will be based on the position of the selected form object. For example, if you choose an object that is placed in the bottom-right part of the area to be displayed, the form size will consist of a rectangle whose upper left corner will be the origin of the form and the lower right corner will correspond to that of the selected object, plus any margin values.<p>
You can choose this option when you want to use active objects placed in an offscreen area (*i.e.*, outside the bounding rectangle of the window) with an automatic size window. Thanks to this option, the presence of these objects will not modify the size of the window.
*	When you select the **Automatic Size** option or a size based on an object, you have the horizontal (`sizingX`) and vertical (`sizingY`)  margin fields. You can then enter values (in pixels) to set additional margins to be added to the edges of the form. These values also determine the bottom and right-hand margins of forms used in the Label editor.
	>For output forms, only the horizontal and vertical properties are available.




### Window Size 
 
When an input form is displayed in a custom application, you ordinarily open the form using the `Open window` or `Open form window` functions.

`Open window` lets you specify the top, left, bottom, and right coordinates of the window as well as the window type. In this case, the size of the window does not depend on that of the form. On the other hand, the resizing possibilities will depend on the form options set and on the window type. `Open form window` creates a new window based on the sizing and resizing properties of the form passed as parameter. 

The following form window resizing options are available:

*	**Fixed Width**: If you check this option, the window width will be locked and it will not be possible for the user to resize it. If this option is not checked, the width of the form window can be modified. In this case, the `windowMinWidth` and `windowMaxWidth` properties can be used to determine the resizing limits.
*	**Fixed Height**: If you check this option, the window height will be locked and it will not be possible for the user to resize it. If this option is not checked, the height of the form window can be modified. In this case, the `windowMinHeight` and `windowMaxHeight` properties can be used to determine the resizing limits.

As a general rule, it is necessary to prevent the user from hiding enterable areas and control buttons.


#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|bottomMargin|integer|minimum: 0|
|formSizeAnchor| string|Name of a 4D object|
|height|integer|minimum: 0|
|rightMargin|integer|minimum: 0|
|sizingX|string|"move", "grow", "fixed"|
|sizingY|string|"move", "grow", "fixed"|
|width|integer|minimum: 0|
|windowMaxHeight|integer|minimum: 0|
|windowMaxWidth|integer|minimum: 0|
|windowMinHeight|integer|minimum: 0|
|windowMinWidth|integer	|minimum: 0|
|windowSizingX|string|"fixed", "variable"|
|windowSizingY|	string|"fixed", "variable"|

---

## Events  

This area sets the events that can lead to the execution of the form method. When the form is used, only the events that you select will actually occur. If you do not select any events, the form method will never be called.

Your database will run faster if you deselect superfluous events.
For more information about form events, refer to the `Form event code` command.

To select or deselect all events, hold down **Ctrl** (Windows) or **Command** (macOS) and click an event.

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|events|String array or number array|onActivate, onAfterEdit, onAfterKeystroke, onAfterSort, onAlternateClick, onBeforeDataEntry, onBeforeKeystroke, onBeginDragOver, onBeginURLLoading, onBoundVariableChange, onClick, onCloseBox, onCloseDetail, onCollapse, onColumnMove, onColumnResize, onDataChange, onDeactivate, onDeleteAction, onDisplayDetail, onDoubleClick, onDragOver, onDrop, onEndURLLoading, onExpand, onFooterClick, onGettingFocus, onHeader, onHeaderClick, onLoad, onLoadRecord, onLongClick, onLosingFocus, onMenuSelect, onMouseEnter, onMouseLeave, onMouseMove, onMouseUp, onOpenDetail, onOpenExternalLink, onOutsideCall, onPagechange, onPluginArea, onPrintingBreak, onPrintingDetail, onPrintingFooter, onResize, onRowMove, onScroll, onSelectionChange, onTimer, onUnload, onURLFiltering, onURLLoadingError, onURLResourceLoading, onValidate, onVPReady, onWindowOpeningDenied|


---


## Help 
 
4D allows you to associate a custom on-line help file with each database. The creation of help files is described in [Appendix A: Assigning a custom help file](https://doc.4d.com/4Dv18/4D/18/Appendix-A-Assigning-a-custom-help-file.300-4575736.en.html). 

Help files can be contextual, which means that they can display information related to the context from which they were called. To do so, you can associate a **Help Topic Number** to a form. Make sure you assign help topic numbers that match numbers defined in the help file. This is done in the “Help” theme of the Property List .

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|tooltip|string|varies|


---



## Hide Grow Box  

Selecting this option hides the grow box in a form window. This option is taken into account when you call the form using the `DIALOG` command for example.

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
||||


---

## Markers  

This area lets you specify the precise location of markers on the vertical ruler of the form. Markers are mainly used in output forms. They control the information that is listed and set header, breaks, detail and footer areas of the form. For more information about the use of control markers, see *Using output control lines* in the *4D Design Reference*.

>The label width triangle on the horizontal ruler controls the width of a label when you create a form for printing mailing labels using the `PRINT LABEL` command.

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|markerBody|integer	|minimum: 0|
|markerBreak|integer/integer array|minimum: 0|
|markerFooter|integer|minimum: 0|
|markerHeader|integer/integer array|integer minimum: 0; integer array minimum: 0|


---

## Print  

The print properties are described in *Printing a form* in the *4D Design Reference*.

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
||||


---



## Published as subform in the host database 
 
This option is useful when developing components that contain forms (see [Sharing of forms](https://doc.4d.com/4Dv18R2/4D/18-R2/Interaction-between-components-and-host-databases.300-4824115.en.html#516628)). 

For a component form to be selected as a subform in a host database, it must have been explicitly designated as a "published form" in the properties dialog box of the form by selecting the Published as subform in the host database option. Only project subforms can be specified as published subforms. 

For more information about specifying and using component subforms, refer to [Developing components](https://doc.4d.com/4Dv18R2/4D/18-R2/Developing-components.300-4824118.en.html).

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
|shared |boolean |true, false|

---

## Save Geometry  

When the option is used, if the window is opened using the `Open form window` command with the * parameter, several form parameters are automatically saved by 4D when the window is closed, regardless of how they were modified during the session:

*	the current page,
*	the position, size and visibility of each form object (including the size and visibility of list box columns).

>This option does not take into account objects generated using the `OBJECT DUPLICAT`E command. In order for a user to recover their environment when using this command, the developer must repeat the sequence of creation, definition and positioning of the objects. 

When this option is used, the `Save Value` option is also available for certain objects. 

#### JSON Grammar

|Name|Data Type|Possible Values|
|---|---|---|
| memorizeGeometry|boolean |true, false|





















