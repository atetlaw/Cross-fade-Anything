This script is provided under the Open Source MIT License.

## Instructions

To set it up all you need is an HTML block element. All immediate descendants become slides. To start the effect you simply have to give the parent element a class of 'crossfade'. If FastInit is present it'll use that to start it automatically, otherwise it'll add a window.onload event. Alternatively you can do it this way:
new Crossfade('example', {interval : 10});
and it'll start after a random amount of time between 100 milliseconds and the interval amount.
If you have a child 'a' element with a class of 'loadimage' the crossfader will replace it with an image tag and load the a.href as the image src. It will also handle pre loading the next image. For example instead of this:

	<li>
		<img src="image1.jpg" />
		<div class="caption">Image 1 is pretty</div>
	</li>

you can have this:

	<li>
		<a href="image1.jpg" class="loadimage"></a>
		<div class="caption">Image 1 is pretty</div>
	</li>

If you have a child 'a' element with a class of 'load' the crossfader will load the slide content from the a.href via Ajax, a GET request. For example:

	<li>
		<a href="ajax.php&arg=1" class="load"></a>
	</li>

Make sure the resource at a.href returns a snippet of plain old HTML.
If you have an element with an id matching the crossfade parent id + '-next' or '-previous' they will become next and previous slide controls. For example if you give your parent element the id of 'slideshow', then give the controls the ids of 'slideshow-next' and 'slideshow-previous'. See the demo for an example.
Transitions

4 transition styles are supplied with the library and you can also make your own.
To specify a transition use an option (below) or add a class name to the parent element. Here are the transitions included:

- Option Name - Class Name
- Crossfade.Transition.Switch - 'transition-switch'
- Crossfade.Transition.Crossfade - 'transition-crossfade'
- Crossfade.Transition.FadeOutFadeIn - 'transition-fadeoutfadein'
- Crossfade.Transition.FadeOutResizeFadeIn - 'transition-fadeoutresizefadein'

If you want to add you own you need to create an object with the following properties:

	var myTransition = { className : 'transition-mytransition', cycle : function(prev, next, show) {}, cancel : function(show){}, prepare : function(show){} };

The cycle() function is called to apply the transition effect. 'prev' is the slide element transitioning out, 'next' is the slide element transitioning in, 'show' is the crossfade object.

The cancel() function is called to cancel the transition effect.

The prepare() function is called when the crossfade object is initialised, in order for the transition to prepare the crossfade object if required.

You can apply your custom transition object via the options or, if you want the class name to be automatically used, then you need to add your transition to the library collection, for example:

	Crossfade.Transition.MyTransition = {...}

Have a look at the included transitions to get an idea of how it all works.

## Options

Option : default
	autoLoad : true
Set this to false if you don't want the script to look for elements to cross-fade based on the selectors.
	autoStart : true
Set this to false if you don't want the slideshow to start autometically.
	interval : 5
Number of second to display each element
	duration : 2
Duration in seconds of the fade effect
	random : false
Set to true to randomise the order.
	randomClassName : 'random'
Add this classname to the crossfade parent element and it'll randomise the order as well (as an alternative to using the above option in Javascript).
	selectors : ['.crossfade']
The selector used for the autoStart feature, you can set it to an array of any prototype selectors.
	transition : Crossfade.Transition.Crossfade
The style of transition used
To change the defaults, while still making use of autoStart feature use Crossfade.setup({options}); for example:
	Crossfade.setup({interval : 10, random : true});
CSS

To give the best presentation consider positioning the parent, and then making all immediate descendants absolutely positioned to tile them on top of each other.