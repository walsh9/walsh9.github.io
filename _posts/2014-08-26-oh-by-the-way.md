---
title: 'Oh by the way...'
author: walsh9
layout: post
categories:
  - notes
---
If you have ASCII art that needs to be programmatically manipulated, but you want to store it in a data file without mangling it too much with weird character escapes, quoting, or unwanted line-breaks, [YAML][1] is great. 

Here's an excerpt of the [raw YAML data][2] from [asciibots.js][3]. (This is later transformed into JSON during the build process.) 

<pre>templates:
 0: |1-
       ___T_     
      | o o |    
      |__-__|    
      /| []|\    
    ()/|___|\()  
       |_|_|     
       /_|_\     
 1: |1-
      \.===./    
      | b d |    
       \_=_/     
    o==|ooo|==o  
       |___|     
      .'._.'.    
      |_| |_| 
</pre>

This uses YAML's [literal block format][4], indicated with the "`|`" character. 

> Inside literal scalars, all (indented) characters are considered to be content, including white space characters. Note that all line break characters are normalized. In addition, empty lines are not folded, though final line breaks and trailing empty lines are chomped.
> 
> There is no way to escape characters inside literal scalars. This restricts them to printable characters. In addition, there is no way to break a long literal line. 

No escape characters! Perfect! It pretty much just works but there are few small considerations. 

  1. Unless your ASCII art is perfectly left-aligned, you have to manually specify an [indentation indicator][5]. If you don't, automatic indentation detection will fail and you'll get errors when trying to parse your YAML. Here I use a "`1`" (1 space) but you can use any value you prefer. You also need to indent your ASCII art to the appropriate level relative to the rest of the document.
  2. You also have to consider whether or not you want to include the trailing line break in your data. In this case I use the "`-`" [chomping indicator][6] to request 'stripping' of the final line break.

So that's what that "`|1-`" means. 

The YAML documentation actually has it's own [ASCII art example][7] but it uses a sample that doesn't require the indentation indicator, so it can be a bit confusing when you just try to drop something else into the example and get parsing errors. Yes my first attempt went like that. Now you don't have to make the same mistake I did.

 [1]: http://www.yaml.org/
 [2]: https://github.com/walsh9/asciibots/blob/master/src/data/asciibots.yml
 [3]: http://walsh9.online/projects/asciibots-js
 [4]: http://www.yaml.org/spec/1.2/spec.html#id2795688
 [5]: http://www.yaml.org/spec/1.2/spec.html#id2793979
 [6]: http://www.yaml.org/spec/1.2/spec.html#id2794534
 [7]: http://www.yaml.org/spec/1.2/spec.html#id2760844