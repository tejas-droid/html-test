
<!DOCTYPE html
  PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html><head>
      <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
   <!--
This HTML was auto-generated from MATLAB code.
To make changes, update the MATLAB code and republish this document.
      --><title>Analysis of ppg signal</title><meta name="generator" content="MATLAB 9.8"><link rel="schema.DC" href="http://purl.org/dc/elements/1.1/"><meta name="DC.date" content="2021-05-12"><meta name="DC.source" content="ppgsignal.m"><style type="text/css">
html,body,div,span,applet,object,iframe,h1,h2,h3,h4,h5,h6,p,blockquote,pre,a,abbr,acronym,address,big,cite,code,del,dfn,em,font,img,ins,kbd,q,s,samp,small,strike,strong,sub,sup,tt,var,b,u,i,center,dl,dt,dd,ol,ul,li,fieldset,form,label,legend,table,caption,tbody,tfoot,thead,tr,th,td{margin:0;padding:0;border:0;outline:0;font-size:100%;vertical-align:baseline;background:transparent}body{line-height:1}ol,ul{list-style:none}blockquote,q{quotes:none}blockquote:before,blockquote:after,q:before,q:after{content:'';content:none}:focus{outine:0}ins{text-decoration:none}del{text-decoration:line-through}table{border-collapse:collapse;border-spacing:0}

html { min-height:100%; margin-bottom:1px; }
html body { height:100%; margin:0px; font-family:Arial, Helvetica, sans-serif; font-size:10px; color:#000; line-height:140%; background:#fff none; overflow-y:scroll; }
html body td { vertical-align:top; text-align:left; }

h1 { padding:0px; margin:0px 0px 25px; font-family:Arial, Helvetica, sans-serif; font-size:1.5em; color:#d55000; line-height:100%; font-weight:normal; }
h2 { padding:0px; margin:0px 0px 8px; font-family:Arial, Helvetica, sans-serif; font-size:1.2em; color:#000; font-weight:bold; line-height:140%; border-bottom:1px solid #d6d4d4; display:block; }
h3 { padding:0px; margin:0px 0px 5px; font-family:Arial, Helvetica, sans-serif; font-size:1.1em; color:#000; font-weight:bold; line-height:140%; }

a { color:#005fce; text-decoration:none; }
a:hover { color:#005fce; text-decoration:underline; }
a:visited { color:#004aa0; text-decoration:none; }

p { padding:0px; margin:0px 0px 20px; }
img { padding:0px; margin:0px 0px 20px; border:none; }
p img, pre img, tt img, li img, h1 img, h2 img { margin-bottom:0px; }

ul { padding:0px; margin:0px 0px 20px 23px; list-style:square; }
ul li { padding:0px; margin:0px 0px 7px 0px; }
ul li ul { padding:5px 0px 0px; margin:0px 0px 7px 23px; }
ul li ol li { list-style:decimal; }
ol { padding:0px; margin:0px 0px 20px 0px; list-style:decimal; }
ol li { padding:0px; margin:0px 0px 7px 23px; list-style-type:decimal; }
ol li ol { padding:5px 0px 0px; margin:0px 0px 7px 0px; }
ol li ol li { list-style-type:lower-alpha; }
ol li ul { padding-top:7px; }
ol li ul li { list-style:square; }

.content { font-size:1.2em; line-height:140%; padding: 20px; }

pre, code { font-size:12px; }
tt { font-size: 1.2em; }
pre { margin:0px 0px 20px; }
pre.codeinput { padding:10px; border:1px solid #d3d3d3; background:#f7f7f7; }
pre.codeoutput { padding:10px 11px; margin:0px 0px 20px; color:#4c4c4c; }
pre.error { color:red; }

@media print { pre.codeinput, pre.codeoutput { word-wrap:break-word; width:100%; } }

span.keyword { color:#0000FF }
span.comment { color:#228B22 }
span.string { color:#A020F0 }
span.untermstring { color:#B20000 }
span.syscmd { color:#B28C00 }
span.typesection { color:#A0522D }

.footer { width:auto; padding:10px 0px; margin:25px 0px 0px; border-top:1px dotted #878787; font-size:0.8em; line-height:140%; font-style:italic; color:#878787; text-align:left; float:none; }
.footer p { margin:0px; }
.footer a { color:#878787; }
.footer a:hover { color:#878787; text-decoration:underline; }
.footer a:visited { color:#878787; }

table th { padding:7px 5px; text-align:left; vertical-align:middle; border: 1px solid #d6d4d4; font-weight:bold; }
table td { padding:7px 5px; text-align:left; vertical-align:top; border:1px solid #d6d4d4; }





  </style></head><body><div class="content"><h1>Analysis of ppg signal</h1><!--introduction--><!--/introduction--><h2>Contents</h2><div><ul><li><a href="#1">Loading the ppg data set and converting the string of data to an array</a></li></ul></div><h2 id="1">Loading the ppg data set and converting the string of data to an array</h2><pre class="codeinput">df = readtable(<span class="string">'ppg.csv'</span>,<span class="string">'PreserveVariableNames'</span>,true);
[r , c] = size(df);
<span class="keyword">for</span> i =1:r
    df.ir(i) = {eval(cell2mat(df.ir(i)))};
    df.red(i) = {eval(cell2mat(df.red(i)))};
<span class="keyword">end</span>
df
</pre><pre class="codeoutput">
df =

  15&times;6 table

    Var1      name              time            before food         red                ir      
    ____    _________    ___________________    ___________    ______________    ______________

      0     {'tejas'}    2021-04-21 13:23:54      {'yes'}      {1&times;200 double}    {1&times;200 double}
      1     {'tejas'}    2021-04-21 13:25:06      {'yes'}      {1&times;200 double}    {1&times;200 double}
      2     {'tejas'}    2021-04-21 15:43:43      {'yes'}      {1&times;200 double}    {1&times;200 double}
      3     {'tejas'}    2021-04-21 16:07:24      {'no' }      {1&times;200 double}    {1&times;200 double}
      4     {'tejas'}    2021-04-21 16:30:03      {'no' }      {1&times;200 double}    {1&times;200 double}
      5     {'tejas'}    2021-04-21 17:15:28      {'no' }      {1&times;200 double}    {1&times;200 double}
      6     {'tejas'}    2021-04-22 14:00:18      {'no' }      {1&times;200 double}    {1&times;200 double}
      7     {'tejas'}    2021-04-22 14:01:57      {'no' }      {1&times;200 double}    {1&times;200 double}
      8     {'tejas'}    2021-04-22 14:03:59      {'no' }      {1&times;200 double}    {1&times;200 double}
      9     {'tejas'}    2021-04-22 14:08:46      {'no' }      {1&times;200 double}    {1&times;200 double}
     10     {'tejas'}    2021-04-22 15:03:56      {'no' }      {1&times;200 double}    {1&times;200 double}
     11     {'tejas'}    2021-04-22 15:16:58      {'no' }      {1&times;200 double}    {1&times;200 double}
     12     {'tejas'}    2021-04-22 15:17:37      {'no' }      {1&times;200 double}    {1&times;200 double}
     13     {'tejas'}    2021-04-22 15:31:15      {'no' }      {1&times;200 double}    {1&times;200 double}
     14     {'tejas'}    2021-04-22 15:32:19      {'no' }      {1&times;200 double}    {1&times;200 double}

</pre><p>Takeing the 7th column for analysis</p><p>Applying base line wandering using detrend matlab function</p><pre class="codeinput">ir =  cell2mat(df.ir(7));
ir = ir(10:end);
figure

plot((ir));
irnew = detrend(ir,1);
irnew = fliplr(irnew);
figure
plot((irnew));
</pre><img vspace="5" hspace="5" src="ppgsignal_01.png" alt=""> <img vspace="5" hspace="5" src="ppgsignal_02.png" alt=""> <pre class="codeinput">y = peak2peak(ir);
<span class="comment">% Peak detection using find peaks</span>

[~, indmax] = findpeaks(irnew,<span class="string">'MinPeakHeight'</span>,350,<span class="string">'MinPeakDistance'</span>,10);
[~, indmin] = findpeaks(-irnew,<span class="string">'MinPeakHeight'</span>,400,<span class="string">'MinPeakDistance'</span>,10);
figure
hold <span class="string">on</span>
plot(irnew)
plot(indmax,irnew(indmax),<span class="string">'o'</span>,<span class="string">'MarkerFaceColor'</span>,<span class="string">'r'</span>,<span class="string">'MarkerSize'</span>,10)
plot(indmin,irnew(indmin),<span class="string">'o'</span>,<span class="string">'MarkerFaceColor'</span>,<span class="string">'g'</span>,<span class="string">'MarkerSize'</span>,10);
hold <span class="string">off</span>
</pre><img vspace="5" hspace="5" src="ppgsignal_03.png" alt=""> <pre class="codeinput">diff = (irnew(indmax)-irnew(indmin));
</pre><p class="footer"><br><a href="https://www.mathworks.com/products/matlab/">Published with MATLAB&reg; R2020a</a><br></p></div><!--
##### SOURCE BEGIN #####
%% Analysis of ppg signal 
%% Loading the ppg data set and converting the string of data to an array
%% 
% 
df = readtable('ppg.csv','PreserveVariableNames',true);
[r , c] = size(df);
for i =1:r
    df.ir(i) = {eval(cell2mat(df.ir(i)))};
    df.red(i) = {eval(cell2mat(df.red(i)))};
end
df
%% 
% Takeing the 7th column for analysis
% 
% Applying base line wandering using detrend matlab function 
ir =  cell2mat(df.ir(7));
ir = ir(10:end);
figure
plot((ir));
irnew = detrend(ir,1);
irnew = fliplr(irnew);
figure
plot((irnew));
%%
y = peak2peak(ir);
% Peak detection using find peaks 
[~, indmax] = findpeaks(irnew,'MinPeakHeight',350,'MinPeakDistance',10);
[~, indmin] = findpeaks(-irnew,'MinPeakHeight',400,'MinPeakDistance',10);
figure
hold on 
plot(irnew)
plot(indmax,irnew(indmax),'o','MarkerFaceColor','r','MarkerSize',10)
plot(indmin,irnew(indmin),'o','MarkerFaceColor','g','MarkerSize',10);
hold off
%%
diff = (irnew(indmax)-irnew(indmin));
%%
%% 
% 
%%
##### SOURCE END #####
--></body></html>
