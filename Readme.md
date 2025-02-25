# How to add custom graphic operations (watermarks) to the built-in editor dialog for a PictureEdit control

The PictureEdit control provides a built-in editor that allows users to perform basic graphic operations on the displayed image.
  - Crop and straighten
  - Adjust brightness, contrast and saturation
  - Mirror
  - Rotate, etc.

This example shows how to extend the editor with custom graphic commands that add watermarks to the current image.

![image](pictureedit-editor-watermark.png)

The steps to add a WatermarkCommand (and other commands) to the image editor are as follows.

1. Create a new class (WatermarkGraphicOperation) that performs an operation on an image. 
The operation must be a BaseCachedGraphicOperation descendant. Users can undo and redo BaseCachedGraphicOperations while the image editor is active.

2. You can allow users to specify the operation's settings in custom controls before the operation is applied. 
Create a panel with controls and implement the IToolSettingsControl interface for the panel. The IToolSettingsControl.GetOperation method must return the customized graphic operation (WatermarkGraphicOperation).

   This example creates a user control (WatermarkToolControl) with controls to enter the watermark-related settings:
   - a TextEditor to enter the watermark text
   - a ColorEditor to specify the font color
   - a SpinEditor to enter the font size
   - a CheckEditor to allow the watermark text to be repeated throughout the image.

3. Handle the PictureEdit.ImageEditorDialogShowing event to add custom commands (buttons) to the editor's main toolbar.

   In the example two commands are added:
   - WatermarkPreset - Invokes the WatermarkGraphicOperation with predefined settings.
   - WatermarkCommand - Displays the WatermarkToolControl in which users can specify custom watermark settings and then apply the WatermarkGraphicOperation.

