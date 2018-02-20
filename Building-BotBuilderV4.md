#Building the BotBuilder

In July of 2017, the Bot Framework team came to the conclusion that a new BotBuilder SDK was needed. In the 2 years since the previous version, [BotBuilder v3](github.com/Microsoft/BotBuilder), was released the team had come to some new understandings, built many bots, and worked with countless partners in this space. 

As we kicked off this effort, we decided upon 4 pillars:
1. **Transparent**. We wanted to build this iteration of the SDK with the full coporation of our partners. This includes 1st party teams at Microsoft such as Cortana and Skype, 3rd parties that build their own specialized frameworks atop our SDK, and developers who build Bots. 
2. **Modular Packages**. By building a modular SDK, with developers able to pull in only the components they need, we believed we could add more value and simplify everything at the same time. This means dependency management is a major component of everything we build and all packages need to be thought-through from a dependency and laying perspective.  
3. **Highly Extensible**. The diversity of developers and scenarios that build Bots is simply amazing. We struggled to envision a design where we build an SDK that was everything to everyone. Instead the SDK would need to embrace components build by the community. 
4. **Multi-Platform Aligned**. Concepts found in the C# SDK should be similar to concepts found in a Javascript SDK, should be similar to concepts found in a Python SDK. Ideally, a single set of documentation should cover all platforms, with only the nuance of language differing between platforms. 

The plan we settled on was the obvious one. 

## **Connector**

The Connector is our protocol layer. Mostly auto-generated from Swagger files using [AutoRest](https://github.com/Azure/autorest), this layer provides a minimal dependency  "Bare Metal" version of the Bot SDK. We add the platform specific authentication code and call that layer done. 

With the connector, you can plug into existing frameworks such as Redux, Restify, or ASP.Net. 

The previous C# SDK had done some of this, but had not split the connector into a seperate package. The v3 Node SDK had hand-authored the REST layer. 

Our first set of work items became improving our code generation. We leverage [AutoRest]() to create code, but we immediatly ran into problems. Generating quality code across many languages (C#, Javascript, Typescript, Python, Java, ++) turns out to be tricky.

 We've gotten to a point where things are working well, and you can see where we're at here.
 - C# ( [Connector](https://github.com/Microsoft/botbuilder-dotnet/tree/master/libraries/Microsoft.Bot.Connector), [Schema](https://github.com/Microsoft/botbuilder-dotnet/tree/master/libraries/Microsoft.Bot.Schema)). Sample [WebAPI Echo Bot](https://github.com/Microsoft/botbuilder-dotnet/tree/master/samples/Connector.EchoBot). 
 - Javascript ([Connector](https://github.com/Microsoft/botbuilder-js/tree/master/libraries/botframework-connector), [Schema](https://github.com/Microsoft/botbuilder-js/tree/master/libraries/botbuilder-schema)). Sample [ES6 / Node Echo Bot](https://github.com/Microsoft/botbuilder-js/tree/master/samples/echobot-connector-es6). 



4. Roadmap. We wanted to let folks know where we're going, and how we're asdfasdfgetting there. Roadmaps, once viewed as restricive and fully of propietary intellectual property, are liberating.