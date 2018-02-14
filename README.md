# Notice of work-in-progess: this project currently requires an unreleased version of Magnolia to compile

[![Build Status](https://travis-ci.org/drivergroup/spray-json-derivation.svg?branch=master)](https://travis-ci.org/drivergroup/spray-json-derivation)
[![Download](https://img.shields.io/maven-central/v/xyz.driver/spray-json-derivation_2.12.svg)](http://search.maven.org/#search|ga|1|xyz.driver%20spray-json-derivation-)

# Spray JSON Format Derivation

This library provides automatic spray JsonFormats for any `case class` and children of `sealed trait`s.

It uses the [Magnolia](http://magnolia.work/) ([source code](https://github.com/propensive/magnolia)) type-derivation library to implicitly generate JSON formats for any product type. Magnolia integrates with spray so seamlessly that it is almost not worth the effort to publish this project as a full fledged repository; a single gist with the contents of [DerivedFormats.scala](src/main/scala/DerivedFormats.scala) would demonstrate almost all functionality.

## Getting Started

Spray JSON Format Derivation is published to maven central as a Scala
library. Include it in sbt by adding the following snippet to your
build.sbt:

```scala
libraryDependencies += "xyz.driver" %% "spray-json-derivation" % "<latest version>"
```

Define some case classes and mix `DerivedFormats` into your JSON
protocol stack. That's it.

```scala
import spray.json._
import xyz.driver.json.DerivedFormats

object Main extends App with DefaultJsonProtocol with DerivedFormats {
  
  case class A(x: Int)
  case class B(a: A, str: String)
  
  println(B(A(42), "hello world").toJson.prettyPrint)

}
```


## Documentation
Check out the main file
[DerivedFormats.scala](src/main/scala/DerivedFormats.scala) and the
[test suite](src/test/scala/ProductTypeFormats.scala) for a complete overview of the project.

## Copying
Copyright 2018 Driver Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
