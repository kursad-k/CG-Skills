# Unreal-Engine - Programming

**Pages:** 10

---

## Coding Standard

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/epic-cplusplus-coding-standard-for-unreal-engine

**Contents:**
- Coding Standard
- Class Organization
- Copyright Notice
- Naming Conventions
- Inclusive Word Choice
  - Racial, ethnic, and religious inclusiveness
  - Gender inclusiveness
  - Slang
  - Overloaded Words
  - Word List

Write maintainable code by adhering to established standards and best practices.

At Epic Games, we have a few simple coding standards and conventions. This document reflects the state of Epic Games' current coding standards. Following the coding standards is mandatory.

Code conventions are important to programmers for several reasons:

80% of the lifetime cost of a piece of software goes to maintenance.

Hardly any software is maintained for its whole life by the original author.

Code conventions improve the readability of software, allowing engineers to understand new code quickly and thoroughly.

If we decide to expose source code to mod community developers, we want it to be easily understood.

Many of these conventions are required for cross-compiler compatibility.

The coding standards below are C++-centric; however, the standard is expected to be followed no matter which language is used. A section may provide equivalent rules or exceptions for specific languages where it's applicable.

Classes should be organized with the reader in mind rather than the writer. Since most readers will use the public interface of the class, the public implementation should be declared first, followed by the class's private implementation.

Any source file (.h, .cpp, .xaml) provided by Epic Games for public distribution must contain a copyright notice as the first line in the file. The format of the notice must exactly match that shown below:

If this line is missing or not formatted properly, CIS will generate an error and fail.

When using Naming Conventions, all code and comments should use U.S. English spelling and grammar.

The first letter of each word in a name (such as type name or variable name) is capitalized. There is usually no underscore between words. For example, Health and UPrimitiveComponent are correct, but lastMouseCoordinates or delta_coordinates are not.

This is PascalCase formatting for users who may be familiar with other object oriented programming languages

Type names are prefixed with an additional upper-case letter to distinguish them from variable names. For example, FSkin is a type name, and Skin is an instance of type FSkin.

Template classes are prefixed by T.

Classes that inherit from UObject are prefixed by U.

Classes that inherit from AActor are prefixed by A.

Classes that inherit from SWidget are prefixed by S.

Classes that are abstract interfaces are prefixed by I.

Epic's concept-alike struct types are prefixed by C.

Enums are prefixed by E.

Boolean variables must be prefixed by b.

Most other classes are prefixed by F, though some subsystems use other letters.

Typedefs should be prefixed by whatever is appropriate for that type, such as:

F for typedef of a struct

U for typedef of a UObject

A typedef of a particular template instantiation is no longer a template and should be prefixed accordingly.

Prefixes are omitted in C#.

Unreal Header Tool requires the correct prefixes in most cases, so it's important to provide them.

Type template parameters and nested type aliases based on those template parameters are not subject to the above prefix rules, as the type category is unknown.

Prefer a Type suffix after a descriptive term.

Disambiguate template parameters from aliases by using an In prefix:

Type and variable names are nouns.

Method names are verbs that either describe the method's effect, or the return value of a method without an effect.

Macro names should be fully capitalized with words separated by underscores, and prefixed with UE_.

Variable, method, and class names should be:

The greater the scope of the name, the greater the importance of a good, descriptive name. Avoid over-abbreviation.

All variables should be declared on their own line so that you can provide comment on the meaning of each variable.

The JavaDocs style requires it.

You can use multi-line or single-line comments before a variable Blank lines are optional for grouping variables.

All functions that return a bool should ask a true/false question, such as IsVisible() or ShouldClearBuffer().

A procedure (a function with no return value) should use a strong verb followed by an Object. An exception is, if the Object of the method is the Object it is in. In this case, the Object is understood from context. Names to avoid include those beginning with "Handle" and "Process" because the verbs are ambiguous.

We encourage you to prefix function parameter names with "Out" if:

The function parameters are passed by reference.

The function is expected to write to that value.

This makes it obvious that the value passed in this argument is replaced by the function.

If an In or Out parameter is also a boolean, put "b" before the In/Out prefix, such as bOutResult.

Functions that return a value should describe the return value. The name should make clear what value the function returns. This is particularly important for boolean functions. Consider the following two example methods:

When you work in the Unreal Engine codebase, we encourage you to strive to use respectful, inclusive, and professional language.

Word choice applies when you:

It applies when you write snippets of user-facing text for the UI, error messages, and notifications. It also applies when writing about code, such as in comments and changelist descriptions.

The following sections provide guidance and suggestions to help you choose words and names that are respectful and appropriate for all situations and audiences, and be a more effective communicator.

Do not use metaphors or similes that reinforce stereotypes. Examples include contrast black and white or blacklist and whitelist.

Do not use words that refer to historical trauma or lived experience of discrimination. Examples include slave, master, and nuke.

Refer to hypothetical people as they, them, and their, even in the singular.

Refer to anything that is not a person as it and its. For example, a module, plugin, function, client, server, or any other software or hardware component.

Do not assign a gender to anything that doesn't have one.

Do not use collective nouns like guys that assume gender.

Avoid colloquial phrases that contain arbitrary genders, like "a poor man's X".

Remember that your words are being read by a global audience that may not share the same idioms and attitudes, and who might not understand the same cultural references.

Avoid slang and colloquialisms, even if you think they are funny or harmless. These may be hard to understand for people whose first language is not English, and might not translate well.

Do not use profanity.

The following list identifies some terminology that we have used in the Unreal codebase in the past, but that we believe should be replaced with better alternatives:

We are actively working to bring our code in line with the principles laid out above.

The int and unsigned int types vary in size across platforms. They are guaranteed to be at least 32 bits in width and are acceptable in code when the integer width is unimportant. Explicitly-sized types are used in serialized or replicated formats.

Below is a list of common types:

bool for boolean values (NEVER assume the size of bool). BOOL will not compile.

TCHAR for a character (NEVER assume the size of TCHAR).

uint8 for unsigned bytes (1 byte).

int8 for signed bytes (1 byte).

uint16 for unsigned shorts (2 bytes).

int16 for signed shorts (2 bytes).

uint32 for unsigned ints (4 bytes).

int32 for signed ints (4 bytes).

uint64 for unsigned quad words (8 bytes).

int64 for signed quad words (8 bytes).

float for single precision floating point (4 bytes).

double for double precision floating point (8 bytes).

PTRINT for an integer that may hold a pointer (NEVER assume the size of PTRINT).

Historically, UE has avoided direct use of the C and C++ standard libraries for the following reasons:

Replace slow implementations with our own that provide additional control over memory allocation.

Add new functionality before it's widely available, such as:

Making desirable, but non-standard, behavioral changes.

Having consistent syntax across the codebase.

Avoiding constructs which are incompatible with UE's idioms.

However, the standard library has matured and includes functionality that we don't want to wrap with an abstraction layer or reimplement ourselves.

When there is a choice between a standard library feature instead of our own, you should prefer the option that gives superior results. It's also important to remember that consistency is valued. If a legacy UE implementation is no longer serving a purpose, we may choose to deprecate it and migrate all usage toward the standard library.

Avoid mixing UE idioms and standard library idioms in the same API. The following table lists common idioms along with recommendations on when to use them.

Standard containers and strings should be avoided except in interop code.

Comments are communication and communication is vital. The following sections detail some important things to keep in mind about comments (from Kernighan & Pike The Practice of Programming).

Write self-documenting code. For example:

Write useful comments. For example:

Do not over comment bad code — rewrite it instead. For example:

Do not contradict the code. For example:

Const is documentation as much as it is a compiler directive. All code should strive to be const-correct. This includes the following guidelines:

Pass function arguments by const pointer or reference if those arguments are not intended to be modified by the function.

Flag methods as const if they do not modify the object.

Use const iteration over containers if the loop isn't intended to modify the container.

Const is also preferred for by-value function parameters and locals. This tells the reader that the variable will not be modified in the body of the function, which makes it easier to understand. If you do this, make sure that the declaration and the definition match, as this can affect the JavaDoc process.

One exception to this is pass-by-value parameters, which are moved into a container. For more information, see the "Move semantics" section on this page.

Put the const keyword on the end when making a pointer itself const (rather than what it points to). References can't be "reassigned" anyway, and so can't be made const in the same way.

Never use const on a return type. This inhibits move semantics for complex types, and will give compile warnings for built-in types. This rule only applies to the return type itself, not the target type of a pointer or reference being returned.

We use a system based on JavaDoc to extract comments from the code and build documentation automatically, therefore we recommend specific comment formatting rules.

The following example demonstrates the format of class, method, and variable comments. Remember that comments should augment the code. Code documents the implementation while comments document the intent. Make sure to update comments when you change the intent of a piece of code.

Note that two different parameter comment styles are supported, shown by the Steep and Sweeten methods. The @param style used by Steep is the traditional multi-line style. For simple functions, it can be clearer to integrate the parameter and return value documentation into the descriptive comment for the function. This is demonstrated in the Sweeten example. Special comment tags like @see or @return should only be used to start new lines following the primary description.

Method comments should only be included once: where the method is publicly declared. The method comments should only contain information relevant to callers of the method, including any information about overrides of the method that may be relevant to the caller. Details about the implementation of the method and its overrides, that are not relevant to callers, should be commented within the method implementation.

Class comments should include:

A description of the problem this class solves.

The reason why was this class created.

Multi-line method comments should include:

Function purpose: Documents the problem this function solves. As previously stated, comments document intent, and code documents implementation.

Parameter comments: Each parameter comment should include:

the range of expected values;

and the meaning of status/error codes.

Return comment: Documents the expected return value, just as an output variable is documented. To avoid redundancy, an explicit @return comment should not be used if the sole purpose of the function is to return this value and that is already documented in the function purpose.

Extra information: @warning, @note, @see, and @deprecated can optionally be used to document additional relevant information. Each should be declared on their own line following the rest of the comments.

Unreal Engine is built to be massively portable to many C++ compilers, so we are careful to use features that are compatible with the compilers we might be supporting. Sometimes, features are so useful that we will wrap them in macros and use them pervasively. However, we usually wait until all the compilers we support are up to the latest standard.

Unreal Engine compiles with a language version of C++20 by default and requires a minimum version of C++20 to build. We use many modern language features that are well-supported across modern compilers. In some cases, we wrap usage of these features in preprocessor conditionals. However, sometimes we decide to avoid certain language features entirely, for portability or other reasons.

Unless specified below, as a modern C++ compiler feature we are supporting, you should not use compiler-specific language features unless they are wrapped in preprocessor macros or conditionals and used sparingly.

The static_assert keyword is valid for use where you need a compile-time assertion.

The override and final keywords are valid for use, and their use is strongly encouraged. There might be many places where these have been omitted, but they will be fixed over time.

You should use nullptr instead of the C-style NULL macro in all cases.

One exception to this is the use of nullptr in C++/CX builds (such as for Xbox One). In this case, the use of nullptr is actually the managed null reference type. It is mostly compatible with nullptr from native C++ except in its type and some template instantiation contexts, and so you should use the TYPE_OF_NULLPTR macro instead of the more usual decltype(nullptr) for compatibility.

You shouldn't use auto in C++ code, except for the few exceptions listed below. Always be explicit about the type you're initializing. This means that the type must be plainly visible to the reader. This rule also applies to the use of the var keyword in C#.

C++20's structured binding feature should also not be used, as it is effectively a variadic auto.

Acceptable use of auto:

When you need to bind a lambda to a variable, as lambda types are not expressible in code.

For iterator variables, but only where the iterator's type is verbose and would impair readability.

In template code, where the type of an expression cannot easily be discerned. This is an advanced case.

It's very important that types are clearly visible to someone who is reading the code. Even though some IDEs are able to infer the type, doing so relies on the code being in a compilable state. It also won't assist users of merge/diff tools, or when viewing individual source files in isolation, such as on GitHub.

If you're sure you are using auto in an acceptable way, always remember to correctly use const, &, or * just like you would with the type name. With auto, this will coerce the inferred type to be what you want.

This is preferred to keep the code easier to understand and more maintainable. When you migrate code that uses old TMap iterators, be aware that the old Key() and Value() functions, which were methods of the iterator type, are now simply Key and Value fields of the underlying key-value TPair.

We also have range replacements for some standalone iterator types.

Lambdas can be used freely but come with additional safety concerns. The best lambdas should be no more than a couple of statements in length, particularly when used as part of a larger expression or statement, for example as a predicate in a generic algorithm.

Be aware that stateful lambdas can't be assigned to function pointers, which we tend to use a lot. Non-trivial lambdas should be documented in the same manner as regular functions. Lambdas can also be used as Delegates for deferred execution using functions like BindWeakLambda where captured variables function as a payload.

Explicit captures should be used rather than automatic capture ([&] and [=]). This is important for readability, maintainability, safety, and performance reasons, particularly when used with large lambdas and deferred execution.

Explicit captures declare the author's intent; therefore, mistakes are caught during code review. Incorrect captures can cause serious bugs and crashes, which are more likely to become problematic as the code is maintained over time. Here are some additional things to keep in mind about lambda captures:

By-reference capture and by-value capture of pointers (including the this pointer) can cause data corruption and crashes if the execution of the lambda is deferred. Local and member variables should never be captured by reference for deferred lambdas.

By-value capture can be a performance concern if it makes unnecessary copies for a non-deferred lambda.

Accidentally captured UObject pointers are invisible to the garbage collector. Automatic capture catches this implicitly if any member variables are referenced, even though [=] gives the impression of the lambda having its own copies of everything.

Delegate wrappers like CreateWeakLambda and CreateSPLambda should be used for deferred execution as they will automatically unbind if the UObject or shared pointer are freed. Other shared objects can be captured as TWeakObjectPtr or TWeakPtr and then validated inside the lambda.

Any deferred lambda use that does not follow these guidelines must have a comment explaining why the lambda capture is safe.

Explicit return types should be used for large lambdas or when you are returning the result of another function call. These should be considered in the same way as the auto keyword.

Enumerated (Enum) classes are a replacement for old-style namespaced enums, both for regular enums and UENUMs. For example:

Enums are supported as UPROPERTYs, and replace the old TEnumAsByte<> workaround. Enum properties can also be any size, not just bytes:

Enums exposed to Blueprints must continue to be based on uint8.

Enum classes used as flags can take advantage of the ENUM_CLASS_FLAGS(EnumType) macro to automatically define all of the bitwise operators:

The one exception to this is the use of flags in a truth context - this is a limitation of the language. Instead, all enum flags should have an enumerator called None which is set to 0 for comparisons:

All of the main container types — TArray, TMap, TSet, FString — have move constructors and move assignment operators. These are often used automatically when passing or returning these types by value. They can also be explicitly invoked by using MoveTemp, UE's equivalent of std::move.

Returning containers or strings by value can be beneficial for expressivity, without the usual cost of temporary copies. Rules around pass-by-value and use of MoveTemp are still being established, but can already be found in some optimized areas of the codebase.

Default member initializers can be used to define the defaults of a class inside the class itself:

Code written like this has the following benefits:

It doesn't need to duplicate initializers across multiple constructors.

It isn't possible to mix the initialization order and declaration order.

The member type, property flags, and default values are all in one place. This helps readability and maintainability.

However, there are also some downsides:

Any change to the defaults requires a rebuild of all dependent files.

Headers can't change in patch releases of the engine, so this style can limit the kinds of fixes that are possible.

Some things can't be initialized in this way, such as base classes, UObject subobjects, pointers to forward-declared types, values deduced from constructor arguments, and members initialized over multiple steps.

Putting some initializers in the header and the rest in constructors in the .cpp file, can reduce readability and maintainability.

Use your best judgment when deciding whether to use default member initializers. As a rule of thumb, default member initializers make more sense with in-game code than engine code. Consider using config files for default values.

Whenever you modify the code to a library that we use in the engine, be sure to tag your changes with a //@UE5 comment, as well as an explanation of why you made the change. This makes merging the changes into a new version of that library easier, and ensures licensees can easily find any modifications we have made.

Any third party code included in the engine should be marked with comments formatted to be easily searchable. For example:

Brace wars are foul. Epic Games has a long standing usage pattern of putting braces on a new line. Please adhere to this usage, regardless of the size of the function or block. For example:

Always include braces in single-statement blocks. For example:

Each block of execution in an if-else statement should be in braces. This helps prevent editing mistakes. When braces are not used, someone could unwittingly add another line to an if block. The extra line wouldn't be controlled by the if expression, which would be bad. It's also bad when conditionally compiled items cause if/else statements to break. So always use braces.

A multi-way if statement should be indented with each else if indented the same amount as the first if; this makes the structure clear to a reader:

Below are some standards for indenting your code.

Indent code by execution block.

Use tabs for whitespace at the beginning of a line, not spaces. Set your tab size to 4 characters. Note, spaces are sometimes necessary and allowed for keeping code aligned regardless of the number of spaces in a tab. For example, when you are aligning code that follows non-tab characters.

If you are writing code in C#, please also use tabs, not spaces. The reason for this is that programmers often switch between C# and C++, and most prefer to use a consistent setting for tabs. Visual Studio defaults to using spaces for C# files, so you need to remember to change this setting when working on Unreal Engine code.

Except for empty cases (multiple cases having identical code), switch case statements should explicitly label that a case falls through to the next case. Either include a break, or include a "falls through" comment in each case. Other code control-transfer commands (return, continue, and so on) are fine as well.

Always have a default case. Include a break just in case someone adds a new case after the default.

You can use namespaces to organize your classes, functions and variables where appropriate. If you do use them, follow the rules below.

Most UE code is currently not wrapped in a global namespace.

Namespaces are not supported by UnrealHeaderTool.

New APIs which aren't UCLASSes, USTRUCTs etc, should be placed in a UE:: namespace, and ideally a nested namespace, e.g. UE::Audio::.

It's okay to put using declarations within another namespace, or within a function body.

If you put using declarations within a namespace, this will carry over to other occurrences of that namespace in the same translation unit. As long as you are consistent, it will be fine.

You can only use using declarations in header files safely if you follow the above rules.

Forward-declared types need to be declared within their respective namespace.

If you declare a lot of classes or types within a namespace, it can be difficult to use those types in other global-scoped classes (for example, function signatures will need to use explicit namespace when appearing in class declarations).

You can use using declarations to only alias specific variables within a namespace into your scope.

Macros cannot live in a namespace.

File names should not be prefixed where possible.

All headers should protect against multiple includes with the #pragma once directive.

Note that all compilers we use support #pragma once.

Try to minimize physical coupling.

Forward declarations are preferred to including headers.

When including a header, be as fine grained as possible.

Try to include every header you need directly to make fine-grained inclusion easier.

Don't rely on a header that is included indirectly by another header you include.

Don't rely on anything being included through another header. Include everything you need.

Modules have Private and Public source directories.

Don't worry about setting up your headers for precompiled header generation.

Split large functions into logical sub-functions.

Don't use a large number of inline functions.

Be conservative in your use of FORCEINLINE.

Enforce encapsulation with the protection keywords. Class members should almost always be declared private unless they are part of the public/protected interface to the class. Use your best judgment, but always be aware that a lack of accessors makes it hard to refactor later without breaking plugins and existing projects.

If particular fields are only intended to be usable by derived classes, make them private and provide protected accessors.

Use final if your class is not designed to be derived from.

Minimize dependency distance.

Split methods into sub-methods where possible.

In function declarations or function call sites, do not add a space between the function's name and the parentheses that precede the argument list.

Address compiler warnings.

Leave a blank line at the end of the file.

Debug code should either be useful and polished, or not checked in.

Always use the TEXT() macro around string literals.

Avoid repeating the same operation redundantly in loops.

Be mindful of hot reload.

Use intermediate variables to simplify complicated expressions.

If you have a complicated expression, it can be easier to understand if you split it into sub-expressions, that are assigned to intermediate variables, with names describing the meaning of the sub-expression within the parent expression. For example:

Should be replaced with:

Pointers and references should only have one space to the right of the pointer or reference.

This makes it easy to quickly use Find in Files for all pointers or references to a certain type. For example:

Shadowed variables are not allowed.

C++ allows variables to be shadowed from an outer scope, but this makes usage ambiguous to a reader. For example, there are three usable Count variables in this member function:

Avoid using anonymous literals in function calls.

Prefer named constants which describe their meaning. This makes intent more obvious to a casual reader as it avoids the need to look up the function declaration to understand it.

Avoid defining non-trivial static variables in headers.

Non-trivial static variables cause an instance to be compiled into in every translation unit that includes that header:

Avoid making extensive changes which do not change the code's behavior (for example: changing whitespace or mass renaming of private variables) as these cause unnecessary noise in source history and are disruptive when merging.

If such a change is important, for example fixing broken indentation caused by an automated merge tool, it should be submitted on its own and not mixed with behavioral changes.

Prefer to fix whitespace or other minor coding standard violations only when other edits are being made to the same lines or nearby code.

Boolean function parameters should be avoided.

In particular, boolean parameters should be avoided for flags passed to functions. These have the same anonymous literal problem as mentioned previously, but they also tend to multiply over time as APIs get extended with more behavior. Instead, prefer an enum (see the advice on use of enums as flags in the Strongly-Typed Enums section):

This form prevents the accidental transposing of flags, avoids accidental conversion from pointer and integer arguments, removes the need to repeat redundant defaults, and is more efficient.

It is acceptable to use bools as arguments when they are the complete state to be passed to a function like a setter, such as void FWidget::SetEnabled(bool bEnabled). Though consider refactoring if this changes.

Avoid overly-long function parameter lists.

If a function takes many parameters then consider passing a dedicated struct instead:

Avoid overloading functions by bool and FString.

This can have unexpected behavior:

Interface classes should always be abstract.

Use the virtual and override keywords when declaring an overriding method.

When declaring a virtual function in a derived class that overrides a virtual function in the parent class, you must use both the virtual and the override keywords. For example:

There is a lot of existing code that doesn't follow this yet, due to the recent addition of the override keyword. The override keyword should be added to that code when convenient.

UObjects should be passed around by pointer, not reference. If null is not expected by a function, this should be documented by the API or handled appropriately. For example:

Platform-specific code should always be abstracted and implemented in platform-specific source files in appropriately named subdirectories, for example:

In general, you should avoid adding any uses of PLATFORM_[PLATFORM]. For example, avoid adding PLATFORM_XBOXONE to code outside of a directory named [PLATFORM]. Instead, extend the hardware abstraction layer to add a static function, for example in FPlatformMisc:

Platforms can then override this function, returning either a platform-specific constant value or even using platform APIs to determine the result. If you force-inline the function it has the same performance characteristics as using a define.

In cases where a define is absolutely necessary, create new #define directives that describe particular properties that can apply to a platform, for example PLATFORM_USE_PTHREADS. Set the default value in Platform.h and override for any platforms which require it in the platform-specific Platform.h file.

For example, in Platform.h we have:

WindowsPlatform.h has:

Cross-platform code can then use the define directly without needing to know the platform.

We centralize the platform-specific details of the engine which allows details to be contained entirely within platform-specific source files. Doing so makes it easier to maintain the engine across multiple platforms, additionally you are able to port code to new platforms without the need to scour the codebase for platform-specific defines.

Keeping platform code in platform-specific folders is also a requirement for NDA platforms such as PlayStation, Xbox and Nintendo Switch.

It is important to ensure the code compiles and runs regardless of whether the [PLATFORM] subdirectory is present. In other words, cross-platform code should never be dependent on platform-specific code.



**Examples:**

Example 1 (yaml):
```yaml
UCLASS()

class EXAMPLEPROJECT_API AExampleActor : public AActor
{
    GENERATED_BODY()
    
public:	
    // Sets default values for this actor's properties
    AExampleActor();

protected:
    
    // Called when the game starts or when spawned
    virtual void BeginPlay() override;
};
```

Example 2 (unknown):
```unknown
// Copyright Epic Games, Inc. All Rights Reserved.
```

Example 3 (jsx):
```jsx
template <typename ObjectType>
      class TAttribute
```

Example 4 (php):
```php
class UActorComponent
```

---

## Control Rig Modules

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/PluginIndex/ControlRigModules

**Contents:**
- Control Rig Modules
- Navigation
- Plugin Dependencies

API > API/PluginIndex

Modules for Control Rig



---

## Creating Custom Modules

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-custom-modules-in-niagara-effects-for-unreal-engine

**Contents:**
- Creating Custom Modules
- Niagara Script Editor Reference
- Versioning Modules in Niagara

This page collects all the pages that will teach you how to create custom modules in Niagara.

Niagara gives you the full flexibility of being able to create your own custom modules. You can use the Niagara Script Editor to define your own logic flow, save your modules, and then apply them in a Niagara stack.

To understand how to use the Script Editor, refer to the Niagara Script Editor Reference page.

When you are iterating on creating new versions of modules, it's a good idea to work with versioning enabled so that you don't end up breaking any scenes that are using an outdated version of your modules. This page can teach you more.

We will continue to add more documentation about creating custom modules in Niagara soon. In the meantime, check out the Content Samples as a good place to pick apart existing modules and understand the logic of how they are built.



---

## Gameplay Architecture

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/programming-with-cpp-in-unreal-engine

**Contents:**
- Gameplay Architecture
- Gameplay Programming Reference Directory

Reference for creating and implementing gameplay classes.

When programming gameplay elements using C++ code, each module can contain many C++ classes.

Each class defines a template for a new Actor or Object. Within the class header file, the class and any class functions and properties are declared. Classes can also contain structs, data structures that help with organization and manipulation of related properties. Structures can also be defined on their own. Interfaces allow additional gameplay behavior to be implemented by different classes.

When programming with Unreal Engine, it is possible to have standard C++ classes, functions, and variables. These can be defined using standard C++ syntax. However, UCLASS(), UFUNCTION(), and UPROPERTY() macros can be used to make Unreal Engine aware of the new classes, functions, and variables. For instance, a variable with a declaration prefaced by a UPROPERTY() macro can be garbage collected by the engine, and can be displayed and edited within Unreal Editor. There are also UINTERFACE() and USTRUCT() macros, and keywords for each macro that can be used to specify the behavior of the class, function, property, interface, or struct within Unreal Engine and Unreal Editor.

In addition to the above macros, there is a UPARAM() macro that is primarily used when exposing C++ code to Blueprints. To see examples of UPARAM() being used, see the Exposing Gameplay Elements to Blueprints documentation.

%programming-and-scripting/programming-language-implementation/unreal-engine-reflection-system/Functions:topic% %programming-and-scripting/programming-language-implementation/unreal-engine-reflection-system/Structs:topic% %programming-and-scripting/programming-language-implementation/unreal-engine-reflection-system/Interfaces:topic%



---

## Mover Integrations

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API/PluginIndex/MoverIntegrations

**Contents:**
- Mover Integrations
- Navigation
- Modules
- Plugin Dependencies

API > API/PluginIndex

Mover Integrations is a Unreal Engine plugin acting as an umbrella to cover a variety of modules supporting Mover's integration with other plugins, such as animation, AI, and other gameplay systems.



---

## Scratch Pad Modules in Niagara

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/niagara-scratch-pad-modules-in-unreal-engine

**Contents:**
- Scratch Pad Modules in Niagara
- Scope
  - Emitter-Based Scratch Pad Module
  - System-Based Scratch Pad Module
  - Niagara Module Script
- Getting Started
  - Create a Niagara System
  - Spawn Particles
    - Fix Dependency Issue
  - Emitter Settings

Learn about using Scratch Pad Modules, Niagara's visual-scripted local modules.

This tutorial is an introduction to scratch pad modules in Unreal Engine. It builds upon a single Niagara system to explore the fundamentals of this feature. The tutorial is less about the final result, and more about learning different ways to use the feature.

Scratch pad modules are local Niagara modules that can be authored using visual scripting graphs. There are two asset types that support the creation of Scratch Pad Modules: Niagara emitters and Niagara systems. The modules are limited in scope to the system or emitter they are created within, and don't appear as standalone assets in the Content Browser.

If a scratch pad module is made inside a Niagara emitter asset, it will apply to all uses of that emitter in whatever Niagara systems it’s been added to. In the NE_Example emitter asset below, the ScratchModuleInEmitter module appears in the modules list, and its stack entry is editable within the emitter.

However, a scratch pad module made in an emitter cannot be used by any other system or emitter assets, and will not appear in a Niagara system's modules list. The example below shows the NE_Example emitter asset used within the NS_Example Niagara system. Just like other modules, the scratch pad module is locked (can be disabled but not deleted) when the emitter is instanced in a Niagara system.

If the Scratch Pad Module is made inside a Niagara System asset, it can be used on any Emitters inside that system. As is the case for all Scratch Pad Modules, they are unavailable to Emitters in other Niagara Systems.

A scratch pad module can be exported as a Niagara module script asset. This export process is covered more in-depth in the Share Scratch Modules section of this tutorial. Niagara module scripts are entirely separate assets that appear in the Content Browser, and can be used by any Niagara emitter and in any Niagara system within your project. This is comparable to how material nodes can be converted into material functions, which then can be used by separate material assets throughout a project.

To create a Scratch Pad Module, you'll need to work within a Niagara System asset or Niagara Emitter asset. This tutorial uses a simple grid-spawned Niagara System as the basis for working with Scratch Pad Modules.

This section explains how to create a Niagara system for new users and those who want to follow this tutorial from beginning to end. If you already have created a Niagara system, you can use that to follow the rest of the tutorial.

To create a new Niagara system, follow these steps:

In the Content Browser, right-click, then click Niagara System.

In the Template menu, select Minimal, and then click Create.

Name the new Niagara system (for example, NS_Minimal). Open the asset by double-clicking or pressing Enter.

By default, the system will have a system node (blue) and a single Minimal emitter (orange).

To make the emitter spawn particles, follow these steps:

Navigate to the Minimal emitter.

In the Emitter Update section, click Add (+).

Search for and click Spawn Particles in Grid option.

You can add often-used modules to the top of the Add New Module menu. Hover over the module's name and click on the star (⭐) icon. The icon will change from an outline to a filled-in star. Close and reopen the menu to see your module listed in the Suggested section. To remove it, click the star icon again.

The new module will have a red dot next to its name, indicating an error. In this case, the Spawn Particles in Grid module also needs a Grid Location module to work correctly.

To fix this issue, click on the module. Review the issue in the Details panel, and then click Fix Issue.

A Grid Location module will be added to the Particle Spawn section of the emitter. After that happens, the dependency will be met, and the error icon in the Spawn Particles in Grid module will be removed.

To configure the emitter for this tutorial, follow these steps:

On the Minimal emitter, select Spawn Particles in Grid.

In the Details panel, do the following:

On the Minimal emitter, select Initialize Particle.

In the Details panel, set the following:

Set Lifetime Mode to Direct Set.

Set Color Mode to Direct Set.

Set Color to 1, 0, 0.

Set Position Mode to Simulation Position.

Set Position Offset to 0, 0, 0.

Set Mass Mode to Unset / (Mass of 1).

Set Sprite Size Mode to Uniform.

Set Uniform Sprite Size to 10.

Set Sprite Rotation Mode to Unset.

Set Sprite UV Mode to Unset.

Set all other mesh and ribbon attributes to Unset.

In this example, the Grid Location module is left with its default values.

On the Minimal emitter, click Add (+) next to the Particle Spawn header. Search for and select the New Scratch Pad Module option.

The scratch module graph opens automatically as a tab next to the original System Overview tab. A Local Modules tab appears below the Preview window, next to the Parameters and User Parameters tabs.

Rename your scratch module to something descriptive (for example, ApplyOffset).

While module names will appear as one word (ApplyOffset) in the Modules list, they are displayed with spaces based on letter capitalization (Apply Offset) in search menus and for stack entries.

In the System Overview graph, the Apply Offset module is now listed as a module in the Minimal Emitter. The new scratch module will also appear in the search menus and be labeled as a scratch pad (rather than Niagara) item.

To open the scratch pad module's graph, you can do any of the following:

Click the scratch module's tab, located next to the System Overview tab.

Select the scratch module in the emitter, then click the scratch pad button in the Details panel.

Double-click the scratch module stack entry in the emitter.

Double-click the scratch module in the Local Modules > Modules list.

Like other graphs in Unreal Engine, the data in a module flows from left to right. The data starts at the red Input Map node, flows through the white Niagara Parameter Map line, and ends at the green Output Module node.

You can use Map Get nodes to extract data from this Niagara Parameter Map line, and use Map Set nodes to set data into it.

Next, add some functionality to the scratch pad module, starting with a location offset.

On the Map Get node, click the Add + pin, then search for and click the PARTICLES Position parameter. This is data that is held on each individual particle.

These parameters are written as one word, with a period between the namespace and the name ( NAMESPACE.Name). If you are accessing parameters (especially user parameters) using code or Blueprints, use the version with the period, not spaces.

On the Map Get node, click the Add (+) pin, then search for and click the Vector (INPUT.Vector) option.

The text inside the colored blocks in parameter names specifies which namespace the data is coming from.

The Position comes from the PARTICLES namespace, meaning the data is held on the particles. This data is persistent from frame to frame throughout the particle's lifetime.

The INPUT namespace, used for the Vector, indicates that its data comes from the module, which a user can modify directly.

Drag from the PARTICLES.Position pin, then search for and click the Add node.

By default, the inputs of the Add node will be dark blue, showing that it is a type of wildcard called the Niagara Numeric. It accepts positions, vectors, floats, and integers. When connected to other nodes with specific types, the pin and connection wire change to reflect the data type used in those pins.

Drag from the INPUT.Vector pin to the second pin of the Add node. It will turn yellow to show that it is a vector type.

After adding the offset amount (INPUT.Vector) to the PARTICLES.Position, the particle data needs to be updated using a Map Set node.

In the existing Map Set node, click the Add (+) pin, then search for and click PARTICLES.Position.

Connect the output of the Add node to the Map Set node's PARTICLES Position pin. This will update (overwrite) the PARTICLES.Position value (accessed in the Map Get node) with the new value.

Click either the Apply or Apply & Save button to commit the changes in the graph to the scratch module and its stack entries in the Niagara system.

In the System Overview graph, select the Apply Offset scratch module stack entry on the Minimal emitter. The Vector input created in the prior steps is now a valid module input.

To test the module's functionality, enter a value into the Vector input and note how it changes the system's visual output in the Niagara system viewport. In this example, changing the Z value from 0 to 200 moves the red particles up 200 units (centimeters).

You can set up modules to be visible and usable only in specific emitter contexts.

In the Apply Offset module graph, click anywhere in the background of the graph. This brings up the module settings in the Details panel. The first setting in the list is the Module Usage Bitmask, which defines where the module can be created and moved to. Click the dropdown menu to check, search, and set the various context options.

The following contexts are available:

Module (enabled by default)

Particle Spawn Script (enabled by default)

Particle Update Script (enabled by default)

Particle Event Script (enabled by default)

Particle Simulation Stage Script (enabled by default)

Emitter Update Script

You can limit where and how the module can be used by checking or unchecking the items in the dropdown menu.

To try this out, disable the Particle Update Script option, then press the Apply button.

Go to the System Overview graph view, and try to drag the Apply Offset module stack entry into the Particle Update section. The bright blue drop line will not appear between the entries of the emitter, and a warning tooltip will appear that says: "This module can't be moved to this section of the stack because it's not valid for this usage context."

Additionally, this context limitation applies to the search results of that restricted section. In this case, the Apply Offset module doesn't appear in the Particle Update section's search.

The Apply Offset module is still available in the Particle Spawn search results.

Enable the Particle Update Script context to continue following this tutorial.

Modules located in the Particle Spawn section of the emitter only execute when the particle is created (spawned).

Modules located in the Particle Update section of the emitter execute every tick.

To demonstrate, drag the Apply Offset stack entry from Particle Spawn to a spot under the Particle Update section. Change the Vector input Z value to 1. In the viewport, the red dots will move upward, as the 1cm offset is applied to the particles every tick.

When you're done, drag it back into the Particle Spawn section to continue following the tutorial.

There are a few ways to let the user (in this case, a VFX artist) rotate the offset around an axis. In this section, you will add rotation inside the module. Later in the tutorial you will learn how to leverage dynamic inputs for user-entered data.

Right-click on the graph background, search for "rotation", and then click XYZRotationToQuaternion.

The next step is creating inputs that the user can access and enter values into. The easiest way is to drag a line from the desired pin (in this example, X, Y, and Z) onto the Add (+) icon in the Map Get node. This creates a corresponding INPUT parameter of the same name and correct type. Do this for all three float values (green pins, XYZ) in the Rotation to Quaternion node.

Drag from the Map Get's INPUT.Vector pin, then search for and click the Multiply Vector With Quaternion node. Drag the output pin of the XYZRotation to Quaternion node to the Quaternion input pin in the Multiply Vector with Quaternion node.

Connect the output pin of the Multiply Vector with Quaternion node to the second pin of the Add node, replacing the plain INPUT.Vector value with the new multiplied Vector and Quaternion value.

Click Apply & Save, then open the System Overview graph.

Select the Apply Offset stack entry (located in the Particle Update section of the emitter), and set the Y value to 30. This causes the red particles to move upward and to the right.

There are two tabs under the viewport in a Niagara system with different data and interaction options.

The Parameters tab lists all the parameters included within a Niagara system. This includes:

System Attributes (such as SYSTEM.Age, SYSTEM.LoopCount)

Emitter Attributes (such as EMITTER.Age, EMITTER.DistanceTraveled)

Particle Attributes (such as PARTICLES.Position, PARTICLES.SpriteSize)

Module Outputs (such as OUTPUT.GRIDLOCATION.GridSpacing, OUTPUT.PARTICLESTATE.FirstFrame)

Engine Provided (such as ENGINE.DeltaTime, ENGINE.EMITTER.NumParticles, ENGINE.OWNER.Velocity)

Stage Transients (such as TRANSIENT.FirstFrame, TRANSIENT.ScalabilityExecutionState)

There are also headings in this tab that will be empty by default:

User Exposed (same as in the User Parameters tab)

Stack Context Sensitive

Niagara Parameter Collection

The User Parameters tab lists all the user parameters created in a Niagara system. It is empty by default. The user parameters here are the same as in the User Exposed section of the Parameters tab.

When you're viewing the graph for a specific module, like Apply Offset, the Parameters list is filtered down to the inputs that you currently have available to you.

In these tabs, you can rename your inputs (like INPUT.RotationAngleX). As with other parts of Unreal Engine, click twice on the input name or press F2.

When you click Apply & Save, the new names are visible in the module's stack entry.

In the Edit Hierarchy window, you can order the inputs, add tooltips, and manage dependencies.

To access the Edit Hierarchy interface, open the scratch pad module you want to edit (in this case, the Apply Offset module).

In the Parameters tab, click Edit Input Hierarchies.

This opens the Edit Hierarchy window.

From the left column, drag the relevant inputs into the center column, where the blue highlight appears.

Drag the inputs in the center column to reorder them.

As in the Details panel, you can access the item's Default Value and Variable settings.

Default Mode: Options include Binding, Custom, Fail if Previously Not Set, and the default value.

Default Value: Based on type, such as float or vector.

Tooltip (and localization options): Add helpful implementation details, units, caveats, or other notes that are valuable to users.

Display Unit: Options include Centimeters, Lumens, Hours, Gigabytes, Grams, Degrees, and the default Unspecified.

Advanced Display: False by default.

Display in Overview Stack: False by default.

Inline Parameter Sort Priority and Color Override: Disabled by default.

Edit Condition and Visible Condition (Input Name and Target Values): None and 0 elements by default.

Property Metadata: 0 elements by default.

Alternate Aliases for Variable: 0 elements by default.

Widget Type: Default.

Min Value: 0 by default.

Max Value: 1 by default.

Step Width: 1 by default.

Broadcast Value Change On Commit Only: False (set to true if you only want values to be updated when committed, not when typing).

Add text into the Tooltip field of the Rotation Angle X input, then click Apply or Apply & Save.

Then, go to the System Overview graph, select the Apply Offset module, and hover over the Rotate Angle X option in the Details panel. Your tooltip will be the first line in the popup, followed by the Name and Type information of the input you're hovering over.

In the Edit Hierarchy window (or the Details panel), change the Display Unit of the value. Select the Rotation Angle X input, and change the Display Unit from Unspecified to Degrees.

Then, change the Vector input's Display Unit to Centimeters.

When making complex modules, you can leverage local parameters to help keep your module graph organized and easy to read. Separating the graph by operations is a common and generally recommended approach.

Local parameters only exist in the module, and are not persistent from frame to frame. They are often used for temporary value storage within a graph.

Right-click the PARTICLES.Position pin from the Map Get and click Remove. Disconnect the node (Alt + click).

Near the Multiply Vector with Quaternion node, add a Map Set node (listed as Parameter Map Set in the right-click menu). Connect it to the Niagara Parameter Map line, between the Input node and the Map Set node.

Drag the Multiply Vector with Quaternion output pin to the Add (+) icon on Map Set. This creates a local parameter of the same name and type as the pin you pulled from. In this case, it creates LOCAL.Vector. Rename this to something more descriptive (for example, LOCAL.Offset).

On the right side of the Map Set node, drag from the white Dest pin, then search for and click the Map Get option.

Click Add (+), then search for and select the LOCAL.Offset created in the previous step.

Now you can use that cached Offset value in another organized section of the graph.

When rearranging or adding nodes in any Unreal Engine graph, you might need to disconnect the wires connecting specific nodes. Use Alt + Left Click on a pin or wire to disconnect it.

To grab and move a pin connection instead, hold Ctrl + Left Click to pick up the wire. Release over a valid pin. The connection will be deleted if you release over empty graph space.

To remove, rename, reorder, or perform other actions on a pin, right-click to bring up a menu and click the desired action.

There are three different types of Transformation Spaces:

Simulation: Calculations are done in whatever context (local or world) that is set in the emitter's Properties section, where Local Space is set to either true or false.

World: Calculations are done in the context of the world values.

Local: Calculations are done in the context of the system itself, regardless of where it is in the world.

For this example, let’s give the user an option to choose which Transformation Space to use in this module.

Create a Transform Vector node. Drag the Map Get's Offset pin to the InVector pin of the Transform Vector node.

To let the user set the Source Space as an input, drag the Transform Vector's Source Space pin back to the Map Get node's Add (+) icon. This creates an input of the same name and type.

Add another Map Set node, and connect it between the previous Map Set and the final Map Set. Create a LOCAL.Offset entry on the Map Set node, and drag it to the Transform Vector’s OutVector pin.

From the new Map Set node, create a Map Get node, and click the Add (+) button to access the LOCAL.Offset variable.

Next, click the Add (+) button to access the PARTICLES.Position parameter.

Add the LOCAL.Offset to the PARTICLES.Position using the Add node from before.

If you want to change the order of the elements in a node, right-click on one of the items and click Move pin up.

Connect the Add node to the Map Set node using the PARTICLES.Position pin, and drag the Dest to the final Output Module.

Click Apply or Apply & Save, then open the System Overview graph. Select the Minimal emitter, then select the Apply Offset stack entry on it. In the Details panel, there's now a Source Space input option.

Comments visually group nodes together, and often include text to describe that portion of the graph or any other notes pertinent to that section. Like with text-based code, leaving comments throughout your work is considered a best practice. Comments make it easier for other developers to understand your decisions.

Open the Scratch Module graph. Select nodes in the graph, and press the C key to create a comment. Rename it to be descriptive (for example, Initial Offset Vector).

With the comment box selected, the Detail panel displays the available settings: Color, Font Size, Show Bubble When Zoomed, Color Bubble, Move Mode, and the Details field.

Commenting provides visual and textual information about what's happening in each section of the graph. Comments on this example graph could include: Initial Offset Vector, Transform Into Space, and Set Position. Each comment box here includes the initial Map Get and the subsequent Map Set node, where the next Map Get starts the next section.

Module outputs can supply extra data to the user without having to fill in particle data. Since emitter stack entries are executed from top to bottom, module output data is available only to stack entries below it. Knowing the outputs and other parameters written to them can be helpful when figuring out how to work with the data in your particle system.

Select any module in the Minimal emitter. In the Details panel, select the gear (⚙️) icon, and enable Show Parameter Writes. The Parameter Writes section is collapsed by default. Click the arrow (🔽) to expand the list and see all the outputs the stack entry writes to.

In the Apply Offset scratch pad module stack entry below, the Parameter Writes section only includes PARTICLES.Position.

Select the Grid Location module stack entry, and expand the Parameter Writes section. It writes to PARTICLES.Position, as well as other OUTPUT parameters.

As an example, let’s use OUTPUT.GRIDLOCATION.GridUVW to change the color of our particles.

To demonstrate this, open the Spawn Particles in Grid stack entry, then change the X, Y, and Z values to 10. You'll see a cube-shaped group of particles, rather than a line of them.

Then, in the Particle Spawn section of the emitter, click the Add (+) button to create a Color module.

Using the drop-down menu next to the Color swatch, search for and click both Make Linear Color from Vector and Float.

Using the dropdown menu next to the new Vector (RGB) field, search for and click OUTPUT.GRIDLOCATION.GridUVW.

Now, the RGB values are determined by the OUTPUT.GRIDLOCATION.GridUVW information.

Open the Apply Offset scratch pad module graph. In the Set Position comment section (the last Map Get and Map Set), drag the Map Get's LOCAL.Offset pin to the Add (+) pin of the Map Set node.

Double-click a connection wire to create a reroute node, then move it as needed to reduce overlap and increase visibility in the graph. You can also manually create reroute nodes through the graph's right-click menu.

Right-click the new LOCAL.Offset pin in the Map Set node. Click Change Namespace > OUTPUT.

This changes the LOCAL namespace to OUTPUT. It also adds a namespace modifier (for example, MODULE) and appends the module name (Apply Offset). The result is OUTPUT.MODULE.Offset in the Map Set node.

Click Apply, then open the System Overview graph. Select the Minimal emitter's Apply Offset stack entry, and expand the Parameter Writes section in the Details panel. The OUTPUT.APPLYOFFSET.Offset parameter will be in the list and available for use by any module stack entries below it.

For example, let's query the offset. Click the Add (+) button to create a Set Parameters stack entry underneath the Apply Offset stack entry. This module appears as Set new or existing parameter directly in the search menu.

In the Details panel, click the Add (+) button to create a Vector (PARTICLES.Vector) item in the list.

In the new entry, click the arrow to open the type menu, then search for and click OUTPUT.APPLYOFFSET.Offset.

When writing a module script, there are a few options for where the functionality can be set up. Many dynamic inputs are available, which can give the user more options and power when implemented.

For example, you can rework the Quaternion in the Apply Offset module. Open the Apply Offset graph, and navigate to the first Map Get in the graph (the one with the separate X, Y, and Z Map Get inputs connected to the Quaternion node).

Handling the Quaternion in this way has some limitations. The rotation angle is exposed separately as X, Y, and Z, and it assumes the angle type is in degrees. These are the only options provided to the user.

It could be more powerful for the user to expose the quaternion as an input, and then let the pre-existing dynamic inputs do the work for us. In this case, you can use the quaternion directly, instead of the rotation angles in the first Map Get.

Right-click and remove each of the X, Y, and Z pins from the first Map Get node. Also, delete the XYZRotation to Quaternion node.

In Map Get, click the Add (+) pin to search for and click INPUT.Quaternion (Quat). Rename it to something descriptive (for example, INPUT.RotationQuaternion). Drag that pin to the Quaternion pin of the Multiply Vector With Quaternion node.

Click Apply, then open the System Overview graph. The Rotation Quaternion is now available in the Apply Offset module's Details panel, and the separate X, Y, and Z options have been removed.

In the emitter’s Apply Offset stack entry, open the drop-down for the Rotation Quaternion item, then search for and click Make Quaternion.

A user can now choose any of the options predefined by the dynamic input. They can change the Angle Type, select XYZ Rotations as the Quaternion From, and specify a different Coordinate Space. These are all built-in options that Niagara provides.

When figuring out how to author and present the modules, consider what's easiest for you to manage and what's most powerful and usable for the user. Try to find a balance between what’s flexible for your end user without being too open-ended.

In this case, the drawback is that a "Rotation Quaternion” might be a bit esoteric or unclear for the user.

To address such potential roadblocks, add tooltips to your inputs. Select the input from the Parameters list, and enter a tooltip in the Details panel Tooltip field. For this input, you can enter something like, "Use the Make Quaternion Dynamic Input." This gives the user a clear next step.

Click Apply. Open the System Overview graph, select the Apply Offset module, and hover over the Rotation Quaternion item in the Details Panel. The custom text will appear as the first line in the tooltip.

Every module, including scratch pad modules, has a Note field available. These Module Usage Notes appear at the top of the Details panel when a module's stack entry is selected in an emitter. You can put information here about how the module works, including any quirks about its usage, and dependency notes.

To find and edit this option, click the graph background to deselect any nodes. This populates the Details panel with information about the module as a whole, rather than a specific part of it. Enter information about the module to the Note Message field.

For the Apply Offset scratch module, a helpful tooltip could be: "This module applies an offset to the particle position. Use the Make Quaternion Dynamic Input as a utility to provide the Quaternion."

Click Apply, then open the System Overview graph. Select the Apply Offset scratch module stack entry, and the Module Usage Note will be at the top of the Details panel.

Notes (and other issues or warnings) at the top of the Details panel can be hidden by clicking Dismiss.

Notes can be made visible again by clicking the gear (⚙️) icon at the top of the module, and clicking Undismiss All Stack Issues.

When dismissed on one stack entry, the Notes section will appear on newly added stack entries of the same module type.

All the parameters and inputs are listed in the Parameters tab.

The list might include parameters and inputs that are no longer in use in your module.

The easiest way to identify what parameters and inputs need to be cleaned up is to check the field on the right of each input. This shows the references for the reads and writes for each input. In this case, all three of the INPUT.RotationAngle parameters (X, Y, and Z) are not in use, because those entries are all listed as having 0 reads and 0 writes (0|0).

Even when its usages are deleted in a module graph, parameters will remain in the Parameters list. You’ll need to manually delete them when you no longer need them.

To remove unused parameters like these, select them in the Parameters list and press the Delete key, or right-click on the parameter and click Delete.

These special data types take information from the general editor and pass it into Niagara, so you can use it to direct your particles or influence your simulation.

To access data interfaces, open your scratch module graph. On a Map Get node, click the Add (+) pin to open the Make New drop-down. Click Data Interface to show a list of options.

Most of these data interfaces have modules already written for them in the engine. Sometimes, you might want to add that functionality directly into your scratch module instead.

For this example, create space between the Transform Into Space and Set Position sections on the graph.

Add a Map Set node before the Set Position section, and reroute the pins. Connect the Map Set from Transform Into Space into the new Map Set node, and drag the Dest pin on the Map Set into the Map Get in Set Position and subsequent Map Set.

Create a Map Get node, and add an INPUT.CameraQuery input.

Drag the INPUT.CameraQuery pin to an empty space on the graph to open the Source Filtering menu. The first entry is specific to the data interface selected, and when expanded, lists all the methods that are available on that data interface.

For this example, click Get Camera Properties CPU/GPU. This provides the Camera Position, Forward Vector, Up Vector, and Right Vector (all in World context). You can use this data to apply an offset towards or away from the camera.

Add an INPUT.Float to the Map Get, and name it something descriptive (for example, CameraOffsetScale).

Use a Multiply node to multiply the Forward Vector World by the new INPUT.CameraOffsetScale float.

Add the LOCAL.Offset to the Map Get node. Add it to the Multiply node's result.

In the Map Set node n this new section, add LOCAL.Offset. Then, connect the result of the Add node to that LOCAL.Offset pin.

Click Apply, then open the System Overview graph. Select the Apply Offset scratch module stack entry. The Details panel now has a Camera Query section with additional options for the user, including the Camera Offset Scale float input.

Change the Camera Offset scale to -200, to see the offset in action.

As a module author, you can hide fields you don't expect or want the user to change.

In this example, you can expect that the user won’t need to edit the Player Controller Index or Require Current Frame Data fields. Therefore, you can hide these options.

Open the Apply Offset scratch pad module graph. In the Details panel (or the Edit Hierarchy view), enable the Advanced Display option. This determines whether this input should be visible if the user has expanded the Advanced section.

In the System Overview graph, select the Apply Offset stack entry. In the Details panel, the extra data interface information is now hidden inside the Advanced options section. The information can be viewed by opening up the Advanced section of the panel. Click the arrow button to expand this section, and click again to collapse it.

This setup allows more advanced users to change these settings, like if they're working with a split-screen game and want to manually set the camera, while removing clutter for most users that won't need to change those settings.

You can use the Edit Hierarchy interface to make the Camera Offset Scale input available in the Details panel even when your Camera Query is set to be in the Advanced section.

In the scratch pad module graph, open the Parameters tab, then open the Edit Hierarchies panel. Drag INPUT.CameraOffsetScale from the left column into the center column to rearrange the order.

Click Apply. In the System Overview graph, select the Apply Offset module stack entry. In the Details panel, the Camera Offset Scale input will be included in the main list of inputs, even with the Advanced panel collapsed.

User parameters let you change Niagara settings without repeatedly opening and editing the Niagara System or module graph. When a Niagara system is added to a level, the user parameters are available in the asset’s Details Panel. This can speed up workflows since users can adjust those parameters directly within the scene’s context.

There is a cost associated with user parameters. Every time a user parameter is adjusted, the parameters get pushed to the corresponding execution context, and all parameters within that same context are updated:

System & Emitter Spawn

System & Emitter Update

Particles Spawn & Particle Updates (per Emitter)

Using a data interface as a user parameter is generally discouraged due to performance concerns. The engine makes a copy of the data interface per instance, and because they are UObjects, they get garbage collected. The main cost of a data interface is when you create an instance. After it’s created, it has the same overhead as if it were elsewhere in the stack.

Module inputs can be promoted to user parameters. To promote a module input, follow these steps:

In the System Overview graph's Minimal emitter, select the Apply Offset stack entry.

Click the Dynamic Input dropdown next to the Camera Offset Scale input.

Search for and click Read from new User parameter.

A new user parameter is created with the same name and value as the Details panel field. The display name for this parameter is USER Camera Offset Scale. If you want to access this or other user parameters in code or Blueprints, it must be formatted as USER.CameraOffsetScale or User.CameraOffsetScale.

The Parameters tab shows user parameters, but they are not editable in that interface. The User Parameters tab provides a field for editing values. For this tutorial, change the USER Camera Offset Scale back to 0.

Open a level, and drag the Niagara system (in this example, NS_Minimal) into the scene. Select the Niagara system in the Outliner. In the Details panel, expand the User Parameters section. The Camera Offset Scale user parameter is included in the list. This means a user can set these parameters interactively, in the context of the world, rather than while in the Niagara viewport.

Static switches control the flow of the script. They are helpful when you want certain parts of your graph compiled out of your module except under certain circumstances.

For this example, make a switch for the USER.CameraOffsetScale parameter. It might be something that an end user would rarely use, so the code wouldn’t need to be available in the emitter most of the time.

Open the Apply Offset scratch module graph, and go to the section that has the USER.CameraOffsetScale.

In this section, right-click and create a Static Switch node.

Rename the Static Switch to something descriptive (for example, Use Camera Offset).

The Static Switch expects a type (often numeric, but not always). Add a type by clicking the Add (+) pin, then search for and select the Niagara Parameter Map type for this example.

Drag the Camera Offset Map Set output to the Static Switch node, then drag the Static Switch output to both the Map Get and Map Set in the Set Position section.

Use Ctrl + Click to pick up connection wires and move them to a different pin.

Then, connect the Map Set of the Transform Into Space section to the False pin of the Static Switch node.

If the Static Switch is false, it will skip (compile out) the Camera Offset section, and go right from the Transform Into Space section to the switch and the following Set Position section. If it's true, the Camera Offset nodes will be used.

By default, the Static Switch type is a Boolean. Other options are available, but use the default Boolean for this example. The Default Value can be set to true or false, but leave it false for this example. The Expose as pin can also be left false for this tutorial. Setting it to true will expose a pin for the setting on the node in the graph, creating a way to set that value using data in the graph.

Open the System Overview graph, and select the Apply Offset scratch module stack entry. The Details panel will now have a Use Camera Offset option. While set to false, no other camera offset options will appear in the list, and the skipped nodes will not affect the Emitter. The Camera Data Interface information has also been removed from the Advanced options section.

While set to true, the Camera Offset nodes are compiled, and all the relevant options (both outside and inside the Advanced section) are available in the Details panel.

To share your scratch module with other Niagara systems or with the rest of your team, you need to export your scratch module as a Niagara nodule script asset.

Open the Apply Offset graph, and click the Local Modules tab. Right-click the listed module's name, then click Create Asset.

This opens the Create Script As window. Name your module (for example, NMS_ApplyOffset), and select the folder where you would like this asset to be located. Then, click Save.

The asset is created, and can be accessed from the Content Browser.

The engine then automatically opens the new Niagara module script asset.

The first thing you'll likely want to change in the Niagara module script asset is the Library Visibility flag in the Script Details panel.

By default, it's set to Unexposed, which means it does not appear in menus and searches with the Library Only option enabled (which is the case by default).

To demonstrate this, open your Niagara System, and use the Add + button to search for ApplyOffset. The only result will be the Scratch Pad, not the NMS asset we just created (which would be listed as Game).

There are two different ways to handle this, depending on how discoverable you want that Niagara module script asset to be.

One option is to leave the module set to Unexposed, and turn the Library Only filter option to false on your workstation. This might be preferred if you don't want or need the module to be easily accessible by users with default filter settings. If anyone else wanted to use this module, they would need to know to uncheck the Library Only option in their Add New Module window as well.

The other option is to change the Niagara module script asset's Library Visibility to Exposed. This would make the module much more discoverable, as it would appear in the Add New Module menu with the default filtering options in place (Library Only set to true). This is ideal for modules that you want to be readily accessible to your team or other end users.

Open the Niagara module script asset, change the Library Visibility to Exposed, then click Compile and Save.

To see this in action, open any Niagara system, and click the Add (+) button to search for Apply Offset. Unlike before, the Niagara module script asset (labeled Game) is included in the search results while the Library Only option is set to true.

Check the new Niagara module script asset's Module Usage Bitmask to ensure the visibility settings are appropriate for this module's intended functionality.

Text in the Niagara module script's Description field is included in the tooltip that appears when hovering over the module in the Add New Module menu. Include any information here that would help a user decide whether or not to use this module. For example, explain what it's meant to do, what circumstances are more or less ideal for this module to be used, and what other factors might make this more or less relevant to your user’s creative or technical goals.

If a Niagara script module is created from a scratch module, the Note field is automatically filled with whatever text was included in the scratch module. If your scratch module didn't include any Note text, this will be blank. This message appears at the top of the Details panel when the module's stack entry is selected within an emitter.

Keywords help make the Niagara module script more discoverable during menu searches. Keywords should be separated by spaces. The Keywords field for the Apply Offset Niagara module script could include "offset position camera", which would allow an end user to search for "camera offset" and have Apply Offset pop up as an option in the menu.

You can use scratch pad modules to directly add new functionality to your emitters and Niagara systems using visual scripting.

For more information about using Niagara, see Creating Visual Effects and Niagara Script Editor Reference.



---

## Unreal Engine C++ API Reference

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API

**Contents:**
- Unreal Engine C++ API Reference
- Modules
  - Developer
  - Editor
  - Runtime
- Plugins
  - Modules

Unreal Engine API Reference

Welcome to the Unreal Engine C++ API Reference! This is an automatically generated reference manual from the Unreal Engine Source code. For tutorials, walkthroughs and detailed guides to programming with Unreal, check out the online documentation for Programming in Unreal Engine.

Unreal Engine's systems and features are packaged in two ways:

Explore all of Unreal Engine's modules, plugins, and their members here, organized hierarchically. You can use the search bar to find a known term, such as a class or function name.

You can also browse the modules and plugins below:

The Developer category provides code that is compiled for every type of build target, but only in non-shipping build configurations. These include development and debug tools, and these modules are not included in Shipping builds.

The Editor category provides access to in-Editor code. These modules are compiled for all build configurations, but for Editor build targets. These include tools used by the Editor and the Unreal Editor itself.

The Runtime category contains functionality necessary to run Unreal Engine. These modules are compiled for every type of build configuration and build target.

A comprehensive list of Unreal Engine's built-in plugins.

The Plugins category contains built-in plugin modules that are available for all Unreal Engine projects. These modules are not immediately compiled and may be any of the Developer, Editor, or Runtime types.



---

## Unreal Engine C++ API Reference

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API?application_version=5.7

**Contents:**
- Unreal Engine C++ API Reference
- Modules
  - Developer
  - Editor
  - Runtime
- Plugins
  - Modules

Unreal Engine API Reference

Welcome to the Unreal Engine C++ API Reference! This is an automatically generated reference manual from the Unreal Engine Source code. For tutorials, walkthroughs and detailed guides to programming with Unreal, check out the online documentation for Programming in Unreal Engine.

Unreal Engine's systems and features are packaged in two ways:

Explore all of Unreal Engine's modules, plugins, and their members here, organized hierarchically. You can use the search bar to find a known term, such as a class or function name.

You can also browse the modules and plugins below:

The Developer category provides code that is compiled for every type of build target, but only in non-shipping build configurations. These include development and debug tools, and these modules are not included in Shipping builds.

The Editor category provides access to in-Editor code. These modules are compiled for all build configurations, but for Editor build targets. These include tools used by the Editor and the Unreal Editor itself.

The Runtime category contains functionality necessary to run Unreal Engine. These modules are compiled for every type of build configuration and build target.

A comprehensive list of Unreal Engine's built-in plugins.

The Plugins category contains built-in plugin modules that are available for all Unreal Engine projects. These modules are not immediately compiled and may be any of the Developer, Editor, or Runtime types.



---

## Unreal Engine C++ API Reference

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/API?application_version=5.6

**Contents:**
- Unreal Engine C++ API Reference
- Modules
  - Developer
  - Editor
  - Runtime
- Plugins
  - Modules

Unreal Engine API Reference

Welcome to the Unreal Engine C++ API Reference! This is an automatically generated reference manual from the Unreal Engine Source code. For tutorials, walkthroughs and detailed guides to programming with Unreal, check out the online documentation for Programming in Unreal Engine.

Unreal Engine's systems and features are packaged in two ways:

Explore all of Unreal Engine's modules, plugins, and their members here, organized hierarchically. You can use the search bar to find a known term, such as a class or function name.

You can also browse the modules and plugins below:

The Developer category provides code that is compiled for every type of build target, but only in non-shipping build configurations. These include development and debug tools, and these modules are not included in Shipping builds.

The Editor category provides access to in-Editor code. These modules are compiled for all build configurations, but for Editor build targets. These include tools used by the Editor and the Unreal Editor itself.

The Runtime category contains functionality necessary to run Unreal Engine. These modules are compiled for every type of build configuration and build target.

A comprehensive list of Unreal Engine's built-in plugins.

The Plugins category contains built-in plugin modules that are available for all Unreal Engine projects. These modules are not immediately compiled and may be any of the Developer, Editor, or Runtime types.



---

## Unreal Engine Modules

**URL:** https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-modules

**Contents:**
- Unreal Engine Modules
- Benefits of Using Modules
- Setting Up a Module
- Understanding the Structure of a Module
  - Configuring Dependencies in the Build.cs File
  - Private and Public Dependencies
  - Using the Private and Public Folders
  - Implementing the Module in C++
- Using Modules in Your Projects
- Controlling How Modules Load

Modules are the building blocks of Unreal Engine's software architecture. You can organize your code into modules to create more efficient and maintainable projects.

Modules are the basic building block of Unreal Engine's (UE) software architecture. These encapsulate specific editor tools, runtime features, libraries, or other functionality in standalone units of code.

All projects and plugins have their own primary module by default, however, you can define other modules outside of these to organize your code.

This page provides an overview of how modules are structured and how they can benefit your Unreal Engine projects.

Unreal Engine modules are not related to C++ 20 modules.

Organizing your project with modules provides the following benefits:

Modules enforce good code separation, providing a means to encapsulate functionality and hide internal parts of the code.

Modules are compiled as separate compilation units. This means only modules that have changed will need to compile, and build times for larger projects will be significantly faster.

Modules are linked together in a dependency graph and limit header includes to code that is actually used, per the Include What You Use (IWYU) standard. This means modules that are not used in your project will be safely excluded from compilation.

You can control when specific modules are loaded and unloaded at runtime. This provides a way to optimize the performance of your project by managing which systems are available and active.

Modules can be included or excluded from your project based on certain conditions, such as which platform the project is being compiled for.

In summary, if you observe best practices with modules, your project's code will be better organized, will compile more efficiently, and will be more reusable than if you put all of your project's code into a single module.

The following is an overview of how to build and implement a module from scratch. If you follow these steps, you will create a gameplay module separate from the primary module that your project includes by default.

Create a directory for your module at the top level of your project's Source folder. This directory should have the same name as your module.

You can place modules in any subdirectory within your Source folder, at any number of levels deep. This makes it possible to use subdirectories to group modules.

Create a [ModuleName].Build.cs file inside your module's root directory and use it to define dependencies with other modules. This makes it possible for the Unreal build system to discover your module.

Create Private and Public subfolders inside your module's root directory.

Create a [ModuleName]Module.cpp file in the Private subfolder for your module. Use this to provide methods for starting up and shutting down your module, as well as other common functions that Unreal Engine uses to manage modules.

To control how and when your module loads, add configuration information for your module in your .uproject or .uplugin file. This includes the name, type, compatible platforms, and loading phase of the module.

List your module as a dependency in the Build.cs file for any module that will need to use it. This may include the Build.cs file for your project's primary module.

Generate the solution files for your IDE any time you modify your [ModuleName].Build.cs file or move source files between folders. You can use any of the following methods to do this:

Run GenerateProjectFiles.bat.

Right-click the .uproject file for your project, then click Generate Project Files.

In the Unreal Editor, click File > Refresh Visual Studio Project.

For more details on these components and how to configure them, continue reading this page. For a more detailed walkthrough of setting up a module, refer to Creating a Gameplay Module.

All modules should be placed in the Source directory for either a plugin or project. The module's root folder should have the same name as the corresponding module.

There should also be a [ModuleName].Build.cs file for each module in its root folder, and its C++ code should be contained in Private and Public folders.

The following is an example of the recommended folder structure for a module:

The Unreal build system builds projects according to Target.cs files in your projects and the Build.cs files in your modules, not according to the solution files for your IDE.

The IDE solution is generated automatically when editing code, but the Unreal Build Tool (UBT) will ignore it when compiling projects.

All modules require a [ModuleName].Build.cs file placed in the module's root directory for the Unreal build system to recognize them.

Inside your [ModuleName].Build.cs file, you need to define your module as a class inherited from the ModuleRules class. Below is an example of a simple Build.cs file:

Sample ModuleTest.Build.cs File

When configuring your Build.cs files, you will mainly use the PrivateDependencyModuleNames and PublicDependencyModuleNames lists. Adding module names to these lists will set the modules that are available to your module's code.

For example, if you add the "Slate" and "SlateUI" module names to your private dependencies list, you will be able to include Slate UI classes within your module.

You should use the PublicDependencyModuleNames list if you use the classes from a module publicly, such as in a public .h file. This will make it possible for other modules that depend on your module to include your header files without issues.

You should put a module's name in the PrivateDependencyModuleNames list if they are only used privately, such as in .cpp files. Private dependencies are preferred wherever possible, as they can reduce your project's compile times.

You can make many dependencies private instead of public by using forward declarations in your header files.

If your module is a regular C++ module (meaning the ModuleType is not set to External in your .uproject or .uplugin), its C++ files should be placed in the Private and Public subfolders inside your module's root directory.

These do not have any relation to the Private, Public, or Protected access specifiers in your C++ code. Instead, they control the availability of the module's code to other modules. If you use these folders, all .cpp files should be placed in the Private folder. Header (.h) files should be placed in the Private and Public folders per the guidelines below.

If you place a header file in the Private folder, its contents will not be exposed to any modules outside its owning module. Classes, structs, and enums in this folder will be accessible to other classes inside the same module, but they will not be available to classes in other modules.

If you place a header in the Public folder, the Unreal build system will expose its contents to any other module that has a dependency on the current module. Classes in outside modules will be able to extend classes contained in the Public folder, and you will be able to create variables and references using classes, structs, and enums in the Public folder as well. The Private, Public, and Protected specifiers will take effect as normal for functions and variables.

If you are working on a module that will not be made a dependency for others, you do not need to use the Private and Public folders. Any code outside of these folders will behave as if it were Private. A typical example of this would be your game's primary module, which will likely be at the end of the dependency chain.

You can further organize your code by creating subfolders within the Public and Private folders. For any new folder you create within Public, create a corresponding folder with the same name in Private. Similarly, for any header file you place in Public, make sure its corresponding .cpp files are always in the corresponding folder in Private.

If you create new classes with the New Class Wizard in Unreal Editor, it will automatically ensure parallel construction between these folders.

To expose a module to the rest of your C++ project, you need to create a class extending IModuleInterface, then provide that class to the IMPLEMENT_MODULE macro.

For the simplest implementation, you can create a .cpp file in the module's Private directory, and name it [ModuleName]Module.cpp, where [ModuleName] is the name of your module. Go on to call the IMPLEMENT_MODULE macro after all other #include declarations, and provide FDefaultModuleImpl as the class.

FDefaultModuleImpl is an empty class that extends IModuleInterface. For a more detailed implementation, you can write your own class to implement in this .cpp file.

IModuleInterface features several functions that trigger when your module loads and unloads, similar to the Startup and Shutdown functions in the GameInstance** **class.

Anytime you make a new Unreal Engine project or plugin, it will automatically set up a primary module of its own, which you can find in the project's Source folder. You can include outside modules in your project by adding them to the Build.cs file for your project's primary module.

For example, to use the Gameplay Tasks system in a project titled MyProject, you need to open MyProject.Build.cs, then add the "GameplayTasks"` module as a dependency.

To optimize compilation speeds, Unreal Build Tool only compiles modules found in the dependency chain for your project. This means that if a module isn't included in any Build.cs files that are used by your project, that module will be skipped during compilation.

Your .uproject and .uplugin files contain a Modules list defining which modules are included in your project and how they will load.

When you regenerate your project files, entries for your modules will be added to this list automatically if they are not already present, provided that you have included them in the dependency chain. Entries in this list will look similar to the following:

Most gameplay modules will simply list their Name, while their Type will be set to Runtime. If their LoadingPhase is not defined it will be set to Default. There are a variety of other module types, loading phases, and additional parameters that control which platforms a module will and won't load on.

For information about the available module types, refer to the API documentation for EHostType::Type.

The most common module types are Runtime and Editor, which are used for in-game classes and editor-only classes, respectively.

For more information about loading phases, refer to the API documentation for ELoadingPhase::Type.

While the Default loading phase is suitable for most gameplay modules in your project, plugins sometimes need to load earlier. If you frequently see errors from Unreal Editor trying to find C++ classes in a plugin, try setting them to PreDefault.

The other parameters used by this list include the following:



**Examples:**

Example 1 (csharp):
```csharp
using UnrealBuildTool;

	public class ModuleTest: ModuleRules

	{

	public ModuleTest(ReadOnlyTargetRules Target) : base(Target)

	{

	PrivateDependencyModuleNames.AddRange(new string[] {"Core"});

	}

	}
```

Example 2 (unknown):
```unknown
#include "Modules/ModuleManager.h"

	IMPLEMENT_MODULE(FDefaultModuleImpl, ModuleTest);
```

Example 3 (json):
```json
"Modules": [

		{

			"Name": "ModuleTest",

			"Type": "Runtime",

	"LoadingPhase": "Default",

		},

	{

	"Name": "ModuleTestEditor",

	"Type": "Editor",

	}

	]
```

---
