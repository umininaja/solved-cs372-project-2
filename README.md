Download Link: https://assignmentchef.com/product/solved-cs372-project-2
<br>
<ol>

 <li>Implement 2-connection client-server network application</li>

 <li>Practice using the <em>sockets</em> API</li>

 <li>Refresh programming skills</li>

</ol>

<strong> </strong>

<strong><u>The Program:</u></strong>

Design and implement a simple file transfer system, i.e., create a file transfer server and a file transfer client.  Write the <em>ftserver</em> and the <em>ftclient</em> programs.  The final version of your programs must accomplish the following tasks:

<ol>

 <li><em>ftserver</em> starts on Host A, and validates command-line parameters (&lt;SERVER_PORT&gt;).</li>

 <li><em>ftserver</em> waits on &lt;PORTNUM&gt; for a client request.</li>

 <li><em>ftclient</em> starts on Host B, and validates any pertinent command-line parameters.</li>

</ol>

(&lt;SERVER_HOST&gt;, &lt;SERVER_PORT&gt;, &lt;COMMAND&gt;, &lt;FILENAME&gt;, &lt;DATA_PORT&gt;, etc…)

<ol start="4">

 <li><em>ftserver</em> and <em>ftclient</em> establish a TCP <u>control</u> connection on &lt;SERVER_PORT&gt;. (For the remainder of this description, call this connection <em>P</em>)</li>

 <li><em>ftserver</em> waits on connection <em>P</em> for <em>ftclient</em> to send a command.</li>

 <li><em>ftclient</em> sends a command (-l (list) or -g &lt;FILENAME&gt; (get)) on connection <em>P</em>.</li>

 <li><em>ftserver</em> receives command on connection <em>P</em>.</li>

</ol>

<strong>If <em>ftclient</em> sent an <u>invalid command</u> </strong>

<ul>

 <li><em>ftserver</em> sends an error message to <em>ftclient</em> on connection <em>P</em>, and <em>ftclient</em> displays the message on-screen.</li>

</ul>

<strong>otherwise </strong>

<ul>

 <li><em>ftserver</em> initiates a TCP <u>data</u> connection with <em>ftclient</em> on &lt;DATA_PORT&gt;. (Call this connection <em>Q</em>)</li>

 <li>If <em>ftclient</em> has sent the -l command,<em> ftserver</em> sends its directory to <em>ftclient</em> on connection <em>Q</em>, and <em>ftclient</em> displays the directory on-screen.</li>

 <li>If <em>ftclient</em> has sent -g &lt;FILENAME&gt;,<em> ftserver</em> validates FILENAME, and <strong>either</strong>

  <ul>

   <li>sends the contents of FILENAME on connection <em>Q</em>. <em>ftclient</em> saves the file in the current default directory (handling “duplicate file name” error if necessary), and displays a “transfer complete” message on-screen <strong>  or  </strong></li>

   <li>sends an appropriate error message (“File not found”, etc.) to <em>ftclient</em> on connection <em>P</em>, and <em>ftclient</em> displays the message on-screen.</li>

  </ul></li>

 <li><em>ftserver</em> closes connection <em>Q (don’t leave open sockets!)</em>.</li>

</ul>

<ol start="8">

 <li><em>ftclient</em> closes connection <em>P (don’t leave open sockets!)</em> and terminates.</li>

 <li><em>ftserver</em> repeats from 2 (above) until terminated by a supervisor (SIGINT).</li>

</ol>

<strong><u>Program Requirements:</u></strong>

<ul>

 <li><em>ftserver</em> must be written in C.</li>

 <li><em>ftclient</em> must be written in Java or Python.</li>

 <li>Of course, your program <strong><u>must be well-modularized and well-documented</u></strong>.</li>

 <li>Your programs must run on a <em>flip</em> server: (<em>flip1</em>, <em>flip2</em>, <em>flip3</em>)<em>.engr.oregonstate.edu</em> o Probably the best way to do this is to use SSH Secure Shell, Putty, or another terminal emulator to log onto <em>engr.oregonstate.edu</em> using your ENGR username/password and note which <em>flip</em> you get.</li>

</ul>

o It will be easiest if you bring up two instances of the shell on the same flip server and use one to run the server, and the other to run the client (this is how I will be testing!).

<ul>

 <li>You may <u>not</u> use <em>sendfile</em> or any other predefined function that makes the problem trivial.</li>

 <li>Your program should be able to send a complete text file. You are not required to handle an “out of memory” error. Separate grading for short text files and long text files.</li>

 <li>Use the directories in which the programs are running. Don’t hard-code any directories that might be inaccessible to the graders.</li>

 <li>Combine all program files into one *.zip archive (no .7z or .gz allowed). The .zip file should not contain any folders – only files!</li>

 <li>If you use additional include-files or make-files, be sure to include them in your .zip file.</li>

 <li>Create a README containing <u>detailed</u> instructions on how to compile and run your server and client.</li>

 <li>Be <em>absolutely</em> sure to cite any references and credit any collaborators. I’m sick of giving failing grades for people not doing this.</li>

</ul>







<strong><u>Options:</u> </strong>

There are many possibilities for extra credit.  All extra credit must be documented and referenced in your program description and README.txt to receive any credit. Here are a few ideas to get you started:

<ul>

 <li>Make your server multi-threaded.</li>

 <li>Implement username/password access to the server.</li>

 <li>Allow client to change directory on the server.</li>

 <li>Transfer files additional to text files (e.g. binary files) (a text file with a non-.txt extension doesn’t count.</li>

 <li>etc…</li>

</ul>

<strong><u>Notes:</u></strong>

<ul>

 <li><em>Beej’s Guide</em> will be helpful. It has many things you’ll need for this assignment.</li>

 <li><u>Don’t</u> hard-code the port numbers</li>

 <li><u>Don’t</u> use the well-known FTP port numbers, or 30021 or 30020, as these will be probably in use (by network services or other students).</li>

 <li>We will test your system with text files only (unless your README specifies additional file types), one very large and one small.</li>

 <li>If you implement extra credit features, be sure to <u>fully</u> describe those features, and how to use them, in your README, or you won’t receive any extra credit.</li>

 <li>Programs will be accepted up to 48 hours late with a 10% penalty per 24-hour period.</li>

</ul>

<strong> </strong>

<strong><u>Example Execution:</u> </strong>

<strong> </strong>

<table width="738">

 <tbody>

  <tr>

   <td colspan="2" width="332">SERVER (flip1)</td>

   <td colspan="2" width="406">CLIENT (flip2)</td>

  </tr>

  <tr>

   <td width="138"><em>Input to console </em></td>

   <td width="194"><em>Output </em></td>

   <td width="250"><em>Input to Console </em></td>

   <td width="156"><em>Output </em></td>

  </tr>

  <tr>

   <td colspan="2" width="332"> </td>

   <td colspan="2" width="406"> </td>

  </tr>

  <tr>

   <td width="138">&gt; ftserver 30021</td>

   <td width="194"> </td>

   <td width="250"> </td>

   <td width="156"> </td>

  </tr>

  <tr>

   <td width="138"> </td>

   <td width="194">Server open on 30021</td>

   <td width="250"> </td>

   <td width="156"> </td>

  </tr>

  <tr>

   <td width="138"> </td>

   <td width="194"> </td>

   <td width="250">&gt; ftclient flip1 30021 –l 30020</td>

   <td width="156"> </td>

  </tr>

  <tr>

   <td width="138"> </td>

   <td width="194">Connection from flip2.</td>

   <td width="250"> </td>

   <td width="156"> </td>

  </tr>

  <tr>

   <td width="138"> </td>

   <td width="194">List directory requested on port 30020.</td>

   <td width="250"> </td>

   <td width="156"> </td>

  </tr>

  <tr>

   <td width="138"> </td>

   <td width="194">Sending directory contents to flip2:30020</td>

   <td width="250"> </td>

   <td width="156"> </td>

  </tr>

  <tr>

   <td width="138"> </td>

   <td width="194"> </td>

   <td width="250"> </td>

   <td width="156">Receiving directory structure from flip1:30020</td>

  </tr>

  <tr>

   <td width="138"> </td>

   <td width="194"> </td>

   <td width="250"> </td>

   <td width="156">shortfile.txt longfile.txt</td>

  </tr>

  <tr>

   <td width="138"> </td>

   <td width="194"> </td>

   <td width="250">&gt; ftclient flip1 30021 –g shortfile.txt 30020</td>

   <td width="156"> </td>

  </tr>

  <tr>

   <td width="138"> </td>

   <td width="194">Connection from flip2.</td>

   <td width="250"> </td>

   <td width="156"> </td>

  </tr>

  <tr>

   <td width="138"> </td>

   <td width="194">File “shortfile.txt” requested on port 30020.</td>

   <td width="250"> </td>

   <td width="156"> </td>

  </tr>

  <tr>

   <td width="138"> </td>

   <td width="194">Sending “shortfile.txt” to flip2:30020</td>

   <td width="250"> </td>

   <td width="156"> </td>

  </tr>

  <tr>

   <td width="138"> </td>

   <td width="194"> </td>

   <td width="250"> </td>

   <td width="156">Receiving “shortfile.txt” from flip1:30020</td>

  </tr>

  <tr>

   <td width="138"> </td>

   <td width="194"> </td>

   <td width="250"> </td>

   <td width="156">File transfer complete.</td>

  </tr>

  <tr>

   <td width="138"> </td>

   <td width="194"> </td>

   <td width="250">&gt; ftclient flip1 30021 –g longfileee.txt 30020</td>

   <td width="156"> </td>

  </tr>

  <tr>

   <td width="138"> </td>

   <td width="194">Connection from flip2.</td>

   <td width="250"> </td>

   <td width="156"> </td>

  </tr>

  <tr>

   <td width="138"> </td>

   <td width="194">File “longfileee.txt” requested on port 30020.</td>

   <td width="250"> </td>

   <td width="156"> </td>

  </tr>

  <tr>

   <td width="138"> </td>

   <td width="194">File not found. Sending error message to flip2:30021</td>

   <td width="250"> </td>

   <td width="156"> </td>

  </tr>

  <tr>

   <td width="138"> </td>

   <td width="194"> </td>

   <td width="250"> </td>

   <td width="156">flip1:30021 says FILE NOT FOUND</td>

  </tr>

  <tr>

   <td width="138"> </td>

   <td width="194"> </td>

   <td width="250">&gt;</td>

   <td width="156"> </td>

  </tr>

 </tbody>

</table>


