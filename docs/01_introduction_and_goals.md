# Introduction and Goals

This document describes the DevOps architecture of **mysite360** project and suites as the DevOps foundation for the architecture vision 2.0.

The main goal of this document is to provide a comprehensive overview of the DevOps architecture, including its components, processes, and best practices. It aims to align the development and operations teams towards a common vision and set of objectives.

The overarching architecture vision 2.0 focuses on the following key aspects:

- **Containerization and Orchestration**: Leveraging containerization technologies like Docker and orchestration tools like Kubernetes to ensure scalability, flexibility, and efficient resource utilization.
- **Test Automation**: Implementing automated testing frameworks to ensure code quality, reduce manual effort, and accelerate the development lifecycle.
- **Continuous Integration and Continuous Deployment (CI/CD)**: Implementing robust CI/CD pipelines to automate the build, test, and deployment processes, enabling faster and more reliable software delivery.
- **Infrastructure as Code (IaC)**: Adopting IaC practices using tools like Terraform and Ansible to manage infrastructure in a version-controlled and automated manner.

The main objectives of this document are:

- To define the key components of the DevOps architecture, including tools, technologies, and processes.
- To outline the roles and responsibilities of team members involved in the DevOps practices.
- To establish best practices for continuous integration, continuous delivery, and infrastructure as code.

## Requirements Overview

**Contents**

Short description of the functional requirements, driving forces,
extract (or abstract) of requirements. Link to (hopefully existing)
requirements documents (with version number and information where to
find it).

**Motivation**

From the point of view of the end users a system is created or modified
to improve support of a business activity and/or improve the quality.

**Form**

Short textual description, probably in tabular use-case format. If
requirements documents exist this overview should refer to these
documents.

Keep these excerpts as short as possible. Balance readability of this
document with potential redundancy w.r.t to requirements documents.

See [Introduction and Goals](https://docs.arc42.org/section-1/) in the
arc42 documentation.

## Quality Goals

**Contents**

The top three (max five) quality goals for the architecture whose
fulfillment is of highest importance to the major stakeholders. We
really mean quality goals for the architecture. Don’t confuse them with
project goals. They are not necessarily identical.

Consider this overview of potential topics (based upon the ISO 25010
standard):

![Categories of Quality
Requirements](images/01_2_iso-25010-topics-EN.drawio.png)

**Motivation**

You should know the quality goals of your most important stakeholders,
since they will influence fundamental architectural decisions. Make sure
to be very concrete about these qualities, avoid buzzwords. If you as an
architect do not know how the quality of your work will be judged…

**Form**

A table with quality goals and concrete scenarios, ordered by priorities

## Stakeholders

**Contents**

Explicit overview of stakeholders of the system, i.e. all person, roles
or organizations that

- should know the architecture

- have to be convinced of the architecture

- have to work with the architecture or with code

- need the documentation of the architecture for their work

- have to come up with decisions about the system or its development

**Motivation**

You should know all parties involved in development of the system or
affected by the system. Otherwise, you may get nasty surprises later in
the development process. These stakeholders determine the extent and the
level of detail of your work and its results.

**Form**

Table with role names, person names, and their expectations with respect
to the architecture and its documentation.

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 40%" />
<col style="width: 40%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Role/Name</th>
<th style="text-align: left;">Contact</th>
<th style="text-align: left;">Expectations</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><p><em>&lt;Role-1&gt;</em></p></td>
<td style="text-align: left;"><p><em>&lt;Contact-1&gt;</em></p></td>
<td style="text-align: left;"><p><em>&lt;Expectation-1&gt;</em></p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p><em>&lt;Role-2&gt;</em></p></td>
<td style="text-align: left;"><p><em>&lt;Contact-2&gt;</em></p></td>
<td style="text-align: left;"><p><em>&lt;Expectation-2&gt;</em></p></td>
</tr>
</tbody>
</table>
