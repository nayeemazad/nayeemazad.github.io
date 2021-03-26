Factory Method design pattern is a creational pattern which defines an interface for creating an object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses. 


Let's see an example of payment system where we can pay with different types of payment methods. 
We will create a payment service and delegate its instantiation logic to Factories. Our project structure will look like this. 

<!-- HTML generated using hilite.me --><div style="background: #000000; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #cccccc">├── composer.json</span>
<span style="color: #cccccc">├── composer.lock</span>
<span style="color: #cccccc">├── src</span>
<span style="color: #cccccc">│   ├── Factories</span>
<span style="color: #cccccc">│   │   └── Payment</span>
<span style="color: #cccccc">│   │       ├── PaymentFactoryInterface.php</span>
<span style="color: #cccccc">│   │       ├── PaypalFactory.php</span>
<span style="color: #cccccc">│   │       └── StripeFactory.php</span>
<span style="color: #cccccc">│   └── Services</span>
<span style="color: #cccccc">│       └── Payment</span>
<span style="color: #cccccc">│           ├── PaymentInterface.php</span>
<span style="color: #cccccc">│           ├── Paypal.php</span>
<span style="color: #cccccc">│           └── Stripe.php</span>
<span style="color: #cccccc">├── tests</span>
<span style="color: #cccccc">│   └── PaymentTest.php</span>
<span style="color: #cccccc">└── vendor</span>
</pre></div>

Create PaymentInterface first.

<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #557799">&lt;?php</span> <span style="color: #008800; font-weight: bold">declare</span>(strict_types<span style="color: #333333">=</span><span style="color: #0000DD; font-weight: bold">1</span>);

<span style="color: #008800; font-weight: bold">namespace</span> App\Services\Payment;

<span style="color: #008800; font-weight: bold">interface</span> PaymentInterface
{
    <span style="color: #008800; font-weight: bold">public</span> <span style="color: #008800; font-weight: bold">function</span> <span style="color: #0066BB; font-weight: bold">pay</span>()<span style="color: #333333">:</span> string;
}
    
<span style="color: #557799">?&gt;</span>
</pre></div>


Paypal service will implement the PaymentInterface


<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #557799">&lt;?php</span> <span style="color: #008800; font-weight: bold">declare</span>(strict_types<span style="color: #333333">=</span><span style="color: #0000DD; font-weight: bold">1</span>);

<span style="color: #008800; font-weight: bold">namespace</span> App\Services\Payment;
<span style="color: #008800; font-weight: bold">use</span> App\Services\Payment\PaymentInterface;

<span style="color: #008800; font-weight: bold">class</span> <span style="color: #BB0066; font-weight: bold">Paypal</span> <span style="color: #008800; font-weight: bold">implements</span> PaymentInterface
{
    <span style="color: #008800; font-weight: bold">public</span> <span style="color: #008800; font-weight: bold">function</span> <span style="color: #0066BB; font-weight: bold">pay</span>()<span style="color: #333333">:</span> string
    {
        <span style="color: #888888">// process payment via paypal</span>
        <span style="color: #008800; font-weight: bold">return</span> <span style="background-color: #fff0f0">&#39;SUCCESS&#39;</span>;
    }
}
<span style="color: #557799">?&gt;</span>
</pre></div>

Similarly Sripe service will implement PaymentInterface.

<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #557799">&lt;?php</span> <span style="color: #008800; font-weight: bold">declare</span>(strict_types<span style="color: #333333">=</span><span style="color: #0000DD; font-weight: bold">1</span>);

<span style="color: #008800; font-weight: bold">namespace</span> App\Services\Payment;
<span style="color: #008800; font-weight: bold">use</span> App\Services\Payment\PaymentInterface;

<span style="color: #008800; font-weight: bold">class</span> <span style="color: #BB0066; font-weight: bold">Stripe</span> <span style="color: #008800; font-weight: bold">implements</span> PaymentInterface
{
    <span style="color: #008800; font-weight: bold">public</span> <span style="color: #008800; font-weight: bold">function</span> <span style="color: #0066BB; font-weight: bold">pay</span>()<span style="color: #333333">:</span> string
    {
        <span style="color: #888888">// process payment via stripe</span>
        <span style="color: #008800; font-weight: bold">return</span> <span style="background-color: #fff0f0">&quot;SUCCESS&quot;</span>;
    }
}
<span style="color: #557799">?&gt;</span>
</pre></div>

Any other payment service in future if you need should also implement this PaymentInterface.
Now, we will create factories.

PaymentFactoryInterface.php

<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #557799">&lt;?php</span> <span style="color: #008800; font-weight: bold">declare</span>(strict_types<span style="color: #333333">=</span><span style="color: #0000DD; font-weight: bold">1</span>);

<span style="color: #008800; font-weight: bold">namespace</span> App\Factories\Payment;

<span style="color: #008800; font-weight: bold">use</span> App\Services\Payment\PaymentInterface;

<span style="color: #008800; font-weight: bold">interface</span> PaymentFactoryInterface
{
    <span style="color: #008800; font-weight: bold">public</span> <span style="color: #008800; font-weight: bold">function</span> <span style="color: #0066BB; font-weight: bold">getInstance</span>()<span style="color: #333333">:</span> PaymentInterface;
}

<span style="color: #557799">?&gt;</span>
</pre></div>

PaypalFactory.php

<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #557799">&lt;?php</span> <span style="color: #008800; font-weight: bold">declare</span>(strict_types<span style="color: #333333">=</span><span style="color: #0000DD; font-weight: bold">1</span>);

<span style="color: #008800; font-weight: bold">namespace</span> App\Factories\Payment;

<span style="color: #008800; font-weight: bold">use</span> App\Services\Payment\Paypal;
<span style="color: #008800; font-weight: bold">use</span> App\Services\Payment\PaymentInterface;
<span style="color: #008800; font-weight: bold">use</span> App\Factories\Payment\PaymentFactoryInterface;


<span style="color: #008800; font-weight: bold">class</span> <span style="color: #BB0066; font-weight: bold">PaypalFactory</span> <span style="color: #008800; font-weight: bold">implements</span> PaymentFactoryInterface
{
    <span style="color: #008800; font-weight: bold">public</span> <span style="color: #008800; font-weight: bold">function</span> <span style="color: #0066BB; font-weight: bold">getInstance</span>()<span style="color: #333333">:</span> PaymentInterface
    {
        <span style="color: #008800; font-weight: bold">return</span> <span style="color: #008800; font-weight: bold">new</span> Paypal();
    }
}

<span style="color: #557799">?&gt;</span>
</pre></div>


StripeFactory.php

<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #557799">&lt;?php</span> <span style="color: #008800; font-weight: bold">declare</span>(strict_types<span style="color: #333333">=</span><span style="color: #0000DD; font-weight: bold">1</span>);

<span style="color: #008800; font-weight: bold">namespace</span> App\Factories\Payment;

<span style="color: #008800; font-weight: bold">use</span> App\Services\Payment\Stripe;
<span style="color: #008800; font-weight: bold">use</span> App\Services\Payment\PaymentInterface;
<span style="color: #008800; font-weight: bold">use</span> App\Factories\Payment\PaymentFactoryInterface;

<span style="color: #008800; font-weight: bold">class</span> <span style="color: #BB0066; font-weight: bold">StripeFactory</span> <span style="color: #008800; font-weight: bold">implements</span> PaymentFactoryInterface
{
    <span style="color: #008800; font-weight: bold">public</span> <span style="color: #008800; font-weight: bold">function</span> <span style="color: #0066BB; font-weight: bold">getInstance</span>()<span style="color: #333333">:</span> PaymentInterface
    {
        <span style="color: #008800; font-weight: bold">return</span> <span style="color: #008800; font-weight: bold">new</span> Stripe();
    }
}

<span style="color: #557799">?&gt;</span>
</pre></div>


Ok. we are done with the service and factories for the payment. Now write phpunit test cases to test the factory method. We will not directly instantiate the services, rather we should use the dedicated factories for the service. Factory will decide which concrete classes may I need to create class object.

<!-- HTML generated using hilite.me --><div style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #557799">&lt;?php</span> <span style="color: #008800; font-weight: bold">declare</span>(strict_types<span style="color: #333333">=</span><span style="color: #0000DD; font-weight: bold">1</span>);
<span style="color: #008800; font-weight: bold">namespace</span> App\Tests;

<span style="color: #008800; font-weight: bold">require_once</span> <span style="background-color: #fff0f0">&#39;./vendor/autoload.php&#39;</span>; 
<span style="color: #008800; font-weight: bold">use</span> App\Factories\Payment\PaypalFactory;
<span style="color: #008800; font-weight: bold">use</span> App\Factories\Payment\StripeFactory;
<span style="color: #008800; font-weight: bold">use</span> App\Services\Payment\Paypal;
<span style="color: #008800; font-weight: bold">use</span> App\Services\Payment\Stripe;
<span style="color: #008800; font-weight: bold">use</span> PHPUnit\Framework\TestCase;

<span style="color: #008800; font-weight: bold">class</span> <span style="color: #BB0066; font-weight: bold">PaymentTest</span> <span style="color: #008800; font-weight: bold">extends</span> TestCase
{
    <span style="color: #008800; font-weight: bold">public</span> <span style="color: #008800; font-weight: bold">function</span> <span style="color: #0066BB; font-weight: bold">testCanCreatePaypalInstance</span>()
    {
        <span style="color: #996633">$paymentFactory</span> <span style="color: #333333">=</span> <span style="color: #008800; font-weight: bold">new</span> PaypalFactory();
        <span style="color: #996633">$payment</span> <span style="color: #333333">=</span> <span style="color: #996633">$paymentFactory</span><span style="color: #333333">-&gt;</span><span style="color: #0000CC">getInstance</span>();

        <span style="color: #996633">$this</span><span style="color: #333333">-&gt;</span><span style="color: #0000CC">assertInstanceOf</span>(Paypal<span style="color: #333333">::</span><span style="color: #0000CC">class</span>, <span style="color: #996633">$payment</span>);
    }

    <span style="color: #008800; font-weight: bold">public</span> <span style="color: #008800; font-weight: bold">function</span> <span style="color: #0066BB; font-weight: bold">testCanCreateStripeInstance</span>()
    {
        <span style="color: #996633">$paymentFactory</span> <span style="color: #333333">=</span> <span style="color: #008800; font-weight: bold">new</span> StripeFactory();
        <span style="color: #996633">$payment</span> <span style="color: #333333">=</span> <span style="color: #996633">$paymentFactory</span><span style="color: #333333">-&gt;</span><span style="color: #0000CC">getInstance</span>();

        <span style="color: #996633">$this</span><span style="color: #333333">-&gt;</span><span style="color: #0000CC">assertInstanceOf</span>(Stripe<span style="color: #333333">::</span><span style="color: #0000CC">class</span>, <span style="color: #996633">$payment</span>);
    }

    <span style="color: #008800; font-weight: bold">public</span> <span style="color: #008800; font-weight: bold">function</span> <span style="color: #0066BB; font-weight: bold">testCanPayWithPaypal</span>()
    {
        <span style="color: #996633">$paymentFactory</span> <span style="color: #333333">=</span> <span style="color: #008800; font-weight: bold">new</span> PaypalFactory();
        <span style="color: #996633">$payment</span> <span style="color: #333333">=</span> <span style="color: #996633">$paymentFactory</span><span style="color: #333333">-&gt;</span><span style="color: #0000CC">getInstance</span>();
        <span style="color: #996633">$response</span> <span style="color: #333333">=</span> <span style="color: #996633">$payment</span><span style="color: #333333">-&gt;</span><span style="color: #0000CC">pay</span>();
        <span style="color: #996633">$this</span><span style="color: #333333">-&gt;</span><span style="color: #0000CC">assertEquals</span>(<span style="color: #996633">$response</span>, <span style="background-color: #fff0f0">&#39;SUCCESS&#39;</span>);
    }

    <span style="color: #008800; font-weight: bold">public</span> <span style="color: #008800; font-weight: bold">function</span> <span style="color: #0066BB; font-weight: bold">testCanPayWithStripe</span>()
    {
        <span style="color: #996633">$paymentFactory</span> <span style="color: #333333">=</span> <span style="color: #008800; font-weight: bold">new</span> StripeFactory();
        <span style="color: #996633">$payment</span> <span style="color: #333333">=</span> <span style="color: #996633">$paymentFactory</span><span style="color: #333333">-&gt;</span><span style="color: #0000CC">getInstance</span>();
        <span style="color: #996633">$response</span> <span style="color: #333333">=</span> <span style="color: #996633">$payment</span><span style="color: #333333">-&gt;</span><span style="color: #0000CC">pay</span>();
        <span style="color: #996633">$this</span><span style="color: #333333">-&gt;</span><span style="color: #0000CC">assertEquals</span>(<span style="color: #996633">$response</span>, <span style="background-color: #fff0f0">&#39;SUCCESS&#39;</span>);
    }
}
</pre></div>



Execute tests

<!-- HTML generated using hilite.me --><div style="background: #000000; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #cccccc">$./vendor/bin/phpunit tests</span>
<span style="color: #cccccc">PHPUnit 7.5.20 by Sebastian Bergmann and contributors.</span>

<span style="color: #cccccc">....                                                                4 / 4 (100%)</span>

<span style="color: #cccccc">Time: 33 ms, Memory: 4.00 MB</span>

<span style="color: #cccccc">OK (4 tests, 4 assertions)</span>
</pre></div>
