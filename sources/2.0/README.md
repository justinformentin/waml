<!--#
title: 'Web Automation Markup Language 2.0'
description: 'Human-readable way to define action sequences to perform on a web resources.'
#-->

# WAML 2.0

[![Build Status](https://travis-ci.org/automate-website/waml.svg?branch=master)](https://travis-ci.org/automate-website/waml) [![Gitter](https://badges.gitter.im/automate-website/waml.svg)](https://gitter.im/automate-website/waml?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge) ![WAML 2.0](https://img.shields.io/badge/WAML-2.0-ee2a7b.svg)

[![Example Scenario](img/scenario-register-at-automate-website-write-and-run.gif)](img/scenario-register-at-automate-website-write-and-run.gif)


**Notice**: WAML is currently in a very early draft version. Feel free to create a pull request in case of useful suggestions.

Refer to the [changelog] for recent notable changes and modifications.


## Abstract
```yaml
# Example of login process automation
name: Sign in
steps:
  - open: 'https://example.com/login'
  - enter:
      selector: input[name=email]
      input: username@example.com
  - enter:
      selector: input[name=password]
      input: s3cr3t
  - click: button[type=submit]
```

Web Automation Markup Language (WAML) is definition of action sequences which can be performed on web resources (e.g. regular web pages) within a context of a web browser to simulate user behavior. The WAML specification defines an application of [YAML 1.2] which allows an expirienced user to create a human and machine readable sequence at one go, reuse sequences in any order, and perform context dependent actions.


## Terminology

The underlying format for WAML is YAML so that it inherits all its benefits such as hosting of multiple document within one stream. A WAML stream may contain multiple _scenarios_. Every _scenario_ must be represented by a set of _metadata_ as well as sequence of _actions_ to execute. Every _action_ must have at least one _criteria_ which is represented as _scalar_ (string, integer, etc.) value or a _mapping_.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119].


## Schema

WAML is based on [JSON Schema] that lives at [waml-schema.org]. WAML schema is available in [YAML][waml-yaml] and [JSON][waml-json] formats. A scenario within a WAML stream may define the preferred schema version by defining ```$schema``` property, otherwise a default parser schema is used.


## Scenario Schema

{{ includeScenario('./sources/2.0/examples/simple-scenario.yaml') }}

A very basic scenario must contain a `name` and `steps` property. The list of actions may be empty, however, it is reasonable to have at least one action.

### Minimal Example

{{ includeScenario('./sources/2.0/examples/full-featured-scenario.yaml') }}

This minimal example demonstrates the simplicity of WAML. The full list of supported metadata is depicted below.

{{ schema2md('./2.0/scenario-schema') }}

Using this properties, the following more comprehensive example can be created:


## Step Schema

The steps property must be represented as a sequence of actions. Every step represents the smallest identifiable user action.

{{ schema2md('./sources/2.0/schema/step-schema.yaml') }}


## Fragment Scenarios

{{ includeScenario('./sources/2.0/examples/fragment-scenario.yaml') }}

Fragment scenarios can not be executed independently but can only be used in ```include``` actions of other scenarios or fragments.


## Actions and Criteria
### Open

{{ includeScenario('./sources/2.0/examples/open-scenario-1.yaml') }}
{{ includeScenario('./sources/2.0/examples/open-scenario-2.yaml') }}

Like for a real user, `open` is often the very first action of a scenarios. It triggers the navigation to a particular URL inside the web browser.
The `http://` scheme should be automatically added to the `url` if no scheme is specified.

#### Open Step Schema

{{ schema2md('./2.0/open-step-schema') }}

#### Open Criteria Schema

{{ schema2md('./2.0/open-criteria-schema') }}

### Ensure

{{ includeScenario('./sources/2.0/examples/ensure-scenario-1.yaml') }}
{{ includeScenario('./sources/2.0/examples/ensure-scenario-2.yaml') }}

To verify the integrity of the page it may be reasonable to ensure the presence of a certain element. The action ```ensure``` verifies, whether the particular element is present on the page.

The depicted simple scenario can be created using the shot-notation of ```ensure``` action:

1. Open a web page.
2. Verify the presence of a header with a certain class.

Using the additional criteria not only the presence of the element can be ensured but also elements content and its appearance within a defined a time constraint.

#### Ensure Step Schema

{{ schema2md('./2.0/ensure-step-schema') }}

#### Ensure Criteria Schema

{{ schema2md('./2.0/ensure-criteria-schema') }}

### Move

{{ includeScenario('./sources/2.0/examples/move-scenario-1.yaml') }}

{{ includeScenario('./sources/2.0/examples/move-scenario-2.yaml') }}

For hidden elements which appear only after the user has hovered a certain element the (mouse) ```move``` action can be used.  

The examples depicts the usage of the ```move``` action. 

#### Move Step Schema

{{ schema2md('./2.0/move-step-schema') }}

#### Move Criteria Schema

{{ schema2md('./2.0/move-criteria-schema') }}

### Click

{{ includeScenario('./sources/2.0/examples/click-scenario-1.yaml') }}
{{ includeScenario('./sources/2.0/examples/click-scenario-2.yaml') }}

Every kind of clicks can be simulated with the ```click``` action.

In the short notation example a click happens on an anchor element selected by CSS. 
Also the ```text``` criteria may be used to verify the wording of the target.

#### Click Step Schema

{{ schema2md('./2.0/click-step-schema') }}

#### Click Criteria Schema

{{ schema2md('./2.0/click-criteria-schema') }}


### Select

{{ includeScenario('./sources/2.0/examples/select-scenario-1.yaml') }}
{{ includeScenario('./sources/2.0/examples/select-scenario-2.yaml') }}

Short notation example of ```select``` and a complex example.

#### Select Step Schema

{{ schema2md('./2.0/select-step-schema') }}

#### Select Criteria Schema

{{ schema2md('./2.0/select-criteria-schema') }}


### Enter

{{ includeScenario('./sources/2.0/examples/enter-scenario-1.yaml') }}

#### Enter Step Schema

{{ schema2md('./2.0/enter-step-schema') }}

#### Enter Criteria Schema

{{ schema2md('./2.0/enter-criteria-schema') }}

### Wait

{{ includeScenario('./sources/2.0/examples/wait-scenario-1.yaml') }}
{{ includeScenario('./sources/2.0/examples/wait-scenario-2.yaml') }}

Short notation examples of ```wait```.

#### Wait Step Schema

{{ schema2md('./2.0/wait-step-schema') }}

#### Wait Criteria Schema

{{ schema2md('./2.0/wait-criteria-schema') }}


### Include

{{ includeScenario('./sources/2.0/examples/include-scenario-1.yaml') }}
{{ includeScenario('./sources/2.0/examples/include-scenario-2.yaml') }}

Short notation example of ```include``` and a complex example.

#### Include Step Schema

{{ schema2md('./2.0/include-step-schema') }}

#### Include Criteria Schema

{{ schema2md('./2.0/include-criteria-schema') }}


### Store

{{ includeScenario('./sources/2.0/examples/store-scenario-1.yaml') }}
{{ includeScenario('./sources/2.0/examples/store-scenario-2.yaml') }}

An example of simple usage of ```store``` as well as a more complex example.

#### Store Step Schema

{{ schema2md('./2.0/store-step-schema') }}

#### Store Criteria Schema

{{ schema2md('./2.0/store-criteria-schema') }}


## Expressions
### Expression Schema

{{ schema2md('./sources/2.0/schema/expression-schema.yaml') }}

## Shared Criteria
### Parent Criteria Schema

{{ schema2md('./2.0/parent-criteria-schema') }}


## Management of Multiple Scenarios

A single WAML file may contain multiple scenarios. Therefore, the capability of YAML to store multiple documents by splitting them with ```---``` is used.


[YAML 1.2]: http://yaml.org/spec/1.2/spec.html
[RFC 2119]: https://www.ietf.org/rfc/rfc2119.txt

[JSON Schema]: http://json-schema.org/
[changelog]: CHANGELOG.md
[waml-json]: dist/waml.json
[waml-yaml]: dist/waml.yaml
[waml-schema.org]: http://waml-schema.org