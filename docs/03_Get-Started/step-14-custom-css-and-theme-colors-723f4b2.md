<!-- loio723f4b2334e344c08269159797f6f796 -->

# Step 14: Custom CSS and Theme Colors

Sometimes we need to define some more fine-granular layouts and this is when we can use the flexibility of CSS by adding custom style classes to controls and style them as we like.



## Preview

   
  
<a name="loio723f4b2334e344c08269159797f6f796__fig_r1j_pst_mr"/>The space between the button and the input field is now smaller and the output text is bold

 ![](images/SAPUI5_Walkthrough_Step_14_15_dc7fa70.png "The space between the button and the input field is now smaller and the
					output text is bold") 

> ### Caution:  
> As stated in the *Compatibility Rules*, the HTML and CSS generated by SAPUI5 is not part of the public API and may change in patch and minor releases. If you decide to override styles, you need to test and update your modifications each time SAPUI5 is updated. A prerequisite for this is that you have control over the version of SAPUI5 being used, for example in a standalone scenario. This is not possible when running your app in the SAP Fiori launchpad where SAPUI5 is centrally loaded for all apps. As such, SAP Fiori launchpad apps should not override styles.



## Coding

You can view and download all files at [Walkthrough - Step 14](https://ui5.sap.com/#/entity/sap.m.tutorial.walkthrough/sample/sap.m.tutorial.walkthrough.14).

```
html[dir="ltr"] .myAppDemoWT .myCustomButton.sapMBtn {
   margin-right: 0.125rem
}

html[dir="rtl"] .myAppDemoWT .myCustomButton.sapMBtn {
   margin-left: 0.125rem
}

.myAppDemoWT .myCustomText {
   display: inline-block;
   font-weight: bold;
}

```

We create a folder `css` which will contain our CSS files. In a new style definition file inside the `css` folder we create our custom classes combined with a custom namespace class. This makes sure that the styles will only be applied on controls that are used within our app.

A button has a default margin of `0` that we want to override: We add a custom margin of `2px` \(or `0.125rem` calculated relatively to the default font size of `16px`\) to the button with the style class `myCustomButton`. We add the CSS class `sapMBtn` to make our selector more specific: in CSS, the rule with the most specific selector "wins".

For right-to-left \(rtl\) languages, like Arabic, you set the left margin and reset the right margin as the app display is inverted. If you only use standard SAPUI5 controls, you don't need to care about this, in this case where we use custom CSS, you have to add this information.

In an additional class `myCustomText` we define a bold text and set the display to `inline-block`. This time we just define our custom class without any additional selectors. We do not set a color value here yet, we will do this in the view.



## webapp/manifest.json

```js
...
  "sap.ui5": {
	...	
	"models": {
	  ...
	},
	"resources": {
	  "css": [
		{
		  "uri": "css/style.css"
		}
	  ]
	}

  }
```

In the `resources` section of the `sap.ui5` namespace, additional resources for the app can be loaded. We load the CSS styles by defining a URI relative to the component. SAPUI5 then adds this file to the header of the HTML page as a `<link>` tag, just like in plain Web pages, and the browser loads it automatically.



## webapp/view/App.view.xml

```xml
<mvc:View
	controllerName="sap.ui.demo.walkthrough.controller.App"
	xmlns="sap.m"
	xmlns:mvc="sap.ui.core.mvc"
	displayBlock="true">
	<Shell>
		<App class="myAppDemoWT">
			<pages>
				<Page title="{i18n>homePageTitle}">
					<content>
						<Panel
							headerText="{i18n>helloPanelTitle}"
							class="sapUiResponsiveMargin"
							width="auto">
							<content>
								<Button
									text="{i18n>showHelloButtonText}"
									press=".onShowHello"
									class="myCustomButton"/>
								<Input
									value="{/recipient/name}"
									valueLiveUpdate="true"
									width="60%"/>
								<FormattedText
									htmlText="Hello {/recipient/name}"
									class="sapUiSmallMargin sapThemeHighlight-asColor myCustomText"/>
							</content>
						</Panel>
					</content>
				</Page>
			</pages>
		</App>
	</Shell>
</mvc:View>

```

The app control is configured with our custom namespace class `myAppDemoWT`. This class has no styling rules set and is used in the definition of the CSS rules to define CSS selectors that are only valid for this app.

We add our custom CSS class to the button to precisely define the space between the button and the input field. Now we have a pixel-perfect design for the panel content.

To highlight the output text, we use a `FormattedText` control which can be styled individually, either by using custom CSS or with HTML code. We add our custom CSS class \(`myCustomText`\) and add a theme-dependent CSS class to set the highlight color that is defined in the theme.

The actual color now depends on the selected theme which ensures that the color always fits to the theme and is semantically clear. For a complete list of the available CSS class names, see [CSS Classes for Theme Parameters](../04_Essentials/css-classes-for-theme-parameters-ea08f53.md).



## Conventions

-   Do not specify colors in custom CSS but use the standard theme-dependent classes instead.


**Parent topic:** [Walkthrough](walkthrough-3da5f4b.md "In this tutorial we will introduce you to all major development paradigms of SAPUI5.")

**Next:** [Step 13: Margins and Paddings](step-13-margins-and-paddings-17b87fb.md "Our app content is still glued to the corners of the letterbox. To fine-tune our layout, we can add margins and paddings to the controls that we added in the previous step.")

**Previous:** [Step 15: Nested Views](step-15-nested-views-df8c9c3.md "Our panel content is getting more and more complex and now it is time to move the panel content to a separate view. With that approach, the application structure is much easier to understand, and the individual parts of the app can be reused.")

**Related Information**  


[Descriptor for Applications, Components, and Libraries \(manifest.json\)](../04_Essentials/descriptor-for-applications-components-and-libraries-manifest-json-be0cf40.md "The descriptor for applications, components, and libraries (in short: app descriptor) is inspired by the WebApplication Manifest concept introduced by the W3C. The descriptor provides a central, machine-readable, and easy-to-access location for storing metadata associated with an application, an application component, or a library.")

[CSS Classes for Theme Parameters](../04_Essentials/css-classes-for-theme-parameters-ea08f53.md "SAPUI5 provides a set of essential adjustable colors behind the generic predefined CSS rules that enable custom content to use the respective CSS classes for the required colors.")

[Creating Themable User Interfaces](../04_Essentials/creating-themable-user-interfaces-a2c67ac.md "There are several things you should keep in mind to ensure that an application can actually be themed.")

[Compatibility Rules](../02_Read-Me-First/compatibility-rules-91f0873.md "The following sections describe what SAP can change in major, minor, and patch releases. Always consider these rules when developing apps, features, or controls with or for SAPUI5.")

[API Reference: `sap.ui.core.theming`](https://ui5.sap.com/#/api/sap.ui.core.theming)

[Samples: `sap.ui.core.theming` ](https://ui5.sap.com/#/entity/sap.ui.core.theming)
