
Dependency Inpervion Principle is one of the SOLID design principle. It states following two thing:
1. High-level modules should not depend on low-level modules. Both should depend on the abstraction.
2. Abstractions should not depend on details. Details should depend on abstractions.

Let's consider the following bad example and find out the problems with it:

<pre class="php" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">class</span> Logger
<span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> <span style="color: #990000;">log</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">:</span> string
    <span style="color: #009900;">&#123;</span>
        <span style="color: #b1b100;">return</span> <span style="color: #0000ff;">&quot;Logger&quot;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
<span style="color: #009900;">&#125;</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">class</span> FileLogger <span style="color: #000000; font-weight: bold;">extends</span> Logger
<span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> <span style="color: #990000;">log</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">:</span> string
    <span style="color: #009900;">&#123;</span>
        <span style="color: #b1b100;">return</span> <span style="color: #0000ff;">&quot;logged in a file&quot;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
<span style="color: #009900;">&#125;</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">class</span> StdoutLogger <span style="color: #000000; font-weight: bold;">extends</span> Logger
<span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> <span style="color: #990000;">log</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">:</span> string
    <span style="color: #009900;">&#123;</span>
        <span style="color: #b1b100;">return</span> <span style="color: #0000ff;">&quot;logged in screen&quot;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
<span style="color: #009900;">&#125;</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">class</span> LoggerManager
<span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000088;">$logger</span><span style="color: #339933;">;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> __construct<span style="color: #009900;">&#40;</span>Logger <span style="color: #000088;">$logger</span><span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">logger</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$logger</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> <span style="color: #990000;">log</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">:</span> string
    <span style="color: #009900;">&#123;</span>
        <span style="color: #b1b100;">return</span> <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">logger</span><span style="color: #339933;">-&gt;</span><span style="color: #990000;">log</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
<span style="color: #009900;">&#125;</span></pre>

In this example. LoggerManager (high level) depends on the Logger class (low level) and it violates dependency inversion principle for tightly coupled dependency to a concrete Logger class from high level module LoggerManager. According to dependency inversion principle they should depend on abstraction. 
Let's refactor this. We will convert the logger class to an interface and logger manager will depend on the interface. This accepts dependency inversion principle now.

<pre class="php" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">interface</span> LoggerInterface
<span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> <span style="color: #990000;">log</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">:</span> string<span style="color: #339933;">;</span>
<span style="color: #009900;">&#125;</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">class</span> FileLogger <span style="color: #000000; font-weight: bold;">implements</span> LoggerInterface
<span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> <span style="color: #990000;">log</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">:</span> string
    <span style="color: #009900;">&#123;</span>
        <span style="color: #b1b100;">return</span> <span style="color: #0000ff;">&quot;logged in a file&quot;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
<span style="color: #009900;">&#125;</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">class</span> StdoutLogger <span style="color: #000000; font-weight: bold;">implements</span> LoggerInterface
<span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> <span style="color: #990000;">log</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">:</span> string
    <span style="color: #009900;">&#123;</span>
        <span style="color: #b1b100;">return</span> <span style="color: #0000ff;">&quot;logged in screen&quot;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
<span style="color: #009900;">&#125;</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">class</span> LoggerManager
<span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000088;">$logger</span><span style="color: #339933;">;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> __construct<span style="color: #009900;">&#40;</span>LoggerInterface <span style="color: #000088;">$logger</span><span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">logger</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$logger</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> <span style="color: #990000;">log</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">:</span> string
    <span style="color: #009900;">&#123;</span>
        <span style="color: #b1b100;">return</span> <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">logger</span><span style="color: #339933;">-&gt;</span><span style="color: #990000;">log</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
<span style="color: #009900;">&#125;</span></pre>

Test cases

<pre class="php" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">&lt;?php</span> <span style="color: #000000; font-weight: bold;">declare</span><span style="color: #009900;">&#40;</span>strict_types<span style="color: #339933;">=</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
<span style="color: #000000; font-weight: bold;">namespace</span> App\DIP\Tests<span style="color: #339933;">;</span>
&nbsp;
<span style="color: #b1b100;">require_once</span> <span style="color: #0000ff;">'./vendor/autoload.php'</span><span style="color: #339933;">;</span> 
<span style="color: #000000; font-weight: bold;">use</span> PHPUnit\Framework\TestCase<span style="color: #339933;">;</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">class</span> DipTest <span style="color: #000000; font-weight: bold;">extends</span> TestCase
<span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> testFileLogger<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
        <span style="color: #000088;">$fileLogger</span> <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> FileLogger<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000088;">$loggerManager</span> <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> LoggerManager<span style="color: #009900;">&#40;</span><span style="color: #000088;">$fileLogger</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
&nbsp;
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">assertRegExp</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">'/logged in a file/'</span><span style="color: #339933;">,</span> <span style="color: #000088;">$loggerManager</span><span style="color: #339933;">-&gt;</span><span style="color: #990000;">log</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> testStdoutLogger<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
        <span style="color: #000088;">$fileLogger</span> <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> StdoutLogger<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000088;">$loggerManager</span> <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> LoggerManager<span style="color: #009900;">&#40;</span><span style="color: #000088;">$fileLogger</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
&nbsp;
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">assertRegExp</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">'/logged in screen/'</span><span style="color: #339933;">,</span> <span style="color: #000088;">$loggerManager</span><span style="color: #339933;">-&gt;</span><span style="color: #990000;">log</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
<span style="color: #009900;">&#125;</span></pre>

Execute test case

./vendor/bin/phpunit tests/DipTest.php 
PHPUnit 7.5.20 by Sebastian Bergmann and contributors.
 
..                                                                  2 / 2 (100%)
 
Time: 30 ms, Memory: 4.00 MB
 
OK (2 tests, 2 assertions)
 
