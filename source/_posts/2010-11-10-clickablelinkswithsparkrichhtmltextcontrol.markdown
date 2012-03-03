---
layout: post
title: Clickable Links With Spark RichEditableText Control
date: 2010-11-10 16:52
comments: true
categories: flex development howto
---
I just ran into a problem adding clickable HTML links to a Spark RichEditableText control, and none of the books that I read or sites 
that I found in Google had a completely workable solution, so I figured I'd post what I came up with here:

**The component declaration**
<code class="language-xml">
	<s:RichEditableText id="description" width="{summaryContainer.width}" textFlow="{descriptionTextFlow(clip)}" 
		editable="false" styleName="description"/>
</code>

**Event Handlers**
<pre><code class="language-javascript">
private function descriptionTextFlow(clip:Object):TextFlow {
	//	Wrap existing HTML in a TextFlow element
	var markup:String = "<TextFlow xmlns='http://ns.adobe.com/textLayout/2008'>" +
		clip.htmlDescription + 	"</TextFlow>"; 
	//	Converts html text into a TextFlow
	var flow:TextFlow = TextConverter.importToFlow(markup, TextConverter.TEXT_FIELD_HTML_FORMAT);
	// Gets dispatched whenever ANY link is clicked
	flow.addEventListener(FlowElementMouseEvent.CLICK,onLinkClickedSpark,false,0,true); 
	return flow;
}
			
private function onLinkClickedSpark(e:FlowElementMouseEvent):void
{
	// Short circuit any further processing
	e.preventDefault();
	e.stopImmediatePropagation();
	// Fire an event for our controller to handle the link - send the href text for processing
	dispatchEvent(new LinkClickedEvent(LinkClickedEvent.LINK_CLICKED,LinkElement(e.flowElement).href));
}
</code></pre>

Pay special attention to the <code class="language-javascript">flow.addEventListener()</code> call. We disable capturing and enable
weak references to cancel the existing control's behavior. Also, we use weak references because this application will replace the TextFlow
frequently with new text, and if we have old TextFlows laying around, they cause problems, and they do not get garbage collected.
