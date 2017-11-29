
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="content-type" content="text/html; charset=UTF-8">
</head>
<body onload="initStyleGuide();">
<div id="content">
<h1>JuJa Platform Style Guide</br>
(based on <a href="https://google.github.io/styleguide/javaguide.html">Google Java Style Guide</a>)</h1>
<div class="vertical_toc" id="tocDiv"></div>

<div class="main_body">

<h2> THIS IS A DRAFT VERSION </h2>

<h2 id="s1-introduction">1 Introduction</h2>

<p>This document is the set coding standards for JuJa Platform's source code in the Java Programming Language.</p>

<p>Like the <a href="http://www.oracle.com/technetwork/java/javase/documentation/codeconvtoc-136057.html">Code Conventions for the Java TM Programming Language</a> it is important to programmers for a number of reasons:</p>
<ol>
  <li>80% of the lifetime cost of a piece of software goes to maintenance.</li>
  <li>Hardly any software is maintained for its whole life by the original author.</li>
  <li>Code conventions improve the readability of the software, allowing engineers to understand new code more quickly and thoroughly.</li>
  <li>If you ship your source code as a product, you need to make sure it is as well packaged and clean as any other product you create.</li>
</ol>


<h3 id="s1.1-terminology">1.1 Terminology notes</h3>

<p>In this document, unless otherwise clarified:</p>

<ol>
  <li>The term <em>class</em> is used inclusively to mean an "ordinary" class, enum class,
  interface or annotation type (<code class="prettyprint lang-java">@interface</code>).</li>

  <li>The term <em>member</em> (of a class) is used inclusively to mean a nested class, field,
  method, <em>or constructor</em>; that is, all top-level contents of a class except initializers
  and comments.

  </li><li>The term <em>comment</em> always refers to <em>implementation</em> comments. We do not
  use the phrase "documentation comments", instead using the common term "Javadoc."</li>
</ol>

<p>Other "terminology notes" will appear occasionally throughout the document.</p>

<h3 id="s1.2-guide-notes">1.2 Guide notes</h3>

<p>Example code in this document is <strong>non-normative</strong>. That is, while the examples
are in Google Style, they may not illustrate the <em>only</em> stylish way to represent the
code. Optional formatting choices made in examples should not be enforced as rules.</p>


<h2 id="s2-source-file-basics">2 Source file basics</h2>

<h3 id="s2.1-file-name">2.1 File name</h3>

<p>The source file name consists of the case-sensitive name of the top-level class it contains
(of which there is <a href="#s3.4.1-one-top-level-class">exactly one</a>), plus the
<code>.java</code> extension.</p>

<h3 id="s2.2-file-encoding">2.2 File encoding: UTF-8</h3>

<p>Source files are encoded in <strong>UTF-8</strong>.</p>

<h3 id="s2.3-special-characters">2.3 Special characters</h3>

<h4 id="s2.3.1-whitespace-characters">2.3.1 Whitespace characters</h4>

<p>Aside from the line terminator sequence, the <strong>ASCII horizontal space
character</strong> (<strong>0x20</strong>) is the only whitespace character that appears
anywhere in a source file. This implies that:</p>

<ol>
  <li>All other whitespace characters in string and character literals are escaped.</li>

  <li>Tab characters are <strong>not</strong> used for indentation.</li>
</ol>

<h4 id="s2.3.2-special-escape-sequences">2.3.2 Special escape sequences</h4>

<p>For any character that has a
<a href="http://docs.oracle.com/javase/tutorial/java/data/characters.html">
  special escape sequence</a>
(<code class="prettyprint lang-java">\b</code>,
<code class="prettyprint lang-java">\t</code>,
<code class="prettyprint lang-java">\n</code>,
<code class="prettyprint lang-java">\f</code>,
<code class="prettyprint lang-java">\r</code>,
<code class="prettyprint lang-java">\"</code>,
<code class="prettyprint lang-java">\'</code> and
<code class="prettyprint lang-java">\\</code>), that sequence
is used rather than the corresponding octal
(e.g.&#160;<code class="badcode">\012</code>) or Unicode
(e.g.&#160;<code class="badcode">\u000a</code>) escape.</p>

<h4 id="s2.3.3-non-ascii-characters">2.3.3 Non-ASCII characters</h4>

<p>For the remaining non-ASCII characters, either the actual Unicode character
(e.g.&#160;<code class="prettyprint lang-java">&#8734;</code>) or the equivalent Unicode escape
(e.g.&#160;<code class="prettyprint lang-java">\u221e</code>) is used. The choice depends only on
which makes the code <strong>easier to read and understand</strong>, although Unicode escapes
outside string literals and comments are strongly discouraged.</p>

<p class="tip"><strong>Tip:</strong> In the Unicode escape case, and occasionally even when actual
Unicode characters are used, an explanatory comment can be very helpful.</p>

<p>Examples:</p>

<table>
  <tbody><tr>
    <th>Example</th>
    <th>Discussion</th>
  </tr>

  <tr>
    <td><code class="prettyprint lang-java">String unitAbbrev = "&#956;s";</code></td>
    <td>Best: perfectly clear even without a comment.</td>
  </tr>

  <tr>
    <td><code class="prettyprint lang-java">String unitAbbrev = "\u03bcs"; // "&#956;s"</code></td>
    <td>Allowed, but there's no reason to do this.</td>
  </tr>

  <tr>
    <td><code class="prettyprint lang-java">String unitAbbrev = "\u03bcs";
      // Greek letter mu, "s"</code></td>
    <td>Allowed, but awkward and prone to mistakes.</td>
  </tr>

  <tr>
    <td><code class="badcode">String unitAbbrev = "\u03bcs";</code></td>
    <td>Poor: the reader has no idea what this is.</td>
  </tr>

  <tr>
     <td><code class="prettyprint lang-java">return '\ufeff' + content;
       // byte order mark</code></td>
     <td>Good: use escapes for non-printable characters, and comment if necessary.</td>
  </tr>
</tbody></table>

<p class="tip"><strong>Tip:</strong> Never make your code less readable simply out of fear that
some programs might not handle non-ASCII characters properly. If that should happen, those
programs are <strong>broken</strong> and they must be <strong>fixed</strong>.</p>


<a name="filestructure"></a>
<h2 id="s3-source-file-structure">3 Source file structure</h2>

<div>
<p>A source file consists of, <strong>in order(Non-default IntelliJ IDEA settings! To be discussed!)</strong>:</p>

<ol>
  <li>License or copyright information, if present</li>
  <li>Package statement</li>
  <li>Import statements</li>
  <li>Exactly one top-level class</li>
</ol>
</div>

<p><strong>Exactly one blank line</strong> separates each section that is present.</p>

<h3 id="s3.1-copyright-statement">3.1 License or copyright information, if present</h3>

<p>If license or copyright information belongs in a file, it belongs here.</p>



<h3 id="s3.2-package-statement">3.2 Package statement</h3>

<p>The package statement is <strong>not line-wrapped</strong>. The column limit (Section 4.4,
<a href="#s4.4-column-limit">Column limit: 120</a>) does not apply to package statements.</p>

<a name="imports"></a>
<h3 id="s3.3-import-statements">3.3 Import statements</h3>

<h4 id="s3.3.1-wildcard-imports">3.3.1 No wildcard imports (<strong>IntelliJ IDEA Settings → Editor → Code Style → Java → Imports → Class count to use... → any big number</strong>)</h4>

<p><strong>Wildcard imports</strong>, static or otherwise, <strong>are not used</strong>.</p>

<h4 id="s3.3.2-import-line-wrapping">3.3.2 No line-wrapping</h4>

<p>Import statements are <strong>not line-wrapped</strong>. The column limit (Section 4.4,
<a href="#s4.4-column-limit">Column limit: 100</a>) does not apply to import
statements.</p>

<h4 id="s3.3.3-import-ordering-and-spacing">3.3.3 Ordering and spacing</h4>

<p>Imports are ordered as follows(<strong>IntelliJ IDEA default settings</strong>):</p>

<ol>
  <li>All static imports in a single block.</li>
  <li>All non-static java core (e.g. javax, java.util) imports in a single block.</li>
  <li>All other non-static imports in a single block.</li>
</ol>

<p>If there are both static and non-static imports, a single blank line separates the two 
blocks. Two single lines separate three blocks if both non-static java core and other non-static packages present. There are no other blank lines between import statements.</p>

<p>Within each block the imported names appear in ASCII sort order. (<strong>Note:</strong>
this is not the same as the import <em>statements</em> being in ASCII sort order, since '.'
sorts before ';'.)</p>



<h4 id="s3.3.4-import-class-not-static">3.3.4 No static import for classes</h4>

<p>Static import is not used for static nested classes. They are imported with
normal imports.</p>

<h3 id="s3.4-class-declaration">3.4 Class declaration</h3>

<a name="oneclassperfile"></a>
<h4 id="s3.4.1-one-top-level-class">3.4.1 Exactly one top-level class declaration</h4>

<p>Each top-level class resides in a source file of its own.</p>

<a name="s3.4.2-class-member-ordering"></a>
<h4 id="s3.4.2-ordering-class-contents">3.4.2 Ordering of class contents</h4>

<p>The order you choose for the members and initializers of your class can have a great effect on
learnability. However, there's no single correct recipe for how to do it; different classes may
order their contents in different ways.</p>

<p>What is important is that each class uses <strong><em>some</em> logical order</strong>, which its
maintainer could explain if asked. For example, new methods are not just habitually added to the end
of the class, as that would yield "chronological by date added" ordering, which is not a logical
ordering.</p>



<a name="overloads"></a>
<h5 id="s3.4.2.1-overloads-never-split">3.4.2.1 Overloads: never split</h5>

<p>When a class has multiple constructors, or multiple methods with the same name, these appear
sequentially, with no other code in between (not even private members).</p>

<h2 id="s4-formatting">4 Formatting</h2>

<p class="terminology"><strong>Terminology Note:</strong> <em>block-like construct</em> refers to
the body of a class, method or constructor. Note that, by Section 4.8.3.1 on
<a href="#s4.8.3.1-array-initializers">array initializers</a>, any array initializer
<em>may</em> optionally be treated as if it were a block-like construct.</p>

<a name="braces"></a>
<h3 id="s4.1-braces">4.1 Braces</h3>

<h4 id="s4.1.1-braces-always-used">4.1.1 Braces are used where optional</h4>

<p>Braces are used with
<code class="prettyprint lang-java">if</code>,
<code class="prettyprint lang-java">else</code>,
<code class="prettyprint lang-java">for</code>,
<code class="prettyprint lang-java">do</code> and
<code class="prettyprint lang-java">while</code> statements, even when the
body is empty or contains only a single statement.</p>

<h4 id="s4.1.2-blocks-k-r-style">4.1.2 Nonempty blocks: K &amp; R style</h4>

<p>Braces follow the Kernighan and Ritchie style
("<a href="http://www.codinghorror.com/blog/2012/07/new-programming-jargon.html">Egyptian brackets</a>")
for <em>nonempty</em> blocks and block-like constructs:</p>

<ul>
  <li>No line break before the opening brace.</li>

  <li>Line break after the opening brace.</li>

  <li>Line break before the closing brace.</li>

  <li>Line break after the closing brace, <em>only if</em> that brace terminates a statement or
  terminates the body of a method, constructor, or <em>named</em> class.
  For example, there is <em>no</em> line break after the brace if it is followed by
  <code class="prettyprint lang-java">else</code> or a comma.</li>
</ul>

<p>Examples:</p>

<pre class="prettyprint lang-java">return () -&gt; {
    while (condition()) {
        method();
    }
};

return new MyClass() {
    @Override public void method() {
        if (condition()) {
            try {
                something();
            } catch (ProblemException e) {
                recover();
            }
        } else if (otherCondition()) {
            somethingElse();
        } else {
            lastThing();
        }
    }
};
</pre>

<p>A few exceptions for enum classes are given in Section 4.8.1,
<a href="#s4.8.1-enum-classes">Enum classes</a>.</p>

<a name="emptyblocks"></a>
<h4 id="s4.1.3-braces-empty-blocks">4.1.3 Empty blocks: may be concise</h4>

<p>An empty block or block-like construct may be in K &amp; R style (as described in
<a href="#s4.1.2-blocks-k-r-style">Section 4.1.2</a>). Alternatively, it may be closed immediately
after it is opened, with no characters or line break in between
(<code class="prettyprint lang-java">{}</code>), <strong>unless</strong> it is part of a
<em>multi-block statement</em> (one that directly contains multiple blocks:
<code class="prettyprint lang-java">if/else</code> or
<code class="prettyprint lang-java">try/catch/finally</code>).</p>

<p>Examples:</p>

<pre class="prettyprint lang-java">  // This is acceptable
    void doNothing() {}

    // This is equally acceptable
    void doNothingElse() {
    }
</pre>
<pre class="prettyprint lang-java badcode">  // This is not acceptable: No concise empty blocks in a multi-block statement
    try {
        doSomething();
    } catch (Exception e) {}
</pre>

<h3 id="s4.2-block-indentation">4.2 Block indentation: <strong>+4 spaces (IntelliJ IDEA default settings)</strong></h3>

<p>Each time a new block or block-like construct is opened, the indent increases by two
spaces. When the block ends, the indent returns to the previous indent level. The indent level
applies to both code and comments throughout the block. (See the example in Section 4.1.2,
<a href="#s4.1.2-blocks-k-r-style">Nonempty blocks: K &amp; R Style</a>.)</p>

<h3 id="s4.3-one-statement-per-line">4.3 One statement per line</h3>

<p>Each statement is followed by a line break.</p>

<a name="columnlimit"></a>
<h3 id="s4.4-column-limit">4.4 Column limit: <strong>120 (IntelliJ IDEA default settings)</strong></h3>

<p>Java code has a column limit of <strong>120 (IntelliJ IDEA default)</strong> characters. A "character" means any Unicode code point.
Except as noted below, any line that would exceed this limit must be line-wrapped, as explained in
Section 4.5, <a href="#s4.5-line-wrapping">Line-wrapping</a>.
</p>

<p class="tip">Each Unicode code point counts as one character, even if its display width is
greater or less. For example, if using
<a href="https://en.wikipedia.org/wiki/Halfwidth_and_fullwidth_forms">fullwidth characters</a>,
you may choose to wrap the line earlier than where this rule strictly requires.</p>

<p><strong>Exceptions:</strong></p>

<ol>
  <li>Lines where obeying the column limit is not possible (for example, a long URL in Javadoc,
  or a long JSNI method reference).</li>

  <li><code class="prettyprint lang-java">package</code> and
  <code class="prettyprint lang-java">import</code> statements (see Sections
  3.2 <a href="#s3.2-package-statement">Package statement</a> and
  3.3 <a href="#s3.3-import-statements">Import statements</a>).</li>

  <li>Command lines in a comment that may be cut-and-pasted into a shell.</li>
</ol>

<h3 id="s4.5-line-wrapping">4.5 Line-wrapping</h3>

<p class="terminology"><strong>Terminology Note:</strong> When code that might otherwise legally
occupy a single line is divided into multiple lines, this activity is called
<em>line-wrapping</em>.</p>

<p>There is no comprehensive, deterministic formula showing <em>exactly</em> how to line-wrap in
every situation. Very often there are several valid ways to line-wrap the same piece of code.</p>

<p class="note"><strong>Note:</strong> While the typical reason for line-wrapping is to avoid
overflowing the column limit, even code that would in fact fit within the column limit <em>may</em>
be line-wrapped at the author's discretion.</p>

<p class="tip"><strong>Tip:</strong> Extracting a method or local variable may solve the problem
without the need to line-wrap.</p>

<h4 id="s4.5.1-line-wrapping-where-to-break">4.5.1 Where to break</h4>

<p>The prime directive of line-wrapping is: prefer to break at a
<strong>higher syntactic level</strong>. Also:</p>

<ol>
  <li>When a line is broken at a <em>non-assignment</em> operator the break comes <em>before</em>
  the symbol. (Note that this is not the same practice used in Google style for other languages,
  such as C++ and JavaScript.)
    <ul>
      <li>This also applies to the following "operator-like" symbols:
        <ul>
          <li>the dot separator (<code class="prettyprint lang-java">.</code>)</li>
          <li>the two colons of a method reference
          (<code class="prettyprint lang-java">::</code>)</li>
          <li>an ampersand in a type bound
          (<code class="prettyprint lang-java">&lt;T extends Foo &amp; Bar&gt;</code>)</li>
          <li>a pipe in a catch block
          (<code class="prettyprint lang-java">catch (FooException | BarException e)</code>).</li>
        </ul>
      </li>
    </ul>
  </li>

  <li>When a line is broken at an <em>assignment</em> operator the break typically comes
  <em>after</em> the symbol, but either way is acceptable.
    <ul>
      <li>This also applies to the "assignment-operator-like" colon in an enhanced
      <code class="prettyprint lang-java">for</code> ("foreach") statement.</li>
    </ul>
  </li>

  <li>A method or constructor name stays attached to the open parenthesis
  (<code class="prettyprint lang-java">(</code>) that follows it.</li>

  <li>A comma (<code class="prettyprint lang-java">,</code>) stays attached to the token that
  precedes it.</li>

  <li>A line is never broken adjacent to the arrow in a lambda, except that a
  break may come immediately after the arrow if the body of the lambda consists
  of a single unbraced expression. Examples:
<pre class="prettyprint lang-java">MyLambda&lt;String, Long, Object&gt; lambda =
    (String label, Long value, Object obj) -&gt; {
        ...
    };

Predicate&lt;String&gt; predicate = str -&gt;
    longExpressionInvolving(str);
</pre>
  </li>
</ol>

<p class="note"><strong>Note:</strong> The primary goal for line wrapping is to have clear
code, <em>not necessarily</em> code that fits in the smallest number of lines.</p>

<a name="indentation"></a>
<h4 id="s4.5.2-line-wrapping-indent">4.5.2 Indent continuation lines at least +4 spaces</h4>

<p>When line-wrapping, each line after the first (each <em>continuation line</em>) is indented
at least +4 from the original line.</p>

<p>When there are multiple continuation lines, indentation may be varied beyond +4 as
desired. In general, two continuation lines use the same indentation level if and only if they
begin with syntactically parallel elements.</p>

<p>Section 4.6.3 on <a href="#s4.6.3-horizontal-alignment">Horizontal alignment</a> addresses
the discouraged practice of using a variable number of spaces to align certain tokens with
previous lines.</p>

<h3 id="s4.6-whitespace">4.6 Whitespace</h3>

<h4 id="s4.6.1-vertical-whitespace">4.6.1 Vertical Whitespace</h4>

<p>A single blank line appears:</p>

<ol>
  <li><em>Between</em> consecutive members or initializers of a class: fields, constructors,
  methods, nested classes, static initializers, and instance initializers.
  <ul>
    <li><span class="exception"><strong>Exception:</strong> A blank line between two consecutive
    fields (having no other code between them) is optional. Such blank lines are used as needed to
    create <em>logical groupings</em> of fields.</span></li>
    <li><span class="exception"><strong>Exception:</strong> Blank lines between enum constants are
    covered in <a href="#s4.8.1-enum-classes">Section 4.8.1</a>.</span></li>
  </ul>
  </li>

  <li>Between statements, <em>as needed</em> to organize the code into logical subsections.
  
  </li><li><em>Optionally</em> before the first member or initializer, or after the last member or
  initializer of the class (neither encouraged nor discouraged).</li>

  <li>As required by other sections of this document (such as Section 3,
  <a href="#s3-source-file-structure">Source file structure</a>, and Section 3.3,
  <a href="#s3.3-import-statements">Import statements</a>).</li>
</ol>

<p><em>Multiple</em> consecutive blank lines are permitted, but never required (or encouraged).</p>

<h4 id="s4.6.2-horizontal-whitespace">4.6.2 Horizontal whitespace</h4>

<p>Beyond where required by the language or other style rules, and apart from literals, comments and
Javadoc, a single ASCII space also appears in the following places <strong>only</strong>.</p>

<ol>
  <li>Separating any reserved word, such as
  <code class="prettyprint lang-java">if</code>,
  <code class="prettyprint lang-java">for</code> or
  <code class="prettyprint lang-java">catch</code>, from an open parenthesis
  (<code class="prettyprint lang-java">(</code>)
  that follows it on that line</li>

  <li>Separating any reserved word, such as
  <code class="prettyprint lang-java">else</code> or
  <code class="prettyprint lang-java">catch</code>, from a closing curly brace
  (<code class="prettyprint lang-java">}</code>) that precedes it on that line</li>

  <li>Before any open curly brace
  (<code class="prettyprint lang-java">{</code>), with two exceptions:
  
  <ul>
    <li><code class="prettyprint lang-java">@SomeAnnotation({a, b})</code> (no space is used)</li>

    <li><code class="prettyprint lang-java">String[][] x = {{"foo"}}; </code> (no space is required
    between <code class="prettyprint lang-java">{{</code>, by item 8 below)</li>
	
  </ul>
  </li>

  <li>On both sides of any binary or ternary operator. This also applies to the following
  "operator-like" symbols:
  <ul>
    <li>the ampersand in a conjunctive type bound:
    <code class="prettyprint lang-java">&lt;T extends Foo &amp; Bar&gt;</code></li>

    <li>the pipe for a catch block that handles multiple exceptions:
    <code class="prettyprint lang-java">catch (FooException | BarException e)</code></li>

    <li>the colon (<code class="prettyprint lang-java">:</code>) in an enhanced
    <code class="prettyprint lang-java">for</code> ("foreach") statement</li>

    <li>the arrow in a lambda expression:
    <code class="prettyprint lang-java">(String str) -&gt; str.length()</code></li>
  </ul>
    but not

  <ul>
    <li>the two colons (<code class="prettyprint lang-java">::</code>) of a method reference, which
    is written like <code class="prettyprint lang-java">Object::toString</code></li>
    <li>the dot separator (<code class="prettyprint lang-java">.</code>), which is written like
    <code class="prettyprint lang-java">object.toString()</code></li>
  </ul>
  </li>

  <li>After <code class="prettyprint lang-java">,:;</code> or the closing parenthesis
  (<code class="prettyprint lang-java">)</code>) of a cast</li>

  <li>On both sides of the double slash (<code class="prettyprint lang-java">//</code>) that
  begins an end-of-line comment. Here, multiple spaces are allowed, but not required.</li>

  <li>Between the type and variable of a declaration:
  <code class="prettyprint lang-java">List&lt;String&gt; list</code></li>

  <li><em>Optional</em> just inside both braces of an array initializer
  <ul>
    <li><code class="prettyprint lang-java">new int[] {5, 6}</code> and
    <code class="prettyprint lang-java">new int[] { 5, 6 }</code> are both valid</li>
  </ul>
  </li>
</ol>

This rule is never interpreted as requiring or forbidding additional space at the start or
end of a line; it addresses only <em>interior</em> space.

<h4 id="s4.6.3-horizontal-alignment">4.6.3 Horizontal alignment: never required</h4>

<p class="terminology"><strong>Terminology Note:</strong> <em>Horizontal alignment</em> is the
practice of adding a variable number of additional spaces in your code with the goal of making
certain tokens appear directly below certain other tokens on previous lines.</p>

<p>This practice is permitted, but is <strong>never required</strong> by Google Style. It is not
even required to <em>maintain</em> horizontal alignment in places where it was already used.</p>

<p>Here is an example without alignment, then using alignment:</p>

<pre class="prettyprint lang-java">private int x; // this is fine
private Color color; // this too

private int   x;      // permitted, but future edits
private Color color;  // may leave it unaligned
</pre>

<p class="tip"><strong>Tip:</strong> Alignment can aid readability, but it creates problems for
future maintenance.  Consider a future change that needs to touch just one line. This change may
leave the formerly-pleasing formatting mangled, and that is <strong>allowed</strong>. More often
it prompts the coder (perhaps you) to adjust whitespace on nearby lines as well, possibly
triggering a cascading series of reformattings. That one-line change now has a "blast radius."
This can at worst result in pointless busywork, but at best it still corrupts version history
information, slows down reviewers and exacerbates merge conflicts.</p>

<a name="parentheses"></a>
<h3 id="s4.7-grouping-parentheses">4.7 Grouping parentheses: recommended</h3>

<p>Optional grouping parentheses are omitted only when author and reviewer agree that there is no
reasonable chance the code will be misinterpreted without them, nor would they have made the code
easier to read. It is <em>not</em> reasonable to assume that every reader has the entire Java
operator precedence table memorized.</p>

<h3 id="s4.8-specific-constructs">4.8 Specific constructs</h3>

<h4 id="s4.8.1-enum-classes">4.8.1 Enum classes</h4>

<p>After each comma that follows an enum constant, a line break is optional. Additional blank
lines (usually just one) are also allowed. This is one possibility:

</p><pre class="prettyprint lang-java">private enum Answer {
  YES {
    @Override public String toString() {
      return "yes";
    }
  },

  NO,
  MAYBE
}
</pre>

<p>An enum class with no methods and no documentation on its constants may optionally be formatted
as if it were an array initializer (see Section 4.8.3.1 on
<a href="#s4.8.3.1-array-initializers">array initializers</a>).</p>

<pre class="prettyprint lang-java">private enum Suit { CLUBS, HEARTS, SPADES, DIAMONDS }
</pre>

<p>Since enum classes <em>are classes</em>, all other rules for formatting classes apply.</p>

<a name="localvariables"></a>
<h4 id="s4.8.2-variable-declarations">4.8.2 Variable declarations</h4>

<h5 id="s4.8.2.1-variables-per-declaration">4.8.2.1 One variable per declaration</h5>

<p>Every variable declaration (field or local) declares only one variable: declarations such as
<code class="badcode">int a, b;</code> are not used.</p>

<p><strong>Exception:</strong> Multiple variable declarations are acceptable in the header of a
<code class="prettyprint lang-java">for</code> loop.</p>

<h5 id="s4.8.2.2-variables-limited-scope">4.8.2.2 Declared when needed</h5>

<p>Local variables are <strong>not</strong> habitually declared at the start of their containing
block or block-like construct. Instead, local variables are declared close to the point they are
first used (within reason), to minimize their scope. Local variable declarations typically have
initializers, or are initialized immediately after declaration.</p>

<h4 id="s4.8.3-arrays">4.8.3 Arrays</h4>

<h5 id="s4.8.3.1-array-initializers">4.8.3.1 Array initializers: can be "block-like"</h5>

<p>Any array initializer may <em>optionally</em> be formatted as if it were a "block-like
construct." For example, the following are all valid (<strong>not</strong> an exhaustive
list):</p>

<pre class="prettyprint lang-java">new int[] {           new int[] {
  0, 1, 2, 3            0,
}                       1,
                        2,
new int[] {             3,
  0, 1,               }
  2, 3
}                     new int[]
                          {0, 1, 2, 3}
</pre>

<h5 id="s4.8.3.2-array-declarations">4.8.3.2 No C-style array declarations</h5>

<p>The square brackets form a part of the <em>type</em>, not the variable:
<code class="prettyprint lang-java">String[] args</code>, not
<code class="badcode">String args[]</code>.</p>

<h4 id="s4.8.4-switch">4.8.4 Switch statements</h4>



<p class="terminology"><strong>Terminology Note:</strong> Inside the braces of a
<em>switch block</em> are one or more <em>statement groups</em>. Each statement group consists of
one or more <em>switch labels</em> (either <code class="prettyprint lang-java">case FOO:</code> or
<code class="prettyprint lang-java">default:</code>), followed by one or more statements (or, for
the <em>last</em> statement group, <em>zero</em> or more statements).</p>

<h5 id="s4.8.4.1-switch-indentation">4.8.4.1 Indentation</h5>

<p>As with any other block, the contents of a switch block are indented <strong>+4 (IntelliJ IDEA default settings)</strong>.</p>

<p>After a switch label, there is a line break, and the indentation level is increased <strong>+4 spaces (IntelliJ IDEA default settings)</strong>, exactly
as if a block were being opened. The following switch label returns to the previous indentation
level, as if a block had been closed.</p>

<a name="fallthrough"></a>
<h5 id="s4.8.4.2-switch-fall-through">4.8.4.2 Fall-through: commented</h5>

<p>Within a switch block, each statement group either terminates abruptly (with a
<code class="prettyprint lang-java">break</code>,
<code class="prettyprint lang-java">continue</code>,
<code class="prettyprint lang-java">return</code> or thrown exception), or is marked with a comment
to indicate that execution will or <em>might</em> continue into the next statement group. Any
comment that communicates the idea of fall-through is sufficient (typically
<code class="prettyprint lang-java">// fall through</code>). This special comment is not required in
the last statement group of the switch block. Example:</p>

<pre class="prettyprint lang-java">switch (input) {
  case 1:
  case 2:
    prepareOneOrTwo();
    // fall through
  case 3:
    handleOneTwoOrThree();
    break;
  default:
    handleLargeNumber(input);
}
</pre>

<p>Notice that no comment is needed after <code class="prettyprint lang-java">case 1:</code>, only
at the end of the statement group.</p>

<h5 id="s4.8.4.3-switch-default">4.8.4.3 The <code>default</code> case is present</h5>

<p>Each switch statement includes a <code class="prettyprint lang-java">default</code> statement
group, even if it contains no code.</p>

<p><strong>Exception:</strong> A switch statement for an <code>enum</code> type <em>may</em> omit
the <code class="prettyprint lang-java">default</code> statement group, <em>if</em> it includes
explicit cases covering <em>all</em> possible values of that type. This enables IDEs or other static
analysis tools to issue a warning if any cases were missed.

</p>

<a name="annotations"></a>
<h4 id="s4.8.5-annotations">4.8.5 Annotations</h4>

<p>Annotations applying to a class, method or constructor appear immediately after the
documentation block, and each annotation is listed on a line of its own (that is, one annotation
per line). These line breaks do not constitute line-wrapping (Section
4.5, <a href="#s4.5-line-wrapping">Line-wrapping</a>), so the indentation level is not
increased. Example:</p>

<pre class="prettyprint lang-java">@Override
@Nullable
public String getNameIfPresent() { ... }
</pre>

<p class="exception"><strong>Exception:</strong> A <em>single</em> parameterless annotation
<em>may</em> instead appear together with the first line of the signature, for example:</p>

<pre class="prettyprint lang-java">@Override public int hashCode() { ... }
</pre>

<p>Annotations applying to a field also appear immediately after the documentation block, but in
this case, <em>multiple</em> annotations (possibly parameterized) may be listed on the same line;
for example:</p>

<pre class="prettyprint lang-java">@Partial @Mock DataLoader loader;
</pre>

<p>There are no specific rules for formatting annotations on parameters, local variables, or types.
</p>

<a name="comments"></a>
<h4 id="s4.8.6-comments">4.8.6 Comments</h4>

<p>This section addresses <em>implementation comments</em>. Javadoc is addressed separately in
Section 7, <a href="#s7-javadoc">Javadoc</a>.</p>

<p>Any line break may be preceded by arbitrary whitespace followed by an implementation comment.
Such a comment renders the line non-blank.</p>

<h5 id="s4.8.6.1-block-comment-style">4.8.6.1 Block comment style</h5>

<p>Block comments are indented at the same level as the surrounding code. They may be in
<code class="prettyprint lang-java">/* ... */</code> style or
<code class="prettyprint lang-java">// ...</code> style. For multi-line
<code class="prettyprint lang-java">/* ... */</code> comments, subsequent lines must start with
<code>*</code> aligned with the <code>*</code> on the previous line.</p>

<pre class="prettyprint lang-java">/*
 * This is          // And so           /* Or you can
 * okay.            // is this.          * even do this. */
 */
</pre>


<p>Comments are not enclosed in boxes drawn with asterisks or other characters.</p>

<p class="tip"><strong>Tip:</strong> When writing multi-line comments, use the
<code class="prettyprint lang-java">/* ... */</code> style if you want automatic code formatters to
re-wrap the lines when necessary (paragraph-style). Most formatters don't re-wrap lines in
<code class="prettyprint lang-java">// ...</code> style comment blocks.</p>

 

<a name="modifiers"></a>
<h4 id="s4.8.7-modifiers">4.8.7 Modifiers</h4>

<p>Class and member modifiers, when present, appear in the order
recommended by the Java Language Specification:
</p>

<pre>public protected private abstract default static final transient volatile synchronized native strictfp
</pre>

<h4 id="s4.8.8-numeric-literals">4.8.8 Numeric Literals</h4>

<p><code>long</code>-valued integer literals use an uppercase <code>L</code> suffix, never
lowercase (to avoid confusion with the digit <code>1</code>). For example, <code>3000000000L</code>
rather than <code class="badcode">3000000000l</code>.</p>

<a name="naming"></a>
<h2 id="s5-naming">5 Naming</h2>

<h3 id="s5.1-identifier-names">5.1 Rules common to all identifiers</h3>

<p>Identifiers use only ASCII letters and digits, and, in a small number of cases noted below,
underscores. Thus each valid identifier name is matched by the regular expression
<code>\w+</code> .</p>

<p>In Google Style special prefixes or
suffixes, like those seen in the examples <code class="badcode">name_</code>,
<code class="badcode">mName</code>, <code class="badcode">s_name</code> and
<code class="badcode">kName</code>, are <strong>not</strong> used.</p>

<h3 id="s5.2-specific-identifier-names">5.2 Rules by identifier type</h3>

<h4 id="s5.2.1-package-names">5.2.1 Package names</h4>

<p>Package names are all lowercase, with consecutive words simply concatenated together (no
underscores). For example, <code>com.example.deepspace</code>, not
<code class="badcode">com.example.deepSpace</code> or
<code class="badcode">com.example.deep_space</code>.</p>

<h4 id="s5.2.2-class-names">5.2.2 Class names</h4>

<p>Class names are written in <a href="#s5.3-camel-case">UpperCamelCase</a>.</p>

<p>Class names are typically nouns or noun phrases. For example,
<code class="prettyprint lang-java">Character</code> or
<code class="prettyprint lang-java">ImmutableList</code>. Interface names may also be nouns or
noun phrases (for example, <code class="prettyprint lang-java">List</code>), but may sometimes be
adjectives or adjective phrases instead (for example,
<code class="prettyprint lang-java">Readable</code>).</p>

<p>There are no specific rules or even well-established conventions for naming annotation types.</p>

<p><em>Test</em> classes are named starting with the name of the class they are testing, and ending
with <code class="prettyprint lang-java">Test</code>. For example,
<code class="prettyprint lang-java">HashTest</code> or
<code class="prettyprint lang-java">HashIntegrationTest</code>.</p>

<h4 id="s5.2.3-method-names">5.2.3 Method names</h4>

<p>Method names are written in <a href="#s5.3-camel-case">lowerCamelCase</a>.</p>

<p>Method names are typically verbs or verb phrases. For example,
<code class="prettyprint lang-java">sendMessage</code> or
<code class="prettyprint lang-java">stop</code>.</p>

<p>Underscores may appear in JUnit <em>test</em> method names to separate logical components of the
name, with <em>each</em> component written in <a href="#s5.3-camel-case">lowerCamelCase</a>.
One typical pattern is <code><i>&lt;methodUnderTest&gt;</i>_<i>&lt;state&gt;</i></code>,
for example <code class="prettyprint lang-java">pop_emptyStack</code>. There is no One Correct
Way to name test methods.</p>

<a name="constants"></a>
<h4 id="s5.2.4-constant-names">5.2.4 Constant names</h4>

<p>Constant names use <code class="prettyprint lang-java">CONSTANT_CASE</code>: all uppercase
letters, with each word separated from the next by a single underscore. But what <em>is</em> a
constant, exactly?</p>

<p>Constants are static final fields whose contents are deeply immutable and whose methods have no
detectable side effects. This includes primitives, Strings, immutable types, and immutable
collections of immutable types. If any of the instance's observable state can change, it is not a
constant. Merely <em>intending</em> to never mutate the object is not enough. Examples:</p>

<pre class="prettyprint lang-java">// Constants
static final int NUMBER = 5;
static final ImmutableList&lt;String&gt; NAMES = ImmutableList.of("Ed", "Ann");
static final ImmutableMap&lt;String, Integer&gt; AGES = ImmutableMap.of("Ed", 35, "Ann", 32);
static final Joiner COMMA_JOINER = Joiner.on(','); // because Joiner is immutable
static final SomeMutableType[] EMPTY_ARRAY = {};
enum SomeEnum { ENUM_CONSTANT }

// Not constants
static String nonFinal = "non-final";
final String nonStatic = "non-static";
static final Set&lt;String&gt; mutableCollection = new HashSet&lt;String&gt;();
static final ImmutableSet&lt;SomeMutableType&gt; mutableElements = ImmutableSet.of(mutable);
static final ImmutableMap&lt;String, SomeMutableType&gt; mutableValues =
    ImmutableMap.of("Ed", mutableInstance, "Ann", mutableInstance2);
static final Logger logger = Logger.getLogger(MyClass.getName());
static final String[] nonEmptyArray = {"these", "can", "change"};
</pre>

<p>These names are typically nouns or noun phrases.</p>

<h4 id="s5.2.5-non-constant-field-names">5.2.5 Non-constant field names</h4>

<p>Non-constant field names (static or otherwise) are written
in <a href="#s5.3-camel-case">lowerCamelCase</a>.</p>

<p>These names are typically nouns or noun phrases.  For example,
<code class="prettyprint lang-java">computedValues</code> or
<code class="prettyprint lang-java">index</code>.</p>

<h4 id="s5.2.6-parameter-names">5.2.6 Parameter names</h4>

<p>Parameter names are written in <a href="#s5.3-camel-case">lowerCamelCase</a>.</p>

<p>One-character parameter names in public methods should be avoided.</p>

<h4 id="s5.2.7-local-variable-names">5.2.7 Local variable names</h4>

<p>Local variable names are written in <a href="#s5.3-camel-case">lowerCamelCase</a>.</p>

<p>Even when final and immutable, local variables are not considered to be constants, and should not
be styled as constants.</p>

<h4 id="s5.2.8-type-variable-names">5.2.8 Type variable names</h4>

<p>Each type variable is named in one of two styles:</p>

<ul>
  <li>A single capital letter, optionally followed by a single numeral (such as
  <code class="prettyprint lang-java">E</code>, <code class="prettyprint lang-java">T</code>,
  <code class="prettyprint lang-java">X</code>, <code class="prettyprint lang-java">T2</code>)
  </li>

  <li>A name in the form used for classes (see Section 5.2.2,
  <a href="#s5.2.2-class-names">Class names</a>), followed by the capital letter
  <code class="prettyprint lang-java">T</code> (examples:
  <code class="prettyprint lang-java">RequestT</code>,
  <code class="prettyprint lang-java">FooBarT</code>).</li>
</ul>

<a name="acronyms"></a>
<a name="camelcase"></a>
<h3 id="s5.3-camel-case">5.3 Camel case: defined</h3>

<p>Sometimes there is more than one reasonable way to convert an English phrase into camel case,
such as when acronyms or unusual constructs like "IPv6" or "iOS" are present. To improve
predictability, Google Style specifies the following (nearly) deterministic scheme.</p>

<p>Beginning with the prose form of the name:</p>

<ol>
  <li>Convert the phrase to plain ASCII and remove any apostrophes. For example, "M&#252;ller's
  algorithm" might become "Muellers algorithm".</li>

  <li>Divide this result into words, splitting on spaces and any remaining punctuation (typically
  hyphens).

  <ul>
    <li><em>Recommended:</em> if any word already has a conventional camel-case appearance in common
    usage, split this into its constituent parts (e.g., "AdWords" becomes "ad&#160;words"). Note
    that a word such as "iOS" is not really in camel case <em>per se</em>; it defies <em>any</em>
    convention, so this recommendation does not apply.</li>
  </ul>
  </li>

  <li>Now lowercase <em>everything</em> (including acronyms), then uppercase only the first
  character of:
  <ul>
    <li>... each word, to yield <em>upper camel case</em>, or</li>
    <li>... each word except the first, to yield <em>lower camel case</em></li>
  </ul>
  </li>

  <li>Finally, join all the words into a single identifier.</li>
</ol>

<p>Note that the casing of the original words is almost entirely disregarded. Examples:</p>

<table>
  <tbody><tr>
    <th>Prose form</th>
    <th>Correct</th>
    <th>Incorrect</th>
  </tr>
  <tr>
    <td>"XML HTTP request"</td>
    <td><code class="prettyprint lang-java">XmlHttpRequest</code></td>
    <td><code class="badcode">XMLHTTPRequest</code></td>
  </tr>
  <tr>
    <td>"new customer ID"</td>
    <td><code class="prettyprint lang-java">newCustomerId</code></td>
    <td><code class="badcode">newCustomerID</code></td>
  </tr>
  <tr>
    <td>"inner stopwatch"</td>
    <td><code class="prettyprint lang-java">innerStopwatch</code></td>
    <td><code class="badcode">innerStopWatch</code></td>
  </tr>
  <tr>
    <td>"supports IPv6 on iOS?"</td>
    <td><code class="prettyprint lang-java">supportsIpv6OnIos</code></td>
    <td><code class="badcode">supportsIPv6OnIOS</code></td>
  </tr>
  <tr>
    <td>"YouTube importer"</td>
    <td><code class="prettyprint lang-java">YouTubeImporter</code><br>
        <code class="prettyprint lang-java">YoutubeImporter</code>*</td>
    <td></td>
  </tr>
</tbody></table>

<p>*Acceptable, but not recommended.</p>

<p class="note"><strong>Note:</strong> Some words are ambiguously hyphenated in the English
language: for example "nonempty" and "non-empty" are both correct, so the method names
<code class="prettyprint lang-java">checkNonempty</code> and
<code class="prettyprint lang-java">checkNonEmpty</code> are likewise both correct.</p>


<h2 id="s6-programming-practices">6 Programming Practices</h2>

<h3 id="s6.1-override-annotation">6.1 <code>@Override</code>: always used</h3>

<p>A method is marked with the <code class="prettyprint lang-java">@Override</code> annotation
whenever it is legal.  This includes a class method overriding a superclass method, a class method
implementing an interface method, and an interface method respecifying a superinterface
method.</p>

<p class="exception"><strong>Exception:</strong>
<code class="prettyprint lang-java">@Override</code> may be omitted when the parent method is
<code class="prettyprint lang-java">@Deprecated</code>.</p>

<a name="caughtexceptions"></a>
<h3 id="s6.2-caught-exceptions">6.2 Caught exceptions: not ignored</h3>

<p>Except as noted below, it is very rarely correct to do nothing in response to a caught
exception. (Typical responses are to log it, or if it is considered "impossible", rethrow it as an
<code class="prettyprint lang-java">AssertionError</code>.)</p>

<p>When it truly is appropriate to take no action whatsoever in a catch block, the reason this is
justified is explained in a comment.</p>

<pre class="prettyprint lang-java">try {
  int i = Integer.parseInt(response);
  return handleNumericResponse(i);
} catch (NumberFormatException ok) {
  // it's not numeric; that's fine, just continue
}
return handleTextResponse(response);
</pre>

<p class="exception"><strong>Exception:</strong> In tests, a caught exception may be ignored
without comment <em>if</em> its name is or begins with <code class="prettyprint lang-java">expected</code>. The
following is a very common idiom for ensuring that the code under test <em>does</em> throw an
exception of the expected type, so a comment is unnecessary here.</p>

<pre class="prettyprint lang-java">try {
  emptyStack.pop();
  fail();
} catch (NoSuchElementException expected) {
}
</pre>

<h3 id="s6.3-static-members">6.3 Static members: qualified using class</h3>

<p>When a reference to a static class member must be qualified, it is qualified with that class's
name, not with a reference or expression of that class's type.</p>

<pre class="prettyprint lang-java">Foo aFoo = ...;
Foo.aStaticMethod(); // good
<span class="badcode">aFoo.aStaticMethod();</span> // bad
<span class="badcode">somethingThatYieldsAFoo().aStaticMethod();</span> // very bad
</pre>

<a name="finalizers"></a>
<h3 id="s6.4-finalizers">6.4 Finalizers: not used</h3>

<p>It is <strong>extremely rare</strong> to override <code class="prettyprint
lang-java">Object.finalize</code>.</p>

<p class="tip"><strong>Tip:</strong> Don't do it. If you absolutely must, first read and understand


  <a href="http://books.google.com/books?isbn=8131726592"><em>Effective Java</em> Item 7,</a>

"Avoid Finalizers," very carefully, and <em>then</em> don't do it.</p>


<a name="javadoc"></a>
<h2 id="s7-javadoc">7 Javadoc</h2>



<h3 id="s7.1-javadoc-formatting">7.1 Formatting</h3>

<h4 id="s7.1.1-javadoc-multi-line">7.1.1 General form</h4>

<p>The <em>basic</em> formatting of Javadoc blocks is as seen in this example:</p>

<pre class="prettyprint lang-java">/**
 * Multiple lines of Javadoc text are written here,
 * wrapped normally...
 */
public int method(String p1) { ... }
</pre>

<p>... or in this single-line example:</p>

<pre class="prettyprint lang-java">/** An especially short bit of Javadoc. */
</pre>

<p>The basic form is always acceptable. The single-line form may be substituted when the entirety
of the Javadoc block (including comment markers) can fit on a single line. Note that this only
applies when there are no block tags such as <code>@return</code>.

</p><h4 id="s7.1.2-javadoc-paragraphs">7.1.2 Paragraphs</h4>

<p>One blank line&#8212;that is, a line containing only the aligned leading asterisk
(<code>*</code>)&#8212;appears between paragraphs, and before the group of block tags if
present. Each paragraph but the first has <code>&lt;p&gt;</code> immediately before the first word,
with no space after.</p>

<a name="s7.1.3-javadoc-at-clauses"></a>

<h4 id="s7.1.3-javadoc-block-tags">7.1.3 Block tags</h4>

<p>Any of the standard "block tags" that are used appear in the order <code>@param</code>,
<code>@return</code>, <code>@throws</code>, <code>@deprecated</code>, and these four types never
appear with an empty description. When a block tag doesn't fit on a single line, continuation lines
are indented four (or more) spaces from the position of the <code>@</code>.
</p>

<h3 id="s7.2-summary-fragment">7.2 The summary fragment</h3>

<p>Each Javadoc block begins with a brief <strong>summary fragment</strong>. This
fragment is very important: it is the only part of the text that appears in certain contexts such as
class and method indexes.</p>

<p>This is a fragment&#8212;a noun phrase or verb phrase, not a complete sentence. It does
<strong>not</strong> begin with <code class="badcode">A {@code Foo} is a...</code>, or
<code class="badcode">This method returns...</code>, nor does it form a complete imperative sentence
like <code class="badcode">Save the record.</code>. However, the fragment is capitalized and
punctuated as if it were a complete sentence.</p>

<p class="tip"><strong>Tip:</strong> A common mistake is to write simple Javadoc in the form
<code class="badcode">/** @return the customer ID */</code>. This is incorrect, and should be
changed to <code class="prettyprint lang-java">/** Returns the customer ID. */</code>.</p>

<a name="s7.3.3-javadoc-optional"></a> 
<h3 id="s7.3-javadoc-where-required">7.3 Where Javadoc is used</h3>

<p>At the <em>minimum</em>, Javadoc is present for every
<code class="prettyprint lang-java">public</code> class, and every
<code class="prettyprint lang-java">public</code> or
<code class="prettyprint lang-java">protected</code> member of such a class, with a few exceptions
noted below.</p>

<p>Additional Javadoc content may also be present, as explained in Section 7.3.4,
<a href="#s7.3.4-javadoc-non-required">Non-required Javadoc</a>.</p>

<h4 id="s7.3.1-javadoc-exception-self-explanatory">7.3.1 Exception: self-explanatory methods</h4>

<p>Javadoc is optional for "simple, obvious" methods like
<code class="prettyprint lang-java">getFoo</code>, in cases where there <em>really and truly</em> is
nothing else worthwhile to say but "Returns the foo".</p>

<p class="note"><strong>Important:</strong> it is not appropriate to cite this exception to justify
omitting relevant information that a typical reader might need to know. For example, for a method
named <code class="prettyprint lang-java">getCanonicalName</code>, don't omit its documentation
(with the rationale that it would say only
<code class="badcode">/** Returns the canonical name. */</code>) if a typical reader may have no idea
what the term "canonical name" means!</p>

<h4 id="s7.3.2-javadoc-exception-overrides">7.3.2 Exception: overrides</h4>

<p>Javadoc is not always present on a method that overrides a supertype method.

</p>



<h4 id="s7.3.4-javadoc-non-required">7.3.4 Non-required Javadoc</h4>

<p>Other classes and members have Javadoc <em>as needed or desired</em>.

</p><p>Whenever an implementation comment would be used to define the overall purpose or behavior of a
class or member, that comment is written as Javadoc instead (using <code>/**</code>).</p>

<p>Non-required Javadoc is not strictly required to follow the formatting rules of Sections
7.1.2, 7.1.3, and 7.2, though it is of course recommended.</p>

 

</div> 
</div>
</body>
</html>
