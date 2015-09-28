# Internal vs External quality of software

- Measuring quality
  - Internal
  - External
- Example
- Constraints on agility
- Regressions from two angles
- Over testing as a form of low internal quality
- Conclusion
- References

## Measuring quality
  Many studies have been conducted in the attempt to formalise the quality of software.
  Some quality models have been established like [SQuaRE](http://www.iso.org/iso/home/store/catalogue_tc/catalogue_detail.htm?csnumber=64764) by [Consortium for IT Software Quality](https://en.wikipedia.org/wiki/CISQ), which takes into consideration 5 key points:  Reliability, Efficiency, Security, Maintainability and (adequate) Size.

  The difficulty in measuring the quality of software is that software is very rarely at the end of it's lifecycle.
  Systems keep growing and evolving to meet new demands.
  Eventually these systems will be replaced or discarded, but they will fight to survive for as long as they can.

  One cannot measure quality based solely on what has already been completed.
  You have to also consider how your system will cope with the next inevatible change request.
  We will see how internal and external quality are tightly coupled, and how external quality dictates internal quality (obviously).

### External Quality (Functional)
  External quality is the usefulness of the system as perceived from outside.
  It provides customer value and meets the product owner's specifications.
  This quality can be measured through feature tests, QA and customer feedback.
  This is the quality affects your clients directly, as opposed to internal quality which affects then indirectly.

### Internal Quality (Structural)
  Internal quality has to do with the way that the system has been constructed.
  It is a much more granular measurement and considers things like clean code, complexity, duplication, component reuse.
  This quality can be measured through predefined standards, linting tools, unit tests etc.
  Internal quality affects your ability to manage and reason about the program.

  Is your program able to cope with new requirements easily moving forward?
  Is your program efficient enough to deal with an inevitable increase in data volume?
  Is your domain logic decoupled from the framework so that it can be updated without breaking the system?
  Do you have tests to guard existing functionality?

  These are some of the questions that need to be answered in order understand internal quality.

 "There are two common aspects of quality: one of them has to do with the consideration of the quality of a thing as an objective reality independent
 of the existence of man. The other has to do with what we think, feel or sense as a result of the objective reality. In other words, there is a
 subjective side of quality. W. A. Shewhart"

## Example
  Suppose you you receive a new requirement that a product can have a main header image.
  The code for optimal internal quality would be something simple like this:

```
@product.gallery.header_image
```

  It is the least amount of work you can do to provide some external quality.
  This code works until the user creates a product without a gallery and the program blows up on a nil error.
  You are forced to increase the [Cyclomatic complexity](https://en.wikipedia.org/wiki/Cyclomatic_complexity) of the code to increase its external quality.

```
if @product.gallery.present? and @product.gallery.header_image.present?
  @product.gallery.header_image
end
```

  Next you realise that the frontend design does not accommodate a missing header image, and you compensate for this.

```
if @product.gallery.present? and @product.gallery.header_image.present?
  @product.gallery.header_image
else
  @product.gallery.default_image
end
```

  As you can see, the cyclomatic complexity of this code has increased drastically in order to facilitate the external quality.
  Unless proper care is taken, this can grow into a mess that has a very low internal quality, inadvertently sabotaging efforts to add external
  quality in the future.
  Ensure that this functionality has [Black box](https://en.wikipedia.org/wiki/Black-box_testing) tests in place so you can refactor it's internals without changing it's behaviour.

## Constraints on agility
  Most clients are unaware of the internal quality constraints on a project.
  Cost goes up and it can be hard for software companies to justify exactly why that is.
  It is usually due to low internal quality, manifested in overly complex code.

  The best thing you can do is to keep your clients informed.
  Allow them to join the daily standup remotely and share your concerns from an internal quality perspective.
  We have been doing this for a while, and have even had a client come in once a week to work in the office with us.
  Needles to say, we have found this to be very productive.  Transparency is crucial.

## Regressions from two angles
  When refactoring code you have to be aware of both internal and external quality regressions.

  We have started manually reviewing our features before they are deployed to production.
  Usually by developers that are not familiar with the project.
  The author of the code will take the other person through what has been done.
  First by looking at the code / tests, and then by exercising the system (usually in a browser) in a way that demonstrates it's usefulness.

  At this point you should have sufficient feature and unit level tests to verify basic correctness.

## Over testing as a form of low internal quality
  Even if you have a really comprehensive test suite, if it was designed in a way that it heavily depends on the implementation details,
  it will hinder your ability to move forward quickly. Mock heavy tests tend to suffer from this.
  You cannot change much of the code without breaking a bunch of unrelated tests.

## Conclusion
  Obviously providing external quality is the reason why we build programs in the first place.
  We always cater for external quality first, but have to be concious of the state of the internal quality which will facilitate future growth.

  If your system is robust, with small flexible components that can be composed in different ways, you will find it easier to add or improve
  external quality.  Good external quality however does not facilitate good internal quality.
  Both play a vital role in contributing to the overall quality of your program.

## References
[Growing Object Oriented Software Guided By Tests](http://www.growing-object-oriented-software.com/)

[Software Quality](https://en.wikipedia.org/wiki/Software_quality)

[Internal And External Software Quality](https://meekrosoft.wordpress.com/2010/10/31/internal-and-external-software-quality/)
