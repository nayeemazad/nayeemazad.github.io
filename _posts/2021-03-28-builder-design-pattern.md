Builder pattern is a creational design pattern which separates the contruction process of complex objects from its representation so that same contruction process can create different representation.

Let's demonstrate this with an example of Pizza.

<pre class="php" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">class</span> Pizza
<span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">private</span> int <span style="color: #000088;">$size</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">private</span> bool <span style="color: #000088;">$pepperoni</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">private</span> bool <span style="color: #000088;">$mushrooms</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">private</span> bool <span style="color: #000088;">$extraCheese</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">private</span> bool <span style="color: #000088;">$onions</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">private</span> bool <span style="color: #000088;">$bacon</span><span style="color: #339933;">;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> __construct<span style="color: #009900;">&#40;</span>
        int <span style="color: #000088;">$size</span><span style="color: #339933;">,</span> 
        bool <span style="color: #000088;">$pepperoni</span><span style="color: #339933;">,</span> 
        bool <span style="color: #000088;">$mushrooms</span><span style="color: #339933;">,</span> 
        bool <span style="color: #000088;">$extraCheese</span><span style="color: #339933;">,</span>
        bool <span style="color: #000088;">$onions</span><span style="color: #339933;">,</span>
        bool <span style="color: #000088;">$bacon</span>
    <span style="color: #009900;">&#41;</span> 
    <span style="color: #009900;">&#123;</span>
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">size</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$size</span><span style="color: #339933;">;</span>
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">pepperoni</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$pepperoni</span><span style="color: #339933;">;</span>
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">mushrooms</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$mushrooms</span><span style="color: #339933;">;</span>
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">extraCheese</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$extraCheese</span><span style="color: #339933;">;</span>
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">onions</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$onions</span><span style="color: #339933;">;</span>
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">bacon</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$bacon</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
&nbsp;
    <span style="color: #666666; font-style: italic;">// getter methods here</span>
<span style="color: #009900;">&#125;</span></pre>

Pizza class looks like this. Let's say we want to have a 12 inch pizza with customised toppings(we want to include extraCheese and bacon). so to instantiate this pizza class in client will be as following

<pre class="php" style="font-family:monospace;"><span style="color: #000088;">$pizza1</span> <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Pizza<span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">12</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">false</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">false</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">true</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">false</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre>

This way, the Problem is that constructor params are not named here which is hard to maintain. It will get more messy in the long run if requirements come to extend. 
Now we can decide to have setters in the Pizza class and create object as following
<pre class="php" style="font-family:monospace;"><span style="color: #000088;">$pizza1</span> <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Pizza<span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">12</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
<span style="color: #000088;">$pizza1</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">setExtraCheese</span><span style="color: #009900;">&#40;</span><span style="color: #009900; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
<span style="color: #000088;">$pizza1</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">setBacon</span><span style="color: #009900;">&#40;</span><span style="color: #009900; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
&nbsp;
&nbsp;</pre>
Now the problem is, this way the object is not immutable. Each use of a setter changing object states.

That's why we can use Builder pattern to solve the problem.
Let's create PizzaBuilder 

<pre class="php" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">class</span> PizzaBuilder
<span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000088;">$size</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000088;">$pepperoni</span> <span style="color: #339933;">=</span> <span style="color: #009900; font-weight: bold;">false</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000088;">$mushrooms</span> <span style="color: #339933;">=</span> <span style="color: #009900; font-weight: bold;">false</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000088;">$extraCheese</span> <span style="color: #339933;">=</span> <span style="color: #009900; font-weight: bold;">false</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000088;">$onions</span> <span style="color: #339933;">=</span> <span style="color: #009900; font-weight: bold;">false</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000088;">$bacon</span> <span style="color: #339933;">=</span> <span style="color: #009900; font-weight: bold;">false</span><span style="color: #339933;">;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> __construct<span style="color: #009900;">&#40;</span>int <span style="color: #000088;">$size</span><span style="color: #009900;">&#41;</span> 
    <span style="color: #009900;">&#123;</span>
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">size</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$size</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> setPepperoni<span style="color: #009900;">&#40;</span>bool <span style="color: #000088;">$pepperoni</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">:</span> PizzaBuilder
    <span style="color: #009900;">&#123;</span>
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">pepperoni</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$pepperoni</span><span style="color: #339933;">;</span>
        <span style="color: #b1b100;">return</span> <span style="color: #000088;">$this</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> setMushrooms<span style="color: #009900;">&#40;</span>bool <span style="color: #000088;">$mushrooms</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">:</span> PizzaBuilder
    <span style="color: #009900;">&#123;</span>
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">mushrooms</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$mushrooms</span><span style="color: #339933;">;</span>
        <span style="color: #b1b100;">return</span> <span style="color: #000088;">$this</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> setExtraCheese<span style="color: #009900;">&#40;</span>bool <span style="color: #000088;">$extraCheese</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">:</span> PizzaBuilder
    <span style="color: #009900;">&#123;</span>
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">extraCheese</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$extraCheese</span><span style="color: #339933;">;</span>
        <span style="color: #b1b100;">return</span> <span style="color: #000088;">$this</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> setOnions<span style="color: #009900;">&#40;</span>bool <span style="color: #000088;">$onions</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">:</span> PizzaBuilder
    <span style="color: #009900;">&#123;</span>
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">onions</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$onions</span><span style="color: #339933;">;</span>
        <span style="color: #b1b100;">return</span> <span style="color: #000088;">$this</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> setBacon<span style="color: #009900;">&#40;</span>bool <span style="color: #000088;">$bacon</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">:</span> PizzaBuilder
    <span style="color: #009900;">&#123;</span>
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">bacon</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$bacon</span><span style="color: #339933;">;</span>
        <span style="color: #b1b100;">return</span> <span style="color: #000088;">$this</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
&nbsp;
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> build<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">:</span> PizzaBuilder
    <span style="color: #009900;">&#123;</span>
        <span style="color: #b1b100;">return</span> <span style="color: #000088;">$this</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
&nbsp;
<span style="color: #009900;">&#125;</span></pre>

and refactor Pizza class to use PizzaBuilder in the constructor

<pre class="php" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">class</span> Pizza
<span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">private</span> int <span style="color: #000088;">$size</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">private</span> bool <span style="color: #000088;">$pepperoni</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">private</span> bool <span style="color: #000088;">$mushrooms</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">private</span> bool <span style="color: #000088;">$extraCheese</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">private</span> bool <span style="color: #000088;">$onions</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">private</span> bool <span style="color: #000088;">$bacon</span><span style="color: #339933;">;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> __construct<span style="color: #009900;">&#40;</span>PizzaBuilder <span style="color: #000088;">$pizzaBuilder</span><span style="color: #009900;">&#41;</span> 
    <span style="color: #009900;">&#123;</span>
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">size</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$pizzaBuilder</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">size</span><span style="color: #339933;">;</span>
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">pepperoni</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$pizzaBuilder</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">pepperoni</span><span style="color: #339933;">;</span>
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">mushrooms</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$pizzaBuilder</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">mushrooms</span><span style="color: #339933;">;</span>
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">extraCheese</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$pizzaBuilder</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">extraCheese</span><span style="color: #339933;">;</span>
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">onions</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$pizzaBuilder</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">onions</span><span style="color: #339933;">;</span>
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">bacon</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$pizzaBuilder</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">bacon</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> getSize<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">:</span> int
    <span style="color: #009900;">&#123;</span>
        <span style="color: #b1b100;">return</span> <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">size</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> getPepperoni<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">:</span> bool
    <span style="color: #009900;">&#123;</span>
        <span style="color: #b1b100;">return</span> <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">pepperoni</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> getMushrooms<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">:</span> bool
    <span style="color: #009900;">&#123;</span>
        <span style="color: #b1b100;">return</span> <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">mushrooms</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> getExtraCheese<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">:</span> bool
    <span style="color: #009900;">&#123;</span>
        <span style="color: #b1b100;">return</span> <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">extraCheese</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> getOnions<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">:</span> bool
    <span style="color: #009900;">&#123;</span>
        <span style="color: #b1b100;">return</span> <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">onions</span><span style="color: #339933;">;</span> 
    <span style="color: #009900;">&#125;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> getBacon<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">:</span> bool
    <span style="color: #009900;">&#123;</span>
        <span style="color: #b1b100;">return</span> <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">bacon</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
&nbsp;
<span style="color: #009900;">&#125;</span></pre>


Now we can create pizza class object with builder as following

<pre class="php" style="font-family:monospace;"><span style="color: #000088;">$pizzaBuilderObject</span> <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> PizzaBuilder<span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">12</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>
    <span style="color: #339933;">-&gt;</span><span style="color: #004000;">setPepperoni</span><span style="color: #009900;">&#40;</span><span style="color: #009900; font-weight: bold;">false</span><span style="color: #009900;">&#41;</span>
    <span style="color: #339933;">-&gt;</span><span style="color: #004000;">setMushrooms</span><span style="color: #009900;">&#40;</span><span style="color: #009900; font-weight: bold;">false</span><span style="color: #009900;">&#41;</span>
    <span style="color: #339933;">-&gt;</span><span style="color: #004000;">setExtraCheese</span><span style="color: #009900;">&#40;</span><span style="color: #009900; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span>
    <span style="color: #339933;">-&gt;</span><span style="color: #004000;">setOnions</span><span style="color: #009900;">&#40;</span><span style="color: #009900; font-weight: bold;">false</span><span style="color: #009900;">&#41;</span>
    <span style="color: #339933;">-&gt;</span><span style="color: #004000;">setBacon</span><span style="color: #009900;">&#40;</span><span style="color: #009900; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span>
    <span style="color: #339933;">-&gt;</span><span style="color: #004000;">build</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
&nbsp;
<span style="color: #000088;">$pizza</span> <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Pizza<span style="color: #009900;">&#40;</span><span style="color: #000088;">$pizzaBuilderObject</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre>

or just specify what we want.
<pre class="php" style="font-family:monospace;"><span style="color: #000088;">$pizzaBuilderObject</span> <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> PizzaBuilder<span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">12</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>
    <span style="color: #339933;">-&gt;</span><span style="color: #004000;">setExtraCheese</span><span style="color: #009900;">&#40;</span><span style="color: #009900; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span>
    <span style="color: #339933;">-&gt;</span><span style="color: #004000;">setBacon</span><span style="color: #009900;">&#40;</span><span style="color: #009900; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span>
    <span style="color: #339933;">-&gt;</span><span style="color: #004000;">build</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
&nbsp;
<span style="color: #000088;">$pizza</span> <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Pizza<span style="color: #009900;">&#40;</span><span style="color: #000088;">$pizzaBuilderObject</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre>


Test cases:

<pre class="php" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">&lt;?php</span> <span style="color: #000000; font-weight: bold;">declare</span><span style="color: #009900;">&#40;</span>strict_types<span style="color: #339933;">=</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
<span style="color: #000000; font-weight: bold;">namespace</span> App\BuilderPattern\Tests<span style="color: #339933;">;</span>
&nbsp;
<span style="color: #b1b100;">require_once</span> <span style="color: #0000ff;">'./vendor/autoload.php'</span><span style="color: #339933;">;</span> 
<span style="color: #000000; font-weight: bold;">use</span> PHPUnit\Framework\TestCase<span style="color: #339933;">;</span>
<span style="color: #000000; font-weight: bold;">use</span> App\BuilderPattern\PizzaBuilder<span style="color: #339933;">;</span>
<span style="color: #000000; font-weight: bold;">use</span> App\BuilderPattern\Pizza<span style="color: #339933;">;</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">class</span> BuilderPatternTest <span style="color: #000000; font-weight: bold;">extends</span> TestCase
<span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000088;">$pizza</span><span style="color: #339933;">;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> setUp<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>
        <span style="color: #000088;">$pizzaBuilderObject</span> <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> PizzaBuilder<span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">12</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>
            <span style="color: #339933;">-&gt;</span><span style="color: #004000;">setExtraCheese</span><span style="color: #009900;">&#40;</span><span style="color: #009900; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span>
            <span style="color: #339933;">-&gt;</span><span style="color: #004000;">setBacon</span><span style="color: #009900;">&#40;</span><span style="color: #009900; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span>
            <span style="color: #339933;">-&gt;</span><span style="color: #004000;">build</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">pizza</span> <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Pizza<span style="color: #009900;">&#40;</span><span style="color: #000088;">$pizzaBuilderObject</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> testIsObjectInstanceOfPizzaClass<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>        
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">assertInstanceOf</span><span style="color: #009900;">&#40;</span>Pizza<span style="color: #339933;">::</span><span style="color: #000000; font-weight: bold;">class</span><span style="color: #339933;">,</span> <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">pizza</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
&nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">function</span> testPizzaHasExtraCheese<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>
    <span style="color: #009900;">&#123;</span>        
        <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">assertEquals</span><span style="color: #009900;">&#40;</span><span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">pizza</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">getExtraCheese</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #009900; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
<span style="color: #009900;">&#125;</span>
&nbsp;
<span style="color: #000000; font-weight: bold;">?&gt;</span></pre>

Execute tests:
./vendor/bin/phpunit tests/BuilderPatternTest.php 
PHPUnit 7.5.20 by Sebastian Bergmann and contributors.
 
..                                                                  2 / 2 (100%)
 
Time: 32 ms, Memory: 4.00 MB
 
OK (2 tests, 2 assertions)
 














