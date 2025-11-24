# Runtime View

**Contents**

The runtime view describes concrete behavior and interactions of the
system’s building blocks in form of scenarios from the following areas:

- important use cases or features: how do building blocks execute
  them?

- interactions at critical external interfaces: how do building blocks
  cooperate with users and neighboring systems?

- operation and administration: launch, start-up, stop

- error and exception scenarios

Remark: The main criterion for the choice of possible scenarios
(sequences, workflows) is their **architectural relevance**. It is
**not** important to describe a large number of scenarios. You should
rather document a representative selection.

**Motivation**

You should understand how (instances of) building blocks of your system
perform their job and communicate at runtime. You will mainly capture
scenarios in your documentation to communicate your architecture to
stakeholders that are less willing or able to read and understand the
static models (building block view, deployment view).

**Form**

There are many notations for describing scenarios, e.g.

- numbered list of steps (in natural language)

- activity diagrams or flow charts

- sequence diagrams

- BPMN or EPCs (event process chains)

- state machines

- …

See [Runtime View](https://docs.arc42.org/section-6/) in the arc42
documentation.

## Runtime Scenario Remote Connect

<https://code.siemens.com/common-device-management/remote-access/remote-access-service/-/blob/main/README.md?ref_type=heads>

This is the interaction between different components for remote connection and disconnection.

## Runtime Scenario Context Hierarchy

<https://code.siemens.com/common-device-management/inventory/context-hierarchy-service/-/blob/main/README.md>

This is the interaction between different components for creating context based hierarchy.

## &lt;Runtime Scenario 2>

## …

## &lt;Runtime Scenario n>
