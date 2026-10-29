---
title: "Warnings on keywords when importing input file to ABAQUS"
date: 2019-01-11 13:27:39
categories:
- "ABAQUS"
redirect_from:
- /archives/qwsw52.html
---

I want to analyze a steel frame with pin connections at both sides or one side at some beams. I found the keyword **\*Release** is very useful and convenient, so I resort to this keyword. I wrote the input file with the same syntax rules, so that it will be more convenient for me to establish more models. However, when I try to run the input file, there are warnings and errors even with the input file generated from a successfully run job in CAE. The problem is described in the following figure.

<!-- more -->

![](/uploads/images/2019/input_file_release.png){:width="1182"}

In ABAQUS/CAE, I used python to establish the model. It should be noted that I merged the whole model in the **Assembly** section. Then I edited the keywords and added the **\*Release** part before the **\*End Instance**. In the generated input file after successfully finished the job analysis, the nodes and elements are established in the **\*Instance** part. When I import this input file into ABAQUS or just run it with Abaqus Command window, warnings and errors occur as the bottom part in the above figure. The model is then established in the **\*Part** part and the keyword **\*Release** cannot be imported.

For the warnings, I rewrite the input file with the nodes and elements definition in the **\*Part** part and then there are no warnings. This is because the independent instance in abaqus and if you use a dependent instance, the nodes and elements definitions will be written in the **\*Part** part in the generated input file. The difference between the dependent and independent instance is the mesh object, part or assembly.

In the [Abaqus Keywords Reference Guide](http://abaqus.software.polimi.it/v6.14/books/key/default.htm?startat=ch17abk14.html#usb-kws-mrelease) , the level of keyword **\*Release** is either **Part** or **Part instance**. However, I added the keywords before the **\*End Instance** or the **\*End Part**, there were still error with the keywords. I tried to add the keywords somewhere else, and the error occurred as follow, which is consistent to the contents in “Abauqs keywords Reference Guide”.

*Error in job Job-1: in keyword \*RELEASE, file “Job-1.inp”, line 3593: The keyword is misplaced. It can be suboption for the following keyword(s)/level(s): instance, part*

Then I tried to run the input file in the other two ways. One method is to create a job in abaqus and to choose input file as source. Another method is to run the input file directly with Abaqus Command. With the code “***abaqus help***”, you can get all the command codes, which is very useful. The code for running the input file directly is “***abaqus job=job-name***”. However, the error still occurred.

Finally, I found the reason about this error, that is the input file directly imported in to abaqus does not support any additional keywords you added and it only support the keywords that can be generated from the commands in ABAQUS/CAE. As the prompt error shows:

*WARNING: The following keywords/parameters are not yet supported by the input file reader:*  
*———————————————————————————*  
*\*RELEASE*

The solution for this is to import the input file and then add the keywords with the function “***Edit Keywords…***” manually, though it is quite troublesome.

<div class="archived-comments" markdown="0">
<h3>4 Comments</h3>
<p class="archived-comments-note">These comments were left on the original WordPress version of this blog.</p>
<ol class="archived-comment-list">
<li class="archived-comment">
<div class="archived-comment-meta"><strong>Peggy</strong> <span>November 8, 2021 at 05:25</span></div>
<div class="archived-comment-body"><p>Great Job on your blog.</p></div>
</li>
<li class="archived-comment">
<div class="archived-comment-meta"><strong>Peggy</strong> <span>November 10, 2021 at 00:36</span></div>
<div class="archived-comment-body"><p>Hi, great explanation.</p><p>What have you added as an element number or element set label?<br/>
I need to release M1, at  beams ends. So I created sets based on the geometry selection, and as an element set label,I put the created set (eg Set-1).<br/>
It worked for a simple one storey frame, but it didn’t for the beams of a multistorey building. Do you have any idea about where the problem is?</p></div>
<ol class="archived-comment-children"><li class="archived-comment">
<div class="archived-comment-meta"><strong>Dorothy</strong> <span>November 15, 2021 at 04:16</span></div>
<div class="archived-comment-body"><p>Hi Peggy,<br/>
I tried to find the model I used in this blog but unfortunately I could not find this one. Since this blog was written years ago, I cannot remember exactly what I added as element set label. But I normally first select the nodes or elements in python script by the locations of them and give a name for the set.<br/>
From my understanding to your model description, I think the assembly of parts might be one possible reason for multistory building. You might need to merge the instances first. Otherwise there will be more than one nodes corresponding to the same position (it actually should be one node there), and then the degrees of freedom of the two or more nodes will be inconsistent. Hope this helps.</p></div>
</li></ol>
</li>
<li class="archived-comment">
<div class="archived-comment-meta"><strong>Peggy</strong> <span>November 21, 2021 at 21:36</span></div>
<div class="archived-comment-body"><p>Thank you for your answer.  I think sets would helpf if I had had merged all the individual parts together. I worked the full model as a whole instance and then I entered the release keyword for just the node labels of the ends. The beam ends were then rereased successfully.</p></div>
</li>
</ol>
</div>
