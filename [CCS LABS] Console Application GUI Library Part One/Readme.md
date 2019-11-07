# [CCS LABS] Console Application GUI Library Part One
## Requires
- Visual Studio 2010
## License
- MS-LPL
## Technologies
- GDI+
- Console
## Topics
- User Interface
- Architecture and Design
- User Experience
## Updated
- 10/04/2012
## Description

<h1>Introduction</h1>
<div><em>Console Applications are normally not designed these days - they are just written. Back in the 1980s in the MS-DOS days we had excellently designed Console Applications - This library will show you how to implement a great GUI for your applications
 so your application can stand out from the crowd looking as professional as it works!</em></div>
<h1><span>Building the Sample</span></h1>
<div><em>The application is written in Visual Studio 2010, on a Windows Server 2012RC machine. It should work on any Windows XP and better machine with .Net 4 installed.</em></div>
<div><span style="font-size:20px; font-weight:bold">Description</span></div>
<div>In this (Part One) of the library build we implement a class which contains some basic text controls so that we can easily position our text, to the left (default), in the Middle of the line, and to the Right of the screen.</div>
<div>We also add the facility to write the desired text backwards (Reverse) and Horizontally on the left of the screen and on the Right of the Screen.</div>
<div>&nbsp;</div>
<div>We have also added to utility functions which waits for a user key press before continuing and another which clears the screen.</div>
<div>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">csharp</span>
<pre class="hidden">using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Drawing; // Not normally used in Console Apps - so add the reference

namespace ccslabsConsoleGUI
{
    class ccslabsGUI
    {

        /// &lt;summary&gt;
        /// Returns a string that will be centered on the current console screen.
        /// &lt;/summary&gt;
        /// &lt;param name=&quot;txt&quot;&gt;
        /// String: The text to center
        /// &lt;/param&gt;
        internal void PrintMiddle(string txt, bool NewLine = true)
        {
            Console.SetCursorPosition((Console.WindowWidth - txt.Length) / 2, Console.CursorTop);
            if (NewLine)
            {
                Console.WriteLine(txt);
            }
            else
            {
                Console.Write(txt);
            }
        }

        internal void PrintLeft(string txt, bool NewLine = true)
        {
            Console.SetCursorPosition(0, Console.CursorTop);
            if (NewLine)
            {
                Console.WriteLine(txt);
            }
            else
            {
                Console.Write(txt);
            }
        }

        internal void PrintRight(string txt, bool NewLine = true)
        {
            Console.SetCursorPosition((Console.WindowWidth - txt.Length), Console.CursorTop);
            if (NewLine)
            {
                Console.WriteLine(txt);
            }
            else
            {
                Console.Write(txt);
            }
        }

        /// &lt;summary&gt;
        /// Reverses the text and prints at the current cursor position
        /// &lt;/summary&gt;
        /// &lt;param name=&quot;txt&quot;&gt;&lt;/param&gt;
        /// &lt;param name=&quot;NewLine&quot;&gt;&lt;/param&gt;
        internal void PrintReverse(string txt, bool NewLine = true)
        {
            char[] nText = new char[txt.Length];
            int idx = 1; // fixes zero initialised arrays

            foreach (char c in txt.ToCharArray())
            {
                nText[(txt.Length) - idx] = c; // Zero initialised arrays !!
                idx&#43;&#43;;
            }

            if (NewLine)
            {
                Console.WriteLine(nText);
            }
            else
            {
                Console.Write(nText);
            }
        }

        internal void PrintHorizontalLeft(string txt)
        {
            int x = Console.CursorLeft;
            int y = Console.CursorTop;

            
            foreach (char c in txt.ToCharArray())
            {
                Console.SetCursorPosition(0, Console.CursorTop &#43; 1);
                Console.Write(c.ToString());
              
            }

            Console.SetCursorPosition(x, y);
        }

        internal void PrintHorizontalRight(string txt)
        {
            int x = Console.CursorLeft;
            int y = Console.CursorTop;


            foreach (char c in txt.ToCharArray())
            {
                Console.SetCursorPosition(Console.WindowWidth-1, Console.CursorTop);
                Console.Write(c.ToString());

            }

            Console.SetCursorPosition(x, y);
        }

        public void CLS()
        {
            Console.Clear();

        }

        public void WaitKey(string txt = &quot;Press Any Key to continue&quot;)
        {
            Console.WriteLine(Environment.NewLine);
            Console.Write(txt);
            Console.ReadKey();
        }
    }
}</pre>
<div class="preview">
<pre class="csharp"><span class="cs__keyword">using</span>&nbsp;System;&nbsp;
<span class="cs__keyword">using</span>&nbsp;System.Collections.Generic;&nbsp;
<span class="cs__keyword">using</span>&nbsp;System.Linq;&nbsp;
<span class="cs__keyword">using</span>&nbsp;System.Text;&nbsp;
<span class="cs__keyword">using</span>&nbsp;System.Drawing;&nbsp;<span class="cs__com">//&nbsp;Not&nbsp;normally&nbsp;used&nbsp;in&nbsp;Console&nbsp;Apps&nbsp;-&nbsp;so&nbsp;add&nbsp;the&nbsp;reference</span>&nbsp;
&nbsp;
<span class="cs__keyword">namespace</span>&nbsp;ccslabsConsoleGUI&nbsp;
{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">class</span>&nbsp;ccslabsGUI&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;Returns&nbsp;a&nbsp;string&nbsp;that&nbsp;will&nbsp;be&nbsp;centered&nbsp;on&nbsp;the&nbsp;current&nbsp;console&nbsp;screen.</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;/summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;param&nbsp;name=&quot;txt&quot;&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;String:&nbsp;The&nbsp;text&nbsp;to&nbsp;center</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;/param&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">internal</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;PrintMiddle(<span class="cs__keyword">string</span>&nbsp;txt,&nbsp;<span class="cs__keyword">bool</span>&nbsp;NewLine&nbsp;=&nbsp;<span class="cs__keyword">true</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.SetCursorPosition((Console.WindowWidth&nbsp;-&nbsp;txt.Length)&nbsp;/&nbsp;<span class="cs__number">2</span>,&nbsp;Console.CursorTop);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>&nbsp;(NewLine)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.WriteLine(txt);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.Write(txt);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">internal</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;PrintLeft(<span class="cs__keyword">string</span>&nbsp;txt,&nbsp;<span class="cs__keyword">bool</span>&nbsp;NewLine&nbsp;=&nbsp;<span class="cs__keyword">true</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.SetCursorPosition(<span class="cs__number">0</span>,&nbsp;Console.CursorTop);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>&nbsp;(NewLine)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.WriteLine(txt);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.Write(txt);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">internal</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;PrintRight(<span class="cs__keyword">string</span>&nbsp;txt,&nbsp;<span class="cs__keyword">bool</span>&nbsp;NewLine&nbsp;=&nbsp;<span class="cs__keyword">true</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.SetCursorPosition((Console.WindowWidth&nbsp;-&nbsp;txt.Length),&nbsp;Console.CursorTop);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>&nbsp;(NewLine)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.WriteLine(txt);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.Write(txt);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;Reverses&nbsp;the&nbsp;text&nbsp;and&nbsp;prints&nbsp;at&nbsp;the&nbsp;current&nbsp;cursor&nbsp;position</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;/summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;param&nbsp;name=&quot;txt&quot;&gt;&lt;/param&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;param&nbsp;name=&quot;NewLine&quot;&gt;&lt;/param&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">internal</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;PrintReverse(<span class="cs__keyword">string</span>&nbsp;txt,&nbsp;<span class="cs__keyword">bool</span>&nbsp;NewLine&nbsp;=&nbsp;<span class="cs__keyword">true</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">char</span>[]&nbsp;nText&nbsp;=&nbsp;<span class="cs__keyword">new</span>&nbsp;<span class="cs__keyword">char</span>[txt.Length];&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">int</span>&nbsp;idx&nbsp;=&nbsp;<span class="cs__number">1</span>;&nbsp;<span class="cs__com">//&nbsp;fixes&nbsp;zero&nbsp;initialised&nbsp;arrays</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">foreach</span>&nbsp;(<span class="cs__keyword">char</span>&nbsp;c&nbsp;<span class="cs__keyword">in</span>&nbsp;txt.ToCharArray())&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;nText[(txt.Length)&nbsp;-&nbsp;idx]&nbsp;=&nbsp;c;&nbsp;<span class="cs__com">//&nbsp;Zero&nbsp;initialised&nbsp;arrays&nbsp;!!</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;idx&#43;&#43;;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>&nbsp;(NewLine)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.WriteLine(nText);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.Write(nText);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">internal</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;PrintHorizontalLeft(<span class="cs__keyword">string</span>&nbsp;txt)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">int</span>&nbsp;x&nbsp;=&nbsp;Console.CursorLeft;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">int</span>&nbsp;y&nbsp;=&nbsp;Console.CursorTop;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">foreach</span>&nbsp;(<span class="cs__keyword">char</span>&nbsp;c&nbsp;<span class="cs__keyword">in</span>&nbsp;txt.ToCharArray())&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.SetCursorPosition(<span class="cs__number">0</span>,&nbsp;Console.CursorTop&nbsp;&#43;&nbsp;<span class="cs__number">1</span>);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.Write(c.ToString());&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.SetCursorPosition(x,&nbsp;y);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">internal</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;PrintHorizontalRight(<span class="cs__keyword">string</span>&nbsp;txt)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">int</span>&nbsp;x&nbsp;=&nbsp;Console.CursorLeft;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">int</span>&nbsp;y&nbsp;=&nbsp;Console.CursorTop;&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">foreach</span>&nbsp;(<span class="cs__keyword">char</span>&nbsp;c&nbsp;<span class="cs__keyword">in</span>&nbsp;txt.ToCharArray())&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.SetCursorPosition(Console.WindowWidth<span class="cs__number">-1</span>,&nbsp;Console.CursorTop);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.Write(c.ToString());&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.SetCursorPosition(x,&nbsp;y);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">public</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;CLS()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.Clear();&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">public</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;WaitKey(<span class="cs__keyword">string</span>&nbsp;txt&nbsp;=&nbsp;<span class="cs__string">&quot;Press&nbsp;Any&nbsp;Key&nbsp;to&nbsp;continue&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.WriteLine(Environment.NewLine);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.Write(txt);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Console.ReadKey();&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
}</pre>
</div>
</div>
</div>
<div class="endscriptcode">&nbsp;In the main console application you can see how these GUI elements can be easily used</div>
<div class="endscriptcode">&nbsp;</div>
<div class="endscriptcode">
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">csharp</span>
<pre class="hidden">using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace ccslabsConsoleGUI
{
    class Program
    {
        static void Main(string[] args)
        {
            ccslabsConsoleGUI.ccslabsGUI GUI = new ccslabsGUI();

            GUI.PrintMiddle(&quot;CCS LABS GUI DEMO&quot;);

            GUI.WaitKey();

            GUI.CLS();

            GUI.PrintLeft(&quot;Writing on the Left&quot;);
            GUI.PrintRight(&quot;Writing on the Right&quot;);
            GUI.PrintMiddle(&quot;Writing in the Middle of the Line&quot;);
            GUI.PrintReverse(&quot;This text is reversed&quot;);
            GUI.PrintHorizontalLeft(&quot;Left AND Down&quot;);
            GUI.PrintHorizontalRight(&quot;Right AND Down&quot;);


            GUI.WaitKey(&quot;Press any key to exit...&quot;);
        }
    }
}</pre>
<div class="preview">
<pre class="csharp"><span class="cs__keyword">using</span>&nbsp;System;&nbsp;
<span class="cs__keyword">using</span>&nbsp;System.Collections.Generic;&nbsp;
<span class="cs__keyword">using</span>&nbsp;System.Linq;&nbsp;
<span class="cs__keyword">using</span>&nbsp;System.Text;&nbsp;
&nbsp;
<span class="cs__keyword">namespace</span>&nbsp;ccslabsConsoleGUI&nbsp;
{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">class</span>&nbsp;Program&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">static</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;Main(<span class="cs__keyword">string</span>[]&nbsp;args)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ccslabsConsoleGUI.ccslabsGUI&nbsp;GUI&nbsp;=&nbsp;<span class="cs__keyword">new</span>&nbsp;ccslabsGUI();&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GUI.PrintMiddle(<span class="cs__string">&quot;CCS&nbsp;LABS&nbsp;GUI&nbsp;DEMO&quot;</span>);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GUI.WaitKey();&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GUI.CLS();&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GUI.PrintLeft(<span class="cs__string">&quot;Writing&nbsp;on&nbsp;the&nbsp;Left&quot;</span>);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GUI.PrintRight(<span class="cs__string">&quot;Writing&nbsp;on&nbsp;the&nbsp;Right&quot;</span>);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GUI.PrintMiddle(<span class="cs__string">&quot;Writing&nbsp;in&nbsp;the&nbsp;Middle&nbsp;of&nbsp;the&nbsp;Line&quot;</span>);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GUI.PrintReverse(<span class="cs__string">&quot;This&nbsp;text&nbsp;is&nbsp;reversed&quot;</span>);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GUI.PrintHorizontalLeft(<span class="cs__string">&quot;Left&nbsp;AND&nbsp;Down&quot;</span>);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GUI.PrintHorizontalRight(<span class="cs__string">&quot;Right&nbsp;AND&nbsp;Down&quot;</span>);&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;GUI.WaitKey(<span class="cs__string">&quot;Press&nbsp;any&nbsp;key&nbsp;to&nbsp;exit...&quot;</span>);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
}</pre>
</div>
</div>
</div>
<div class="endscriptcode">&nbsp;The library can be used in ANY .Net application regardless of the language used.</div>
<div class="endscriptcode">In the next installment I will be adding colour facilities - then menuing... eventually we will have a fully managed .Net Console GUI library which can be used to create really sophisticated console user interfaces like these:</div>
<div class="endscriptcode">&nbsp;</div>
<div class="endscriptcode">&nbsp;<img id="64856" src="64856-wgui078.jpg" alt="" width="600" height="449"></div>
<div class="endscriptcode"></div>
<div class="endscriptcode">This has buttons, a mouse, fields and labels... a lot better than norma?</div>
<div class="endscriptcode"></div>
<div class="endscriptcode"><img id="64857" src="64857-20110721terminal.png" alt="" width="397" height="280">l</div>
<div class="endscriptcode">Although not as pretty as the previous one - this shows you that colums can be used!</div>
<div class="endscriptcode"></div>
<div class="endscriptcode"><img id="64858" src="64858-5820439352_f8dfb0cfb3.jpg" alt="" width="500" height="374"></div>
<div class="endscriptcode"></div>
<div class="endscriptcode">Each of the sections in the image above are separate windows which update independantly of wach other!</div>
<div class="endscriptcode"></div>
<div class="endscriptcode">Although this and more will be available by the time this library is completed along with a GUI Designer! So stay tuned and place your requests for features in the Q &amp; A.</div>
</div>
</div>
<h1><em>&nbsp;</em>&nbsp;</h1>