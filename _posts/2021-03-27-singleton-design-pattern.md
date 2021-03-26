Singleton pattern is a creational software design pattern that restricts the instantiation of a class to one "single" instance. This is useful when exactly one object is needed to coordinate actions across the system. It also provides a global endpoint to access the single instance.

For example, Let's make database connection class to have only one instance across the whole system.

<pre class="php" style="font-family:monospace;">&nbsp;
<span style="color: #000000; font-weight: bold;">&lt;?php</span> <span style="color: #000000; font-weight: bold;">declare</span><span style="color: #009900;">&#40;</span>strict_types<span style="color: #339933;">=</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
<span style="color: #000000; font-weight: bold;">namespace</span> App\Singleton<span style="color: #339933;">;</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">class</span> DB <span style="color: #009900;">&#123;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">private</span> static <span style="color: #000088;">$instance</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000088;">$connection</span><span style="color: #339933;">;</span>
&nbsp;
    <span style="color: #666666; font-style: italic;">// private constructor</span>
    <span style="color: #000000; font-weight: bold;">private</span> final <span style="color: #000000; font-weight: bold;">function</span>  __construct<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #666666; font-style: italic;">// implement connection to database here</span>
    <span style="color: #009900;">&#125;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> static <span style="color: #000000; font-weight: bold;">function</span> getInstance<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span><span style="color: #339933;">!</span><span style="color: #990000;">isset</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">self</span><span style="color: #339933;">::</span><span style="color: #000088;">$instance</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">self</span><span style="color: #339933;">::</span><span style="color: #000088;">$instance</span> <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> DB<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
        <span style="color: #b1b100;">return</span> <span style="color: #000000; font-weight: bold;">self</span><span style="color: #339933;">::</span><span style="color: #000088;">$instance</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> getConnection<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #b1b100;">return</span> <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #000088;">$connection</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
<span style="color: #009900;">&#125;</span>
<span style="color: #000000; font-weight: bold;">?&gt;</span></pre>


Let's write test cases to verify only single instance is created.

<pre class="php" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">&lt;?php</span> <span style="color: #000000; font-weight: bold;">declare</span><span style="color: #009900;">&#40;</span>strict_types<span style="color: #339933;">=</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
<span style="color: #000000; font-weight: bold;">namespace</span> App\Singleton\Tests<span style="color: #339933;">;</span>
&nbsp;
<span style="color: #b1b100;">require_once</span> <span style="color: #0000ff;">'./vendor/autoload.php'</span><span style="color: #339933;">;</span> 
<span style="color: #000000; font-weight: bold;">use</span> App\Singleton\DB<span style="color: #339933;">;</span>
<span style="color: #000000; font-weight: bold;">use</span> PHPUnit\Framework\TestCase<span style="color: #339933;">;</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">class</span> SingletonTest <span style="color: #000000; font-weight: bold;">extends</span> TestCase
<span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> testSingleton<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
        <span style="color: #000088;">$dbObj1</span> <span style="color: #339933;">=</span> DB<span style="color: #339933;">::</span><span style="color: #004000;">getInstance</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000088;">$dbObj2</span> <span style="color: #339933;">=</span> DB<span style="color: #339933;">::</span><span style="color: #004000;">getInstance</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">assertEquals</span><span style="color: #009900;">&#40;</span><span style="color: #000088;">$dbObj1</span><span style="color: #339933;">,</span> <span style="color: #000088;">$dbObj2</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> testIsInstanceOfDB<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
        <span style="color: #000088;">$dbObj</span> <span style="color: #339933;">=</span> DB<span style="color: #339933;">::</span><span style="color: #004000;">getInstance</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">assertInstanceOf</span><span style="color: #009900;">&#40;</span>DB<span style="color: #339933;">::</span><span style="color: #000000; font-weight: bold;">class</span><span style="color: #339933;">,</span> <span style="color: #000088;">$dbObj</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
<span style="color: #009900;">&#125;</span></pre>


Execute tests.
<pre class="powershell" style="font-family:monospace;">$.<span style="color: pink;">/</span>vendor<span style="color: pink;">/</span>bin<span style="color: pink;">/</span>phpunit tests<span style="color: pink;">/</span>SingletonTest.php 
PHPUnit 7.5.20 by Sebastian Bergmann and contributors.
&nbsp;
..                                                                  <span style="color: #804000;">2</span> <span style="color: pink;">/</span> <span style="color: #804000;">2</span> <span style="color: #000000;">&#40;</span><span style="color: #804000;">100</span><span style="color: pink;">%</span><span style="color: #000000;">&#41;</span>
&nbsp;
Time: <span style="color: #804000;">31</span> ms<span style="color: pink;">,</span> Memory: <span style="color: #804000;">4.00</span> MB
&nbsp;
OK <span style="color: #000000;">&#40;</span><span style="color: #804000;">2</span> tests<span style="color: pink;">,</span> <span style="color: #804000;">2</span> assertions<span style="color: #000000;">&#41;</span>
&nbsp;</pre>



