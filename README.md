# readme.md


The Reuse/Release Equivalence Principle (REP)
The granule of reuse is the granule of release.
What do you expect from the author of a class library that you are planning to reuse? Certainly, you
want good documentation, working code, well-specified interfaces, and so on. But there are other
things you want, too.
First, to make it worth your while to reuse this person's code, you want the author to guarantee to
maintain it for you. After all, if you have to maintain it, you are going to have to invest a tremendous
amount of time into it, time that might be better spent designing a smaller and better component for
yourself.
Second, you are going to want the author to notify you of any changes planned to the interface and
functionality of the code. But notification is not enough. The author must give you the choice to
refuse to use any new versions. After all, the author might introduce a new version just as you are
entering a severe schedule crunch or might make changes to the code that are simply incompatible
with your system.
In either case, should you decide to reject that version, the author must guarantee to support your
use of the old version for a time. Perhaps that time is as short as 3 months or as long as a year; that
is something for the two of you to negotiate. But the author can't simply cut you loose and refuse to
support you. If the author won't agree to support your use of older versions, you may have to
seriously consider whether you want to use that code and be subject to the author's capricious
changes.
This issue is primarily political. It has to do with the clerical and support effort that must be provided
if other people are going to reuse code. But those political and clerical issues have a profound effect
on the packaging structure of software. In order to provide the guarantees that reusers need,
authors organize their software into reusable components and then track those components with
release numbers.
Thus, REP states that the granule of reuse, a component, can be no smaller than the granule of
release. Anything that we reuse must also be released and tracked. It is not realistic for a developer
to simply write a class and then claim that it is reusable. Reusability comes only after a tracking
system is in place and offers the guarantees of notification, safety, and support that the potential
reusers will need.


The Common Reuse Principle (CRP)
The classes in a component are reused together. If you reuse one of the
classes in a component, you reuse them all.
This principle helps us to decide which classes should be placed into a component. CRP states that
classes that tend to be reused together belong in the same component.
Classes are seldom reused in isolation. Generally, reusable classes collaborate with other classes that
are part of the reusable abstraction. CRP states that these classes belong together in the same
component. In such a component, we would expect to see classes that have lots of dependencies on
each other. A simple example might be a container class and its associated iterators. These classes
are reused together because they are tightly coupled. Thus, they ought to be in the same
component.
But CRP tells us more than simply what classes to put together into a component. It also tells us
what classes not to put in the component. When one component uses another, a dependency is
created between the components. It may be that the using component uses only one class within the
used component. However, that doesn't weaken the dependency. The using component still depends
on the used component. Every time the used component is released, the using component must be
revalidated and rereleased. This is true even if the used component is being released because of
changes to a class that the using component doesn't care about.
Moreover, it is common for components to live in DLLs. If the used component is released as a DLL,
the using code depends on the entire DLL. Any modification to that DLL, even if that modification is to
a class that the using code does not care about, will still cause a new version of the DLL to be
released. The new DLL will still have to be redeployed, and the using code will still have to be
revalidated.
Thus, I want to make sure that when I depend on a component, I depend on every class in that
component. To say this another way, I want to make sure that the classes that I put into a
component are inseparable, that it is impossible to depend on some and not the others. Otherwise, I
will be revalidating and redeploying more than is necessary and will be wasting significant effort.
Therefore, CRP tells us more about what classes shouldn't be together than what classes should be
together. CRP says that classes that are not tightly bound to each other with class relationships
should not be in the same component.


The Common Closure Principle (CCP)
The classes in a component should be closed together against the same kinds
of changes. A change that affects a component affects all the classes in that
component and no other components.
This is the Single-Responsibility Principle (SRP) restated for components. Just as SRP says that a
class should not contain multiple reasons to change, CCP says that a component should not have
multiple reasons to change.
In most applications, maintainability is more important that reusability. If the code in an application
must change, you would prefer the changes to occur all in one component rather than being
distributed through many components. If changes are focused into a single component, we need
redeploy only the one changed component. Other components that don't depend on the changed
component do not need to be revalidated or redeployed.
CCP prompts us to gather together in one place all the classes that are likely to change for the same
reasons. If two classes are so tightly bound, either physically or conceptually, that they always
change together, they belong in the same component. This minimizes the workload related to
releasing, revalidating, and redistributing the software.
This principle is closely associated with the Open/Closed Principle (OCP). For it is "closure" in the OCP
sense of the word that this principle is dealing with. OCP states that classes should be closed for
modification but open for extension. But as we learned, 100 percent closure is not attainable. Closure
must be strategic. We design our systems such that they are closed to the most common kinds of
changes that we have experienced.
CCP amplifies this by grouping together classes that are open to certain types of changes into the
same components. Thus, when a change in requirements comes along, that change has a good
chance of being restricted to a minimal number of components.
