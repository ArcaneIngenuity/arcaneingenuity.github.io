---
layout: post
title: Arc Framework&#58; Runthrough and Loose Ends
tags:
- arc
---

Today I'll be talking about [arc](https://github.com/ArcaneIngenuity/arc), which is the basis for War & Adventure. This will only be of interest to developers and techish sorts; others will have to wait until tomorrow when I'll post some visuals of engine work to date.

Working back toward visuals
---------------------------

I'm in a stage of heavy code refactoring at the moment. Visuals are almost all down, except for an item or two needed for testing. Here's why.

Arc is an open source framework I've written over the last few years to ease game development while keeping the developer close to the metal. Over the last few months I've ported it to C and improved it further to meet the task of implementing War & Adventure. Let's just jump in at the deep end.

Arc, as a real-time MVC framework, benefits us by its flexible configuration system. An ordinary `arc.config`, without user `Extension`s, might be so&#58;

```

<?xml version="1.0"?>
<hub>
	<apps>
		<app class="AWarAdventure" id="WA">
			<model class="MRoot">
			</model>
			<view class="VRoot" id="root">
				...
				<view class="VMenu" id="menu">
					...
				</view>
				<view class="VPlayArea" id="play">
					<view class="VBeltBar" id="belt">
					</view>
				</view>
			</view>
			<ctrl class="CRoot" id="root">
				<ctrl class="CInput" id="input" model="&.input"/>
			</ctrl>
		</app>
	</apps>
</hub>

```

You can see the `<app/>` element which contains basic structure for this app. This allows us to review our app skeleton at a glance, noting how its various components tie together. Every `View` may contain sub-`View`s, forming a tree rooted on the `App`, and even `Ctrl`s (controllers) may optionally contain sub-`Ctrl`s. You can easily get away with just one root `Ctrl` e.g. just use `CRoot` per the above, while tying into your own  helper classes which needn't be implemented as `Ctrl`s. The benefit of implementing `CInput` as a `Ctrl` here is that I can handle input via a recognisable interface `Updater` which is the basis for `Ctrl`s and `View`s. As one becomes more familiar with arc, this interface becomes desirable to work with.

The real power in `arc.config` comes from its ability to include user-written `Extension`s via a very simple interface. Let's take another look at the XML, this time filling in contents of the `VRoot` and `VMenu` from the last example:

```

			<view class="VRoot" id="root">
				<extension class="XShaderLoader" id="shaderLoader">
					<shaders>
						<shader id="ui.vert" type="vertex"/>
						<shader id="ui.frag" type="fragment"/>
						<shader id="eye.vert" type="vertex"/>
						<shader id="eye.frag" type="fragment"/>
						<shader id="billboard.vert" type="vertex"/>
						<shader id="billboard.frag" type="fragment"/>
					</shaders>
					<programs>
						...
					</programs>
				</extension>
				<view class="VMenu" id="menu">
					<extension class="XUniformMap" id="uniformsByName">
						<uniforms>
							<uniform name="offset"
								model="&.position"
								type="UniformVector"
								typeNumeric="UniformFloat"
								componentsMajor="3"
								componentsMinor="0"
								elements="1">
							</uniform>
						</uniforms>
					</extension>
				</view>
				...
			</view>

```

See how the body of `<view>` `VRoot` is now an `<extension>`, and similar for `VMenu`? The `<extension>` as such is not part of the arc framework, but rather a user-created element that implements the `Extension` interface specified by arc, allowing arc to recognise an `Extension`, parse it, and slot it into its containing `View`. Now `VRoot` (the `View` in question) has runtime access to our custom `XShaderLoader` instance, while `VMenu` similarly has access to the `XUniformMap`. And since `VRoot` is the parent / container of `VMenu`, `VMenu` can also access its parent's shader information.... useful.

Extensions allow for user-written, easily-configurable code (instances) to be included in the otherwise limited MVC setup we saw in the first example.


This is where the real power of arc lies - write less code while having a better overview of the app. Rather than having discrete source (and header) files scattered all over the show, `arc.config` offers an architectural overview of your application, at a glance. ("arc" is short for "architecture".)

Why am I telling you all this? Well, have look here&#58;

```
<ctrl class="CInput" id="input" model="&.general.input" />
...
<uniform name="offset"
	values="&.position"
	type="UniformVector"
	typeNumeric="UniformFloat"
	componentsMajor="3"
	componentsMinor="0"
	elements="1">
```

Both of these have something that looks like `&.<name>.<other name>` in them. This is a way to drill down through struct/class members and get a reference to some data we need to use,

 * in the 1st case as the base model used by a particular `Ctrl`,
 * in the 2nd case as the value to source an OpenGL uniform variable from, within the user extension known as `XUniformMap`.

At the moment, arc doesn't allow the second case. In the JavaScript version of arc this was trivial, but in C less so because C has no runtime type (member) information. Fortunately the majority of the groundwork has already been laid. I'm tweaking today and over the weekend to enable this.

In closing...
-------------

As I'm deep in this refactoring process at the moment, visuals are offline. Tomorrow I will get an older version of the framework/engine running just to show you fundamentals from earlier in October before I began blogging.