---
layout: post
title: DataGrid ItemEditor in Flex 4
date: 2010-10-10 16:52
comments: true
categories: development code howto
---
I had a simple need: I have a data grid that needs to be editable. I also have an
application that has a lot of custom skinning and styling. It is simple to style
the rows of a DataGrid using CSS doing something like this:

<pre><code class="language-css">
.table
{
	header-background-skin: ClassReference("styles.DarkDataGridHeaderBackgroundSkin");
	header-style-name: tableHeader;
	alternating-item-colors: #181818, #222222;
	color: #aaaaaa;
	roll-over-color: #444444;
	selection-color: #666666;
	text-selected-color: #000000;
}

.tableHeader
{
	color: #aaaaaa;
}
</code></pre>

but those styles do not seem to apply to the cell when it is being edited:

<img src="http://idisk.me.com/cameron.pope/Public/Pictures/Skitch/TableApp.html-20101010-001817.jpg" alt="TableApp.html"/>
(notice how the editable cell has a completely different background and no contrast?)

I looked around for ways to set the style in a DataGrid when it is in an editable state
but I did not find anything. Then I figured the solution was to create an ItemEditor
that would expose a `styleName` property. That worked until it was time to actually
persist the values. I ran into strange behavior where I could not modify cells, and sometiems
the cells would become blank when clicking on them. I figured it was because the data
was not making it into the `ItemEditor` properly and it was not getting saved when editing
is complete. After a lot of searching, I finally found a spec on [Adobe's Open Source site.](http://opensource.adobe.com/wiki/display/flexsdk/Spark+ItemRenderers+for+MX+DataGrid,+Tree,+AdvancedDataGrid+(MXItemRenderer)+Specification)

It turns out there is some magic. Unless told otherwise, Flex looks for the value of 
the `editor` property of the item. Then you need to be sure to properly initialize its
value. This is the simplest `ItemEditor` that I could create in Spark for an MX DataGrid
that actualy works:

<code class="language-xml">
    <?xml version="1.0" encoding="utf-8"?>
    <s:MXDataGridItemRenderer xmlns:fx="http://ns.adobe.com/mxml/2009" 
                                                      xmlns:s="library://ns.adobe.com/flex/spark" 
                                                      xmlns:mx="library://ns.adobe.com/flex/mx" 
                                                      focusEnabled="true">	 
            <s:TextInput id="editor" top="0" left="0" right="0" bottom="0" text="{fieldData}" styleName="input" />
            <fx:Script>
                    <![CDATA[
                            [Bindable(event='newFieldData')] 
                            public function get fieldData():String
                            {
                                    return data[dataGridListData.dataField];
                            }
                            
                            override public function set data(d:Object):void
                            {
                                    super.data = d;
                                    dispatchEvent(new Event('newFieldData'));
                            }
                    ]]>
            </fx:Script>
    </s:MXDataGridItemRenderer>
</code>

And for a simple app that uses this:

<code>
    <?xml version="1.0" encoding="utf-8"?>
    <s:Application xmlns:fx="http://ns.adobe.com/mxml/2009" 
                               xmlns:s="library://ns.adobe.com/flex/spark" 
                               xmlns:mx="library://ns.adobe.com/flex/mx" minWidth="955" minHeight="600" xmlns:components="components.*">
            <fx:Declarations>
            </fx:Declarations>
            <fx:Script>
                    <![CDATA[
                            import mx.collections.ArrayCollection;
                            [Bindable] public var rows:ArrayCollection = new ArrayCollection([{val:"Row 1"},{val:"Row 2"},{val:"Row 3"}]);
                    ]]>
            </fx:Script>
            <fx:Style source="styles/main.css"/>
            <mx:DataGrid id="timelineFields" dataProvider="{rows}" top="0" left="0" bottom="0" right="0" editable="true" styleName="table">
                    <mx:columns>
                            <mx:DataGridColumn headerText="Field" dataField="val" />
                    </mx:columns>
            </mx:DataGrid>	
    </s:Application>

</code>

A simpler, working, stylable item editor would be welcome!
