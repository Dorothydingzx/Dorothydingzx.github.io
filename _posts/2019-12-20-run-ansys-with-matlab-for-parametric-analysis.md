---
title: "Run ANSYS with MATLAB for parametric analysis"
date: 2019-12-20 08:10:18
categories:
- "ANSYS"
redirect_from:
- /archives/dry5hf.html
---

I switched from ABAQUS to ANSYS for my current research, though I am more familiar with ABAQUS. I currently have all the APDL for my model and want to do parametric analysis which requires about 7 to 8 hours for the calculation of one model with 2 cores. To improve the efficiency of running macro files in ANSYS, I decide to use MATLAB to run ANSYS.

<!-- more -->

I never used this function before and I am also a beginner in ANSYS. I searched on Google and found there are different ways to realize this function. I asked a friend for help and she sent me three files, but I still cannot understand how to do. So I focused on her method and searched again. The descriptions are not so friendly for beginners, at least for me. How I hope there was a tutorial explaining how to run ANSYS with MATLAB for parametric study. After tried and tried again, finally I could run the model one by one automatically. I decided to record the method in this article and hope I can help someone else.

**First file: run_ansys.bat**

```null
SET ANS_CONSEC=YES
SET ANSYS_LOCK=OFF
SET KMP_STACKSIZE=1024k
"C:\Program Files\ANSYS Inc\v181\ansys\bin\winx64\ANSYS181.exe" -b -i ansysinputreader.txt -o out.txt
```

The codes in the last line means ANSYS will read the ansysinputreader.txt file and store output to out.txt file. It should be noted that the default value for KMP_STACKSIZE is 512k, which may not be able to run your analysis. So you can set the value for your case. When I set it to 2048k (2 cores) in my laptop, it showed no responding in task manager. Thus, this value cannot be too large to be the same case as mine.

**Second file: ansysinputreader.txt**

```null
/INPUT,test,'txt','C:\ANSYS\paper1\',,0
```

This file tell ANSYS which file to be run and also the location of the file. One thing I should record is that I tried many times and the output file showed it could not find test.txt file. Latter I found it worked if I just use `test,'txt'` , while all the sources I could find online use `'test','txt'`. I think this difference may be caused by different versions of ANSYS.

After you have the two files and then you can run the following codes in MATLAB. I put all the files in the same folder to avoid any error resulting from location of files.

**Run in MATLAB:**

```matlab
cd 'C:\ANSYS\paper1'
!run_ansys.bat
```

After you successfully run the APDL codes in test.txt file, you will have out.txt file in your folder (defined in the first file) and the following codes will be in this file. You can also find errors, if any, in this file.

```null
         *****  ANSYS COMMAND LINE ARGUMENTS  *****
 BATCH MODE REQUESTED (-b)    = LIST
 INPUT FILE COPY MODE (-c)    = COPY

RELEASE= Release 18.1         BUILD= 18.1      UP20170403   VERSION=WINDOWS x64 
CURRENT JOBNAME=file  12:50:41  DEC 19, 2019 CP=      0.281

    1  /INPUT,test,'txt','C:\ANSYS\paper1\',,0 

RUN SETUP PROCEDURE FROM FILE= C:\Program Files\ANSYS Inc\v181\ANSYS\apdl\start.ans

/INPUT FILE= C:\Program Files\ANSYS Inc\v181\ANSYS\apdl\start.ans  LINE=       0

/INPUT FILE= C:\ANSYS\paper1\test.txt  LINE=       0

*** ANSYS - ENGINEERING ANALYSIS SYSTEM  RELEASE Release 18.1     18.1     ***
ANSYS Mechanical Enterprise                       
00000000  VERSION=WINDOWS x64   12:50:41  DEC 19, 2019 CP=      0.375
```

Parametric analysis

I want to do parametric analysis with ANSYS and thus I should use MATLAB to run different models one by one. I used a for loop in MATLAB to write the second file test.txt everytime and then run bat file. The simplified codes of for loop is demonstrated below. I used `disp(wind_speed)`to remind me which model has been run.

```matlab
matrix = [60,70,80];
for wind_speed = matrix
    fileID = fopen(filename, 'w+');
    fprintf(fileID, '/CLEAR \n');
    fprintf(fileID, '/PREP7 \n');
    fclose(fileID);
    !run_ansys.bat 
    cd 'C:\ANSYS\paper1'
    disp(wind_speed)
end
```

<div class="archived-comments" markdown="0">
<h3>5 Comments</h3>
<p class="archived-comments-note">These comments were left on the original WordPress version of this blog.</p>
<ol class="archived-comment-list">
<li class="archived-comment">
<div class="archived-comment-meta"><strong>Sateesh</strong> <span>April 14, 2021 at 18:22</span></div>
<div class="archived-comment-body"><p>Sir,<br/>
After getting output.txt…. I want to extract stress values at different nodes stored in that output file… Can you help me out to solve it</p></div>
<ol class="archived-comment-children"><li class="archived-comment">
<div class="archived-comment-meta"><strong>Dorothy</strong> <span>April 15, 2021 at 03:47</span></div>
<div class="archived-comment-body"><p>Hi Sateesh,<br/>
You might need Matlab or Python to deal with the txt file. You can search on google to see if there are some available codes to do this.</p></div>
<ol class="archived-comment-children"><li class="archived-comment">
<div class="archived-comment-meta"><strong>Sateesh</strong> <span>April 15, 2021 at 03:48</span></div>
<div class="archived-comment-body"><p>I tried with matlab sir, but not working properly…..</p></div>
</li></ol>
</li></ol>
</li>
<li class="archived-comment">
<div class="archived-comment-meta"><strong>Sateesh</strong> <span>April 15, 2021 at 03:49</span></div>
<div class="archived-comment-body"><p>There are no codes available in this topic sir…..</p></div>
</li>
<li class="archived-comment">
<div class="archived-comment-meta"><strong>Gustavo</strong> <span>June 6, 2022 at 03:43</span></div>
<div class="archived-comment-body"><p>hello, first of all. Thanks for this kind of material is rare.<br/>
And how did you run in parametric way? Could you shared more material about ? Thanks a lot.</p></div>
</li>
</ol>
</div>
