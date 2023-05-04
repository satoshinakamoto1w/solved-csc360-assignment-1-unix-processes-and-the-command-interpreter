Download Link: https://assignmentchef.com/product/solved-csc360-assignment-1-unix-processes-and-the-command-interpreter
<br>
To learn about UNIX processes, and the command interpreter.

Background

A UNIX <strong>shell</strong> is a program that makes the facilities of the operating system available to interactive users. There are several popular UNIX shells: <em>sh</em> (the Bourne shell), <em>csh</em> (the C shell), and <em>bash</em> (the Bourne Again shell) are just a few. In this assignment, you will build <em>kapish</em>.

Your Task

You need to create a program named <em>kapish</em>. <em>kapish</em> should be a minimal but realistic <strong>k</strong>iller <strong>a</strong>pplication <strong>i</strong>nteractive UNIX <strong>sh</strong>ell.

<h1>Initialization and Termination</h1>

When first started, <em>kapish</em> should read and interpret lines from the file <em>.kapishrc</em> in your HOME directory, provided that the file exists and is readable. Note the the file name is <strong>.kapishrc</strong> (with the leading “.”, not kapishrc), and that it resides in the user’s <strong>HOME</strong> directory (not the <strong>current</strong> directory). Typically, the <em>.kapishrc</em> file contains commands to specify the terminal type and environment.

To facilitate your debugging and our testing, <em>kapish</em> should print each line that it reads from .kapishrc immediately after reading it. <em>kapish</em> should print a question mark and a space (? ) before each line.

<em>kapish</em> should terminate when the user types Control-D or <strong>exit</strong>.

<h1>Interactive Operation</h1>

After startup processing, <em>kapish</em> should read lines from the terminal, prompting with a question mark and a space (<em>? )</em>. Specifically, <em>kapish</em> repeatedly should perform the these actions:

Read a line from standard input.

Lexically analyze the line to form an array of <strong>tokens</strong>.

Syntactically analyze (i.e. parse) the token array to form <strong>command [options] [args]</strong> typically fed to the command interpreter.

Execute the <strong>command</strong>.

<h1>Lexical Analysis</h1>

Informally, a <strong>token</strong> should be a word. More formally, a token should consist of a sequence of non-whitespace characters that is separated from other tokens by whitespace characters. <em>kapish</em> should assume that no line of standard input is longer than 512 characters. If a line of standard input is longer than 512 characters, then <em>kapish</em> need not handle it properly; but it should not corrupt memory.

<h1>Execution</h1>

If the command is a <em>kapish</em> built-in, then <em>kapish</em> should execute it directly (i.e. without forking a child process). <em>kapish</em> should interpret four shell built-in commands:

If environment variable <em>var</em> does not exist, then <em>kapish</em> should create it. <em>kapish </em>should set the value of <em>var</em> to <em>value</em>, or to the empty string if <em>value</em> is omitted. Note: Initially, <em>kapish</em> inherits environment variables from its parent. <em>kapish </em>setenv <em>var </em>should be able to modify the value of an existing environment variable or create

[<em>value</em>] a new environment variable via the setenv command. <em>kapish</em> should be able to set the value of any environment variable; but the only environment variables that it explicitly uses are HOME and PATH.

unsetenv <em>var      kapish</em> should destroy the environment variable <em>var</em>. <em>kapish</em> should change<em> kapish</em>‘s working directory to <em>dir</em>, or to the HOME cd [<em>dir</em>]

directory if <em>dir</em> is omitted.

exit                     <em>kapish</em> should exit.

Note that those built-in commands should neither read from standard input nor write to standard output.

If the command is not an <em>kapish</em> built-in, then <em>kapish</em> should consider the command-name to be the name of a file that contains executable binary code. <em>kapish</em> should use the PATH environment variable to locate the binary, fork a child process and pass the filename, along with its arguments, to the <strong>execvp</strong> system call. If the attempt to execute the file fails, then <em>kapish</em> should print an error message indicating the reason for the failure.

<em>kapish</em> should print its prompt for the next standard input line only when a command has finished executing.

<h1>Process Control</h1>

All child processes forked by <em>kapish</em> should run in the foreground; <em>kapish</em> need not support background process control. However, the user must be able to kill the current child processes using Control-C. Control-C should not kill <em>kapish</em> itself.

<h1>Error Handling</h1>

<em>kapish</em> should handle an erroneous line gracefully by rejecting the line and writing a descriptive error message to standard error. <em>kapish</em> should handle <strong>all</strong> user errors; it should be impossible for the user’s input to cause <em>kapish</em> to crash.

<h1>Memory Management</h1>

<em>kapish</em> should contain no memory leaks. For every call to <strong>malloc</strong> or <strong>calloc</strong>, there should eventually be a call to <strong>free</strong>.

<h1>History Mechanism (for extra credit)</h1>

<em>kapish</em> should support a history mechanism that includes:

A <strong>history</strong> built-in command. The history command should print a list of all previously issued commands. Note that the <strong>history</strong> command should write data to standard output.

The ability to re-execute a previously issued command by typing a prefix of that command preceded by an exclamation point (<strong>!<em>commandprefix</em>)</strong>.

<em>kapish</em> need not support editing of the previously issued command. <strong>Logistics</strong>

Develop on linux.csc.uvic.ca.

The expectation is that you will devote substantial effort to creating and running test cases.

You should submit:

Your source code files.

A makefile. The first dependency rule should build your entire program, compiling with the -Wall and Werror options. The makefile should maintain object (.o) files to allow for partial builds.  A readme file.