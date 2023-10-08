#WPF - Ian Griffiths

# Introduction

- Why WPF?
	- Support for higher resolution (high dpi/ pixels per inch)
	- auto scaling
	- dev has access to graphics card power
	- Non dev tool used by web designers via a markup language
	- WPF provides all features available on all systems in one umbrella

## Integration
	
	- composability (button can have an image and text)
	- Button supports only one child because it does not have to be in charge of the layout of its children.
	
	- So we can use a stack panel to layout the children
	
	- AutoSize is controlled via Alignment properties i.e. if your requirement is "be as tall as you can be to fit the content", use VerticalAlignment="Center", to center the elements.

## WPF Design

- Kernel - Unmanaged - .NET

- DirectX (to get pixel into screen, direct 3d)

- Even though you have a 3d scene, your screen is flat, so a 3d scene has to be flattened.
- WPF hooks into the rendering pipeline after the scene is already flattened.

- Composition engine (Media Integration Layer)

- It is in unmanaged layer is because it has to interact with directx. Directx api is very chatty. Such calls work over COM and become very expensive if done from managed layer.

- Presentation Core (public face of the MIL)
- Presentation Framework

- defines a concept of control
- databinding
- events etc-

## XAML

- WPF does not need xaml and vice versa
- eXtensible Application Markup Language - XAML
- _ underscore is used instead of & ampersand for accelerators in XAML as & does not work well with XML
- To use the '&', use '&amp;' in XAML
- It is a language for building .NET object
- XAML can be used for building any objects and  is not tied to WPF

- XAML knows which type it is working with by the namespaces defined at the top of the xaml document.

## UI Trees

- XAML objects are arranged in a tree structure
- Logical Tree vs Visual Tree

- Visual tree is the SUPERSET of the logical tree.
- Logical Tree is what you write in xaml

- Events And Commands

- Bubbling and tunneling events

- Tunneling event : Event that fires on the parent before the child (e.g. Preview<eventname>)
- Bubbling event: Event that fires on the child before the parent (e.g. <eventname>)

- Preview Events provided to the parent so as to allow them to respond first. For e.g. if you wrote the code for a screen, you want to be able to handle any preview event before the internal controls start handling those events.

- Controls #MarkupExtension #PropertyElement #ContentPresenter 

- Controls in WinForms is different than in WPF
- Controls in WPF are such as a Button, provides a click event (api feature, user interaction), content model (composition) for presentation (api feature), accept focus (interactivity feature), has automation feature
- Classes that derive from Control have a Template. Other classes such as Rectangle etc derive from FrameworkElement which do not have a Template.
- WPF has look-less control, a control that does not have a distinct look. Its look is provided by a template, because a Button does not know how to render itself.
- WPF separates the control into two parts: the look - defined by the template & everything else defined by the control itself
- PropertyElement syntax = <Button.Template> => I want to set the template property of the button.  
    <Button.Template>
		<Control.Template TargetType="Button">
			<Rectange Fill="Blue" RadiusX="5" RadiusY="5" />
		</Control.Template>
	</Button.Template>

- Now we can use binding to bind the rectangle color to the color of the button

 <Button Width="75" Height="24" Background="Red">
	 <Button.Template>
		 <Control.Template TargetType="Button">
		 <Rectange Fill="{TemplateBinding Background}" RadiusX="5" RadiusY="5" />
		   </Control.Template>
	 </Button.Template>
</Button>


## MarkupExtension

- Fill="{... property name}"
- The curly braces signify that it is not a normal property value. It tells XAML that it is a markup extension, which decide at runtime how the property is going to behave.
- First it creates an instance of the TemplateBinding class, passing Background as a constructor parameter. WPF will expect the whole thing to derive from MarkupExtension. That base class provides an abstract method called ProvideValue which will be called at runtime.
- You can create a custom markup extension where this can be used.

- Control like a button can have only one child. So we use a layout manager like a Grid which knows how to layout multiple controls.
- How to put any type of Content inside a button?  
    <Button Width="75" Height="24" Background="Red">
		 <Button.Template>
			 <Control.Template TargetType="Button">
			 <Rectange Fill="{TemplateBinding Background}" RadiusX="5" RadiusY="5" />
			 <TextBlock Text={TemplateBinding Content}" />
			   </Control.Template>
		 </Button.Template>
		 ClickMe!
	 </Button>

- This will display a button with text ClickMe. However if you want to show something else, say an ellipse then you will replace ClickMe! with <Ellipse Fill="Red" Width="60" Height="14" />
- This does not display anything as TextBlock is a primitive element which knows only how to display text. So we have a  special thing for this purpose called #ContentPresenter  
    <Button Width="75" Height="24" Background="Red">
		 <Button.Template>
			 <Control.Template TargetType="Button">
			 <Rectange Fill="{TemplateBinding Background}" RadiusX="5" RadiusY="5" />
				 <ContentPresenter Content={TemplateBinding Content}" RecognizerAccessKey="True"
				 HorizontalAlignment={TemplateBinding HorizontalContentAlignment}"
				 VerticalAlignment={TemplateBinding VerticalContentAlignment}" />
			   </Control.Template>
		 </Button.Template>
	 ClickMe!
	 </Button>

## Layout

- Grid
- Canvas
- DockPanel
- StackPanel
- WrapPanel

## Flowed Text

- FlowDocument

## HTML-Like feature set
- Reader controls

## Data

### DataTemplate

- Defines how a particular type of data should look.
- Some class has property and another property... which are applied via data template with markup with bindings to apply on the UI

## Deployment

- Classic MSI
- ClickOnce (FullTrust needed)
- XBAP (Java applet like, does not require FullTrust, runs inside browser, .Net framework is required)
- .NET 3.5 sp1

- client only framework, setup bootstrapper
- deploy via clickonce 

- Silverlight
## Designers

- Blend
- Visual Studio

## Controls #attachedproperty 

- Built-in controls  
    System.Windows.Controls
- System.Windows.Controls.Primitive (to be used as a part of other widgets and not to be used as is)

## Buttons

- RepeatButton (in primitive)
- Buttons have a content model that allows anything to be used for the caption. It could be plain text, graphics or data.
- Combination of content possible; Button>StackPanel>controls......
- Ubiquitous pattern
- Accelerator key

## Grouping

- Expander
- GroupBox

- Complex element provided for a Header by using PropertyELEMENT Syntax

- <GroupBox.Header>  
    <GroupBox.Header>
- <StackPanel>...

## Text Input

- WPF has flow document model for text formatting
- Rich Text Box in WPF has nothing to do with rtf format, but uses FlowDocumentMOdel
- PasswordBox does not share the same base class as that of RichTextBox & TextBox
- Spell Checking can be enabled by SpellCheck.IsEnabld="True"

- when XAML looks at a property set like SpellCheck.IsEnabled, it knows that it is an #attachedproperty syntax.
- TextBox control is the only one which has a magic SpellCheck property to make this work.
- Usually, the Class SpellCheck has a SetIsEnabled method

- SpellCheck.SetIsEnabled(myTextBox, true) which is the same as the previous one

- Label in front of the textbox, may need a access specifier. Label is a content control which knows only how to render its content.  
    <Label Target="{Binding ElementName=myTxt}">
- _Name:
- </Label>
- <TextBox x:Name="myTxt" />

- In Label, you can use data binding syntax to point to the target

## Events (low level control)

- Tunnelling and Bubbling events follow in pairs
- Tunnel

## Preview

- PreviewMouseDown

- Bubble

- Main event

- MouseDown

- Direct

- MouseEnter

- Commands (higher level abstractions)

- For Beginners #read:bookmark  
    https://rachel53461.wordpress.com/category/wpf-2/
## DataGrid

- Tabbing from cell to cell does not focus control #read:bookmark  
    https://mtpatel.blogspot.com/2013/05/wpf-datagrid-tabbing-from-cell-to-cell.html
- Add UserControl to each row of grid  
    https://social.msdn.microsoft.com/Forums/en-US/6658931e-e61f-492e-9f26-99b66a56b816/adding-my-usercontrol-to-each-row-of-datagrid?forum=wpf
- IEditableCollectionView  
    https://blogs.msdn.microsoft.com/vinsibal/2008/05/20/wpf-3-5-sp1-feature-ieditablecollectionview/
- WPF DataGrid pasting  
    https://stackoverflow.com/questions/4118617/wpf-datagrid-pasting
- DataGrid Tutorial  
    https://www.tutorialspoint.com/wpf/wpf_datagrid.htm
- Custom checkbox in DataGrid does not update binding  
    https://stackoverflow.com/questions/2926533/custom-checkbox-in-wpf-datagrid-does-not-update-binding
- DataGrid won't update ViewModel  
    https://stackoverflow.com/questions/14034502/datagrid-wont-update-viewmodel
- WPF DataGrid: Tabbing from cell to cell does not set focus on control  
    https://iyalovoi.wordpress.com/2009/08/21/wpf-datagrid-tabbing-from-cell-to-cell-does-not-set-focus-on-control/
- Using user control in Data Grid  
    https://zamjad.wordpress.com/2009/12/30/using-user-control-in-data-grid/
- Added new row not showing  
    https://www.infragistics.com/community/forums/f/ultimate-ui-for-wpf/19860/add-new-row-not-showing
- DataGrid Columns  
    https://www.wpf-tutorial.com/datagrid-control/custom-columns/
- WPF DataGrid application with dynamically built columns and handling events at cell level  
    https://social.msdn.microsoft.com/Forums/en-US/14a6efdf-fcd8-434c-bd46-a68aa7df1ac8/wpf-datagrid-application-with-dynamically-built-columns-and-handling-events-at-cell-level?forum=wpf
- how to Set the position of Column in datagrid wpf  
    https://stackoverflow.com/questions/3734824/how-to-set-the-position-of-column-in-datagrid-wpf
- Grid lines visibility and thickness  
    <DataGrid GridLinesVisibility="Horizontal">
         <DataGrid.CellStyle>
             <Style TargetType="DataGridCell">
                 <Setter Property="BorderThickness" Value="0,0,3,0"/>
                 <Setter Property="BorderBrush" Value="Red"/>
             </Style>
         </DataGrid.CellStyle>
- [Copy Paste](https://stackoverflow.com/questions/4118617/wpf-datagrid-pasting) / [Drag Drop](https://docs.microsoft.com/en-us/dotnet/desktop/wpf/advanced/walkthrough-enabling-drag-and-drop-on-a-user-control?view=netframeworkdesktop-4.8)

## Issues

- Menu / window/ Dialog disappears into background (behind the main app)  
    https://support.microsoft.com/en-us/help/2954125/the-wpf-dialog-box-disappears-when-it-displays-a-tooltip-or-drop-down

## How-To

- Add watermark to a textbox  
    https://docs.microsoft.com/en-us/dotnet/framework/wpf/controls/how-to-add-a-watermark-to-a-textbox
- Implementing a Window  
    https://docs.microsoft.com/en-us/dotnet/framework/wpf/app-development/wpf-windows-overview
- ColumnWidth issue - WPF DataGridColumn Width Property Works When in App but IDE gives errors  
    https://social.msdn.microsoft.com/Forums/vstudio/en-US/3a4280d6-d075-407f-8e9a-a03b38132dcd/wpf-datagridcolumn-width-property-works-when-in-app-but-ide-gives-errors
- Telerik Examples  
    https://docs.telerik.com/devtools/wpf/controls/radgridview/sdk-examples
- WPF UserControl and Trigger for Validation Error on Container  
    https://social.msdn.microsoft.com/Forums/vstudio/en-US/81c13e26-b9ea-48fe-add5-3c6258e875ac/wpf-usercontrol-and-trigger-for-validation-error-on-container?forum=wpf
- Add Validation Rule to controls with Data Binding  
    https://social.technet.microsoft.com/wiki/contents/articles/31422.wpf-passing-a-data-bound-value-to-a-validation-rule.aspx
- Data validation in WPF #read:bookmark  
    https://blog.magnusmontin.net/2013/08/26/data-validation-in-wpf/
- Radio Buttons Group Name Usercontrol  
    http://www.interact-sw.co.uk/iangblog/2010/11/15/radio-groupname-scope
- How to know if window resizing ended

- In the window constructor  
    Loaded += OnLoaded;
- Hooks into win32  
    private void OnLoaded(object sender, RoutedEventArgs e)
 {
 HwndSource source = HwndSource.FromHwnd(new WindowInteropHelper(this).Handle);
 source.AddHook(new HwndSourceHook(WndProc));

 }
 const int WM_SIZING = 0x214;
 const int WM_EXITSIZEMOVE = 0x232;
 private static bool WindowWasResized = false;
 private static IntPtr WndProc(IntPtr hwnd, int msg, IntPtr wParam, IntPtr lParam, ref bool handled)
 {
	 if (msg == WM_SIZING)
	 {
		
		 if (WindowWasResized == false)
		 {
		
		 //    'indicate the the user is resizing and not moving the window
		 WindowWasResized = true;
		 }
	 }

	 if (msg == WM_EXITSIZEMOVE)
	 {
		 // 'check that this is the end of resize and not move operation          
		 if (WindowWasResized == true)
		 {
		
		 // your stuff to do 
		 //Console.WriteLine("End");
		 HwndSource hwndSource = HwndSource.FromHwnd(hwnd);
		
		 var window = hwndSource.RootVisual as BasketRFQWindow;
		
		 window.ResetSizeToContent();
		
		 // 'set it back to false for the next resize/move
		 WindowWasResized = false;
		 }
	 }
	
	 return IntPtr.Zero;
 }

## Reference

- WPF Playlist

- [https://youtu.be/mG4l0AaYBTM](https://youtu.be/mG4l0AaYBTM)

- WPF Tutorial

- [https://www.wpftutorial.net/XAML.html](https://www.wpftutorial.net/XAML.html)

- MVVM

- MVVM Explained  
    https://www.wintellect.com/model-view-viewmodel-mvvm-explained/
- XAML Anti-Patterns  
    https://www.codemag.com/article/1505101/XAML-Anti-Patterns-Code-Behind

## Window Event Sequence  
    https://wpf.2000things.com/2012/07/30/613-window-event-sequence/
- The full sequence of events fired for a Window object are as follows.
- On application startup, if the Window is the application’s main window.  (Application events are also shown in the correct sequence).

- Application.Startup
- Window.Initialized
- Window.IsVisibleChanged
- Window.SizeChanged
- Window.LayoutUpdated
- Window.SourceInitialized
- Application.Activated
- Window.Activated
- Window.PreviewGotKeyboardFocus
- Window.IsKeyboardFocusWithinChanged
- Window.IsKeyboardFocusedChanged
- Window.GotKeyboardFocus
- Window.LayoutUpdated
- Window.Loaded
- Window.ContentRendered

- On normal application shutdown, the event sequence is:

- Window.Closing
- Window.IsVisibleChanged
- Window.Deactivated
- Application.Deactivated
- Window.IsKeyboardFocusWithinChanged
- Window.IsKeyboardFocusedChanged
- Window.LostKeyboardFocus
- Window.Closed
- Application.Exit

- When application/window loses focus (user switches to another application):

- Window.Deactivated
- Application.Deactivated
- Window.IsKeyboardFocusWithinChanged
- Window.IsKeyboardFocusedChanged
- Window.LostKeyboardFocus

- When application/window gains focus (user switches back to application):

- Application.Activated
- Window.Activated
- Window.PreviewGotKeyboardFocus
- Window.IsKeyboardFocusWithinChanged
- Window.IsKeyboardFocusChanged
- Window.GotKeyboardFocus
- Window Events  
    https://wpf.2000things.com/2010/08/22/41-window-events-at-startup-and-shutdown/
- #41 – Window Events at Startup and Shutdown

- At application startup, the Window events that are fired (in order) for the main window are:

- Initialized – Main window is being created
- IsVisibleChanged – IsVisible property set to true
- SizeChanged – Size property set to size of window
- LayoutUpdated – Window layout changes
- SourceInitialized – Window is attached to Win32 window handle
- Activated – Window becomes foreground window
- PreviewGotKeyboardFocus – Window getting focus
- IsKeyboardFocusWithinChanged – IsKeyboardFocusWithin property set to true
- IsKeyboardFocusedChanged – IsKeyboardFocused property set to true
- GotKeyboardFocus – Window now has keyboard focus
- LayoutUpdated – Window layout changes
- Loaded – Window is now laid out, fully rendered
- ContentRendered – All window content has been rendered

- At application shutdown, the Window events fired (in order) are:

- Closing – Window is going to close
- IsVisibleChanged – IsVisible property set to false
- Deactivated – Window becomes background window
- IsKeyboardFocusWithinChanged – IsKeyboardFocusWithin property set to false
- IsKeyboardFocusedChanged – IsKeyboardFocused property set to false
- LostKeyboardFocus – Window no longer has keyboard focus
- MeasureOverride ArrangeOverride  
    http://ikeptwalking.com/wpf-measureoverride-arrangeoverride-explained/

## Memory Leaks  
    https://blog.jetbrains.com/dotnet/2014/09/04/fighting-common-wpf-memory-leaks-with-dotmemory/

- Key Retention Paths  
    https://www.jetbrains.com/help/dotmemory/Key_Retention_Paths.html?Wave=12

- DataTemplateSelector  
    https://docs.microsoft.com/en-us/dotnet/api/system.windows.controls.datatemplateselector?redirectedfrom=MSDN&view=netframework-4.7.2
- Dynamic Data Templates  
    [https://www.jerriepelser.com/blog/3-ways-dynamic-data-templates/](https://www.jerriepelser.com/blog/3-ways-dynamic-data-templates/)
- Using ContentTemplateSelector  
    [https://zamjad.wordpress.com/2011/09/21/using-contenttemplateselector/http://blog.ploeh.dk/2010/12/02/Interfacesarenotabstractions/](https://zamjad.wordpress.com/2011/09/21/using-contenttemplateselector/http://blog.ploeh.dk/2010/12/02/Interfacesarenotabstractions/)
- ContentTemplate with DataTemplateSelector  
    [https://stackoverflow.com/questions/10751419/contentcontrol-with-datatemplateselector-help-needed](https://stackoverflow.com/questions/10751419/contentcontrol-with-datatemplateselector-help-needed)
- Weak Event Pattern  
    https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/weak-event-patterns
- Value Coersion  
    [http://drwpf.com/blog/category/wpf/](http://drwpf.com/blog/category/wpf/)

## History

- Older system was to use GDI/GDI+ & User32

- In Windows3.0, User32 was simply User, because software hadn't yet entered the 32-bit world

- So Microsoft created DirectX where the mandate was speed. MS worked with hardware vendors to make DirectX speedy
- DirectX API was poor for writing business software. It was a more like a game developer's toolkit API
- It understood the higher-level ingredients such as texture and gradients, that can be rendered directly by the video card. GDI/GDI+ doesn't so it needs to convert them to pixel-by-pixel instructions, which are rendered much more slowly by modern video cards.
- WPF still uses User32 because

- WPF needs to know which part of the screen belongs to which application
- WPF needs to handle & route input events

- What is WPF?

- It is a modern graphical display system for WINDOWS
- It has built-in hardware acceleration

- It is intelligent enough to have a software fallback for every hardware acceleration. 

- WPF uses DirectX under the hood for everything.
- It provides:-

- Web-like layout rather than fixed layout
- Rich drawing model, true transparent controls, ability to stack multiple layers with different opacities and native 3-D support
- Rich text model
- Animation is a first class programming concept
- Support for Audio and Video media
- Styles and templates
- Commands
- Declarative user interface
- Page based applications

- Display

- WPF uses the _system_ DPI setting and not the DPI of your physical device. E.g. if you are displaying on a 100inch projector, you will be standing several feet away and expect a jumbo sized version of controls.
- A WPF window and all the elements inside are measured using _device independent units_
- WPF assumes it takes 96 pixels to make an inch when Windows tells WPF about the standard Windows DPI setting (96 dpi)

- Physical unit size = device independent unit size * system dpi  
                         = 1/96 inch * 96 dpi
-      = 1 pixel
- For a 19inch monitor with 1600 * 1200 pixels, the pixel density is
-                      = sqrt(1600^2 + 1200^2)/19 inches
-      = 100 dpi
- Since it is more than what Windows assumes (96dpi), 96*96 pixel button will appear slightly smaller than 1 inch

- But for a 15inch monitor with resolution of 1024*768, the pixel density is
-      = sqrt(1024^2 + 768^2) / 15 inches
-        = 85 dpi
- Here a 96*96 pixel button will appear slightly larger than 1 inch
- Depending on the system DPI, the calculated pixel size may be a fractional value. In this case, WPF does not round off the values. **If an edge of an element falls between pixels, it uses anti-aliasing to blend that edge into the adjacent pixel.**

- Always use Vector graphics image rather than a bitmap. Vector graphics are defined as a set of shapes and as such they can be scaled to any size.

- Architecture

- Multilayer architecture

- Managed Layer

- PresentationFramework.dll

- Holds top level WPF types, including those that represent windows, panels, and other types of controls. 
- It also implements higher level abstractions such as styles.
- Has classes to be used directly from this assembly

- PresentationCore.dll

- Holds base types such as UIELement, Visual, from which all shapes and controls derive. 

- WindowsBase.dll

- Holds DependencyObject and DispatcherObject.

- Unmanaged Layer

- milcore.dll (Media Integration Layer Core)

- Core of the WPF rendering systems
- Has the COMPOSITION ENGINE which translates visual elements like controls into triangle and textures that Direct3D expects.
- DWM Desktop Windows Manager uses milcore.dll to render desktop
- Is considered as the engine of the managed graphics
- Just as CLR manages lifetime of a .NET application, it manages display state
- Just as CLR manages releasing objects and reclaiming memory, it manages invalidating and repainting a window.

- Grid

- RowDefinition

- Default RowHeight = Auto

- WPF performance #read:bookmark  
    https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/optimizing-performance-controls
- How to display TRACE information  
    https://docs.microsoft.com/en-us/visualstudio/debugger/how-to-display-wpf-trace-information?view=vs-2019
- Resource Dictionary And XAML Resource References #read:bookmark  
    https://docs.microsoft.com/en-us/windows/uwp/design/controls-and-patterns/resourcedictionary-and-xaml-resource-references
- Reveal Highlight Effect #read:bookmark  
    https://docs.microsoft.com/en-us/windows/uwp/design/style/reveal
- Loading XAML dynamically #read:bookmark  
    https://blogs.msmvps.com/bsonnino/2016/07/21/loading-xaml-dynamically-part-1-loading-views-dynamically/
- Move two windows together #read:bookmark  
    https://stackoverflow.com/questions/19429090/wpf-move-two-windows-together
- Style

- Change theme at runtime #read:bookmark  
    https://stackoverflow.com/questions/6229724/change-theme-at-runtime
- https://svetoslavsavov.blogspot.com/2009/07/switching-wpf-interface-themes-at.html

- XAML Performance #read:bookmark  
    https://blogs.windows.com/windowsdeveloper/2015/10/07/optimizing-your-xaml-app-for-performance-10-by-10/

- https://channel9.msdn.com/Events/Windows/Developers-Guide-to-Windows-10-RTM/Improving-XAML-Performance

- https://view.officeapps.live.com/op/view.aspx?src=http%3a%2f%2ffiles.channel9.msdn.com%2fthumbnail%2fd78b39b7-e5c3-4d64-8d12-3aecf8502152.pptx