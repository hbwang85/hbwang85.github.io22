---
layout: post
title: "Storyboard for tableview"
date: 2015-06-16 10:49:44 +0800
comments: true
categories: 
---

##Background
Our team switch to use storyboard for configuring UI components for currrent project.  In the past, I used code to configuring UI components, and there was no issue for tablecell height autofit by using layoutSubviews or other methods. However, as a newbie for storyboard, I encountered this issue. I cann't layout tablecell with correct height. After days of learning and research, I have found the method to resolve it so I'd like to write an article to summary it.  
<!--more-->  

##Storyboard  

1. I use UILabel to show multiple lines content. The bottom spacing between label and parent view should not be constant but should be required, it shouble be greater than XX, which is shown as follow:  
{% img center /images/tableview/bottom_space.png %}  

2. The content for the label will be in the vertical center by default, which will show white space on the top and bottom of the label,  if you want to compress the label size you can set the "content hugging priority":  
{% img center /images/tableview/content_hugging_priority.png %}  

3. If you want to customize one imageview height for e.g. 100 in general, and should be considered the first one to compress the size, you should add two constraints, one is height equal 100 as required, another is height less than 100 as required, and reduce the "Content Comperssion Resistance Priority" from 750 to a small number, e.g. 250:  
{% img /images/tableview/imageview_height.png %}
{% img /images/tableview/compression_resistance_priority.png %}  

##Code

1. Should create a global tablecell variable to calculate tablecell height;  
2. In the API"htightForRowAtIndexPath":  
    - Stuff the content to tablecell firstly;  
    - update tablecell bounds to CGRectMake(0, 0, CGRectGetWidth(tableView.frame), tableView.rowHeight) in case of rotation or other scenario;  
    - set the label's preferredMaxLayoutWidth to bounds.size.width-XX, XX is equal to the left padding + right padding + 32, this step could be move to the update bounds function;
3. calculate the total height by systemLayoutSizeFittingSize(UILayoutFittingCompressedSize).height+1 (1 is the padding between content view and table cell);
4. Can cache tablecell height by using NSDictionary and using indexPath as the key;
5. If you use UITextView instead of UILabel, the total height shouble the height calculated by systemLayoutSizeFittingSize + the UITextView height. you can read the reference for more detail.  

##Reference  
1. http://www.cocoachina.com/industry/20140604/8668.html  
